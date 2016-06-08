---
# required metadata

title: Autenticação ADAL para seu aplicativo habilitado para RMS | Azure RMS
description: Descreve o processo de autenticação com ADAL
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
** Este conteúdo do SDK não é atual. Por um curto período, encontre a [versão atual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) da documentação no MSDN. **
# Autenticação ADAL para seu aplicativo habilitado para RMS

Autenticação com Azure RMS para seu aplicativo usando o Azure ADAL, agora é parte do cliente RMS 2.1.

Ao atualizar seu aplicativo para usar a autenticação ADAL em vez do Assistente de Conexão do Microsoft Online, você e seus clientes poderão:

- Usar a autenticação multifator
- Instalar o cliente do RMS 2.1 sem exigir privilégios administrativos no computador
- Certificar o aplicativo para o Windows 10

## Duas abordagens de autenticação

Este tópico contém duas abordagens de autenticação com exemplos de código correspondentes.

- **Autenticação interna** -autenticação OAuth gerenciada pelo RMS SDK. Use essa abordagem se quiser que o cliente RMS exiba um prompt de autenticação ADAL quando a autenticação for necessária. Para obter detalhes sobre como configurar seu aplicativo, consulte a seção "Autenticação interna".

> [!NOTE] Se seu aplicativo usa atualmente o AD RMS SDK 2.1 com o assistente de conexão, é recomendável que você use o método de autenticação interna como o caminho de migração do aplicativo.

- **Autenticação externa** -autenticação OAuth gerenciada pelo seu aplicativo. Use essa abordagem se quiser que seu aplicativo para gerenciar sua própria autenticação OAuth. Com essa abordagem, o cliente RMS usará um retorno de chamada definido pelo aplicativo quando a autenticação for necessária. Para obter um exemplo detalhado, consulte "Autenticação externa" no final deste tópico.

> [!NOTE] Autenticação externa não implica a capacidade de alterar usuários. o cliente RMS sempre usa o usuário padrão para determinado locatário do RMS.

### Autenticação interna

Você precisará do seguinte:

- Um [assinatura do Microsoft Azure](https://azure.microsoft.com/en-us/) (uma avaliação gratuita é suficiente):
- Uma assinatura do Microsoft Azure Rights Management (uma conta gratuita [RMS para pessoas físicas](https://technet.microsoft.com/en-us/library/dn592127.aspx) é suficiente).

> [!NOTE] Pergunte ao seu administrador de TI se você tem ou não uma assinatura do Microsoft Azure Rights Management e peça que ele execute as etapas abaixo. Se sua organização não tiver uma assinatura, peça que o administrador de TI crie uma. Além disso, seu administrador de TI deve assinar com uma conta corporativa ou de estudante, em vez de uma conta da Microsoft (por exemplo, Hotmail).

Após inscrever-se no Microsoft Azure:

- Faça logon no [Portal de Gerenciamento do Azure](https://manage.windowsazure.com) de sua organização usando uma conta com privilégios administrativos.

![Logon no Azure](../media/AzurePortalLogin.png)

- Navegue até o aplicativo **Active Directory** no lado esquerdo do portal.

![Selecionar o Active Directory](../media/AzureADPick.png)

- Se você ainda não tiver criado um diretório, escolha o botão **Novo** localizado no canto inferior esquerdo do portal.

![Selecionar NOVO](../media/AzureNewBtn.png)

- Selecione a guia **Rights Management** e verifique se o **Status do Rights Management** é **Ativo**, **Desconhecido** ou **Não autorizado**. Se o status for **Inativo**, escolha o botão **Ativar** na parte inferior, na região central do portal, e confirme sua seleção.

![Escolher ATIVAR](../media/RMTab.png)

- Agora, crie um novo *Aplicativo nativo* em seu diretório, selecionando o diretório e escolhendo Aplicativos.

![Selecionar APLICATIVOS](../media/CreateNativeApp.png)

- Escolha o botão **ADICIONAR** botão localizado na parte inferior, na região central do portal.

![Selecionar ADICIONAR](../media/AddAppBtn.png)

- No prompt, escolha **Adicionar um aplicativo que minha organização está desenvolvendo**.

![Selecione Adicionar um aplicativo que minha organização está desenvolvendo](../media/AddAnAppPick.png)

- Nomeie o aplicativo selecionando **APLICATIVO CLIENTE NATIVO** e escolhendo o botão **AVANÇAR**.

![Nomear seu aplicativo](../media/TellUsInput.png)

- Adicione um URI de redirecionamento e escolha Avançar. O redirecionamento de URI deve ser um URI válido e exclusivo do diretório. Por exemplo, você pode usar algo como `com.mycompany.myapplication://authorize`.

![Adicionar URI de redirecionamento](../media/RedirectURI.png)

- Selecione seu aplicativo no diretório e escolha **CONFIGURAR**.

![Escolher CONFIGURAR](../media/ConfigYourApp.png)

>[!NOTE] Copie a **ID DO CLIENTE** e a **URI de REDIRECIONAMENTO** e armazene-os para uso futuro ao configurar o cliente RMS.

- Navegue até a parte inferior das configurações do aplicativo e escolha o botão **Adicionar aplicativo** em **Permissões para outros aplicativos**.

![Selecionar Adicionar aplicativo](../media/PermissionsToOtherBtn.png)

- Agora, adicione esse GUID `00000012-0000-0000-c000-000000000000` à caixa de edição **COMEÇANDO COM** e escolha o botão de seleção.

![Adicionar GUID](../media/AddGUID.png)

- Escolha o sinal de mais (+) ao lado de **Microsoft Rights Management**.

![Selecionar o botão +](../media/ChoosePlusBtn.png)

- Agora, escolha a marca de seleção localizada no canto inferior esquerdo da caixa de diálogo.

![Escolher a marca de seleção](../media/ChooseCheck.png)

- Agora você está pronto para adicionar uma dependência ao seu aplicativo para o Azure RMS. Para adicionar a dependência, selecione a nova entrada **Microsoft Rights Management Services** em **permissões para outros aplicativos** e marque a caixa de seleção **Criar e acessar conteúdo protegido para usuários** na caixa suspensa **Permissões Delegadas:**.

![Configurar permissões](../media/AddDependency.png)

- Salve seu aplicativo para manter as alterações, escolhendo o ícone **SALVAR** localizado na parte inferior, na região central do portal.

![Selecionar SALVAR](../media/SaveApplication.png)

- Agora você está pronto para configurar seu aplicativo para usar a autenticação interna do ADAL fornecido pelo RMS SDK 2.1. Para configurar o cliente RMS, adicione uma chamada a [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) logo após a chamada a [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) para configurar o cliente RMS. Use o trecho de código a seguir como exemplo.


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### Autenticação externa

- Use esse código como um exemplo de como gerenciar seus próprios tokens de autenticação.


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey) { IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT { wstring wstrToken; HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken); return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr; };

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
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### Tópicos relacionados
- [Tipos de dados](/rights-management/sdk/2.1/api/win/Data%20types)
- [Propriedades de ambiente](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=Jun16_HO1-->


