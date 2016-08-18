---
title: "Configurando a política do Azure Information Protection | RMS do Azure"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 781632c5a28377339431cd6537b1b9e11d0a3259
ms.openlocfilehash: 0e31053a83c30d8552cfb78914d0d13baac25f42


---

# Configurando a política do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Para configurar a classificação, a rotulagem e a proteção, você deverá configurar a política do Azure Information Protection. Em seguida, essa política será baixada nos computadores que tenham instalado o [cliente Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Para configurar a política do Azure Information Protection durante a versão de preview do Azure Information Protection:

1. Entre no [Portal do Azure](https://portal.azure.com).

2. Navegue até a folha **Azure Information Protection**: por exemplo, no menu hub, clique em **Procurar** e comece a digitar **Information Protection** na caixa Filtro. Nos resultados, selecione **Azure Information Protection**. 

    Em seguida, será exibida a folha **Azure Information Protection**, em que você poderá configurar a política do Azure Information Protection, que contém os seguintes elementos:

    - Título e dica de ferramenta da barra do Information Protection que aparecem para os usuários em seus aplicativos do Office.

    - Rótulos que permitem que você e os usuários classifiquem documentos e emails.

    - A opção para aplicar a classificação quando os usuários salvam documentos e enviam emails.

    - A opção para definir um rótulo padrão como ponto de partida para classificar documentos e emails.

    - A opção para solicitar que os usuários forneçam um motivo ao selecionarem um rótulo com um nível de confidencialidade inferior ao original.


O Azure Information Protection vem com uma [política padrão](configure-policy-default.md), que contém os rótulos **Pessoal**, **Público**, **Interno**, **Confidencial** e **Secreto**. Você pode usar os rótulos padrão sem alterações ou personalizá-los, ou você pode excluí-los e criar novos rótulos.

Ao fazer alterações em uma folha do Azure Information Protection, clique em **Salvar** para salvar as alterações ou em **Descartar** para reverter para a última configuração salva. 

Ao concluir as alterações desejadas, clique em **Publicar**. 

O cliente Azure Information Protection verifica se há alterações sempre que um aplicativo do Office com suporte é iniciado e baixa as alterações como sua política do Azure Information Protection.

## Configurando a política da organização

Use as seguintes informações para ajudá-lo a configurar a política do Azure Information Protection:

- [A política padrão do Information Protection](configure-policy-default.md)

- [Como definir as configurações da política global](configure-policy-settings.md)

- [Como criar um novo rótulo](configure-policy-new-label.md)

- [Como excluir ou reordenar um rótulo](configure-policy-delete-reorder.md)

- [Como alterar ou personalizar um rótulo existente](configure-policy-change-label.md)

- [Como configurar um rótulo para aplicar proteção](configure-policy-protection.md)

- [Como configurar um rótulo para aplicar marcações visuais](configure-policy-markings.md)

- [Como configurar condições para classificação automática e recomendada](configure-policy-classification.md)

## Próximas etapas

Para obter um exemplo de como personalizar a política padrão e ver o comportamento resultante em um aplicativo do Office, experimente o [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Aug16_HO2-->


