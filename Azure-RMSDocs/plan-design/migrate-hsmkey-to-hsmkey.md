---
# required metadata

title: Passo 2&colon; Migração de chave protegida por HSM para chave protegida por HSM | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Passo 2: migração de chave protegida por HSM para chave protegida por HSM

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*


Estas instruções fazem parte do [caminho de migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e são aplicáveis apenas se a sua chave do AD RMS estiver protegida por HSM e pretender migrar para o Azure Rights Management com uma chave de inquilino protegida por HSM. 

Se este não for o cenário de configuração escolhido, volte ao [Passo 2. Exporte os dados de configuração do AD RMS, importe-os para o Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) e escolha uma configuração diferente.

> [!NOTE]
> Estas instruções partem do princípio de que a sua chave do AD RMS está protegida por um módulo. Este é o caso comum. Se a sua chave do AD RMS estiver protegida por OCS, contacte [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) antes de aplicar estas instruções.

Trata-se de um procedimento de duas partes para importar a sua chave HSM e a configuração do AD RMS para o Azure RMS, que resultará na sua chave de inquilino do Azure RMS que é gerida por si (BYOK).

Primeiro, tem de compactar a sua chave HSM para que fique pronta a transferir para o Azure RMS e, em seguida, importá-la com os dados de configuração.

## Parte 1: compactar a sua chave HSM para que fique pronta a transferir para o Azure RMS

1.  Siga os passos na secção [Implementar BYOK (traga a sua própria chave)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de [Planear e Implementar a Chave de Inquilino do Azure Rights Management](plan-implement-tenant-key.md), utilizando o procedimento **Gerar e transferir a chave de inquilino – através da Internet** com as seguintes exceções:

    -   Não siga os passos para **Gerar a chave de inquilino**, porque já tem o equivalente da sua implementação do AD RMS. Tem de identificar a chave utilizada pelo seu servidor AD RMS na instalação da Thales e utilizar esta chave durante a migração. Os ficheiros de chave encriptados da Thales são normalmente denominados **key_(keyAppName)_(keyIdentifier)** localmente no servidor.

    -   Não siga os passos para **Transferir a chave de inquilino para o Azure RMS**, que utiliza o comando Add-AadrmKey.  Em vez disso, transfira a chave HSM preparada quando carregar o domínio de publicação fidedigno exportado, utilizando o comando Import-AadrmTpd.

2.  Na estação de trabalho com ligação à Internet, na sessão do Windows PowerShell, volte a ligar-se ao serviço do Azure RMS.

Agora que já preparou a chave HSM para o Azure RMS, está pronto para importar o ficheiro da chave HSM e os dados de configuração do AD RMS.

## Parte 2: importar a chave HSM e os dados de configuração para o Azure RMS

1.  Ainda na estação de trabalho com ligação à Internet e na sessão do Windows PowerShell, carregue o primeiro ficheiro de domínio de publicação fidedigno (.xml) exportado. Se tiver mais do que um ficheiro .xml, porque tinha vários domínios de publicação fidedignos, escolha o ficheiro que contém o domínio de publicação fidedigno exportado que corresponde à chave de HSM que pretende utilizar no Azure RMS para proteger o conteúdo após a migração. Utilize o seguinte comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Por exemplo: **Import -TpdFile E:\no_key_tpd_contosokey1.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Quando for solicitado, introduza a palavra-passe que especificou anteriormente e confirme que pretende efetuar esta ação.

2.  Quando o comando for concluído, repita o passo 1 para cada ficheiro .xml restante que criou ao exportar os seus domínios de publicação fidedignos. No entanto, para esses ficheiros, defina **-Active** para **false** ao executar o comando Import.  Por exemplo: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Utilize o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desligar do serviço do Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Agora, está pronto para ir para o [Passo 3. Ativar o inquilino do RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO4-->


