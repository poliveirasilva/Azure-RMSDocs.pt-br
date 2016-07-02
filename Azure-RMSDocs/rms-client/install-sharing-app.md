---
title: Baixar e instalar o aplicativo de compartilhamento Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: 5ec740b4de63c90c9713916dcf104316e727498b


---

# Baixar e instalar o aplicativo Rights Management sharing

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Você não precisa ser administrador local para instalar o aplicativo RMS sharing. No entanto, se você não é administrador e usa o Office 2010, existem algumas limitações. Para obter mais informações, consulte a seção [Se você não for um administrador local e usar o Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) nesta página.

## Para baixar e instalar o aplicativo de compartilhamento do Rights Management

1.  Vá à página do [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) no site da Web da Microsoft.

2.  Na seção **Computadores** , clique no ícone do **aplicativo RMS para Windows** e salve o arquivo **Setup.exe** para instalar o aplicativo de compartilhamento Microsoft Rights Management.

3.  Clique duas vezes no arquivo Setup.exe que foi baixado. Se você for solicitado a continuar, clique em **Sim**.

4.  Na página de **Instalação do Microsoft RMS** clique em **Próximo**, e aguarde a conclusão da instalação.

    > [!NOTE]
    > O aplicativo RMS sharing requer o Microsoft .NET Framework versão mínima 4.0. A instalação verifica se ele está instalado e, se não estiver, você verá uma mensagem com um link para instalá-lo.

5.  Ao final da instalação, clique em **Reiniciar** para reiniciar o computador e concluir a instalação. Ou, clique em **Fechar** e reinicie o computador posteriormente para concluir a instalação.

Agora que a sua conta foi criada, você pode começar a proteger ou ler arquivos que outras pessoas protegeram.

## Se você não é um administrador local e usa o Office 2010
Se você entrar no seu computador e não tiver direitos administrativos locais, e a instalação detecta que você tem o Office 2010 instalado, verá uma mensagem de aviso de que alguns cenários não funcionarão com essa configuração. Esses cenários são:

-   Se sua organização usar o Azure RMS em vez de uma versão local do RMS:

    -   Os recursos do IRM (Gerenciamento de Direitos de Informação) do Office não estarão disponíveis. Por exemplo, a opção **Não Encaminhar** para emails e as permissões **Restringir Acesso** que você pode definir no menu **Arquivo** do Word e do Excel. Você pode usar a opção Compartilhamento Protegido na faixa de opções e as opções do botão direito do Explorador de Arquivos.

-   Se sua organização usa uma versão local do RMS em vez do Azure RMS:

    -   Você não pode ler um documento protegido enviado a você por alguém de outra organização que está usando o Azure RMS.

Se você não é um administrador local e usa o Office 365 ou Office 2013, você não vê essa mensagem e esses cenários são suportados.

Você pode continuar a instalação com essas limitações conhecidas. Ou você pode parar a instalação e executar novamente com a opção **Executar como administrador** ao executar Setup.exe na etapa 3, ou pedir para um administrador instalar para você. Os administradores podem [fazer o script desta instalação](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application) para você de modo que ela seja instalada automaticamente.

## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)




<!--HONumber=Jun16_HO4-->


