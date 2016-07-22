---
title: "Configurar aplicações para o Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 8fe934c51e852791d19fbb336deaf9cd7be9817b


---

# Configurar aplicações para o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

> [!NOTE]
> Estas informações destinam-se aos administradores de TI e consultores que tenham implementado o Azure Rights Management. Se estiver à procura de ajuda de utilizador e de informações acerca de como utilizar o Rights Management para uma aplicação específica ou como abrir um ficheiro que está protegido por direitos, utilize a ajuda e as orientações incluídas com a sua aplicação.
>
> Por exemplo, para aplicações do Office, clique no ícone Ajuda e introduza termos de pesquisa, como **Rights Management** ou **IRM**. Para a aplicação de partilha RMS para Windows, consulte o [Guia do utilizador da aplicação de partilha Rights Management](../rms-client/sharing-app-user-guide.md).

Depois de ter implementado o Azure Rights Management (Azure RMS) na sua organização, utilize as seguintes informações para configurar aplicações e serviços para suportar o Azure RMS. Incluem aplicações do Office como o Word 2013 e o Word 2010, bem como serviços como o Exchange Online (regras de transporte, prevenção de perda de dados, não reencaminhar e encriptação de mensagens) e o SharePoint Online (bibliotecas protegidas). Para obter informações acerca de como estas aplicações e serviços suportam o Rights Management, consulte [Como as aplicações suportam o Azure Rights Management](../understand-explore/applications-support.md).

> [!IMPORTANT]
> Para obter informações sobre as versões suportadas e outros requisitos, consulte [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

-   [Office 365: configuração para clientes e serviços online](configure-office365.md)

    -   [Exchange Online: configuração de IRM](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online e OneDrive para Empresas: configuração de IRM](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Aplicações do Office: configuração para clientes](configure-office-apps.md)

    -   [Office 2016 e Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Aplicação de partilha Rights Management: instalação e configuração para clientes](configure-sharing-app.md)

    -   [A aplicação de partilha RMS para o Windows: instalação e configuração](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [A aplicação de partilha RMS para plataformas móveis: instalação e gestão](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Para configurar os servidores no local, como o Exchange Server e o SharePoint Server, consulte [Implementar o conector Azure Rights Management](deploy-rms-connector.md).

> [!TIP]
> Para obter exemplos gerais e capturas de ecrã das aplicações configuradas para utilizar o Azure RMS, consulte [O Azure RMS em ação: conteúdo visto pelos administradores e utilizadores](../understand-explore/what-admins-users-see.md).


Além destas aplicações e serviços, existem outras aplicações que suportam as APIs de RMS. Esta categoria inclui aplicações de linha de negócio que são escritas internamente através do SDK RMS, bem como aplicações de fornecedores de software que são escritas através do SDK RMS. Para estas aplicações, siga as instruções fornecidas com a aplicação.

## Passos seguintes
Depois de configurar as suas aplicações para suportar o Azure Rights Management, utilize o [Plano de implementação do Azure Rights Management](../plan-design/deployment-roadmap.md) para verificar se existem outros passos de configuração que queira realizar antes de implementar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para utilizadores e administradores. Caso contrário, as informações operacionais que se seguem podem ser-lhe úteis:

- [Verificar o Azure Rights Management](verify.md)

- [Ajudar os utilizadores a proteger ficheiros ao utilizar o Azure Rights Management](help-users.md)

- [Registo e análise do Azure Rights Management](log-analyze-usage.md)

- [Operações para a sua chave de inquilino do Azure Rights Management](operations-tenant-key.md)





<!--HONumber=Jun16_HO4-->


