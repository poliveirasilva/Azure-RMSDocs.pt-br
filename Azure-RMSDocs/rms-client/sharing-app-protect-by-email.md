---
title: "Proteger um ficheiro que partilha por e-mail ao utilizar a aplicação de partilha Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: ea7f186e01606ca5e487bdfaab87d1eb0f2f41d3


---

# Proteger um ficheiro que partilha por e-mail ao utilizar a aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Quando protege um ficheiro que partilha por e-mail, cria uma nova versão do ficheiro original. O ficheiro original permanece desprotegido e a nova versão é protegida e automaticamente anexada a uma mensagem de e-mail que envia em seguida.

Em alguns casos (para os ficheiros que são criados pelo Microsoft Word, Excel e PowerPoint), a aplicação de partilha RMS cria duas versões do ficheiro que anexa à mensagem de e-mail. A segunda versão do ficheiro tem uma extensão de nome de ficheiro **.ppdf** e é uma cópia sombra em PDF do ficheiro. Esta versão do ficheiro garante que os destinatários podem sempre ler o ficheiro, mesmo que não tenham instalada a mesma aplicação que utilizou para o criar. Isto acontece frequentemente quando as pessoas leem os e-mails nos seus dispositivos móveis e pretendem ver os respetivos anexos. Tudo o que precisam para abrir o ficheiro é da aplicação de partilha RMS. Em seguida, podem ler o ficheiro anexado, mas não o podem alterar até abrirem a outra versão do ficheiro com uma aplicação que suporte RMS.

Se a sua organização utilizar o Azure RMS, pode controlar os ficheiros que protege ao partilhar:

-   Selecione uma opção para receber e-mails quando alguém tentar abrir estes anexos protegidos. Sempre que alguém aceder ao ficheiro, será notificado sobre quem tentou abrir o ficheiro e quando o fez, bem como se teve êxito (se a autenticação foi efetuada com êxito) ou não.

-   Utilize o site de controlo de documentação. Pode, inclusive, deixar de partilhar o ficheiro ao revogar o acesso ao mesmo no site de controlo de documentos. Para obter mais informações, consulte [Controlar e revogar os documentos quando utiliza a aplicação de partilha RMS](sharing-app-track-revoke.md).

## Utilizar o Outlook: para proteger um ficheiro que partilha por e-mail

1.  Crie a sua mensagem de e-mail e anexe o ficheiro. Em seguida, no separador **Mensagem**, no grupo **RMS**, clique em **Partilhar Protegido** e, em seguida, clique em **Partilhar Protegido** novamente:

    ![Suplemento do Outlook para a aplicação de partilha RMS](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    Se não vir este botão, é provável que a aplicação de partilha RMS não esteja instalada no seu computador, que a versão mais recente não esteja instalada ou que seja necessário reiniciar o computador para concluir a instalação. Para obter mais informações sobre como instalar a aplicação de partilha, consulte [Transferir e instalar a aplicação de partilha Rights Management](install-sharing-app.md).

2.  Especifique as opções que pretende para este ficheiro na [caixa de diálogo partilhar protegido](sharing-app-dialog-box.md) e, em seguida, clique em **Enviar Agora**.

### Outras formas de proteger um ficheiro que partilha por e-mail
Além de partilhar um ficheiro protegido com o Outlook, também pode utilizar estas alternativas:

-   A partir do Explorador de Ficheiros: este método funciona para todos os ficheiros.

-   A partir de uma aplicação do Office: este método funciona para as aplicações que a aplicação de partilha RMS suporta através do suplemento do Office, de modo a ver o grupo **RMS** no friso.

#### Utilizar o Explorador de Ficheiros ou uma aplicação do Office: para proteger um ficheiro que partilha por e-mail

1.  Utilize uma das seguintes opções:

    -   Para o Explorador de Ficheiros: clique com o botão direito do rato no ficheiro, selecione **Proteger com RMS** e, em seguida, selecione **Partilhar Protegido**:

        ![Opção de menu Partilhar protegido](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Para as aplicações do Office, Word, Excel e PowerPoint: certifique-se primeiro de que guardou o ficheiro. Em seguida, no separador **Base**, no grupo **RMS**, clique em **Partilhar Protegido** e, em seguida, clique em **Partilhar Protegido** novamente:

        ![Suplemento para a barra de ferramentas do Office](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    Se não vir estas opções de proteção, é provável que a aplicação de partilha RMS não esteja instalada no seu computador, que a versão mais recente não esteja instalada ou que seja necessário reiniciar o computador para concluir a instalação. Para obter mais informações sobre como instalar a aplicação de partilha, consulte [Transferir e instalar a aplicação de partilha Rights Management](install-sharing-app.md).

2.  Especifique as opções que pretende para este ficheiro na [caixa de diálogo partilhar protegido](sharing-app-dialog-box.md) e, em seguida, clique em **Enviar**.

3.  Poderá ver momentaneamente uma caixa de diálogo para lhe indicar que o ficheiro está a ser protegido e, em seguida, verá uma mensagem de e-mail criada para si que indica aos destinatários que os anexos estão protegidos com o Microsoft RMS e que devem iniciar sessão. Quando clicam na ligação para iniciar sessão, veem instruções e ligações para garantir que podem abrir o anexo protegido.

    Exemplo:

    ![Mensagem de e-mail do Azure RMS](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    Está a perguntar-se [O que é o ficheiro .ppdf criado automaticamente?](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)

4.  Opcional: pode alterar tudo o que pretender nesta mensagem de e-mail. Por exemplo, pode adicionar ou alterar o assunto ou o texto da mensagem.

    > [!WARNING]
    > Embora possa adicionar ou remover pessoas desta mensagem de e-mail, isso não altera as permissões para o anexo que especificou na caixa de diálogo **partilhar protegido**. Se pretender alterar essas permissões, por exemplo, para fornecer permissões a uma nova pessoa para abrir o ficheiro, feche a mensagem de e-mail sem a guardar ou enviar e regresse ao passo 1.

5.  Envie a mensagem de e-mail.

## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, veja as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jun16_HO4-->


