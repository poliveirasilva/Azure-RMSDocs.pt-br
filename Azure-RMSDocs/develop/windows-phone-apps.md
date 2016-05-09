---
# required metadata

title: Configuração do Windows Phone | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71119aa7-ffc6-46e0-82ae-0b3b614c2cad

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Configuração do Windows Phone


Os aplicativos do Windows Phone podem usar o Microsoft Rights Management SDK 4.2 para habilitar a proteção integrada de informações em seus aplicativos usando o AAD RM (Azure Active Directory Rights Management).

Este tópico orientará você pela configuração de seu ambiente para criação de seus próprios aplicativos novos.

-   [Pré-requisitos](#prerequisites)
-   [Configurando o ambiente de desenvolvimento](#configuring_your_development_environment)
-   [Consulte também](#see_also)

## Pré-requisitos


Você deve ter o seguinte software em seu sistema de desenvolvimento:

-   O sistema operacional [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet).
-   [Ferramentas de desenvolvimento (SDK) do Windows Phone 8.1](http://dev.windowsphone.com/en-us/downloadsdk)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) ou posterior, ou o Visual Studio Express 2012, que está incluído no Windows Phone SDK 8.0/8.1
-   O pacote do MS RMS SDK 4.2 para Windows Phone. Para obter mais informações, consulte [Introdução](get-started.md).
-   Biblioteca de autenticação: recomendamos o uso da [Biblioteca de Autenticação do Azure AD](https://msdn.microsoft.com/en-us/library/jj573266.aspx), e outras bibliotecas de autenticação podem ser usadas.

Leia o tópico [Novidades](release-notes.md) para saber mais sobre as atualizações de API, informações sobre ambientes e dispositivos, notas de versão e perguntas frequentes.

Examine as informações no [guia de desenvolvimento do Windows Phone](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx) no Centro de Desenvolvimento do Windows Phone.

## Configurando o ambiente de desenvolvimento


-   Abra o *Visual Studio*.
-   Clique em **Arquivo**. No menu **Arquivo**, clique em **Novo** e em **Projeto**.
-   Na caixa de diálogo **Novo Projeto**, selecione **Visual C#** e selecione **Aplicativo em branco (Windows Phone)**; em seguida, clique em **OK**.

    ![](../media/wpsetup-newproj.png)

-   No Gerenciador de Soluções, clique com o botão direito do mouse em seu projeto e selecione **Adicionar Referência** para abrir a caixa de diálogo **Adicionar Referência**.

    ![](../media/wpsetup-addref.png)

-   Clique em **Procurar** na caixa de diálogo **Adicionar Referência** e selecione o arquivo *Microsoft.RightsManagment.dll* que está localizado na pasta em que você extraiu o pacote.
-   **Aplicativos gerenciados** - para compilar um aplicativo gerenciado, você precisará adicionar essa referência; selecione **Windows 8.1**-&gt;**Extensões** e marque a caixa **Pacote de tempo de execução do Windows Visual C++ para Windows**

    ![](../media/wpsetup-refmngr.png)

-   **Adicionando funcionalidades** - seu aplicativo precisará da funcionalidade de "Internet (cliente e servidor)" para usar o SDK. Para adicionar essa funcionalidade ao seu aplicativo, abra o arquivo *Package.appxmanifest* no projeto e navegue até a guia **Funcionalidades** para adicionar.

Agora você está pronto para criar seus próprios aplicativos novos do Windows Phone.

### Consulte também

[Introdução](get-started.md)

[Novidades](release-notes.md)

[Conceitos básicos](core-concepts.md)

[Desenvolvimento do Windows Phone](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)

[Referência de API do Windows](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows Phone SDK](http://dev.windowsphone.com/en-us/downloadsdk)

 

 





<!--HONumber=Apr16_HO3-->


