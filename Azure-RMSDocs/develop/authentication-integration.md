---
# required metadata

title: Como adicionar autenticação ao seu aplicativo | Azure RMS
description: Descreve os conceitos básicos da autenticação do usuário para seu aplicativo habilitado para RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como adicionar autenticação ao seu aplicativo

Este tópico descreve os conceitos básicos da autenticação do usuário para seu aplicativo habilitado para RMS.

## O que é a autenticação de usuário
Autenticação de usuário é uma etapa essencial para estabelecer a comunicação entre o aplicativo do dispositivo e a infraestrutura de RMS. Esse processo de autenticação usa o protocolo OAuth 2.0 padrão, que exige as informações a seguir sobre o usuário atual e sua solicitação de autenticação; **autoridade**, **recursos** e **userId**.

**Observação** O escopo não é usado atualmente, mas pode ser e, portanto, é reservado para uso futuro.

 

**Retorno de chamada de autenticação de usuário** - O Microsoft Rights Management SDK 4.2 usará sua implementação de um retorno de chamada de autenticação quando você não fornecer um token de acesso, quando o token de acesso precisar ser atualizado ou quando o token de acesso expirar.

Cada uma das APIs de RMS da plataforma tem um retorno de chamada que deve ser implementado a fim de permitir a autenticação do usuário.

-   A API do Android usa as interfaces [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) e [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java).
-   A API do iOS/OS X usa o protocolo [**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc).
-   A API do WinPhone usa a interface [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback).
-   A API do Linux usa a interface [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

## Qual biblioteca usar para a autenticação

Para implementar o retorno de chamada da autenticação, você precisará baixar uma biblioteca apropriada e configurar seu ambiente de desenvolvimento para usá-la. Você encontrará as bibliotecas ADAL para essas plataformas no GitHub. Cada um dos recursos a seguir contém instruções para configurar seu ambiente e usar a biblioteca.

-   [ADAL (Windows Azure Active Directory Authentication Library) para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [ADAL (Windows Azure Active Directory Authentication Library) para Mac](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [ADAL (Windows Azure Active Directory Authentication Library) para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [ADAL (Windows Azure Active Directory Authentication Library) para dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Para o SDK do Linux, a biblioteca ADAL acompanha a fonte do SDK, disponível no [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

**Observação** Recomendamos o uso de uma das ADAL (Active Directory Authentication Libraries) acima, mas você pode usar outras bibliotecas de autenticação.

## Entradas para a autenticação com a ADAL (Azure Active Director Authentication Library)

A ADAL exige vários parâmetros para autenticar um usuário no Azure RMS (ou AD RMS). São os parâmetros padrão do OAuth 2.0, que geralmente são necessários para qualquer aplicativo do Azure AD, assim como em aplicativos habilitados para RMS. Encontre as diretrizes atuais sobre o uso da ADAL no arquivo LEIAME nos repositórios correspondentes do Github, listados anteriormente.

Essas diretrizes e parâmetros são necessários para os fluxos de trabalho do RMS:

-   **Autoridade** – a URL do ponto de extremidade de autenticação, normalmente AAD ou ADFS. Esse parâmetro é fornecido ao seu aplicativo pelo retorno de chamada de autenticação do RMS SDK.
-   **Recursos** - a URL/URI do aplicativo de serviço que você está tentando acessar, normalmente Azure RMS ou AD RMS. Esse parâmetro é fornecido ao seu aplicativo pelo retorno de chamada de autenticação do RMS SDK.
-   **Id de usuário** – o UPN, normalmente o endereço de email, do usuário que deseja acessar o aplicativo. Esse parâmetro pode estar vazio se o usuário ainda não for conhecido, e também é usado para armazenamento em cache do token do usuário ou para solicitar um token do cache. Também é usado normalmente como uma "dica" para uma solicitação ao usuário.
-   **Id do Cliente** – a ID do aplicativo cliente. Deve ser uma ID de aplicativo válida do Azure AD. Para saber mais, confira Como obter uma ID de aplicativo do Azure.
-   **Uri de redirecionamento** – fornece a biblioteca de autenticação com um URI de destino para o código de autenticação. Observe que iOS e Android exigem formatos específicos, explicados nos arquivos LEIAME dos repositórios correspondente do ADAL no GitHub.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

**Observação** Se o seu aplicativo não seguir essas diretrizes, os fluxos de trabalho do Azure RMS e do Azure AD provavelmente falharão e não terão o suporte do Microsoft.com. Além disso, o RMLA (Contrato de licença de gerenciamento de direitos) pode ser violado se uma Id de Cliente inválida for usada em um aplicativo de produção.

## Qual deve ser a aparência da implementação de um retorno de chamada de autenticação

**Exemplos de código de autenticação** - Este SDK tem exemplos de código mostrando o uso de retornos de chamada de autenticação. Para sua conveniência, esses exemplos de código estão representados aqui e também em cada um dos tópicos vinculados a seguir.

**Autenticação de usuário do Android** - para saber mais, confira [Exemplos de código do Android](android-code.md), **Etapa 2** do primeiro cenário, "Consumo de um arquivo RMS protegido".


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**Autenticação de usuário do iOS/OS X** - para saber mais, confira [Exemplos de código de iOS/OS X](ios-os-x-code-examples.md),

**Etapa 2** do primeiro cenário, "Consumo de um arquivo RMS protegido".


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Autenticação de usuário do Linux/C++** - para saber mais, confira [Exemplos de código de Linux](linux-c-code-examples.md)



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }



 

 


<!--HONumber=Apr16_HO4-->


