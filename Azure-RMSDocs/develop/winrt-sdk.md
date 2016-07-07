---
title: "Configuração da Windows Store | Azure RMS"
description: "Aplicativos Windows Store podem usar o Microsoft Rights Management SDK 4.2 para habilitar a proteção integrada de informações em seus aplicativos."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 0b8e0fb6d872506ac3529bd137286f0e8fa562ee


---

# Configuração da Windows Store

Os aplicativos da Windows Store podem usar o Microsoft Rights Management SDK 4.2 para habilitar a proteção integrada de informações em seus aplicativos usando o AAD RM (Azure Active Directory Rights Management).

Este tópico orientará você durante a configuração de seu ambiente para criação de seus próprios aplicativos novos.

-   [Pré-requisitos](#prerequisites)
-   [Opcional](#optional)
-   [Configurando o ambiente de desenvolvimento](#configuring-your-development-environment)
-   [Consulte também](#see-also)

## Pré-requisitos


Você deve ter o seguinte software em seu sistema de desenvolvimento:

-   O sistema operacional [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet)
-   O [SDK do Windows para Windows 8.1](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) ou posterior, ou o Visual Studio Express 2012, que está incluído no SDK do Windows para Windows 8.0/8.1.
-   O pacote do MS RMS SDK 4.2 para aplicativos da Windows Store. Para obter mais informações, consulte [Introdução](get-started.md).
-   Biblioteca de autenticação: recomendamos o uso da [Biblioteca de Autenticação do Azure AD](https://msdn.microsoft.com/en-us/library/jj573266.aspx), e outras bibliotecas de autenticação podem ser usadas.

Leia o tópico [Novidades](release-notes.md) para saber mais sobre as atualizações de API, informações sobre ambientes e dispositivos, notas de versão e perguntas frequentes.

## Opcional

Nossa biblioteca de interface de usuário fornece uma interface de usuário reutilizável para operações de consumo e proteção para desenvolvedores que não querem criar sua própria interface de usuário personalizada - [Biblioteca de interface do usuário para aplicativos da Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore). Nós também fornecemos um aplicativo de exemplo da Windows Store - [aplicativo RMS de exemplo da Windows Store](https://github.com/AzureADSamples/rms-samples-for-windowsstore).

## Configurando o ambiente de desenvolvimento


-   Abra o Visual Studio.
-   Clique em **Arquivo**, em **Novo** e em **Projeto**.
-   Na caixa de diálogo **Novo Projeto**, clique em **Visual C#\#** e selecione **Aplicativo em branco (Windows)**, em seguida, clique em **OK**.

    ![Criar novo projeto](../media/winrtsetup-newproj.png)

-   No **Gerenciador de Soluções**, clique com o botão direito do mouse em seu projeto e selecione **Adicionar Referência** para abrir a caixa de diálogo **Adicionar Referência**.

    ![Adicionar referência](../media/winrtsetup-addref.png)

-   Na caixa de diálogo **Adicionar Referência**, clique em **Procurar** e selecione o arquivo *Microsoft.RightsManagement.dll* que está localizado na pasta em que você extraiu o pacote SDK.
-   **Aplicativos gerenciados** - Para compilar um aplicativo gerenciado, você precisará adicionar essa referência; selecione **Windows 8.1**-&gt;**Extensões** e marque a caixa **Pacote de tempo de execução do Windows Visual C++ para Windows**

    ![Adicionar extensões](../media/winrtsetup-refmngr.png)

-   **Adicionando funcionalidades** - seu aplicativo precisará da funcionalidade de "Internet (cliente e servidor)" para usar o SDK. Para adicionar essa funcionalidade ao seu aplicativo, abra o arquivo *Package.appxmanifest* no projeto e navegue até a guia **Funcionalidades** para adicionar.

Agora você está pronto para criar seus próprios aplicativos novos da Windows Store.

### Consulte também

[Introdução](get-started.md)

[Novidades](release-notes.md)

[Termos e conceitos de desenvolvedor](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Referência de API do Windows](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)



<!--HONumber=Jun16_HO4-->


