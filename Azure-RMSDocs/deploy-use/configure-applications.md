---
# required metadata

title: Configurando aplicativos do Azure Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuração de aplicativos do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

> [!NOTE]
> Essas informações são para os administradores de TI e consultores que implantaram o Azure Rights Management. Se você estiver procurando ajuda e informações sobre como usar o Rights Management para um aplicativo específico ou como abrir um ficheiro com direitos protegidos, use a ajuda e orientação que acompanha o seu aplicativo.
>
> Por exemplo, para aplicativos do Office, clique no ícone de Ajuda e insira termos de pesquisa como **Rights Management** ou **IRM**. Para o aplicativo de compartilhamento RMS para Windows, consulte o [Guia de usuário de aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-user-guide.md).

Após ter implantado o Azure Rights Management (Azure RMS) para a sua organização, use a seguinte informação para configurar aolicações e serviços para oferecer suporte ao Azure Rights Management (RMS). Isso inclui aplicativos do Office como Word 2013 e Word 2010 e serviços como o Exchange Online (regras de transporte, prevenção de perda de dados, não encaminhar e criptografia de mensagens) e o SharePoint Online (bibliotecas protegidas). Para obter mais informações sobre como esses aplicativos dão suporte ao Azure RMS, consulte [Como os aplicativos dão suporte ao Azure Rights Management](../understand-explore/applications-support.md).

> [!IMPORTANT]
> Para obter informações sobre as versões com suporte e outros requisitos, consulte [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

-   [Office 365: Configuração para clientes e serviços online](configure-office365.md)

    -   [Exchange Online: Configuração do IRM](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online e OneDrive para a empresa: Configuração do IRM](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Aplicativos do Office: configuração para clientes](configure-office-apps.md)

    -   [Office 2016 e Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Aplicativo de compartilhamento do Rights Management: Instalação e configuração para clientes](configure-sharing-app.md)

    -   [O aplicativo de compartilhamento do RMS para Windows: Instalação e configuração](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [O aplicativo RMS sharing para plataformas móveis: instalação e gerenciamento](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Para configurar servidores locais, como o Exchange Server e o SharePoint Server, consulte [Implantando o conector do Azure Rights Management](deploy-rms-connector.md).

> [!TIP]
> Para obter exemplos de alto nível e capturas de tela de aplicativos configurados para usar o Azure RMS, consulte a seção [O Azure RMS em ação: o que administradores e usuários veem](../understand-explore/what-admins-users-see.md).


Além desses aplicativos e serviços, há outros aplicativos que dão suporte às APIs do RMS. Esta categoria inclui aplicativos de linha de negócios que são gravados internamente por meio do RMS SDK e aplicativos de fornecedores de software que são gravados por meio do RMS SDK. Para esses aplicativos, siga as instruções que são fornecidas com o aplicativo.

## Próximas etapas
Depois de configurar seus aplicativos para dar suporte ao Azure Rights Management, use o [Roteiro de implantação do Azure Rights Management](../plan-design/deployment-roadmap.md) para verificar se existem outras etapas de configuração que você pode fazer antes de implementar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para os usuários e administradores. Caso contrário, você pode achar úteis as informações operacionais a seguir:

- [Verificando o Azure Rights Management](verify.md)

- [Ajudando os usuários a proteger os arquivos usando o Azure Rights Management](help-users.md)

- [Registrando em log e analisando o Azure Rights Management](log-analyze-usage.md)

- [Operações para sua chave de locatário do Azure Rights Management](operations-tenant-key.md)




<!--HONumber=Apr16_HO4-->


