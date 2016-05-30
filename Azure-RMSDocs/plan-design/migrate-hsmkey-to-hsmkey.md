---
# required metadata

title: Etapa 2&colon; Migração de chave protegida por HSM para chave protegida por HSM | Azure RMS
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

# Etapa 2: migração de chave protegida por HSM para chave protegida por HSM

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*


Estas instruções são parte do [caminho de migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e são aplicáveis somente se a chave do AD RMS é protegida por HSM e se você deseja migrar para o Azure Rights Management com uma chave de locatário protegida por HSM. 

Se este não for o cenário de configuração escolhido, volte para a [Etapa 2. Exporte os dados de configuração do AD RMS e importe-os para o Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) e escolha uma configuração diferente.

> [!NOTE]
> Essas instruções presumem que a sua chave do AD RMS é protegido por módulo. Este é o caso comum. Se sua chave do AD RMS é protegida por OCS, entre em contato com [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) antes de seguir essas instruções.

Esse é um procedimento de duas partes para importar a sua chave HSM e configuração do AD RMS para o Azure RMS, para resultar na sua chave de locatário do Azure RMS gerenciada por você (BYOK).

Primeiro, empacote a sua chave HSM para que assim esteja pronta para ser transferida para o Azure RMS e, em seguida, importe os dados de configuração.

## Parte 1: Empacotar sua chave HSM para que esteja pronta para transferir para o Azure RMS

1.  Siga as etapas na seção [Implementando sua própria chave (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) do [Planejando e implementando sua chave de locatário do Azure Rights Management](plan-implement-tenant-key.md), usando o procedimento **Gerar e transferir sua chave de locatário – na Internet** com as seguintes exceções:

    -   Não siga as instruções para **gerar sua chave de locatário**, porque você já tem o equivalente da sua implantação do AD RMS. Identifique a chave usada pelo servidor do AD RMS na instalação da Thales e use essa chave durante a migração. Os arquivos de chave criptografada Thales geralmente são nomeados **key_(keyAppName)_(keyIdentifier)** localmente no servidor.

    -   Não siga as etapas para **Transferir sua chave de locatário para o Azure RMS**, que usa o comando Add-AadrmKey.  Em vez disso, você transferirá sua chave HSM preparada quando você carregar seu domínio exportado de publicação confiável, usando o comando de importação AadrmTpd.

2.  Na estação de trabalho conectada à Internet, na sessão do Windows PowerShell, reconectar-se ao serviço do Azure RMS.

Agora que você preparou sua chave HSM para o Azure RMS, você está pronto para importar o arquivo de chave de HSM e os dados de configuração do AD RMS.

## Parte 2: Importe a chave HSM e os dados de configuração para o Azure RMS

1.  Ainda na estação de trabalho conectada à Internet e na sessão do Windows PowerShell, carregue o primeiro arquivo exportado (.xml) do domínio de publicação confiável. Se você tiver mais de um arquivo. xml porque você tinha vários domínios de publicação confiáveis, escolha o arquivo que contenha o domínio de publicação confiável exportado que corresponda à chave HSM que você deseja usar no Azure RMS para proteger o conteúdo após a migração. Execute o seguinte comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Por exemplo: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Quando solicitado, digite a senha que você especificou antes e confirme que deseja executar esta ação.

2.  Quando o comando for concluído, repita a etapa 1 para cada arquivo .xml que você criou exportando domínios de publicação confiáveis. Mas, para esses arquivos, defina **-Active** como **false** ao executar o comando de importação.  Por exemplo: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Use o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para se desconectar do serviço do Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Agora você está pronto para ir para a [Etapa 3. Ativar locatário do RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO4-->


