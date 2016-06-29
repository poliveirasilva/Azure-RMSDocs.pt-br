---
# required metadata

title: Configurar o Azure RMS para autenticação ADAL | Azure RMS
description: Descreve os passos para configurar a autenticação baseada no Azure ADAL
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

# Configurar o Azure RMS para autenticação ADAL

Este tópico descreve os passos para configurar a autenticação baseada no Azure ADAL.

## Configuração da Autenticação Azure

Será necessário o seguinte:

- Uma [subscrição do Microsoft Azure](https://azure.microsoft.com/en-us/) (uma avaliação gratuita é suficiente). Para obter mais informações, consulte o artigo [Como iniciar sessão no RMS para utilizadores](../understand-explore/rms-for-individuals-user-sign-up.md)
- Uma subscrição do Microsoft Azure Rights Management (uma conta [RMS para Indivíduos](https://technet.microsoft.com/en-us/library/dn592127.aspx) gratuita é suficiente).

> [!NOTE] Pergunte ao seu Administrador de TI se possui ou não uma subscrição do Microsoft Azure Rights Management e, em seguida, peça ao Administrador de TI para realizar os passos abaixo. Se a sua organização não tiver uma subscrição, deve pedir ao seu administrador de TI para criar uma. Além disso, o Administrador de TI deve subscrever com uma conta *Escolar ou profissional*, em vez de uma *conta Microsoft* (por exemplo, Hotmail).

Após a inscrição no Microsoft Azure:

- Inicie sessão no [Portal de Gestão do Azure](https://manage.windowsazure.com) para a organização que utiliza uma conta com privilégios administrativos.

![Início de sessão no Azure](../media/AzurePortalLogin.png)

- Navegue para baixo até à aplicação do **Active Directory**, no lado esquerdo do portal.

![Selecionar Active Directory](../media/AzureADPick.png)

- Se ainda não tiver criado um diretório, escolha o botão **Novo**, situado no canto inferior esquerdo do portal.

![Selecionar NOVO](../media/AzureNewBtn.png)

- Selecione o separador **Rights Management** e certifique-se de que o **Estado do Rights Management** é **Ativo**, **Desconhecido** ou **Não Autorizado**. Se o estado for **Inativo**, escolha o botão **Ativar** ,na parte inferior central do portal, e confirme a seleção.

![Escolher ATIVAR](../media/RMTab.png)

- Agora, crie uma nova *Aplicação Nativa* no diretório ao selecionar o diretório e ao escolher Aplicações.

![Selecionar APLICAÇÕES](../media/CreateNativeApp.png)

- Em seguida, escolha o botão **Adicionar** situado na parte inferior central do portal.

![Selecionar ADICIONAR](../media/AddAppBtn.png)

- Na linha de comandos, escolha **Adicionar uma aplicação que a minha organização está a desenvolver**.

![Selecionar Adicionar uma aplicação que a minha organização está a desenvolver](../media/AddAnAppPick.png)

- Atribua um nome à aplicação ao selecionar **APLICAÇÃO CLIENTE NATIVA** e escolher o botão **Seguinte**.

![Atribuir um nome à aplicação](../media/TellUsInput.png)

- Adicione um URI de redirecionamento e selecione seguinte.
  O URI redirecionamento tem de ser um URI válido e exclusivo para o seu diretório. Por exemplo, pode utilizar algo como `com.mycompany.myapplication://authorize`.

![Adicionar URI de redirecionamento](../media/RedirectURI.png)

- Selecione a aplicação no diretório e escolha **CONFIGURAR**.

![Escolher CONFIGURAR](../media/ConfigYourApp.png)

>[!NOTE] Copie a **ID DE CLIENTE** e o **URI DE REDIRECIONAMENTO** e armazene-os para utilização futura quando configurar o cliente RMS.

- Navegue até à parte inferior das definições da aplicação e escolha o botão **Adicionar aplicação** em **permissões para outras aplicações**.

>[!NOTE] As **Permissões de Delegado** apresentadas para o Windows Azure Active Directory estão corretas por predefinição – deve ser selecionada apenas a opção **Iniciar sessão e ler o perfil de utilizador**.

![Selecionar Adicionar aplicação](../media/PermissionsToOtherBtn.png)

- Agora, adicione este GUID `00000012-0000-0000-c000-000000000000` à caixa de edição **QUE INICIE COM** e selecione o botão de verificação.

![Adicionar GUID](../media/AddGUID.png)

- Selecione o sinal de adição junto de **Microsoft Rights Management**.

![Selecionar o botão +](../media/ChoosePlusBtn.png)

- Agora, selecione a marca de verificação situada no canto inferior esquerdo da caixa de diálogo.

![Escolher a marca de verificação](../media/ChooseCheck.png)

- Está agora preparado para adicionar uma dependência à sua aplicação do Azure RMS. Para adicionar a dependência, selecione a nova entrada do **Microsoft Rights Management Services** em **permissões para outras aplicações** e escolha a caixa de verificação **Criar e aceder a conteúdo protegido para utilizadores** na pasta de depósito **Permissões delegadas:**.

![Permissões de configuração](../media/AddDependency.png)

- Guarde a aplicação para manter as alterações escolhendo o ícone **Guardar** situado na parte inferior central do portal.

![Selecionar GUARDAR](../media/SaveApplication.png)


<!--HONumber=Jun16_HO2-->


