---
# required metadata

title: Etapa 2&colon; Migração de chave protegida por software para chave protegida por HSM | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Etapa 2: migração de chave protegida por software para chave protegida por HSM

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*


Estas instruções fazem parte do [caminho de migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e são aplicáveis somente se a chave do AD RMS é protegida por software e se você deseja migrar para o Azure Rights Management com uma chave de locatário protegida por HSM. 

Se este não for o cenário de configuração escolhido, volte para a [Etapa 2. Exporte os dados de configuração do AD RMS e importe-os para o Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) e escolha uma configuração diferente.

Esse é um procedimento de três partes para importar a configuração do AD RMS para o Azure RMS, para resultar na sua chave de locatário do Azure RMS gerenciada por você (BYOK).

Extraia primeiro a sua chave do certificado de licenciante para servidor (SLC) dos dados de configuração e transfira-a para um HSM da Thales local e, em seguida, empacote e transfira a chave HSM para o Azure RMS e importe os dados de configuração.

## Parte 1: extrair o SLC dos dados de configuração e importar a chave para o HSM local

1.  Use as seguintes etapas na seção [Implementando "traga a sua própria chave (BYOK)"](plan-implement-tenant-key.md#BKMK_ImplementBYOK) do tópico [Planejando e implementando sua chave de locatário do Azure Rights Management](plan-implement-tenant-key.md):

    -   **Gerar e transferir a chave de locatário - pela Internet**: **Prepare a sua estação de trabalho conectada à Internet**

    -   **Gerar e transferir a chave de locatário - pela Internet**: **Prepare a sua estação de trabalho desconectada**

    Não siga as instruções para gerar sua chave de locatário, porque você já tem o equivalente no arquivo exportado (.xml) de dados de configuração. Em vez disso, execute um comando para extrair essa chave do arquivo e importá-la para o seu HSM local.

2.  Na estação de trabalho desconectada, execute o seguinte comando:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Por exemplo, para a América do Norte:: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Informação adicional:

    -   O parâmetro ImportRmsCentrallyManagedKey indica que a operação é para importar a chave SLC.

    -   Se não especificar a senha no comando, você receberá uma solicitação para especificá-la

    -   O parâmetro KeyIdentifier é um nome de chave fácil que cria o nome do arquivo de chave. Use apenas caracteres ASCII minúsculos.

    -   O parâmetro ExchangeKeyPackage especifica um pacote (KEK) de chave de troca de chaves específica de região que possui um nome que começa com BYOK-KEK-pkg-.

    -   O parâmetro NewSecurityWorldPackage especifica um pacote mundial de segurança específico de região que possui um nome que começa com BYOK-SecurityWorld-pkg-.

    Esse comando resulta no seguinte:

    -   Um arquivo de chave do HSM: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   Arquivo de dados de configuração do RMS com o SLC removido: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  Se tiver mais de um arquivo de dados de configuração do RMS, repita a etapa 2 para o restante desses arquivos.

Agora que o SLC foi extraído para ser uma chave baseada em HSM, você já pode empacotá-lo e transferi-lo para o Azure RMS.

## Parte 2: Empacotar e transferir a sua chave HSM para o Azure RMS

1.  Use as seguintes etapas da seção [Implementando "traga a sua própria chave (BYOK)"](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de [Planejando e implementando sua chave de locatário do Azure Rights Management](plan-implement-tenant-key.md):

    -   **Gerar e transferir a chave de locatário - pela Internet**: **Prepare sua chave de locatário para transferência**

    -   **Gerar e transferir a chave de locatário - pela Internet**: **Transfira sua chave de locatário para o Azure RMS**

Agora que já transferiu a chave HSM para o Azure RMS, você já pode importar os dados de configuração do AD RMS que contêm somente um ponteiro para a chave de locatário que acabou de ser transferida.

## Parte 3: Importar os dados de configuração para o Azure RMS

1.  Ainda na estação de trabalho conectada à Internet e na sessão do Windows PowerShell, copie os arquivos de configuração do RMS com o SLC removido (na estação de trabalho desconectada, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Fazer upload do primeiro arquivo. Se você tiver mais de um arquivo. xml porque você tinha vários domínios de publicação confiáveis, escolha o arquivo que contenha o domínio de publicação confiável exportado que corresponda à chave HSM que você deseja usar no Azure RMS para proteger o conteúdo após a migração. Execute o seguinte comando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Por exemplo: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Quando solicitado, digite a senha que você especificou antes e confirme que deseja executar esta ação.

3.  Quando o comando for concluído, repita a etapa 2 para cada arquivo .xml que você criou exportando seus domínios de publicação confiáveis. Mas, para esses arquivos, defina **-Active** como **false** ao executar o comando de importação. Por exemplo: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Use o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para se desconectar do serviço do Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Agora você está pronto para ir para a [Etapa 3. Ativar locatário do RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).




<!--HONumber=Apr16_HO4-->


