---
title: "Como definir as configurações globais da política do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 508161474bf6fd7406668de3976206947de254de


---

# Como definir as configurações globais da política do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Há três configurações na política do Azure Information Protection que se aplicam a todos os usuários e a todos os dispositivos:

![Configurações globais da política do Azure Information Protection](../media/info-protect-policy-settings.png)


Para definir essas configurações:

1. Se você ainda não fez isso, entre no [portal do Azure](https://portal.azure.com) e navegue até a folha **Azure Information Protection**. 
    
    Por exemplo, no menu hub, clique em **Procurar** e comece a digitar **Information** na caixa Filtro. Selecione **Azure Information Protection**.

2. Na folha **Azure Information Protection**, defina estas configurações globais:

    - **Todos os documentos e emails devem ter um rótulo**: quando essa opção for configurada como **Ativado**, todos os documentos salvos e os email enviados deverão ter um rótulo aplicado. Os rótulos podem ser atribuídos manualmente por um usuário, automaticamente como resultado de uma [condição](configure-policy-classification.md) ou por padrão (ao definir a opção **Selecione o rótulo padrão**). 

    Se um rótulo não for atribuído quando um usuário salvar um documento ou enviar um email, será solicitado que ele selecione um rótulo:

    ![Aviso do Azure Information Protection se a nova classificação for inferior](../media/info-protect-enforce-label.png)

    - **Selecione o rótulo padrão**: ao definir essa opção, selecione o rótulo para atribuir a documentos e emails que não têm um rótulo. Você não pode definir como padrão um rótulo que tenha sub-rótulos. 

    - **Os usuários devem fornecer justificativa ao diminuir o nível de confidencialidade**: quando você define esta opção como **Ativado** e um usuário altera o rótulo de um documento ou email existente para um rótulo com um nível de confidencialidade inferior (por exemplo, de **Secreto** para **Público**), é solicitado que o usuário forneça uma explicação para essa ação. Por exemplo, o usuário pode explicar que o documento deixou de conter informações confidenciais. A ação e o motivo de justificativa são registrados no log de eventos local do Windows: **Aplicativo** > **Microsoft Azure Information Protection**.  

    ![Aviso do Azure Information Protection se a nova classificação for inferior](../media/info-protect-lower-justification.png)

    Essa opção não se aplica a sub-rótulos.

3. Para salvar suas alterações, clique em **Salvar**.

4. Para disponibilizar as alterações aos usuários, clique em **Publicar**.

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  












<!--HONumber=Aug16_HO2-->


