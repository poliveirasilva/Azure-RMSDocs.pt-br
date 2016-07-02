---
title: "Autenticação ADAL para seu aplicativo habilitado para RMS | Azure RMS"
description: "Descreve o processo de autenticação com ADAL"
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4c3625676c7e794ef133c75881f666bae80e0513
ms.openlocfilehash: 9200ea44671776ced8781c1e13e71871f5bdf014


---

# Como usar a autenticação de ADAL

Autenticação com o Azure RMS para seu aplicativo usando o ADAL (Azure Active Directory Authentication Library).

Ao atualizar seu aplicativo para usar a autenticação ADAL em vez do Assistente de Conexão do Microsoft Online, você e seus clientes poderão:

- Usar a autenticação multifator
- Instalar o cliente do RMS 2.1 sem exigir privilégios administrativos no computador
- Certificar o aplicativo para o Windows 10

## Duas abordagens de autenticação

Este tópico contém duas abordagens de autenticação com exemplos de código correspondentes.

- **Autenticação interna** -autenticação OAuth gerenciada pelo RMS SDK.

  Use essa abordagem se quiser que o cliente RMS exiba um prompt de autenticação ADAL quando a autenticação for necessária. Para obter detalhes sobre como configurar seu aplicativo, consulte a seção "Autenticação interna".

  > [!Note] 
  > Se seu aplicativo usa atualmente o AD RMS SDK 2.1 com o assistente de conexão, é recomendável que você use o método de autenticação interna como o caminho de migração do aplicativo.

- **Autenticação externa** -autenticação OAuth gerenciada pelo seu aplicativo.

  Use essa abordagem se quiser que seu aplicativo para gerenciar sua própria autenticação OAuth. Com essa abordagem, o cliente RMS usará um retorno de chamada definido pelo aplicativo quando a autenticação for necessária. Para obter um exemplo detalhado, consulte "Autenticação externa" no final deste tópico.

  > [!Note] 
  > Autenticação externa não implica a capacidade de alterar usuários. o cliente RMS sempre usa o usuário padrão para determinado locatário do RMS.

## Autenticação interna

1. Siga as etapas de configuração do Azure em [Configurar o Azure RMS para autenticação de ADAL](adal-auth.md) e retorne para a próxima etapa de inicialização do aplicativo.
2. Agora você está pronto para configurar seu aplicativo para usar a autenticação interna do ADAL fornecido pelo RMS SDK 2.1.

Para configurar o cliente RMS, adicione uma chamada a [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) logo após a chamada a [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) para configurar o cliente RMS. Use o trecho de código a seguir como exemplo.

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## Autenticação externa

Use esse código como um exemplo de como gerenciar seus próprios tokens de autenticação.
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

      HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
      {
          IPC_OAUTH2_CALLBACK pfGetADALToken =
          [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
          {
              wstring wstrToken;
              HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
              return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
          };

          IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
          {
              sizeof(IPC_OAUTH2_CALLBACK_INFO),
              pfGetADALToken,
              pContextForAdal
          };

          IPC_CREDENTIAL credentialContext =
          {
              IPC_CREDENTIAL_TYPE_OAUTH2,
              NULL
          };
          credentialContext.pcOAuth2 = &callbackCredentialContext;

          IPC_PROMPT_CTX promptContext =
          {
              sizeof(IPC_PROMPT_CTX),
              NULL,
              IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
              NULL,
              &credentialContext
          };

          hKey = 0L;
          return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
      }

## Tópicos relacionados

* [Tipos de dados](/rights-management/sdk/2.1/api/win/data%20types)
* [Propriedades de ambiente](/rights-management/sdk/2.1/api/win/environment%20properties#msipc_environment_properties)
* [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreateoauth2token)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC_CREDENTIAL)
* [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC_NAME_VALUE_LIST)
* [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/ipc_oauth2_callback_info#msipc_ipc_oath2_callback_info)
* [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC_PROMPT_CTX)
* [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/ipc_aad_application_id#msipc_ipc_aad_application_id)



<!--HONumber=Jul16_HO1-->


