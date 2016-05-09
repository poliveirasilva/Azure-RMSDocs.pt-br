---
# required metadata

title: Como este SDK é melhor | Azure RMS
description: Esse tópico descreve como o RMS SDK 2.1 é uma melhoria significativa com relação ao Active Directory Rights Management Services SDK original.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ee4989d6-3903-4ed2-ac62-d5692e2ef494

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Como este SDK é melhor
Este tópico descreve como o Rights Management Services SDK 2.1 é uma melhoria significativa em relação a [SDK original do Active Directory Rights Management Services](https://msdn.microsoft.com/library/Cc530379) em termos de esforço de desenvolvimento necessário para criar um aplicativo habilitado para direitos.

**Superfície de API** - a superfície de API foi reduzida significativamente por abstração, liberando você de muitos dos detalhes de implementação de back-end. De uma superfície de API de 84 funções para o SDK do RMS, o RMS SDK 2.1 inclui apenas 20 funções de API. A maioria dos aplicativos precisará usar apenas um pequeno subconjunto dessa superfície de API.

**Tempo de aprendizado** -com o RMS SDK 2.1, você poderá seguir um guia passo a passo para identificar quais recursos do aplicativo são confidenciais e como protegê-los. Isso é diferente do RMS SDK, com a qual você precisava ter conhecimento avançado dos certificados, formatos e topologias e escrever códigos complexos para multithreading.

**Suporte múltiplas topologias** - o RMS SDK 2.1 ajuda a minimizar a regravação de código. Seu aplicativo deve funcionar com todas as topologias à medida que eliminamos a complexidade de topologia para os desenvolvedores. Com o RMS SDK, era necessário entender todas as topologias com suporte, em seguida, escrever e testar o código específico para cada.

**À prova de obsolência** - o RMS SDK 2.1 ajuda a minimizar a regravação de seu código de ativação de direitos; seu aplicativo deve funcionar em qualquer ambiente de RMS e automaticamente tirar proveito dos novos recursos quando recursos principais atualizados do RMS forem lançados. Isso é diferente do AD RMS SDK, que você precisava atualizar seu aplicativo para aproveitar os novos recursos explicitamente.

**Aviso importante**  
Todos os tópicos no [Active Directory Rights Management Services SDK original](https://msdn.microsoft.com/library/Cc530379) na biblioteca MSDN agora começam com a seguinte instrução de suporte:

O AD RMS SDK, que aproveita a funcionalidade exposta pelo cliente em Msdrm.dll, está disponível para uso no Windows Server 2008, Windows Vista, Windows Server 2008 R2, Windows 7, Windows Server 2012 e Windows 8. Ele poderá ser alterado ou ficar indisponível em versões subsequentes. Em seu lugar, use o [Active Directory Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md), que aproveita a funcionalidade exposta pelo cliente em *Msipc.dll*.

 

## Tópicos relacionados ##
* [Visão geral](ad-rms-overview.md)
* [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Apr16_HO3-->


