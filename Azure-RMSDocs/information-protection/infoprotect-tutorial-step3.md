---
title: "Etapa 3 do tutorial de início rápido do Azure Information Protection | Azure Rights Management"
description: "Etapa 3 de um tutorial de introdução para testar rapidamente o Microsoft Azure Information Protection para sua organização com apenas 4 etapas que devem levar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 65596a71b07e830377c55dc04b7187251315a634


---

# Etapa 3: Instalar o cliente do Azure Information Protection 

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Nesta etapa, você instalará o cliente do Azure Information Protection para que a política que acabou de configurar seja baixada em um computador Windows e mostre os rótulos nos aplicativos do Office. 

1. Em um computador que tenha o Office instalado (mas o Word não esteja aberto no momento), [baixe o cliente do Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) do Centro de Download da Microsoft. 

2. Execute **AZInfoProtection.exe** e siga os prompts para instalar o cliente.

    Para este tutorial, não importa se você selecionar a opção para instalar uma política de demonstração, porque a política que acabamos de configurar será baixada do Azure e substituirá a política de demonstração se ela estiver instalada. No entanto, você pode usar a opção de política de demonstração se desejar apenas testar os rótulos padrão, sem se conectar ao Azure Information Protection. 

3. Verifique se o cliente foi instalado abrindo o Word e um novo documento em branco (não o salve desta vez). Se você for solicitado a inserir seu nome de usuário e senha, insira os detalhes de sua conta de administrador global. Quando o documento for carregado, você verá dois itens novos:

    - Uma guia **Página Inicial**, um novo grupo **Proteção** com um botão rotulado como **Proteger**.

        Clique em **Proteger** > **Ajuda e comentários** e, na caixa de diálogo **Microsoft Azure Information Protection**, confirme o status do cliente. Ela deve exibir **Information Protection policy is installed** (A política do Information Protection está instalada) e o horário de uma conexão recente. Verifique se o nome de usuário exibido está correto para seu locatário.

    - Uma nova barra é exibida abaixo da faixa de opções, a barra do Information Protection. Ela exibe o título de **Confidencialidade** e o rótulo padrão que configuramos de **Interno**. 


![Etapa 3 do tutorial de início rápido do Azure Information Protection – cliente instalado](../media/word2013-callouts.png)

Você está pronto para a etapa final, para ver a classificação, a rotulação e a proteção em ação.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Sobre a instalação do cliente|[Instalando o cliente Azure Information Protection](info-protect-client.md)|


>[!div class="step-by-step"]
[&#171; Etapa 2](infoprotect-tutorial-step2.md)
[Etapa 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Jul16_HO5-->


