---
title: "Configurar o Azure RMS para autenticação de ADAL | Azure RMS"
description: "Descreve as etapas para configurar a autenticação baseada no Azure ADAL"
keywords: "autenticação, RMS, ADAL"
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
ms.sourcegitcommit: 56d0538243af49580f24c701ad5097b30f3059b0
ms.openlocfilehash: 9b912a2a66838dc6e6a3b227bcfe4ac589fe06c1


---

# Configurar o Azure RMS para autenticação de ADAL

Este tópico descreve as etapas para configurar a autenticação baseada no Azure ADAL.

## Instalação da Autenticação do Azure

Você precisará do seguinte:

- Uma [assinatura do Microsoft Azure](https://azure.microsoft.com/en-us/) (uma avaliação gratuita é suficiente). Para obter mais informações, consulte [How users sing up for RMS for individuals](../understand-explore/rms-for-individuals-user-sign-up.md) (Como usuários se inscrevem no RMS para as pessoas)
- Uma assinatura do Microsoft Azure Rights Management (uma conta gratuita [RMS para pessoas físicas](https://technet.microsoft.com/en-us/library/dn592127.aspx) é suficiente).

> [!NOTE] 
> Pergunte ao seu administrador de TI se você tem ou não uma assinatura do Microsoft Azure Rights Management e peça que ele execute as etapas abaixo. Se sua organização não tiver uma assinatura, peça que o administrador de TI crie uma. Além disso, seu administrador de TI deve assinar com uma *Conta corporativa ou de estudante*, em vez de uma *Conta da Microsoft* (por exemplo, Hotmail).

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

- Adicione um URI de redirecionamento e escolha Avançar.
  O redirecionamento de URI deve ser um URI válido e exclusivo do diretório. Por exemplo, você pode usar algo como `com.mycompany.myapplication://authorize`.

![Adicionar URI de redirecionamento](../media/RedirectURI.png)

- Selecione seu aplicativo no diretório e escolha **CONFIGURAR**.

![Escolher CONFIGURAR](../media/ConfigYourApp.png)

>[!NOTE] 
> Copie a **ID DO CLIENTE** e a **URI de REDIRECIONAMENTO** e armazene-os para uso futuro ao configurar o cliente RMS.

- Navegue até a parte inferior das configurações do aplicativo e escolha o botão **Adicionar aplicativo** em **Permissões para outros aplicativos**.

>[!NOTE] 
> As **Permissões Delegadas** que são mostradas para o Microsoft Azure Active Directory estão corretas por padrão – somente uma opção deve ser selecionada e essa opção é **Entrar e ler o perfil do usuário**.

![Selecionar Adicionar aplicativo](../media/PermissionsToOtherBtn.png)

- Agora, adicione esse GUID `00000012-0000-0000-c000-000000000000` à caixa de edição **COMEÇANDO COM** e escolha o botão de seleção.

![Adicionar GUID](../media/AddGUID.png)

- Escolha o sinal de mais ao lado de **Microsoft Rights Management**.

![Selecionar o botão +](../media/ChoosePlusBtn.png)

- Agora, escolha a marca de seleção localizada no canto inferior esquerdo da caixa de diálogo.

![Escolher a marca de seleção](../media/ChooseCheck.png)

- Agora você está pronto para adicionar uma dependência ao seu aplicativo para o Azure RMS. Para adicionar a dependência, selecione a nova entrada **Microsoft Rights Management Services** em **permissões para outros aplicativos** e marque a caixa de seleção **Criar e acessar conteúdo protegido para usuários** na caixa suspensa **Permissões Delegadas:**.

![Configurar permissões](../media/AddDependency.png)

- Salve seu aplicativo para manter as alterações, escolhendo o ícone **Salvar** localizado na parte inferior, na região central do portal.

![Selecionar SALVAR](../media/SaveApplication.png)



<!--HONumber=Jul16_HO3-->


