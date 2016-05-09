---
# required metadata

title: Operações para sua chave de locatário do Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Operações para sua chave de locatário do Azure Rights Management
Dependendo da topologia da sua chave de locatário (gerenciada pela Microsoft ou gerenciada pelo cliente), você tem diferentes níveis de controle e responsabilidade para sua chave de locatário do Microsoft Azure Rights Management (Azure RMS) após ser implantado.

Quando você gerencia sua própria chave de locatário, esta é geralmente chamada de trazer sua própria chave (BYOK). Para obter mais informações sobre esse cenário e de como escolher entre as duas topologias de chave de locatário, consulte [Planejamento e implementação da sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

A tabela a seguir identifica as operações que você pode realizar, dependendo da topologia escolhida para sua chave de locatário do Azure RMS.

|Operação do ciclo de vida|Gerenciada pela Microsoft (padrão)|Gerenciada pelo cliente (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Revogue sua chave de locatário|Não (automático)|Não (automático)|
|Crie novamente sua chave de locatário|Sim|Sim|
|Faça backup e recupere sua chave de locatário|Não|Sim|
|Exportar sua chave de locatário|Sim|Não|
|Responder a uma violação|Sim|Sim|

Depois de ter identificado a topologia que você implementou, use uma das seções a seguir para obter mais informações sobre estas operações para sua chave de locatário do Azure RMS:


- [Chave de locatário gerenciada pela Microsoft](operations-microsoft-managed-tenant-key.md)
- [Chave de locatário gerenciada pelo cliente](operations-customer-managed-tenant-key.md)






<!--HONumber=Apr16_HO3-->


