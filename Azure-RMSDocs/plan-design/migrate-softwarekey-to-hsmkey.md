---
title: "Passo 2&colon; Migração de chave protegida por software para chave protegida por HSM | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 173641b9dada2673b48a1c210419cb933cdd9f13


---

# Passo 2: migração de chave protegida por software para chave protegida por HSM

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*


Estas instruções fazem parte do [caminho de migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e são aplicáveis apenas se a sua chave de AD RMS estiver protegida por software e pretender migrar para o Azure Rights Management com uma chave de inquilino protegida por HSM. 

Se este não for o cenário de configuração escolhido, volte ao [Passo 2. Exporte os dados de configuração do AD RMS, importe-os para o Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) e escolha uma configuração diferente.

Trata-se de um procedimento de três partes para importar a configuração do AD RMS para o Azure RMS, que resultará na sua chave de inquilino do Azure RMS que é gerida por si (BYOK).

Primeiro, deve extrair a chave do certificado de licenciante para servidor (SLC) dos dados de configuração e transferir a chave para um HSM da Thales no local e, em seguida, compactar e transferir a chave HSM para o Azure RMS e importar os dados de configuração.

## Parte 1: extrair o SLC dos dados de configuração e importar a chave para o seu HSM no local

1.  Siga os passos na secção [Implementar BYOK (traga a sua própria chave)](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) de [Planear e implementar a chave de inquilino do Azure Rights Management](plan-implement-tenant-key.md), utilizando o procedimento **Gerar e transferir a chave de inquilino – através da Internet** com as seguintes exceções:

    -   **Gerar e transferir a chave de inquilino – através da Internet**: **preparar a estação de trabalho com ligação à Internet**

    -   **Gerar e transferir a chave de inquilino – através da Internet**: **preparar a estação de trabalho desligada**

    Não siga os passos para gerar a chave de inquilino, porque já tem o equivalente no ficheiro dos dados de configuração exportados (.xml). Em vez disso, deverá executar um comando para extrair esta chave do ficheiro e importá-la para o seu HSM no local.

2.  Na estação de trabalho desligada, execute o seguinte comando:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Por exemplo, para a América do Norte: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Informações adicionais:

    -   O parâmetro ImportRmsCentrallyManagedKey indica que a operação é para importar a chave SLC.

    -   Se não especificar a palavra-passe no comando, será solicitado a especificá-la.

    -   O parâmetro KeyIdentifier destina-se a um nome amigável de chave que cria o nome do ficheiro de chave. Deve utilizar apenas carateres ASCII minúsculos.

    -   O parâmetro ExchangeKeyPackage especifica um pacote de chave de troca de chaves (KEK) específico da região que tem um nome que começa por BYOK-KEK-pkg-.

    -   O parâmetro NewSecurityWorldPackage especifica um pacote de universo de segurança específico da região que tem um nome que começa por BYOK-SecurityWorld-pkg-.

    Este comando resulta no seguinte:

    -   Um ficheiro de chave HSM: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   Ficheiro de dados de configuração de RMS com o SLC removido: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  Se tiver mais do que um ficheiro de dados de configuração de RMS, repita o passo 2 para o resto dos ficheiros.

Agora que o seu SLC foi extraído para que seja uma chave baseada em HSM, está pronto para compactá-lo e transferi-lo para o Azure RMS.

## Parte 2: compactar e transferir a chave HSM para o Azure RMS

1.  Utilize os passos seguintes da secção [Implementar BYOK (traga a sua própria chave)](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) do tópico [Planear e implementar a chave de inquilino do Azure Rights Management](plan-implement-tenant-key.md):

    -   **Gerar e transferir a chave de inquilino – através da Internet**: **preparar a chave de inquilino para a transferência**

    -   **Gerar e transferir a chave de inquilino – através da Internet**: **transferir a chave de inquilino para o Azure RMS**

Agora que transferiu a chave HSM para o Azure RMS, está pronto para importar os dados de configuração do AD RMS, que contêm apenas um ponteiro para a chave de inquilino transferida recentemente.

## Parte 3: importar os dados de configuração para o Azure RMS

1.  Ainda na estação de trabalho com ligação à Internet e na sessão do Windows PowerShell, copie os ficheiros de configuração do RMS com SLC removido (da estação de trabalho desligada, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Carregue o primeiro ficheiro. Se tiver mais do que um ficheiro .xml, porque tinha vários domínios de publicação fidedignos, escolha o ficheiro que contém o domínio de publicação fidedigno exportado que corresponde à chave de HSM que pretende utilizar no Azure RMS para proteger o conteúdo após a migração. Utilize o seguinte comando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Por exemplo: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Quando for solicitado, introduza a palavra-passe que especificou anteriormente e confirme que pretende efetuar esta ação.

3.  Quando o comando for concluído, repita o passo 2 para cada ficheiro .xml restante que criou ao exportar os seus domínios de publicação fidedignos. No entanto, para esses ficheiros, defina **-Active** para **false** ao executar o comando Import. Por exemplo: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Utilize o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desligar do serviço do Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Agora está pronto para ir para o [Passo 3. Ativar o seu inquilino do RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).





<!--HONumber=Jun16_HO4-->


