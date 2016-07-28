---
title: "Tutorial de início rápido do Azure Information Protection | Azure Rights Management"
description: "Um tutorial de introdução para testar rapidamente o Microsoft Azure Information Protection para sua organização com apenas 4 etapas que devem levar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1260b9e5-dba1-41de-84fd-609076587842
translationtype: Human Translation
ms.sourcegitcommit: cac95dec84f99d2e6caa3458dc8284defe2324bc
ms.openlocfilehash: 7dc988365c1fa86827d1a7edc33c0a2eb6180f0e


---

# Tutorial de início rápido do Azure Information Protection 

*Aplica-se a: visualização do Azure Information Protection*

Use esse tutorial para testar rapidamente a visualização do Azure Information Protection para sua organização com apenas 4 etapas que devem levar menos de 15 minutos. Opcionalmente, você ativará o Azure Rights Management Service, examinará e modificará a política padrão do Azure Information Protection, instalará o cliente do Azure Information Protection e usará um documento Word para ver a classificação, o rotulamento e a proteção em ação.

Este tutorial é destinado a administradores de TI e consultores, para ajudar a avaliar o Azure Information Protection como uma solução de proteção de informações corporativas para uma organização. Em um ambiente de produção, as instruções para ativar o serviço, configurar a política do Information Protection e instalar o cliente para os usuários seriam realizadas por um administrador. As instruções para rotular o documento seriam realizadas pelos usuários finais. Ambos os conjuntos de instruções estão incluídos neste tutorial, para demonstrar o cenário completo de classificação, rotulação e proteção dos dados da sua organização. 

Se você tiver problemas para concluir este tutorial, usando a versão de visualização do Azure Information Protection, ou quiser ver o que as pessoas estão dizendo sobre ele, vá até o [site do Yammer sobre o Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all).

## Pré-requisitos 
Para concluir este tutorial, você precisará do seguinte:

- Qualquer assinatura que inclua o Azure Rights Management, que lhe dará acesso à versão de visualização do Azure Information Protection. O Azure Information Protection está disponível em todas as regiões que dão suporte ao Azure Rights Management. Para obter mais informações sobre as assinaturas disponíveis e os links para avaliações gratuitas, consulte [Requisitos do Azure RMS: assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).

- Uma assinatura do Azure, para que possa acessar o Portal do Azure para configurar a política do Azure Information Protection. Se você ainda não tiver uma assinatura do Azure para sua organização, poderá obtê-la se inscrevendo em uma avaliação gratuita: vá para a [página Introdução ao Azure](https://account.windowsazure.com/organization) e siga as instruções.

  > [!TIP] 
  > Se precisar obter uma ou ambas as assinaturas, faça isso com antecedência, pois esse processo pode levar um tempo para ser concluído.

- Uma conta de administrador global para entrar no Centro de administração do Office 365 ou no Portal Clássico do Azure, se você precisar ativar o Rights Management Service. Essa conta também deve ter um endereço de email e um serviço de email em atividade (por exemplo, Exchange Online ou Exchange Server).

- Um computador executando o Windows (no mínimo, Windows 7 com Service Pack 1) e que tenha instalado o Office 2016, Office 2013 com Service Pack 1 ou Office 2010. 

- Se você tiver o AD RMS (Active Directory Rights Management Services) implantado em sua organização: o computador precisará ser um computador de grupo de trabalho que não usou o AD RMS anteriormente. Isso é necessário se você quiser proteger documentos e garantir que o computador baixe modelos apenas do Azure Rights Management. Não há suporte para um computador se conectar ao AD RMS e ao Azure RMS ao mesmo tempo. Se você estiver interessado em informações sobre a migração, consulte [Migrando do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).   

Vamos começar.

>[!div class="step-by-step"]
[&#187; Etapa 1](infoprotect-tutorial-step1.md)





<!--HONumber=Jul16_HO3-->


