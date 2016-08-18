---
title: "Como configurar um rótulo para aplicar a proteção do Rights Management | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 798fb423ff8dab3e9777a33e7b2c483bceb81016


---

# Como configurar um rótulo para aplicar a proteção do Rights Management

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Você pode proteger seus documentos e emails mais confidenciais usando o Azure Rights Management, que usa políticas de criptografia, identidade e autorização para ajudar a prevenir a perda de dados. Essa proteção é aplicada quando você configura um rótulo para usar um modelo do Rights Management. 

Esse modelo pode ser um dos modelos padrão que são criados automaticamente quando você ativa o Azure Rights Management ou um modelo personalizado. Há suporte para modelos departamentais do Azure Rights Management, mas eles somente aplicam a proteção quando o autor do documento ou email está dentro do escopo configurado do modelo. Se o usuário não estiver dentro do escopo, ele verá uma mensagem de que o Azure Information Protection não pode aplicar o rótulo.

## Como funciona a proteção

Quando um documento ou email estiver protegido pelo Rights Management, ele será criptografado em repouso e em trânsito e somente poderá ser descriptografado por usuários autorizados. Essa criptografia permanecerá no documento ou email, mesmo se ele for renomeado. Além disso, você pode configurar os direitos e as restrições de uso, como os exemplos a seguir:

- Somente os usuários de sua organização podem abrir o documento ou email confidencial da empresa.

- Somente os usuários do departamento de marketing podem editar e imprimir o documento ou email que contêm comunicado promocional, enquanto todos os outros usuários na organização somente podem lê-lo.

- Os usuários não podem encaminhar um email que contém notícias sobre uma reorganização interna.

- A lista de preços atual enviada ao parceiros de negócios não pode ser aberta após uma data especificada.

Para obter mais informações sobre os modelos do Azure Rights Management e como configurar essas restrições e direitos de uso, veja [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para obter mais informações sobre o Azure Rights Management e como ele funciona, consulte [O que é o Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Para configurar um rótulo para aplicar a proteção do Azure Rights Management, o serviço Azure Rights Management deve ser ativado para sua organização. Se isso ainda não foi feito, consulte [Ativando o Azure Rights Management](../deploy-use/activate-service.md).


## Para configurar um rótulo para aplicar a proteção do Rights Management

1. Se você ainda não fez isso, entre no [portal do Azure](https://portal.azure.com) como administrador global para que você possa recuperar os modelos do Azure Rights Management. Em seguida, navegue até a folha **Azure Information Protection**. 

    Por exemplo, no menu hub, clique em **Procurar** e comece a digitar **Information** na caixa Filtro. Selecione **Azure Information Protection**.

2. Na folha **Azure Information Protection**, selecione o rótulo que deseja configurar para aplicar a proteção do Rights Management.

3. Na folha **Rótulo**, na seção **Definir modelo do RMS para proteger documentos e emails que contêm este rótulo**, em **Selecionar modelo do RMS de**, selecione **Azure RMS** ou **AD RMS (VISUALIZAÇÃO)**.
    
    Na maioria dos casos, você selecionará **Azure RMS**. Não selecione o AD RMS, a menos que você tenha lido e entendido os pré-requisitos e as restrições que acompanham esta configuração, que às vezes é denominada HYOK (“*mantenha sua própria chave*”). Para obter mais informações, veja [Requisitos e restrições de HYOK (Mantenha sua própria chave) para a proteção do AD RMS](configure-adrms-restrictions.md).
    
4. Se você selecionou o Azure RMS: em **Selecionar modelo do RMS**, clique na caixa suspensa e selecione o modelo que deseja usar para proteger documentos e emails com este rótulo.

    > [!NOTE] 
    > Se você criar um novo modelo depois de abrir a folha **Rótulo**, feche essa folha e retorne à etapa 2, para que o novo modelo seja recuperado do Azure e possa ser selecionado.
    
5. Se você selecionou o AD RMS: forneça o GUID do modelo e a URL de licenciamento referente ao cluster do AD RMS.

5. Clique em **Salvar**.

6. Para disponibilizar as alterações aos usuários, na folha **Azure Information Protection**, clique em **Publicar**.

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  



<!--HONumber=Aug16_HO2-->


