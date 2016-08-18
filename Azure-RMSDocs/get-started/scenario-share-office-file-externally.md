---
title: "Cenário - compartilhar um arquivo do Office com usuários em outra organização | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c10a4d7b-f57a-4a43-b66e-477777be59cc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 6a6f9d8c0a98752413a99d30926f2b5bc8af193d


---

# Cenário - compartilhar um arquivo do Office com usuários em outra organização

*Aplica-se a: Azure Rights Management, Office 365*

Esse cenário e a documentação do usuário de suporte correspondente usam o Azure Rights Management para que os usuários possam enviar um arquivo do Office por email com segurança a pessoas em outra organização. Por exemplo, o arquivo do Office pode ser um documento do Word, planilha do Excel ou apresentação do PowerPoint contendo informações da lista de preços para um parceiro, uma lista de produtos para um revendedor ou uma lista de linhas de tempo de entrega com clientes em potencial. Quando os usuários seguirem as instruções, o arquivo anexado à mensagem de email estará protegido pelo Azure Rights Management.

Este cenário é adequado para o seguinte conjunto de circunstâncias:

-   O funcionário tem que enviar informações de fora da organização via email, na forma de um anexo de documento do Office.

-   O documento contém informações que não são públicas, mas não são exclusivamente para uso interno.

-   Os usuários do destinatário não tem um requisito para compartilhar essas informações com outras pessoas, imprimi-la ou usá-la como parte de sua própria documentação. Se esse não for o caso, você pode alterar as instruções do usuário de selecionar permissões de somente exibição para outra opção que permita que o destinatário altere o anexo.

-   O funcionário está potencialmente interessado em saber quando este documento for aberto pelo usuário externo.

## Instruções de implantação
![Instruções do administrador para implantação rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Verifique se os requisitos a seguir estão satisfeitos antes de prosseguir para a documentação do usuário.

## Requisitos para este cenário
Para ver as instruções de usuário para este cenário funcionarem, os seguintes requisitos devem estar em vigor:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|Você preparou contas e grupos do Office 365 ou o Azure Active Directory|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|O aplicativo Rights Management sharing é implantado nos computadores dos usuários que executam o Windows|[Implantação automática para o aplicativo de compartilhamento Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|Os usuários têm o Outlook do Office 2013|Se os usuários têm o Office 2010, substitua a captura de tela por uma versão equivalente para que a imagem corresponda a que os usuários veem.|
|Sua assinatura do Azure RMS inclui rastreamento de documento|Se sua assinatura do Azure RMS não inclui controle de documento e revogação, os usuários não poderão concluir todas as etapas nas instruções do usuário. Nesse caso, adquira também uma assinatura que ofereça suporte a esses recursos ou modifique as instruções do usuário para remover as etapas que usam esses recursos.<br /><br />Para verificar o suporte de assinatura: [Comparação de Ofertas do Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).|

## Instruções sobre a documentação do usuário
Usando o modelo a seguir, copie e cole as instruções do usuário em uma comunicação para seus usuários finais e faça com que essas modificações reflitam o seu ambiente:

1.  Substitua o *&lt;nome do tipo de documento do Office&gt;* pelo tipo de documento que seus usuários estarão enviando. Use palavras específicas e conhecidas para seus fluxos de trabalho, como “lista de preços”, “tempo de entrega”, e “proposta de oferta” em vez de “Documento do Word” e “Planilha do Excel”. Essas palavras mais específicas ajudam a aumentar a probabilidade de que eles seguirão as instruções ao trabalhar com esses documentos.

2.  Substitua *&lt;detalhes de contato&gt;* por instruções de como os usuários podem entrar em contato com o suporte técnico, como um link de site, endereço de email ou número de telefone.

3.  **Modificações adicionais que talvez você queira fazer:**

    -   Na etapa 2, sugerimos **Visualizador - Somente Exibir** para as permissões, que torna o documento anexado (mas não o original) somente leitura para os destinatários. Se essa restrição não for adequada para suas necessidades de negócios, altere essa opção para outro conjunto de permissões, como **Revisor - Exibir e Editar**.

    -   Na etapa 3, sugerimos **Permitir que eu revogue o acesso a esses documentos imediatamente** para que não exista nenhum atraso se os seus usuários revogarem o documento mais tarde, mas a definição desta opção requer que o destinatário sempre tenha uma conexão com a Internet para abrir o anexo. Esta etapa também requer que você tenha uma assinatura que ofereça suporte ao controle de documentos e revogação. Exclua esta etapa se ela não for adequada para seus usuários.

    -   Na etapa 4, sugerimos a opção **Envie-me um email quando alguém tentar abrir este documento**. Se os usuários controlarem seus documentos usando o portal de controle de documento, você pode decidir que a notificação por email não é necessária e excluir esta etapa.

    -   As etapas não incluem a definição de uma data de expiração. Caso as informações não devam ser usadas após uma data específica, adicione outra etapa para definir um tempo de expiração apropriado, como 90 dias a partir do envio da mensagem de email.

    > [!NOTE]
    > Para obter mais informações sobre cada uma das opções que os usuários podem selecionar, consulte [Opções da caixa de diálogo para o aplicativo Rights Management sharing](https://technet.microsoft.com/library/dn574738.aspx)

4.  Faça outras modificações que deseje para este conjunto de instruções e, em seguida, envie-o para esses usuários.

A documentação de exemplo mostra como essas instruções pode parecer para os usuários, após as personalizações.

![Documentação de usuário do modelo para implantação rápida de RMS do Azure](../media/AzRMS_UsersBanner.png)

### Como compartilhar um &lt;nome de tipo de documento do Office&gt;

1.  Crie a mensagem de email, especificando os endereços de email, digite sua mensagem e anexe o *&lt;nome do tipo de documento do Office&gt;* à mensagem de email. Depois, na guia **Message** no grupo do **RMS** , clique em **Compartilhamento Protegido** e clique em **Compartilhamento Protegido** novamente:

    ![Captura de tela de como compartilhar documentos do Office usando o Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Na caixa de diálogo **compartilhamento protegido** , selecione **Viewer – View Only**:

    ![compartilhar caixa de diálogo protegida - Visualizador - Somente exibição](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Selecione **Permitir que eu revogue o acesso a esses documentos imediatamente**.

    ![compartilhar caixa de diálogo protegida - revogar instantaneamente](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Selecione **Enviar-me um email quando alguém tentar abrir esses documentos**:

    ![compartilhar caixa de diálogo protegida - enviar email para mim](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Clique em **Enviar agora**.

Quando alguém nas linas **Para**, **Cc**, ou **Cco** linha recebe o email, vê uma mensagem que fornece instruções de como ler o arquivo anexado *&lt;nome do tipo de documento do Office&gt;*. Eles podem ler o documento em vários dispositivos, incluindo iPads, iPhones, tablets Android e telefones, computadores Mac e computadores com Windows.

Use o [portal de acompanhamento de documento](https://track.azurerms.com/) para acompanhar se e quando o &lt;nome do tipo de documento do Office&gt; é aberto. Considere entrar em contato com eles com uma chamada por telefone de acompanhamento logo depois que eles abrirem o &lt;nome do tipo de documento do Office&gt;.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Proteger um arquivo que você compartilha por email](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [Rastrear e revogar seus documentos](https://technet.microsoft.com/library/dn986611.aspx)

-   Entre em contato com o suporte técnico:

    -   *&lt;detalhes de contato&gt;*

### Documentação do usuário personalizada de exemplo
![Documentação de usuário de exemplo para implantação rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Como compartilhar uma lista de preços com o cliente

1.  Crie a mensagem de email, especificando o endereço ou endereços de email do cliente, digite sua mensagem e anexe lista depreços mais recente à mensagem de email. Depois, na guia **Message** no grupo do **RMS** , clique em **Compartilhamento Protegido** e clique em **Compartilhamento Protegido** novamente:

    ![Captura de tela de como compartilhar documentos do Office usando o Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Na caixa de diálogo **compartilhamento protegido** , selecione **Viewer – View Only**:

    ![compartilhar caixa de diálogo protegida - Visualizador - Somente exibição](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Selecione **Permitir que eu revogue o acesso a esses documentos imediatamente**.

    ![compartilhar caixa de diálogo protegida - revogar instantaneamente](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Selecione **Enviar-me um email quando alguém tentar abrir esses documentos**:

    ![compartilhar caixa de diálogo protegida - enviar email para mim](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Clique em **Enviar agora**.

Quando alguém nos campos **Para**, **Cc**ou **Cco** receber este email, eles veem uma mensagem que fornece as instruções sobre como ler o a lista de preços anexa. Eles podem ler o documento em vários dispositivos, incluindo iPads, iPhones, tablets Android e telefones, computadores Mac e computadores com Windows.

Use o [portal de controle de documento](https://track.azurerms.com/) para controlar se e quando abrirem lista de preços anexa. Considere entrar em contato com eles com uma chamada por telefone de acompanhamento logo depois que você vir que eles abriram a lista de preços.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Proteger um arquivo que você compartilha por email](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [Rastrear e revogar seus documentos](https://technet.microsoft.com/library/dn986611.aspx)

-   Entre em contato com o suporte técnico:

    -   Email: helpdesk@vanarsdelltd.com




<!--HONumber=Jul16_HO3-->


