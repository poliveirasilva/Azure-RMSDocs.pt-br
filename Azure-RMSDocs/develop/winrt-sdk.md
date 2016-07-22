---
title: "Configuração da Loja Windows | Azure RMS"
description: "As aplicações da Loja Windows podem utilizar o SDK Microsoft Rights Management 4.2 para ativar a proteção de informações integrada na respetiva aplicação."
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
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 0b8e0fb6d872506ac3529bd137286f0e8fa562ee


---

# Configuração da Loja Windows

As aplicações da Loja Windows podem utilizar o SDK Microsoft Rights Management 4.2 para ativar a proteção de informações integrada na respetiva aplicação utilizando o Azure Active Directory Rights Management (AAD RM).

Este tópico descreve como configurar o ambiente para criar as suas novas aplicações.

-   [Pré-requisitos](#prerequisites)
-   [Opcional](#optional)
-   [Configurar o ambiente de desenvolvimento](#configuring-your-development-environment)
-   [Consulte Também](#see-also)

## Pré-requisitos


Tem de possuir o seguinte software no sistema de desenvolvimento:

-   O sistema operativo [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet)
-   O [Windows SDK para Windows 8.1](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) ou superior, ou Visual Studio Express 2012, que está incluído no Windows SDK para Windows 8.0/8.1
-   O pacote do SDK MS RMS 4.2 para Aplicações da Loja Windows. Para obter mais informações, consulte [Introdução](get-started.md).
-   Biblioteca de autenticação: recomendamos que utilize a [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/en-us/library/jj573266.aspx), mas é possível utilizar outras bibliotecas de autenticação.

Consulte o tópico [Novidades](release-notes.md) para obter informações acerca de atualizações de API, informações de dispositivos e de ambiente, notas de versão e perguntas mais frequentes (FAQ).

## Opcional

A nossa biblioteca da interface de utilizador fornece uma IU reutilizável para operações de consumo e proteção para programadores que não pretendem criar a sua IU personalizada – [Biblioteca da IU para aplicações da Loja Windows](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore). Fornecemos também uma aplicação de exemplo de aplicação da Loja Windows – [Aplicação de exemplo do RMS para a Loja Windows](https://github.com/AzureADSamples/rms-samples-for-windowsstore).

## Configurar o ambiente de desenvolvimento


-   Abra o Visual Studio.
-   Clique em **Ficheiro**, clique em **Novo** e, em seguida, em **Projeto**.
-   Na caixa de diálogo **Novo Projeto**, clique em **Visual C\#** e selecione **Aplicação em Branco (Windows)** e, em seguida, clique em **OK**.

    ![Criar novo projeto](../media/winrtsetup-newproj.png)

-   No **Explorador de Soluções**, clique com o botão direito do rato no projeto e selecione **Adicionar Referência** para abrir a caixa de diálogo **Adicionar Referência**.

    ![Adicionar referência](../media/winrtsetup-addref.png)

-   Na caixa de diálogo **Adicionar Referência**, clique em **Procurar** e selecione o ficheiro *Microsoft.RightsManagment.dll*, situado na pasta da qual extraiu o pacote SDK.
-   **Aplicações Geridas** – Para criar uma aplicação gerida, terá de adicionar esta referência; selecione **Windows 8.1**-&gt;**Extensões** e marque a caixa de **Pacote do Windows Visual C++ Runtime para Windows**

    ![Adicionar extensões](../media/winrtsetup-refmngr.png)

-   **Adicionar Capacidades** – A sua aplicação necessitará da capacidade “Internet (Cliente e Servidor)” para utilizar o SDK. Para adicionar esta capacidade à sua aplicação, abra o ficheiro *Package.appxmanifest* no projeto e navegue para o separador **Capacidades** a adicionar.

Agora, está pronto para criar as suas novas aplicações da Loja Windows.

### Consulte Também

[Introdução](get-started.md)

[Novidades](release-notes.md)

[Conceitos e termos de programação](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Referência da API do Windows](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)



<!--HONumber=Jul16_HO2-->


