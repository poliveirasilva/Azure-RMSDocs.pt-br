---
# required metadata

title: Configuração do Windows Phone | Azure RMS
description: As aplicações do Windows Phone podem utilizar o SDK Microsoft Rights Management 4.2 para ativar a proteção de informações integrada na respetiva aplicação.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuração do Windows Phone


As aplicações do Windows Phone podem utilizar o SDK Microsoft Rights Management 4.2 para ativar a proteção de informações integrada na respetiva aplicação utilizando o Azure Active Directory Rights Management (AAD RM).

Este tópico descreve como configurar o ambiente para criar as suas novas aplicações.

-   [Pré-requisitos](#prerequisites)
-   [Configurar o ambiente de desenvolvimento](#configuring_your_development_environment)
-   [Consulte Também](#see_also)

## Pré-requisitos


Tem de possuir o seguinte software no sistema de desenvolvimento:

-   O sistema operativo [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet).
-   [Ferramentas de Desenvolvimento do Windows Phone 8.1 (SDK)](http://dev.windowsphone.com/en-us/downloadsdk)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) ou superior, ou Visual Studio Express 2012, que está incluído no Windows Phone SDK 8.0/8.1
-   O pacote do SDK MS RMS 4.2 para Windows Phone. Para obter mais informações, consulte [Introdução](get-started.md).
-   Biblioteca de autenticação: recomendamos que utilize a [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/en-us/library/jj573266.aspx), mas é possível utilizar outras bibliotecas de autenticação.

Consulte o tópico [Novidades](release-notes.md) para obter informações acerca de atualizações de API, informações de dispositivos e de ambiente, notas de versão e perguntas mais frequentes (FAQ).

Reveja as informações no guia de [desenvolvimento do Windows Phone](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx) no Windows Phone Dev Center.

## Configurar o ambiente de desenvolvimento


-   Abra o *Visual Studio*.
-   Clique em **Ficheiro**. No menu **Ficheiro**, clique em **Novo** e, em seguida, em **Projeto**.
-   Na caixa de diálogo **Novo Projeto**, selecione **Visual C\#**, selecione **Aplicação em Branco (Windows Phone)** e, em seguida, clique em **OK**.

    ![Criar novo projeto](../media/wpsetup-newproj.png)

-   No Explorador de Soluções, clique com o botão direito do rato no projeto e, em seguida, selecione **Adicionar Referência** para abrir a caixa de diálogo **Adicionar Referência**.

    ![Adicionar referência](../media/wpsetup-addref.png)

-   Clique em **Procurar** na parte inferior esquerda da caixa de diálogo **Adicionar Referência** e selecione o ficheiro *Microsoft.RightsManagment.dll*, situado na pasta da qual extraiu o pacote.
-   **Aplicações Geridas** – Para criar uma aplicação gerida, terá de adicionar esta referência; selecione **Windows 8.1**-&gt;**Extensões** e marque a caixa de **Pacote do Windows Visual C++ Runtime para Windows**

    ![Adicionar extensões](../media/wpsetup-refmngr.png)

-   **Adicionar Capacidades** – A sua aplicação necessitará da capacidade “Internet (Cliente e Servidor)” para utilizar o SDK. Para adicionar esta capacidade à sua aplicação, abra o ficheiro *Package.appxmanifest* no projeto e navegue para o separador **Capacidades** a adicionar.

Agora, está pronto para criar as suas novas aplicações do Windows Phone.

### Consulte Também

[Introdução](get-started.md)

[Novidades](release-notes.md)

[Conceitos principais](core-concepts.md)

[Desenvolvimento do Windows Phone](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)

[Referência da API do Windows](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows Phone SDK](http://dev.windowsphone.com/en-us/downloadsdk)

 

 





<!--HONumber=May16_HO2-->


