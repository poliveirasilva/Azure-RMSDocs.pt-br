---
# required metadata

title: Autenticação ADAL para a aplicação com suporte RMS | Azure RMS
description: Descreve o processo para a autenticação com a ADAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedimentos: utilizar a autenticação ADAL

Autenticação com o Azure RMS para a sua aplicação com o ADAL (Azure Active Directory Authentication Library).

Ao atualizar a aplicação para utilizar a autenticação ADAL em vez do Assistente de Início de Sessão Online da Microsoft, o utilizador e os seus clientes poderão:

- Utilizar a autenticação multifator
- Instalar o cliente RMS 2.1 sem necessidade de privilégios administrativos no computador
- Certificar a aplicação para o Windows 10

## Duas abordagens para autenticação

Este tópico contém duas abordagens para autenticação com os exemplos de código correspondentes.

- **Autenticação interna** – Autenticação OAuth gerida pelo SDK RMS.

  Utilize esta abordagem se pretender que o cliente RMS apresente um pedido de autenticação ADAL quando a autenticação for necessária. Para obter detalhes sobre como configurar a sua aplicação, consulte a secção “Autenticação interna”.

  > [!Note] Se a sua aplicação utilizar atualmente o SDK AD RMS 2.1 com o assistente de início de sessão, recomendamos que utilize o método de autenticação interno como o caminho de migração da sua aplicação.

- **Autenticação externa** – Autenticação OAuth gerida pela sua aplicação.

  Utilize esta abordagem se pretender que a aplicação efetue a gestão da sua própria autenticação OAuth. Com esta abordagem, o cliente RMS irá exercer uma chamada de retorno definida pela aplicação quando a autenticação for necessária. Para obter um exemplo detalhado, consulte “Autenticação externa” no final deste tópico.

  > [!Note] A autenticação externa não implica a capacidade de alterar os utilizadores. O cliente RMS utiliza sempre o utilizador predefinido de um inquilino do RMS especificado.

## Autenticação interna

1. Siga os passos da configuração do Azure em [Configurar o Azure RMS para autenticação ADAL](adal-auth.md) e, em seguida, volte ao passo de inicialização de aplicação seguinte.
2. Agora está pronto para configurar a sua aplicação para utilizar a autenticação ADAL interna fornecida pelo SDK RMS 2.1.

Para configurar o cliente RMS, adicione uma chamada para [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) imediatamente após chamar [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) para configurar o cliente RMS. Utilize o seguinte fragmento de código como um exemplo.

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

## Autenticação Externa

Utilize este código como um exemplo de como gerir os seus próprios tokens de autenticação.
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

* [Tipos de dados](/rights-management/sdk/2.1/api/win/datatypes)
* [Propriedades de ambiente](/rights-management/sdk/2.1/api/win/environmentproperties)
* [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreateoauth2token)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC_CREDENTIAL)
* [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC_NAME_VALUE_LIST)
* [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IIPC_OAUTH2_CALLBACK_INFO)
* [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC_PROMPT_CTX)
* [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IIPC_AAD_APPLICATION_ID)


<!--HONumber=Jun16_HO2-->


