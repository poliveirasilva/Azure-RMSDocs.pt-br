---
title: "Noções básicas sobre restrições de uso | Azure RMS"
description: "Todos os aplicativos habilitados para RMS devem impor restrições de uso."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 872bb0c20db2ef8d661d321598a2b1fe61d69316
ms.openlocfilehash: 2d2cbe580349e1615371a6a76e78140f6577e890


---

# Noções básicas sobre restrições de uso

Todos os aplicativos habilitados para RMS devem impor restrições de uso. Uma restrição de uso é uma condição que ocorre quando um usuário tenta executar uma ação (por exemplo, imprimir um documento), mas a política do RMS para esse documento não concede a ele permissão ou direito de executar essa ação (por exemplo, o direito PRINT).

As permissões do usuário para um documento podem ser consultadas usando a função [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck).

## Noções básicas sobre restrições de uso

-   Familiarize-se com direitos RMS padrão

    Para o conjunto completo de direitos RMS que seu aplicativo pode impor, consulte [Referência de restrição de uso](usage-restriction-reference.md).

    Observe que o aplicativo definiu direitos específicos para sua situação e que vão além dos direitos RMS padrão que podem ser criados.

-   Identificar os pontos de imposição de restrição de uso

    Um *ponto de imposição da restrição de uso* é um lugar no fluxo de controle do seu aplicativo em que é necessário impor uma restrição de uso. O tópico [Referência de restrição de uso](usage-restriction-reference.md) fornece vários exemplos de pontos de imposição comuns.

    Avalie seu próprio aplicativo para determinar quais pontos de restrição de uso se aplicam.

    Seu aplicativo pode não precisar de todos os pontos de imposição descritos na [Referência de restrição de uso](usage-restriction-reference.md). Por exemplo, se seu aplicativo não permitir que os usuários imprimam o conteúdo, ele não precisará verificar o direito **IPC\_GENERIC\_PRINT**.

-   Atualizar seu código para executar uma verificação de acesso em cada ponto de imposição

    Para obter diretrizes de como impor direitos específicos, consulte [Referência de restrição de uso](usage-restriction-reference.md).

## Tópicos relacionados

* [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck)
* [Referência de restrição de uso](usage-restriction-reference.md)
 

 



<!--HONumber=Jun16_HO4-->


