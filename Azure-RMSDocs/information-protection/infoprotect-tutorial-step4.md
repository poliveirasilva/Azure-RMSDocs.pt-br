---
title: "Etapa 4 do tutorial de início rápido do Azure Information Protection | Azure Rights Management"
description: "Etapa 4 de um tutorial de introdução para testar rapidamente o Microsoft Azure Information Protection para sua organização com apenas 4 etapas que devem levar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: e80ea074fb1f6e571b846969b15c08cf7108b11c
ms.openlocfilehash: dcb34eb8bfee6232d32245634dc56f717257b644


---

# Etapa 4: Ver a classificação, a rotulação e a proteção em ação 

*Aplica-se a: visualização do Azure Information Protection*

Agora que você tem um documento do Word aberto com o cliente do Azure Information Protection instalado, está pronto para ver como é fácil começar a rotular e proteger seu documento usando a política que configuramos.

A classificação e a proteção acontecem quando você salva o documento, mas antes de fazermos isso, usaremos nosso documento não salvo para ver como é fácil aplicar e alterar os rótulos.

### Para alterar manualmente nosso rótulo padrão:

- Na barra Information Protection, clique no ícone Editar rótulo ao lado de **Interno**. Isso exibe os rótulos disponíveis. Escolha **Pessoal** e você será solicitado a justificar o motivo de estar diminuindo o nível de classificação. Selecione **This file no longer requires that classification** (Este arquivo não precisa mais da classificação) e clique em **Confirmar**.  

    Você verá o **Confidencialidade** mudar para **Pessoal**.

    ![Etapa 4 do tutorial de início rápido do Azure Information Protection – solicitação para confirmar o motivo da diminuição](../media/confirm-lowering.png)

### Para remover completamente a classificação:

- Na barra Information Protection, clique no ícone Editar rótulo ao lado de **Pessoal**. Isso exibe os rótulos disponíveis. Mas, em vez de escolher um dos rótulos, desta vez, clique no ícone Remover rótulo. Clique em **OK** para confirmar e fornecer uma justificativa para essa ação.  

    Você verá o valor **Confidencialidade** mostrar **Não definido**, que é o que os usuários veem inicialmente se você não definir um rótulo padrão.

    ![Etapa 4 do tutorial de início rápido do Azure Information Protection – remover classificação](../media/sensitivity-not-set.png)


### Para ver um prompt de recomendação para a rotulação e proteção automática:

1. No documento do Word, digite um número de cartão de crédito válido, por exemplo: **4242-4242-4242-4242**. 

2. Salve o documento (use qualquer nome de arquivo, qualquer localização). 

3. Agora você vê o prompt: **It is recommended to label this file as Confidential** (É recomendável rotular esse arquivo como Confidencial). Clique em **Alterar agora**.

    ![Etapa 4 do tutorial de início rápido do Azure Information Protection – prompt de recomendação](../media/change-now.png)

    Imediatamente, você verá a marca-d'água do nome da sua organização na largura da página, além do rodapé de **Sensitivity: Confidential** (Confidencialidade: Confidencial). 

    Se você escolher a opção de aplicar um modelo de RMS, o documento também será protegido com o modelo do Azure Rights Management especificado, que você pode confirmar ao clicar na guia **Arquivo** guia e exibir as informações de **Proteger Documento**. Se você usou o modelo Confidencial padrão, verá as informações de que o documento é restrito aos usuários internos (os usuários fora da sua organização não poderão abrir o documento) e seu conteúdo não pode ser copiado ou impresso. Como o proprietário do documento, você pode copiá-lo e imprimi-lo, mas se enviá-lo por email para outro usuário na sua organização, ele não poderá executar essas ações.

> [!NOTE]
>Se você tiver problemas ao concluir essas etapas, na guia **Página Inicial**, no grupo **Proteção**, clique em **Proteger** e clique em **Ajuda e Comentários**. 
>
>Na caixa de diálogo **Microsoft Azure Information Protection**, clique em **Enviar comentários**. Isso envia um email para a equipe do Information Protection e anexa automaticamente os arquivos de log do seu computador para ajudar a diagnosticar os problemas.

##  Próximas etapas

Agora você já viu a política padrão do Azure Information Protection e como personalizá-la e como a rotulação funciona para um documento do Word, experimente algumas outras configurações e veja como elas funcionam em outros aplicativos do Office que dão suporte ao Azure Information Protection: Excel, PowerPoint, Outlook. Se esses aplicativos estavam abertos quando você instalou o cliente do Azure Information Protection, feche-os e reabra-os antes de tentar usá-los com o Azure Information Protection.

Por exemplo, você pode alterar o título padrão de **Confidencialidade** na barra do Information Protection para um título de sua escolha. Pode alterar as dicas de ferramentas, as cores de rótulo, a ordem dos rótulos e seus nomes. Pode criar novos rótulos e definir suas próprias regras automáticas. Pode ajustar as marcas-d'água, configurando o tamanho e a cor e alterar de diagonal para horizontal.

Observe que se você estiver usando marcas-d'água com o Excel, elas serão visíveis somente nos modos Layout de página e Visualização de impressão e ao serem impressas.

Sempre que você alterar qualquer configuração no Portal do Azure para a política do Information Protection, lembre-se de **salvar** a política e depois **publicá-la**. Como você pode fazer alterações em várias folhas, é uma boa ideia verificar se todas as folhas não mostram o botão **Salvar** como habilitado, o que indica que você tem alterações não salvas. Se seu aplicativo do Office estava aberto quando você publicou novas alterações, feche o aplicativo e abra-o novamente para baixar a política mais recente.

Quando terminar seus próprios testes, talvez seja útil para examinar as [perguntas frequentes sobre o Azure Information Protection](faq.md).




<!--HONumber=Jul16_HO3-->


