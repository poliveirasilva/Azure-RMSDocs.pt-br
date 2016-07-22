---
title: "Transferir e instalar a aplicação de partilha Rights Management | Azure RMS"
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

# Transferir e instalar a aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Não é necessário ser um administrador local para instalar a aplicação de partilha RMS. No entanto, se não for e utilizar o Office 2010, existem algumas limitações. Para obter mais informações, consulte a secção [Se não for um administrador local e utilizar o Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) nesta página.

## Para transferir e instalar a aplicação de partilha Rights Management

1.  Aceda à página do [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) no site da Microsoft.

2.  Na secção **Computadores**, clique no ícone da **aplicação RMS para Windows** e guarde o ficheiro **Setup.exe** para instalar a aplicação de partilha Microsoft Rights Management.

3.  Faça duplo clique no ficheiro Setup.exe transferido. Se lhe for pedido para continuar, clique em **Sim**.

4.  Na página **Configurar o Microsoft RMS**, clique em **Seguinte** e aguarde até que a instalação esteja concluída.

    > [!NOTE]
    > A aplicação de partilha RMS requer o Microsoft .NET Framework, versão mínima 4.0. A configuração verifica se isto foi instalado e, em caso negativo, verá uma mensagem com uma ligação para a instalação.

5.  Quando a instalação estiver concluída, clique em **Reiniciar** para reiniciar o computador e concluir a instalação. Em alternativa, pode clicar em **Fechar** e reiniciar o computador mais tarde para concluir a instalação.

Agora, está pronto para começar a proteger os ficheiros ou ler ficheiros que outras pessoas protegeram.

## Se não for um administrador local e utilizar o Office 2010
Se iniciar sessão no computador e não tiver direitos administrativos locais e a Configuração detetar que tem o Office 2010 instalado, verá uma mensagem de aviso a indicar que alguns cenários não funcionarão com esta configuração. Os cenários são:

-   Se a sua organização utilizar o Azure RMS em vez de uma versão no local do RMS:

    -   As funcionalidades da Gestão de Direitos de Informação (IRM) do Office não estarão disponíveis. Por exemplo, a opção **Não Reencaminhar** para e-mails e as permissões **Restringir Acesso** que pode definir no menu **Ficheiro** no Word e Excel. Pode utilizar a opção Partilhar Protegido no friso e as opções de clique com o botão direito do rato do Explorador de Ficheiros.

-   Se a sua organização utilizar uma versão no local do RMS em vez do Azure RMS:

    -   Não será possível ler um documento protegido que lhe foi enviado por alguém de outra organização que esteja a utilizar o Azure RMS.

Se não for um administrador local e utilizar o Office 365 ou Office 2013, não verá esta mensagem e estes cenários serão suportados.

Pode continuar a instalação com estas limitações conhecidas. Em alternativa, pode interromper a instalação e voltar a executá-la com a opção **Executar como administrador** quando executar Setup.exe no passo 3 ou pedir a um administrador que o instale por si. Os administradores podem [efetuar o script desta instalação](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application) para instalar automaticamente.

## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, veja as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)




<!--HONumber=Jun16_HO4-->


