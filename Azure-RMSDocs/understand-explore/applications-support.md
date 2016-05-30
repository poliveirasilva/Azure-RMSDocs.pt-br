---
# required metadata

title: Como os aplicativos dão suporte ao Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como os aplicativos dão suporte ao Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use as informações a seguir para ajudar a entender como os aplicativos de usuário final usados com mais frequência (como os aplicativos Office, Word, Excel, PowerPoint e Outlook) e serviços (como o Exchange e SharePoint) podem usar a Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para ajudar a proteger os dados da sua organização. 
> [!NOTE] Para verificar os aplicativos e as versões aos quais o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) dá suporte, consulte [Requisitos para o Azure Rights Management](../get-started/requirements-azure-rms.md).

Em alguns casos, a proteção de informações é aplicada automaticamente, de acordo com as políticas que você configurar. Por exemplo, esse é o caso de bibliotecas do SharePoint, arquivos confidenciais e regras de transporte do Exchange. Em outros casos, os usuários devem aplicar a proteção das informações diretamente em seus aplicativos, seja selecionando um modelo ou opções específicas. Por exemplo, este é o caso quando os usuários compartilham um arquivo por email ou protegem um arquivo no local, restringindo o acesso ou o uso a usuários selecionados ou usuários fora da organização.

Os modelos facilita para os usuários (e administradores que configuram políticas) a aplicação do nível correto de proteção e restringir o acesso a pessoas dentro de sua organização. Embora o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] seja fornecido com dois modelos padrão, é recomendável criar modelos personalizados para reduzir as ocasiões em que eles precisam especificar as opções individuais. Para obter mais informações, consulte [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para os casos em que os próprios usuários devem aplicar as informações de proteção, lembre-se de dar orientações e instruções sobre como e quando fazer isso. As instruções devem ser específicas para o aplicativo e as versões que eles usam e como usam, e as orientações sobre quando e como aplicar as informações de proteção devem ser adequadas para seu negócio. Para obter mais informações, consulte [Ajudar os usuários a proteger os arquivos usando o Azure Rights Management](../deploy-use/help-users.md).

Para obter informações de como configurar esses aplicativos para o Azure RMS, consulte [Configurando aplicativos para o Azure Rights Management](../deploy-use/configure-applications.md).

> [!TIP] Para obter exemplos e capturas de tela de aplicativos usando o Azure RMS, consulte [Azure RMS em ação: o que administradores e usuários veem](what-admins-users-see.md).

Serviços de pesquisa podem se integrar ao Rights Management de maneiras diferentes. Por exemplo: 

- Exchange Online e o Exchange Server usam indexação de serviço de indexação para que os emails protegidos do RMS de um usuário sejam automaticamente exibidos nos resultados da pesquisa. 

- O SharePoint Online e o SharePoint Server aplicam proteção RMS ao arquivos somente no download, o que significa que a indexação e os resultados da pesquisa no SharePoint não são afetados por essa solução de proteção de documento. No entanto, se você tiver um documento que deseja armazenar no SharePoint e não deve ser retornado nos resultados da pesquisa, o RMS protegerá o arquivo antes de carregá-lo no SharePoint.

- O Windows Desktop Search usa um índice compartilhado entre diferentes usuários do dispositivo e para manter os dados de documentos protegidos seguros, ele não indexa arquivos protegidos por RMS. Isso significa que embora os resultados da pesquisa não incluam arquivos protegidos, você pode ter certeza de que os arquivos que contêm dados confidenciais não serão exibidos nos resultados da pesquisa para outros usuários que podem entrar ou se conectar ao seu computador. 



## Próximas etapas

Saiba mais sobre como cada um dos seguintes aplicativos dá suporte para o Azure RMS:

-   [Aplicativo de compartilhamento RMS para Windows e plataformas móveis](sharing-app-support.md)

-   [Aplicativos e serviços do Office](office-apps-services-support.md)

-   [Servidores de arquivos que executam o Windows Server e usam o File Classification Infrastructure (FCI)](file-server-support.md)

-   [Outros aplicativos que dão suporte às APIs do RMS](api-support.md)



<!--HONumber=May16_HO3-->


