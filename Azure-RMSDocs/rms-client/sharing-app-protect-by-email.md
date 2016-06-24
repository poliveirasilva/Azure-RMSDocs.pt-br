---
# required metadata

title: Proteger um arquivo que você compartilha por email usando o aplicativo de compartilhamento Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteja arquivos que você compartilha por email usando o aplicativo de compartilhamento Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Ao proteger um arquivo que você compartilha por email, será criada uma nova versão do arquivo original. Enquanto o arquivo original permanecerá desprotegido, a nova versão será protegida e automaticamente anexada a um e-mail para você enviar.

Em alguns casos (para arquivos criados no Microsoft Word, Excel e PowerPoint), o aplicativo de RMS sharing cria duas versões do arquivo que anexa à mensagem de email. A segunda versão tem a extensão de nome de arquivo **.ppdf** , e é uma cópia de sombra do arquivo PDF. Esta versão garante que os destinatários sempre poderão ler o arquivo, mesmo sem terem instalado o aplicativo que você usou para criá-lo. Isso costuma ocorrer quando as pessoas acessam emails corporativos em dispositivos móveis e desejam exibir anexos de email. Para abrir o arquivo, elas precisam apenas do aplicativo RMS sharing. Assim, elas podem ler o arquivo anexado, mas não poderão alterá-lo até abrirem a outra versão do arquivo usando um aplicativo que dê suporte ao RMS.

Se a sua organização usa o Azure RMS, você pode manter o controle dos arquivos protegidos por compartilhamento:

-   Selecione uma opção para receber emails quando alguém tentar abrir anexos protegidos. Cada vez que o arquivo é acessado, você será notificado sobre quem tentou abrir o arquivo e quando, e se foram bem-sucedidos (autenticados com êxito) ou não.

-   Use o site de rastreamento do documento. Você pode até mesmo interromper o compartilhamento do arquivo, revogando o acesso a ele no site de rastreamento do documento. Para obter mais informações, consulte [Acompanhar e revogar seus documentos ao usar o aplicativo de compartilhamento RMS](sharing-app-track-revoke.md)..

## Usando o Outlook: Para proteger um arquivo que você compartilha por email

1.  Crie sua mensagem de email e anexe o arquivo. Depois, na guia **Mensagem** no grupo **RMS** , clique em **Compartilhamento protegido** , e então clique em **Compartilhamento protegido** novamente:

    ![Suplemento do Outlook para o aplicativo de compartilhamento de RMS](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    Se você não estiver vendo esse botão, é provável que o aplicativo RMS sharing não esteja instalado no seu computador, a versão mais recente não esteja instalada, ou seu computador deve ser reiniciado para concluir a instalação. Para obter mais informações sobre como instalar o aplicativo de compartilhamento, consulte [Baixar e instalar o aplicativo de compartilhamento do Rights Management](install-sharing-app.md).

2.  Especifique as opções que você deseja para esse arquivo na [caixa de diálogo do compartilhamento protegido](sharing-app-dialog-box.md), e então clique em **Enviar Agora**.

### Outras maneiras de proteger um arquivo que você compartilha por email
Além de compartilhar um arquivo protegido usando o Outlook, você também pode usar essas alternativas:

-   No Explorador de Arquivos: Esse método funciona para todos os arquivos.

-   De um aplicativo do Office: esse método funciona para aplicativos aos quais o aplicativo RMS sharing dá suporte usando o suplemento do Office para que você veja o grupo **RMS** na faixa de opções.

#### Usando o Explorador de Arquivos ou um aplicativo do Office: Para proteger um arquivo que você compartilha por email

1.  Use uma das seguintes opções:

    -   Para o Explorador de Arquivos: clique com o botão direito do mouse, selecione **Proteger com RMS** e, em seguida, selecione **Compartilhamento Protegido**:

        ![Compartilhar opção de menu protegido](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Para aplicativos do Office, Word, Excel e PowerPoint: Primeiro, verifique se você salvou o arquivo. Depois, na guia **Início** no grupo do **RMS** , clique em **Compartilhamento Protegido** , e então clique em **Compartilhamento Protegido** novamente:

        ![Suplemento da bBarra de ferramentas do Office](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    Se você não estiver vendo essas opções para proteção, é provável que o aplicativo RMS sharing não esteja instalado no seu computador, a versão mais recente não esteja instalada, ou seu computador deve ser reiniciado para concluir a instalação. Para obter mais informações sobre como instalar o aplicativo de compartilhamento, consulte [Baixar e instalar o aplicativo de compartilhamento do Rights Management](install-sharing-app.md).

2.  Especifique as opções que você deseja para esse arquivo na [caixa de diálogo do compartilhamento protegido](sharing-app-dialog-box.md) e, então, clique em **Enviar**.

3.  Rapidamente, pode ser que seja exibida uma caixa de diálogo para informar que o arquivo está sendo protegido, e, logo depois, será criada uma mensagem de email informando aos destinatários que os anexos são protegidos com Microsoft RMS, e que eles devem entrar. Quando eles clicarem no link para entrar, eles verão instruções e links para garantir que eles poderão abrir o anexo protegido.

    Exemplo:

    ![Mensagem de email para o Azure RMS](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    Você está pensando: [o que é o arquivo .ppdf, criado automaticamente?](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)

4.  Opcional: Você pode alterar o que quiser nesta mensagem de email. Por exemplo, você pode adicionar ou alterar o assunto, ou o texto da mensagem.

    > [!WARNING]
    > Embora você possa adicionar ou remover pessoas desta mensagem de email, isso não altera as permissões para o anexo, que você especificou na caixa de diálogo **compartilhamento protegido** . Se você quiser alterar essas permissões para conceder permissões, por exemplo, para uma nova pessoa abrir o arquivo, feche a mensagem de email sem salvar ou enviá-la e retorne à etapa 1.

5.  Envie a mensagem de email.

## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


