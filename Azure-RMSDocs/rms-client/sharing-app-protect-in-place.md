---
# required metadata

title: Proteger um ficheiro num dispositivo (proteger no local) ao utilizar a aplicação de partilha Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteger um ficheiro num dispositivo (proteger no local) ao utilizar a aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Quando protege um ficheiro no local, este substitui o ficheiro original, que está desprotegido. Em seguida, pode deixar o ficheiro onde se encontra, copiá-lo para outra pasta ou dispositivo ou partilhar a pasta onde está e o ficheiro permanece protegido. Também pode anexar o ficheiro protegido a uma mensagem de e-mail, embora a forma recomendada para partilhar um ficheiro protegido por e-mail seja diretamente a partir do Explorador de Ficheiros ou de uma aplicação do Office (consulte [Proteger um ficheiro que partilha por e-mail ao utilizar a aplicação de partilha Rights Management](sharing-app-protect-by-email.md)).

> [!TIP]
> Se vir algum erro ao tentar proteger ficheiros, consulte a [FAQ acerca da Aplicação de Partilha Microsoft Rights Management para Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

## Para proteger um ficheiro num dispositivo (proteger no local)

1.  No Explorador de Ficheiros, selecione um ficheiro a proteger. Clique com o botão direito do rato, selecione **Proteger com RMS** e, em seguida, selecione **Proteger no local**. Por exemplo:

    ![Opção de menu Proteger no local](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Se não vir a opção **Proteger com RMS**, é provável que a aplicação de partilha RMS não esteja instalada no seu computador ou que seja necessário reiniciar o computador para concluir a instalação. Para obter mais informações sobre como instalar a aplicação de partilha RMS, consulte [Transferir e instalar a aplicação de partilha Rights Management](install-sharing-app.md).

2.  Efetue uma das seguintes ações:

    -   Selecione um modelo de política: estas são permissões predefinidas que, normalmente, restringem o acesso e a utilização a pessoas na sua organização. Por exemplo, se o nome da sua organização for “Contoso, Lda.”, poderá ver **Contoso, Lda. – Apenas Visualização Confidencial**. Se for a primeira vez que protege um ficheiro neste computador, primeiro terá de selecionar **Proteção Definida pela Empresa** para transferir os modelos.

        Da próxima vez que clicar na opção **Proteger no local**, irá ver até 10 modelos à escolha. Se existirem mais de 10 modelos disponíveis e aquele que pretende não for apresentado, clique em **Proteção Definida pela Empresa** para transferir e ver todos os modelos.

        Quando seleciona um modelo de política, também pode proteger vários ficheiros e uma pasta. Quando seleciona uma pasta, todos os ficheiros nessa pasta são selecionados automaticamente para proteção, mas os novos ficheiros que criar nessa pasta não serão automaticamente protegidos.

    -   Selecione **Permissões Personalizadas**: escolha esta opção se os modelos não fornecerem o nível de proteção de que necessita ou se pretender definir explicitamente as opções de proteção. Especifique as opções que pretende para este ficheiro na [caixa de diálogo adicionar proteção](sharing-app-dialog-box.md) e, em seguida, clique em **Aplicar**.

3.  Poderá ver momentaneamente uma caixa de diálogo que lhe indica que o ficheiro está a ser protegido e, em seguida, o foco regressa ao Explorador de Ficheiros. O ficheiro ou ficheiros selecionados estão agora protegidos. Em alguns casos (quando a adição de proteção altera a extensão de nome de ficheiro), o ficheiro original no Explorador de Ficheiros é substituído por um novo ficheiro que tem o ícone de cadeado de proteção do Rights Management. Por exemplo:

    ![Ficheiro protegido com ícone de cadeado da aplicação de partilha RMS](../media/ADRMS_MSRMSApp_Pfile.png)

Se precisar de remover a proteção de um ficheiro mais tarde, consulte [Remover a proteção de um ficheiro ao utilizar a aplicação de partilha Rights Management](sharing-app-remove-protection.md).

## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, consulte as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


