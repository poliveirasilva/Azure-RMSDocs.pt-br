---
title: "Etapa 2 do tutorial de início rápido do Azure Information Protection | Azure Rights Management"
description: "Etapa 2 de um tutorial de introdução para testar rapidamente o Microsoft Azure Information Protection para sua organização com apenas 4 etapas que devem levar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: cab45baf19af4ab548f5f112946d168d93a95d49
ms.openlocfilehash: fa17a5b18162ca7ca1ac0cf9a1052dd01d2057aa


---

# Etapa 2: Configurar e publicar a política do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Embora o Azure Information Protection seja fornecido com uma política padrão que pode ser usada sem configuração, analisaremos essa política e faremos algumas alterações.

1. Entre no [Portal do Azure](https://portal.azure.com).
 
2. No menu hub, clique em **Procurar** e comece a digitar **Information** na caixa de filtro. Selecione **Azure Information Protection**.

- Você verá agora folha **Azure Information Protection** principal, mostrando a política padrão do Information Protection que é criada automaticamente. Essa política padrão contém os seguintes rótulos para classificação: **Pessoal**, **Público**, **Interno**, **Confidencial** e **Segredo**. Leia a dica de ferramenta para entender como os rótulos devem ser usados. Observe que **Segredo** tem dois sub-rótulos: **Todos os Funcionários** e **Meu Grupo**, que fornecem um exemplo de como uma categoria pode ter subcategorias.

- Com as configurações padrão, **Interno**, **Confidencial** e **Segredo** têm marcas visuais configuradas (como rodapé, cabeçalho, marca-d'água) e nenhum dos rótulos têm a proteção definida. Além disso, as três configurações globais estão definidas, de forma que todos os documentos e emails não precisem ter um rótulo, não haja um rótulo padrão e os usuários não tenham que fornecer justificativas ao reduzir o nível de confidencialidade.

    ![Etapa 3 do tutorial de início rápido do Azure Information Protection – política padrão](../media/info-protect-policy.png)

Para nosso tutorial, vamos alterar algumas dessas configurações globais para que você possa ver como elas funcionam:

-  **Select the default label** (Selecionar o rótulo padrão): defina essa opção como **Interno**.

- **Users must provide justification when lowering the sensitivity level** (Os usuários devem fornecer uma justificativa ao reduzir o nível de confidencialidade): defina essa opção como **Ativo**.

Agora, alteraremos as configurações de um dos rótulos, **Confidencial**:

1. Clique na entrada de rótulo **Confidencial**.

2. Na folha **Label: Confidential** (Rótulo: Confidencial), você verá agora as configurações que estão disponíveis para cada rótulo. Faça as seguintes alterações:

    a. Se você tiver ativado o Azure Rights Management: na seção **Definir modelo RMS para proteger documentos e emails que contenham este rótulo**, caso **Selecionar modelo RMS de** seja exibido, mantenha o padrão **RMS do Azure**. Em seguida, para **Selecionar modelo RMS**, clique na caixa suspensa e selecione o modelo padrão **\<nome da sua organização > – Confidencial**. Por exemplo, se o nome da organização for VanArsdel, Ltd, você verá e selecionará **VanArsdel, Ltd - Confidencial**. Se você tiver desabilitado esse modelo padrão do Azure Rights Management, selecione um modelo alternativo. No entanto, se você selecionar um modelo de departamento, certifique-se de que sua conta esteja incluída no escopo.
    
    Se você não tiver ativado o Azure Rights Management, não poderá usar essa opção.
    
    b. **Documents with this label have a watermark** (Documentos com este rótulo têm uma marca-d'água): clique em **Ativado** e, na caixa **Texto**, digite o nome da organização. Por exemplo, **VanArsdel, Ltd**. 
    
    c. Clique em **Adicionar uma nova condição** e, em seguida, na folha **Condição**, selecione o seguinte:
    
    - **Choose the type of condition** (Escolher o tipo de condição): **Interna**
    
    - **Selecionar interno**: **Número do Cartão de Crédito**
    
    - **Minimum number of occurrences** (Número mínimo de ocorrências): **1**
    
    - **Contar ocorrências apenas com valores exclusivos**: **Ativado**
    
    - Clique em **Salvar** para retornar para a folha **Label: Confidential** (Rótulo: Confidencial).

3. Na folha **Label: Confidential** (Rótulo: Confidencial), você verá que **Número do Cartão de Crédito** é mostrado como o **NOME DA CONDIÇÃO** com **1** **OCORRÊNCIA**.

4. Deixe **Select how this label is applied** (Selecionar como esse rótulo é aplicado): **Recomendado**

5. Na caixa **Enter notes for internal housekeeping** (Inserir observações para manutenção interna), digite **Somente para finalidade de teste**.

6. Clique em **Salvar** nesta folha **Label: Confidential** (Rótulo: Confidencial) e, na folha **Azure Information Protection** principal, clique em **Salvar** novamente.

7. Agora que fizemos e salvamos nossas alterações, queremos disponibilizá-las para os usuários, então clique em **Publicar** e em **Sim** para confirmar.

![Etapa 3 do tutorial de início rápido do Azure Information Protection – política padrão configurada](../media/info-protect-policy-configured.png)

Você pode fechar o Portal do Azure ou deixá-lo aberto para experimentar as opções de configuração adicionais depois de concluir este tutorial.

Agora que você analisou a política padrão e fez algumas alterações, a próxima etapa é instalar o cliente do Azure Information Protection.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Sobre as opções de configuração da política|[Configurando a política do Azure Information Protection](configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Etapa 1](infoprotect-tutorial-step1.md)
[Etapa 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Jul16_HO5-->


