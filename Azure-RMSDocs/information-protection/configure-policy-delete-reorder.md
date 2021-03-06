---
title: "Como excluir ou reordenar um rótulo do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 3b4066c8e5770e6f4a502ecaebfd961400e9df2d


---

# Como excluir ou reordenar um rótulo do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Você pode excluir ou reordenar os rótulos que aparecem para os usuários na barra do Information Protection, definindo essa configuração na política do Azure Information Protection.

![Excluir ou reordenar rótulos na política do Azure Information Protection](../media/info-protect-contextmenu.png)

Em vez de excluir um rótulo, convém simplesmente desabilitá-lo, mantendo sua configuração, mas impedindo sua exibição na barra do Information Protection.

Ordene os rótulos para que sejam exibidos aos usuários em uma progressão lógica na barra do Information Protection. Por exemplo, ordene os rótulos por aumento de confidencialidade para que os usuários vejam o rótulo menos confidencial primeiro e o mais confidencial por último. A [política padrão](configure-policy-default.md) usa essa configuração.

> [!IMPORTANT]
>Se você configurar [condições](configure-policy-classification.md) para os rótulos que possam se aplicar a mais de um rótulo, você deverá ordenar os rótulos do menos confidencial para o mais confidencial. Essa ordenação garantirá que o rótulo mais confidencial seja aplicado quando as condições forem avaliadas.


Use as instruções a seguir para fazer essas alterações.

1. Se você ainda não fez isso, entre no [portal do Azure](https://portal.azure.com) e navegue até a folha **Azure Information Protection**. 
    
    Por exemplo, no menu hub, clique em **Procurar** e comece a digitar **Information** na caixa Filtro. Selecione **Azure Information Protection**.

2. Na folha **Azure Information Protection**, realize uma das ações a seguir para excluir, desabilitar ou reorganizar um rótulo:

    - Para excluir um rótulo: clique com o botão direito do mouse ou selecione o menu de contexto (**...**) do rótulo que deseja excluir, clique em **Excluir esse rótulo**, e clique em **Sim** para confirmar. Em seguida, clique em **Salvar**. 

    - Para desabilitar um rótulo: selecione o rótulo que deseja desabilitar. Na folha **Rótulo**, para **Habilitado**, clique em **Desativado** e, em seguida, clique em **Salvar**.

    - Para reordenar um rótulo: clique com o botão direito do mouse ou selecione o menu de contexto (**...**) do rótulo que deseja reordenar e clique em **Mover para cima** ou em **Mover para baixo** até que o rótulo fique na ordem desejada. Em seguida, clique em **Salvar**. 

3. Para disponibilizar as alterações aos usuários, na folha **Azure Information Protection**, clique em **Publicar**.

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  





<!--HONumber=Aug16_HO2-->


