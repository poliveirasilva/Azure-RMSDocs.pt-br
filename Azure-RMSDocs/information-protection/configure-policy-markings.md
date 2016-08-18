---
title: "Como configurar um rótulo para marcações visuais do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 78b68c7a502776c6492437e9b8a5c3f1ebf27f95


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

- Você pode especificar apenas uma cadeia de texto ou usar [variáveis](#using-variables-in-the-text-string) para criar a cadeia de texto de forma dinâmica quando o cabeçalho, o rodapé ou a marca d’água é aplicada. 

Use as instruções a seguir para configurar marcações visuais para um rótulo.

1. Se você ainda não fez isso, entre no [portal do Azure](https://portal.azure.com) e navegue até a folha **Azure Information Protection**. 
    
    Por exemplo, no menu hub, clique em **Procurar** e comece a digitar **Information** na caixa Filtro. Selecione **Azure Information Protection**.

2. Na folha **Azure Information Protection**, selecione o rótulo que deseja configurar para marcações visuais.

3. Na folha **Rótulo**, na seção **Definir marcação visual (como cabeçalho ou rodapé)**, defina as configurações dos marcadores visuais que deseja e, em seguida, clique em **Salvar**:

    - Para configurar um cabeçalho: em **Documentos com este rótulo tem um cabeçalho**, selecione **Ativado** se quiser um cabeçalho e **Desativado** se não quiser. Se você selecionar **Ativado**, especifique o texto, o tamanho, a cor e o alinhamento do cabeçalho.
    
    - Para configurar um rodapé: em **Documentos com este rótulo tem um rodapé**, selecione **Ativado** se quiser um rodapé e **Desativado** se não quiser. Se você selecionar **Ativado**, especifique o texto, o tamanho, a cor e o alinhamento do rodapé para o cabeçalho.
    
    - Para configurar uma marca-d’água: em **Documentos com este rótulo tem uma marca-d’água**, selecione **Ativado** se quiser uma marca-d’água e **Desativado** se não quiser. Se você selecionar **Ativado**, especifique o texto, o tamanho, a cor e o alinhamento da marca-d’água para o cabeçalho. 

4. Para disponibilizar as alterações aos usuários, na folha **Azure Information Protection**, clique em **Publicar**.

## Usando variáveis na cadeia de texto

É possível usar as seguintes variáveis na cadeia de texto do cabeçalho, do rodapé ou da marca d’água:

- `${Item.Label}` para o rótulo selecionado

- `${Item.Name}` para o nome do arquivo ou assunto do email

- `${Item.Location}` para o caminho do arquivo

- `${User.Name}` para o proprietário do documento ou email

- `${Event.DateTime}` para a data e hora em que o rótulo selecionado foi definido 
    
Exemplo: se você especificar a cadeia de caracteres `Document: ${item.name} Sensitivity: ${item.label}` para o rodapé do rótulo Segredo, o texto do rodapé aplicado a um project.docx nomeado e documentado será **Documento: project.docx Confidencialidade: Segredo**.

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  





<!--HONumber=Aug16_HO2-->


