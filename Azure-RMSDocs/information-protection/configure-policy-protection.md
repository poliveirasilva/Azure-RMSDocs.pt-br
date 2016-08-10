---
title: "Como configurar um rótulo para aplicar a proteção do Rights Management | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# Como configurar um rótulo para aplicar a proteção do Rights Management

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Você pode proteger seus documentos e emails mais confidenciais usando o Azure Rights Management, que usa políticas de criptografia, identidade e autorização para ajudar a evitar a perda de dados. Essa proteção é aplicada quando você configura um rótulo para usar um modelo do Rights Management. 

Esse modelo pode ser um dos modelos padrão que são criados automaticamente quando você ativa o Azure Rights Management ou um modelo personalizado. Há suporte para modelos departamentais, mas eles somente aplicam a proteção quando o autor do documento ou email está dentro do escopo configurado do modelo. Se o usuário não estiver dentro do escopo, ele verá uma mensagem de que o Azure Information Protection não pode aplicar o rótulo.

## Como funciona a proteção

Quando um documento ou email estiver protegido pelo Azure Rights Management, ele será criptografado em repouso e em trânsito e somente poderá ser descriptografado por usuários autorizados. Essa criptografia permanecerá no documento ou email, mesmo se ele for renomeado. Além disso, você pode configurar os direitos e as restrições de uso, como os exemplos a seguir:

- Somente os usuários da sua organização podem abrir o documento ou email.

- Somente os usuários no departamento de marketing podem editar e imprimir o documento ou email, enquanto todos os outros usuários na sua organização somente podem exibi-lo.

- Os usuários não podem encaminhar um email.

- Documentos ou emails enviados aos parceiros comerciais não podem ser abertos após uma data especificada.

Para obter mais informações sobre os modelos e como configurar essas restrições e direitos de uso, consulte [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para obter mais informações sobre o Azure Rights Management e como ele funciona, consulte [O que é o Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Para configurar um rótulo para aplicar a proteção do Rights Management, o serviço do Azure Rights Management deve ser ativado para sua organização. Se isso ainda não foi feito, consulte [Ativando o Azure Rights Management](../deploy-use/activate-service.md).


## Para configurar um rótulo para aplicar a proteção do Rights Management

1. Entre no [Portal do Azure](https://portal.azure.com).
 
2. No menu hub, clique em **Procurar** e comece a digitar **Information** na caixa de filtro. Selecione **Azure Information Protection**.

3. Na folha **Azure Information Protection**, selecione o rótulo que deseja configurar para aplicar a proteção do Rights Management.

4. Na folha **Rótulo**, na seção **Definir modelo RMS para proteger documentos e emails que contenham este rótulo**, configure o seguinte:

    - Se aparecer **Selecionar modelo RMS de**:, selecione **RMS do Azure**. 
    
        Não selecione **AD RMS** e as opções de configuração associadas sem assistência da Microsoft. Se você tiver interesse em testar o Azure Information Protection com o Active Directory Rights Management Services, envie um email para askipteam@microsoft.com. 
    
    - Em **Selecionar modelo RMS**: clique na caixa suspensa e selecione o modelo que deseja usar para proteger documentos e emails com este rótulo.

        > [!NOTE] Se você criar um novo modelo depois de abrir a folha **Rótulo**, feche essa folha e retorne à etapa 3, para que o novo modelo seja recuperado do Azure e possa ser selecionado.

5. Clique em **Salvar**.

6. Para disponibilizar as alterações aos usuários, na folha **Azure Information Protection**, clique em **Publicar**.

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  



<!--HONumber=Jul16_HO5-->


