---
# required metadata

title: Aplicação de partilha Rights Management&colon; instalação e configuração para clientes | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Aplicação de partilha Rights Management: instalação e configuração para clientes

*Aplica-se a: Azure Rights Management, Office 365*

A aplicação de partilha Rights Management (RMS) é necessária para os computadores cliente utilizarem o Azure RMS com Office 2010 e é recomendada para todos os computadores e dispositivos móveis que suportam o Azure RMS. A aplicação de partilha RMS integra-se com aplicações do Office através da instalação de um suplemento do Office para que os utilizadores possam facilmente proteger ficheiros e e-mails diretamente do friso. De igual modo, proporciona proteção genérica a tipos de ficheiros que não são suportados nativamente pelo Azure RMS e possibilita um site de controlo de documentos para os utilizadores controlarem e revogarem ficheiros protegidos por eles.

## A aplicação de partilha RMS para o Windows: instalação e configuração
Para instalar e configurar a aplicação de partilha RMS para Windows para uma implementação empresarial, consulte o [Guia do administrador da aplicação de partilha Rights Management](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Se pretender instalar rapidamente e testar a aplicação de partilha RMS para um único computador, consulte [Transferir e instalar a aplicação de partilha Rights Management](../rms-client/install-sharing-app.md) no [Guia do utilizador da aplicação de partilha Rights Management](../rms-client/sharing-app-user-guide.md).

## A aplicação de partilha RMS para plataformas móveis: instalação e gestão
Para instalar a aplicação de partilha RMS para plataformas móveis, pode transferir a aplicação relevante utilizando as ligações na [página Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). Não é necessária nenhuma configuração para utilizar o Azure RMS com esta aplicação.

**Se tiver o Microsoft Intune**: uma vez que a aplicação de partilha RMS inclui o Microsoft Intune App Software Development Kit, tem as seguintes opções:

-   Para dispositivos que são inscritos pelo Intune, pode implementar e gerir a aplicação de partilha RMS para dispositivos com o iOS e Android. Para obter mais informações, consulte [Configurar e implementar políticas de gestão de aplicações móveis na consola do Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) na documentação do Intune. Para o Passo 2, utilize as instruções para publicar uma aplicação gerida por política.

-   Para os dispositivos que não são inscritos pelo Intune, pode gerir a aplicação de partilha RMS para dispositivos que executam Android. Para obter mais informações, consulte [Criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune).



<!--HONumber=Apr16_HO4-->


