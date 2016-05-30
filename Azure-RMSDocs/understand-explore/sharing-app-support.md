---
# required metadata

title: Aplicativo RMS sharing para Windows e plataformas móveis | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Aplicativo de compartilhamento RMS para Windows e plataformas móveis

*Aplica-se a: Azure Rights Management, Office 365*

O aplicativo de compartilhamento de RMS é um aplicativo gratuito, que pode ser baixado e que é necessário para suportar o Office 2010, mas também recomendado para computadores com Windows, computadores MAC e dispositivos móveis. Uma das suas vantagens é que ele pode aplicar proteção genérica para aplicativos e arquivos que não dão suporte ao [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] nativamente, o que significa que todos os arquivos podem ser protegidos. Para obter mais informações sobre os diferentes níveis de proteção, consulte a seção [Nível de proteção - nativa e genérica](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) do tópico [Guia de administrador do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-admin-guide.md).

Quando os usuários protegem seus arquivos usando o aplicativo de compartilhamento de RMS podem também controlar os documentos protegidos e se necessário, revogar o acesso a eles. Eles fazem isso usando o [site de acompanhamento de documento](http://go.microsoft.com/fwlink/?LinkId=529562).

Para computadores Windows, o aplicativo de compartilhamento RMS se integra de maneira discreta e melhora os aplicativos que os usuários já utilizam:

-   É instalado um complemento do Office para Word, Excel, PowerPoint e Outlook. Isso fornece aos usuários um botão **Compartilhamento Protegido** na faixa de opções, que chama uma caixa de diálogo de configurações fácil de usar que são mais comumente usadas para proteger os arquivos a serem enviados por email. Esse botão também fornece uma maneira rápida de acessar o site de acompanhamento de documento.

-   Uma nova opção de clicar com o botão direito do mouse para o Explorador de Arquivos. Isso fornece aos usuários uma opção de **Proteção in-loco**, que invoca uma caixa de diálogo de configurações fácil de usar, configurações que são mais comumente usadas para proteger os arquivos armazenados em um disco.

-   Um visualizador para abrir arquivos que foram protegidos pelo [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Esse visualizador será automaticamente invocado quando não houver outro aplicativo instalado que possa abrir o arquivo protegido.

-   Configuração de back-end para o Office 2010 que permite que o Word, Excel, PowerPoint e Outlook deste pacote funcionem perfeitamente com [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

Embora o compartilhamento de aplicativos para Windows RMS possa ser baixado e instalado para um único computador usando a [página do Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), ele também suporta uma implantação corporativa para instalação silenciosa e configuração personalizada. Para obter mais informações, consulte os seguintes recursos:

-   [guia de administrador do aplicativo de compartilhamento do Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guia do usuário do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-user-guide.md)

O aplicativo de compartilhamento RMS para dispositivos móveis é compatível com os dispositivos móveis utilizados com mais frequência, como iPad e iPhone, Android, Windows Phone e Windows RT. Os usuários podem baixar esse aplicativo da loja relevante, e há links para elas na [página do Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).

**Se você tiver o Microsoft Intune**: já que o aplicativo RMS sharing inclui o Software Development Kit do Aplicativo do Microsoft Intune, você poderá usar as seguintes opções:

-   Implantar e gerenciar o aplicativo para dispositivos iOS e Android registrados pelo Intune.

-   Gerenciar o aplicativo para dispositivos iOS e Android não registrados pelo Intune.


## Próximas etapas
Para ver como outros aplicativos e serviços dão suporte ao Azure Rights Management, consulte [Como os aplicativos dão suporte ao Azure Rights Management](applications-support.md).



<!--HONumber=Apr16_HO4-->


