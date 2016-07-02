---
title: "Aplicativo de compartilhamento Rights Management&colon; instalação e configuração para clientes | Azure RMS"
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
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: d3f923cf6f140c2caa75b7b0c8ac90a42be962a7


---

# Aplicativo de compartilhamento do Rights Management: Instalação e configuração para clientes

*Aplica-se a: Azure Rights Management, Office 365*

O aplicativo de compartilhamento do Rights Management (RMS) é necessário para computadores clientes usarem o Azure RMS com o Office 2010 e é recomendado para todos os computadores e dispositivos móveis que oferecem suporte ao Azure RMS. O aplicativo de compartilhamento do RMS se integra com os aplicativos do Office por meio da instalação de um suplemento do Office para que os usuários possam proteger facilmente arquivos e emails diretamente da faixa de opções. Ele também torna possível proteger todos os tipos de arquivos que não tenham suporte nativo pelo Azure Rights Management, além disso oferece um site para controle de documentos, em que usuários podem controlar e revogar os arquivos que tenham protegido.

## O aplicativo de compartilhamento do RMS para Windows: Instalação e configuração
Para instalar e configurar o aplicativo RMS sharing para Windows para uma implantação corporativa, consulte o [Guia do administrador do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Se você quiser instalar e testar o aplicativo RMS sharing para um único computador rapidamente, consulte [Baixar e instalar o aplicativo de compartilhamento do Rights Management](../rms-client/install-sharing-app.md) do [Guia do usuário do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-user-guide.md).

## O aplicativo RMS sharing para plataformas móveis: instalação e gerenciamento
Para instalar o aplicativo de compartilhamento do RMS para plataformas móveis, baixe o aplicativo relevante usando os links na [página do Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). Nenhuma configuração é necessária para usar o Azure RMS com este aplicativo.

**Se você tiver o Microsoft Intune**: já que o aplicativo RMS sharing inclui o Software Development Kit do Aplicativo do Microsoft Intune, você tem as seguintes opções:

-   Para dispositivos registrados pelo Intune, você pode implantar e gerenciar o aplicativo RMS sharing para dispositivos que executam o iOS e o Android. Para obter mais informações, consulte [Configurar e implantar políticas de gerenciamento de aplicativo móvel no console do Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console). Para a Etapa 2, use as instruções para publicar um aplicativo gerenciado por política.

-   Para dispositivos não registrados pelo Intune, você pode gerenciar o aplicativo RMS sharing para dispositivos que executam o Android. Para obter mais informações, consulte [Criar e implantar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune).




<!--HONumber=Jun16_HO4-->


