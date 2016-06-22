---
# required metadata

title: Como registrar e habilitar seu aplicativo para RMS com o Azure AD | Azure RMS
description: Descreve os conceitos básicos da autenticação do usuário para seu aplicativo habilitado para RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 06/15/2016
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

# Como registrar e habilitar seu aplicativo para RMS com o Azure AD

Este tópico o orientará sobre os fundamentos de registro do aplicativo e a habilitação de RMS por meio do portal do Azure seguido por autenticação do usuário com a ADAL (Azure Active Directory Authentication Library).

## O que é a autenticação de usuário
Autenticação de usuário é uma etapa essencial para estabelecer a comunicação entre o aplicativo do dispositivo e a infraestrutura de RMS. Esse processo de autenticação usa o protocolo OAuth 2.0 padrão, que requer informações importantes sobre o usuário atual e a solicitação de autenticação.

## Registro por meio do portal do Azure
Comece seguindo este guia para configurar o registro do seu aplicativo por meio do portal do Azure, [Configure Azure RMS for ADAL authentication](adal-auth.md) (Configurar o Azure RMS para autenticação da ADAL). Certifique-se de copiar e salvar a **ID do Cliente** e o **URI de Redirecionamento** desse processo para uso posterior.

## Implementar autenticação de usuário para seu aplicativo
Cada API do RMS tem um retorno de chamada que deve ser implementado para habilitar a autenticação do usuário. O RMS SDK 4.2 então usará sua implementação do retorno de chamada quando você não fornecer um token de acesso, quando seu token de acesso precisar ser atualizado ou quando o token de acesso tiver expirado.

- Android – interfaces de [AuthenticationRequestCallback](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) e [AuthenticationCompletionCallback](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java).
- iOS/OS X – protocolo [MSAuthenticationCallback](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc).
-  Windows Phone/Windows RT – interface [IAuthenticationCallback](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback).
- Linux – interface [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

### Qual biblioteca usar para a autenticação
Para implementar o retorno de chamada da autenticação, você precisará baixar uma biblioteca apropriada e configurar seu ambiente de desenvolvimento para usá-la. Você encontrará as bibliotecas ADAL para essas plataformas no GitHub.

Cada um dos recursos a seguir contém instruções para configurar seu ambiente e usar a biblioteca.

-   [ADAL (Windows Azure Active Directory Authentication Library) para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [ADAL (Windows Azure Active Directory Authentication Library) para Mac](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [ADAL (Windows Azure Active Directory Authentication Library) para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [ADAL (Windows Azure Active Directory Authentication Library) para dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Para o SDK do Linux, a biblioteca ADAL acompanha a fonte do SDK, disponível no [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

>[!NOTE]  É recomendável usar uma ADAL, embora você possa usar outras bibliotecas de autenticação.

### Parâmetros de autenticação

A ADAL exige várias informações para autenticar com sucesso um usuário para o Azure RMS (ou AD RMS). Esses são parâmetros padrão do OAuth 2.0 e geralmente são exigidos de qualquer aplicativo Azure AD. Você encontrará as diretrizes atuais para uso da ADAL no arquivo LEIAME dos repositórios do Github correspondentes, listados anteriormente.

- **Autoridade** – a URL do ponto de extremidade de autenticação, normalmente AAD ou ADFS.
- **Recursos** - a URL/URI do aplicativo de serviço que você está tentando acessar, normalmente Azure RMS ou AD RMS.
- **Id de usuário** – o UPN, normalmente o endereço de email, do usuário que deseja acessar o aplicativo. Esse parâmetro pode estar vazio se o usuário ainda não for conhecido, e também é usado para armazenamento em cache do token do usuário ou para solicitar um token do cache. Também costuma ser usado como uma *dica* para solicitação ao usuário.
- **Id do Cliente** – a ID do aplicativo cliente. Deve ser uma ID de aplicativo válida do Azure AD.
e vem da etapa de registro anterior por meio do portal do Azure.
- **Uri de redirecionamento** – fornece a biblioteca de autenticação com um URI de destino para o código de autenticação. Formatos específicos são necessários para iOS e Android. Eles são explicados nos arquivos README dos repositórios GitHub correspondentes da ADAL. Esse valor vem da etapa de registro anterior por meio do portal do Azure.

>[!NOTE] **Escopo** não é usado atualmente, mas pode ser, portanto, está reservado para uso futuro.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

>[!NOTE] Se o seu aplicativo não seguir essas diretrizes, os fluxos de trabalho do Azure RMS e do Azure AD provavelmente falharão e não terão suporte em Microsoft.com. Além disso, o RMLA (Contrato de licença de gerenciamento de direitos) pode ser violado se uma Id de Cliente inválida for usada em um aplicativo de produção.

### Qual deve ser a aparência da implementação de um retorno de chamada de autenticação
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


**Autenticação de usuário do iOS/OS X** – para saber mais, confira [iOS/OS X code examples](ios-os-x-code-examples.md) (Exemplos de código do iOS/OS X), *Etapa 2 do primeiro cenário, "Consumo de um arquivo RMS protegido".*


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



**Autenticação de usuário do Linux** – para saber mais, confira os [Linux code examples](linux-c-code-examples.md) (Exemplos de código do Linux).



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



 

 


<!--HONumber=Jun16_HO3-->


