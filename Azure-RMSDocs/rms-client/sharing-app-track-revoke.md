---
# required metadata

title: Rastrear e revogar seus documentos ao usar o aplicativo RMS sharing | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 61f349ce-bdd2-45c1-acc5-bc83937fb187

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rastreie e revogue seus documentos ao usar o aplicativo RMS sharing

*Aplica-se a: Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Depois de ter protegido seus documentos usando o aplicativo RMS sharing, se sua organização usar o Azure Rights Management e não o Active Directory Rights Management Services, será possível acompanhar quantas pessoas estão usando seus documentos protegidos. Se necessário, você também pode revogar acesso a estes documentos quando quiser parar de compartilhá-los. Para fazer isso, use o **site de rastreamento de documentos**, que pode ser acessado de computadores Windows, Mac e até mesmo de tablets e celulares.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Ao acessar esse site, basta conectar para acompanhar seus documentos. Levando em conta que sua organização tem uma [assinatura que dá suporte a rastreamento e revogação de documentos](https://technet.microsoft.com/dn858608.aspx) e que você tenha sido atribuído a uma licença para esta assinatura, você poderá, então, ver quem tentou abrir os arquivos protegidos e se obteve êxito (se eles foram autenticados com êxito) ou não. Cada vez que tentaram acessar o documento e sua localização na ocasião. Além disso:

-   Se você precisar interromper o compartilhamento de um documento: Clique em **Revogar acesso**, observe o período de tempo em que o documento continuará disponível e decida se quer informar às pessoas que você está revogando o acesso ao documento antes compartilhado e forneça uma mensagem personalizada. Quando você revoga um documento, o documento que você compartilhou não é excluído, mas usuários autorizados já não serão capazes de abri-lo.

-   Se quiser exportar para o Excel: Clique em **Abrir no Excel**, de modo que você possa modificar os dados e criar seus próprios modos de exibição e gráficos.

-   Se quiser configurar notificações por email: Clique em **Configurações** e selecione como e se deseja enviar um email quando o documento for acessado.

-   Se você tiver dúvidas ou quiser fazer comentários sobre o site de acompanhamento de documentos: clique no ícone Ajuda para acessar as [Perguntas frequentes sobre acompanhamento de documentos](http://go.microsoft.com/fwlink/?LinkId=523977).

## Usando o Office para acessar o site de rastreamento de documentos

-   Para aplicativos do Office, Word, Excel e PowerPoint: na guia **Página Inicial**, no grupo **RMS**, clique em **Compartilhamento Protegido**e em **Acompanhar Uso**.

    ![Acompanhar o uso de aplicativos do Office ao usar o aplicativo de compartilhamento RMS ](../media/ADRMS_MSRMSApp_OfficeToolbarTrackUsage.png)

-   Para o Outlook: Na guia **Página Inicial** , no grupo  **RMS** , clique em **Acompanhar Uso**:

    ![Selecione Acompanhar Uso do Outlook ao usar o aplicativo de compartilhamento RMS ](../media/ADRMS_MSRMSApp_OutlookTrackUsage.png)

Se você não vir essas opções para o RMS, é provável que o aplicativo RMS sharing não esteja instalado no seu computador, a versão mais recente não esteja instalada ou o computador deve ser reiniciado para concluir a instalação. Para obter mais informações sobre como instalar o aplicativo de compartilhamento, consulte [Baixar e instalar o aplicativo de compartilhamento do Rights Management](install-sharing-app.md).

### Outras maneiras de rastrear e revogar seus documentos
Além de controlar seus documentos em computadores Windows usando aplicativos do Office, você também pode usar estas alternativas:

-   **Usando um navegador da Web**: Esse método funciona para todos os arquivos compatíveis.

-   **Utilizando o Explorador de Arquivos**: Esse método funciona para computadores Windows.

-   **Usando uma mensagem de email do Outlook**: Esse método funciona para computadores Windows.

#### Usando um navegador da Web para acessar o site de rastreamento de documentos

-   Usando um navegador com suporte, vá para o [site de acompanhamento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562).

    Navegadores compatíveis: É recomendável usar o Internet Explorer, no mínimo a versão 10, mas você pode usar qualquer um dos seguintes navegadores para usar o site de rastreamento de documentos:

    -   Internet Explorer: No mínimo a versão 10

    -   Internet Explorer 9 com, no mínimo, MS12-037: atualização de segurança cumulativa para o Internet Explorer: 12 de junho de 2012

    -   Mozilla Firefox: No mínimo a versão 12

    -   Apple Safari 5: No mínimo a versão 5

    -   Google Chrome: No mínimo a versão 18

#### Usando o Explorador de Arquivos para acessar o site de rastreamento de documentos

-   Clique com o botão direito do mouse no arquivo, selecione **Proteger com RMS** e, em seguida, selecione **Acompanhar Uso**:

    ![Selecione Acompanhar Uso do Explorer ao usar o aplicativo de compartilhamento RMS](../media/ADRMS_MSRMSApp_ExplorerTrackUsage.png)

#### Usando uma mensagem de email do Outlook para acessar o site de rastreamento de documentos

-   Em uma mensagem de email, na guia **Mensagem** , no grupo  **RMS** , clique em **Compartilhamento protegido**e em **Acompanhar Uso**:

    ![Selecione Acompanhar Uso do Outlook ao usar o aplicativo de compartilhamento RMS](../media/ADRMS_MSRMSApp_OutlookMessageTrackUsage.png)

## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


