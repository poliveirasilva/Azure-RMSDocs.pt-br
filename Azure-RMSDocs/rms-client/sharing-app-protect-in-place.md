---
title: Proteger um arquivo em um dispositivo (proteger in-loco) usando o aplicativo de compartilhamento Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 638c2f27c8d552653dcf3f41d8fad6d44cb08887
ms.openlocfilehash: 5150351ec6772b95d77698dc39a1f69105c02d2c


---

# Proteger um arquivo em um dispositivo (proteger in-loco) usando o aplicativo Rights Management sharing

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Quando você protege um arquivo in-loco, ele substitui o arquivo original, desprotegido. Em seguida, você pode deixar o arquivo onde ele está, copiar para outra pasta ou dispositivo ou compartilhar a pasta em que ele se encontra e o arquivo continuará protegido. Você também pode anexar o arquivo protegido a uma mensagem de email, embora a maneira recomendada para compartilhar um arquivo protegido por email seja diretamente do Explorador de arquivos ou de um aplicativo do Office (consulte [Proteja um arquivo que você compartilha por email usando o aplicativo de compartilhamento Rights Management](sharing-app-protect-by-email.md)).

> [!TIP]
> Se você encontrar erros ao tentar proteger arquivos, consulte [Perguntas frequentes sobre o aplicativo de compartilhamento Microsoft Rights Management para Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

## Para proteger um arquivo em um dispositivo (proteger in-loco)

1.  No Explorador de arquivos, selecione um arquivo para proteger. Clique com o botão direito do mouse, selecione **Proteger com RMS** e, em seguida, selecione **Proteger in-loco**. Por exemplo:

    ![Opção de menu Proteger in-loco](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Se você não vir a opção **Proteger com RMS** , é provável que o aplicativo RMS sharing não esteja instalado no seu computador ou que o computador tenha de ser reiniciado para concluir a instalação. Para obter mais informações sobre como instalar o aplicativo RMS sharing, consulte [Baixar e instalar o aplicativo de compartilhamento Rights Management](install-sharing-app.md).

2.  Realize um dos seguintes procedimentos:

    -   Selecione um modelo de política: essas são permissões predefinidas que normalmente restringem o acesso e o uso para as pessoas em sua organização. Por exemplo, se o nome da sua organização é “Contoso, Ltd”, você deverá encontrar **Contoso, Ltd - Somente Exibição Confidencial**. Se esta for a primeira vez que protege um arquivo neste computador, você primeiro precisará selecionar **Proteção definida pela empresa** para baixar os modelos.

        Da próxima vez que você clicar na opção **Proteger in-loco**, você verá até 10 modelos dentre os quais escolher. Se houver mais de 10 modelos disponíveis e o que você quiser não for exibido, clique em **Proteção Definida pela Empresa** para baixar e ver todos os modelos.

        Quando seleciona um modelo de política, você também pode proteger vários arquivos e uma pasta. Quando você seleciona uma pasta, todos os arquivos nessa pasta serão automaticamente selecionados para proteção, mas novos arquivos criados nessa pasta não serão automaticamente protegidos.

    -   Selecione **Permissões personalizadas**: escolha esta opção se os modelos não fornecerem o nível de proteção que você precisa ou se você deseja definir explicitamente as opções de proteção por conta própria. Especifique as opções que você deseja para esse arquivo na [caixa de diálogo Adicionar Proteção](sharing-app-dialog-box.md) e, em seguida, clique em **Aplicar**.

3.  Você pode ver rapidamente uma caixa de diálogo para informar que o arquivo está sendo protegido e, em seguida, retorna o foco para o Explorador de arquivos. O(s) arquivo(s) selecionado(s) agora está(ão) protegido(s). Em alguns casos (quando a adição de proteção altera a extensão de nome de arquivo), o arquivo original no Explorador de arquivos é substituído por um novo arquivo com o ícone de bloqueio de proteção do Rights Management. Por exemplo:

    ![Arquivo protegido com ícone de bloqueio para o aplicativo de compartilhamento RMS](../media/ADRMS_MSRMSApp_Pfile.png)

Se você mudar de ideia sobre as permissões ou precisar modificá-las posteriormente, basta proteger o arquivo novamente.

Se você precisar posteriormente remover a proteção de um arquivo, consulte [Remover a proteção de um arquivo usando o aplicativo de compartilhamento Rights Management](sharing-app-remove-protection.md).

## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jul16_HO3-->


