---
# required metadata

title: Controlar e revogar os documentos quando utiliza a aplicação de partilha RMS | Azure RMS
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

# Controlar e revogar os documentos quando utiliza a aplicação de partilha RMS

*Aplica-se a: Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Depois de proteger os documentos com a aplicação de partilha RMS, se a sua organização utilizar o Azure Rights Management em vez dos Serviços de Gestão de Direitos do Active Directory, pode controlar a forma como as pessoas utilizam os documentos protegidos. Se necessário, também pode revogar o acesso a esses documentos quando pretender deixar de os partilhar. Para tal, utilize o **site de controlo de documentos**, ao qual pode aceder a partir de computadores com o Windows, computadores Mac e até mesmo telemóveis e tablets.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Ao aceder a este site, inicie sessão para controlar os seus documentos. Desde que a sua organização tenha uma [subscrição que suporte a revogação e o controlo de documentos](https://technet.microsoft.com/dn858608.aspx) e lhe tenha sido atribuída uma licença para esta subscrição, pode ver quem tentou abrir os ficheiros que protegeu e se o fizeram com êxito (se a autenticação foi efetuada com êxito) ou não. Também pode ver todas as vezes que alguém tentou aceder ao documento e a respetiva localização nesse momento. Além disso:

-   Se precisar deixar de partilhar um documento: clique em **Revogar acesso**, tome nota do período de tempo durante o qual o documento continuará disponível, decida se pretende informar as pessoas de que está a revogar o acesso ao documento partilhado anteriormente e forneça uma mensagem personalizada. Ao revogar um documento, não elimina o documento que partilhou, mas os utilizadores autorizados deixam de o poder abrir.

-   Se pretender exportar para Excel: clique em **Abrir no Excel**, para que possa modificar os dados e criar as suas próprias vistas e gráficos.

-   Se pretender configurar notificações por e-mail: clique em **Definições** e selecione como e se deve receber um e-mail quando alguém aceder ao documento.

-   Se tiver dúvidas ou pretender fornecer comentários sobre o site de controlo de documentos: clique no ícone de Ajuda para aceder à [FAQ acerca do Controlo de Documentos](http://go.microsoft.com/fwlink/?LinkId=523977).

## Utilizar o Office para aceder ao site de controlo de documentos

-   Para as aplicações do Office, Word, Excel e PowerPoint: no separador **Base**, no grupo **RMS**, clique em **Partilhar Protegido** e, em seguida, clique em **Controlar a Utilização**.

    ![Controlar a utilização de aplicações do Office ao utilizar a aplicação de partilha RMS ](../media/ADRMS_MSRMSApp_OfficeToolbarTrackUsage.png)

-   Para o Outlook: no separador **Base**, no grupo **RMS**, clique em **Controlar a Utilização**:

    ![Selecionar Controlar a Utilização do Outlook ao utilizar a aplicação de partilha RMS ](../media/ADRMS_MSRMSApp_OutlookTrackUsage.png)

Se não vir estas opções do RMS, é provável que a aplicação de partilha RMS não esteja instalada no seu computador, que a versão mais recente não esteja instalada ou que seja necessário reiniciar o computador para concluir a instalação. Para obter mais informações sobre como instalar a aplicação de partilha, consulte [Transferir e instalar a aplicação de partilha Rights Management](install-sharing-app.md).

### Outras formas de controlar e revogar os documentos
Além de controlar os seus documentos em computadores com o Windows através da utilização de aplicações do Office, também pode utilizar estas alternativas:

-   **Utilizar um browser**: este método funciona para todos os dispositivos suportados.

-   **Utilizar o Explorador de Ficheiros**: este método funciona para os computadores com o Windows.

-   **Utilizar uma mensagem de e-mail do Outlook**: este método funciona para os computadores com o Windows.

#### Utilizar um browser para aceder ao site de controlo de documentos

-   Num browser suportado, aceda ao [site de controlo de documentos](http://go.microsoft.com/fwlink/?LinkId=529562).

    Browsers suportados: recomendamos que utilize, pelo menos, a versão 10 do Internet Explorer, mas pode utilizar qualquer um dos seguintes browsers para aceder ao site de controlo de documentos:

    -   Internet Explorer: pelo menos, versão 10

    -   Internet Explorer 9 com, pelo menos, MS12-037: Atualização de Segurança Cumulativa para o Internet Explorer: 12 de junho de 2012

    -   Mozilla Firefox: pelo menos, versão 12

    -   Apple Safari 5: pelo menos, versão 5

    -   Google Chrome: pelo menos, versão 18

#### Utilizar o Explorador de Ficheiros para aceder ao site de controlo de documentos

-   Clique com o botão direito do rato no ficheiro, selecione **Proteger com RMS** e, em seguida, selecione **Controlar a Utilização**:

    ![Selecionar Controlar a Utilização do Explorador ao utilizar a aplicação de partilha RMS](../media/ADRMS_MSRMSApp_ExplorerTrackUsage.png)

#### Utilizar uma mensagem de e-mail do Outlook para aceder ao site de controlo de documentos

-   Numa mensagem de e-mail, no separador **Mensagem**, no grupo **RMS**, clique em **Partilhar Protegido** e, em seguida, clique em **Controlar a Utilização**:

    ![Selecionar Controlar a Utilização do Outlook ao utilizar a aplicação de partilha RMS](../media/ADRMS_MSRMSApp_OutlookMessageTrackUsage.png)

## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, consulte as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


