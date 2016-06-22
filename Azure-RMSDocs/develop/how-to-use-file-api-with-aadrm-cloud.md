---
# required metadata

title:
How-to: enable your service application to work with cloud based RMS | Azure RMS
description: This topic outlines steps for setting up your service application to use Azure Rights Management.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como habilitar seu aplicativo de serviço a operar com RMS baseado em nuvem

Este tópico descreve as etapas para configurar seu aplicativo de serviço para usar o Azure Rights Management. Para saber mais, confira [Introdução ao Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx).

**Importante**  
Para usar seu aplicativo de serviço do Rights Management Services SDK 2.1 com o Azure RMS, você precisará criar seus próprios locatários. Para obter mais informações, consulte [Requisitos do Azure RMS: assinaturas de nuvem que dão suporte ao Azure RMS](/rights-management/get-started/requirements-subscriptions.md)

## Pré-requisitos

-   O SDK 2.1 do RMS deve estar instalado e configurado. Para saber mais, confira [Introdução ao SDK 2.1 do RMS](getting-started-with-ad-rms-2-0.md).
-   Você deve [criar uma identidade de serviço por meio do ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) usando a opção de chave simétrica, ou por outros meios, e registrar as informações sobre a chave desse processo.

## Conectar-se ao serviço Azure Rights Management

-   Chame [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize).
-   Defina [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Observação** Para saber mais, confira [Definição do modo de segurança de API](setting-the-api-security-mode-api-mode.md)

     
-   As etapas a seguir são a configuração para a criação de uma instância de uma estrutura [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) com o membro **pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) preenchido com as informações de conexão do serviço Azure Rights Management.
-   Use as informações da criação de sua identidade do serviço de chave simétrica (consulte os pré-requisitos listados neste tópico) para definir os parâmetros **wszServicePrincipal**, **wszBposTenantId** e **cbKey** ao criar uma instância de uma estrutura [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Observação** Devido a uma condição existente com nosso serviço de descoberta, se você não estiver na América do Norte, as credenciais de chave simétrica não serão aceitas de outras regiões, portanto, você deve especificar as URLs de seu locatário diretamente. Isso é feito por meio do parâmetro [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) de [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) ou [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist).

## Gerar uma chave simétrica e coletar as informações necessárias

### Instruções para gerar uma chave simétrica

-   Instale o [Assistente de Conexão do Microsoft Online](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   Instale o [Módulo do Powershell do Azure AD](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)

**Observação** Você deve ser um administrador de locatário para usar os cmdlets do Powershell.

-   Inicie o Powershell e execute os seguintes comandos para gerar uma chave         `Import-Module MSOnline`
            `Connect-MsolService` (digite suas credenciais de administrador)         `New-MsolServicePrincipal` (digite um nome de exibição)
-   Após a geração de uma chave simétrica, ele retornará informações sobre chave, incluindo a própria chave e **AppPrincipalId**.


    A seguinte chave simétrica foi criada como uma que não foi fornecida ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### Instruções para descobrir o **TenantBposId** e as **Urls**

-   Instale o [Módulo do Powershell do Azure RMS](https://technet.microsoft.com/en-us/library/jj585012.aspx)
-   Inicie o Powershell e execute os seguintes comandos para obter a configuração de RMS do locatário.

    `Import-Module aadrm`

    `Connect-AadrmService` (digite suas credenciais de administrador)

    `Get-AadrmConfiguration`


-   Crie uma instância de um [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) e defina alguns membros.

    // Crie uma estrutura de chave.
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // Defina cada membro com informações de criação do serviço.
    symKey.wszBase64Key = "your service principal key"; symKey.wszAppPrincipalId = "your app principal identifier"; symKey.wszBposTenantId = "your tenent identifier";


Para obter mais informações, consulte [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

-   Crie uma instância de uma estrutura [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) que contém sua instância do [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Observação**  Os membros de *conectionInfo* são definidos com URLs da chamada anterior para `Get-AadrmConfiguration` e são indicados aqui com esses nomes de campo.

    // Create a credential structure.
    IPC_CREDENTIAL cred = {0};

    IPC_CONNECTION_INFO connectionInfo = {0};
    connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
    connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

    // Set each member.
    cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
    cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

    // Create your prompt control.
    IPC_PROMPT_CTX promptCtx = {0};

    // Set each member.
    promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
    promptCtx.hwndParent = NULL;
    promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
    promptCtx.hCancelEvent = NULL;
    promptCtx.pcCredential = &cred;

### Identificar um modelo e, depois, criptografar

-   Selecione um modelo a ser usado para a criptografia
    Chame [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) passando na mesma instância do [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Com o modelo do começo deste tópico, chame [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile), passando a mesma instância do [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).

Exemplo de uso de [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile):

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Exemplo de uso de [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile):

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Agora você concluiu as etapas necessárias para permitir que seu aplicativo use o Azure Rights Management.

## Tópicos relacionados

* [Introdução ao Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Introdução ao SDK 2.1 do RMS](getting-started-with-ad-rms-2-0.md)
* [Criar uma identidade de serviço por meio do ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 


<!--HONumber=Jun16_HO2-->


