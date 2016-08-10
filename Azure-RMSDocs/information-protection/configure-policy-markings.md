---
title: "Como configurar um rótulo para marcações visuais do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 9f2d28e4f162891497a7b0518322338628118b9d


---

# Como configurar um rótulo para marcações visuais do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Ao atribuir um rótulo a uma mensagem de email ou a um documento, você pode selecionar várias opções para facilitar a visualização da classificação escolhida. Essas marcações visuais são um cabeçalho, um rodapé e uma marca-d'água:

As marcações visual são aplicadas a documentos do Word, Excel e PowerPoint quando o rótulo é aplicado e quando o documento é salvo. Para mensagens de email, as marcações visuais são aplicadas quando a mensagem de email é enviada.

Informações adicionais sobre esses marcadores visuais:

- Cabeçalhos e rodapés aplicam-se ao Word, Excel, PowerPoint e Outlook.

- Marcas-d'água aplicam-se ao Word, Excel e PowerPoint:

    - Excel: as marcas-d'água somente são visíveis nos modos de Layout da Página e de visualização de Impressão e na impressão.

    - PowerPoint: as marcas-d'água são aplicadas ao slide mestre, como uma imagem de tela de fundo.

Use as instruções a seguir para configurar marcações visuais para um rótulo.

1. Entre no [Portal do Azure](https://portal.azure.com).
 
2. No menu hub, clique em **Procurar** e comece a digitar **Information** na caixa de filtro. Selecione **Azure Information Protection**.

3. Na folha **Azure Information Protection**, selecione o rótulo que deseja configurar para marcações visuais.

4. Na folha **Rótulo**, na seção **Definir marcação visual (como cabeçalho ou rodapé)**, defina as configurações dos marcadores visuais que deseja e, em seguida, clique em **Salvar**:

    - Para configurar um cabeçalho: em **Documentos com este rótulo tem um cabeçalho**, selecione **Ativado** se quiser um cabeçalho e **Desativado** se não quiser. Se você selecionar **Ativado**, especifique o texto, o tamanho, a cor e o alinhamento do cabeçalho.

    - Para configurar um rodapé: em **Documentos com este rótulo tem um rodapé**, selecione **Ativado** se quiser um rodapé e **Desativado** se não quiser. Se você selecionar **Ativado**, especifique o texto, o tamanho, a cor e o alinhamento do rodapé para o cabeçalho.

    - Para configurar uma marca-d’água: em **Documentos com este rótulo tem uma marca-d’água**, selecione **Ativado** se quiser uma marca-d’água e **Desativado** se não quiser. Se você selecionar **Ativado**, especifique o texto, o tamanho, a cor e o alinhamento da marca-d’água para o cabeçalho.

5. Para disponibilizar as alterações aos usuários, na folha **Azure Information Protection**, clique em **Publicar**.

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  





<!--HONumber=Jul16_HO5-->


