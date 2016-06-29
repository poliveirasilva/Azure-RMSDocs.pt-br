---
# required metadata

title: Cenário – Partilhar um ficheiro do Office com os utilizadores noutra organização | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cenário – Partilhar um ficheiro do Office com os utilizadores noutra organização

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação do utilizador associada utilizam o Azure Rights Management para que os utilizadores possam enviar em segurança um ficheiro do Office por e-mail para pessoas noutra organização. Por exemplo, o ficheiro do Office poderá ser um documento do Word, uma folha de cálculo do Excel ou uma apresentação do PowerPoint com informações sobre a lista de preços de um parceiro, uma lista de produtos de um revendedor ou uma lista de prazos de entrega com potenciais clientes. Se os utilizadores seguirem as instruções, o ficheiro anexado à mensagem de e-mail será protegido pelo Azure Rights Management.

Este cenário aplica-se às seguintes circunstâncias:

-   O empregado tem de enviar informações para fora da organização, por e-mail, sob a forma de um anexo de documento do Office.

-   O documento contém informações que não são públicas, mas que não se destinam exclusivamente a utilização interna.

-   Os destinatários não precisam de partilhar estas informações com outras pessoas, imprimi-las ou utilizá-las como parte da sua própria documentação. Se não for este o caso, pode alterar as instruções de utilizador na seleção de permissões só de visualização para outra opção que permita ao destinatário alterar o anexo.

-   O empregado está possivelmente interessado em saber quando este documento é aberto pelo utilizador externo.

## Instruções de implementação
![Instruções do administrador para a Implementação Rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Certifique-se de que os seguintes requisitos estão em vigor antes de avançar para a documentação do utilizador.

## Requisitos para este cenário
Para que as instruções de utilizador para este cenário funcionem, é necessário que os seguintes aspetos estejam implementados:

|Requisito|Se precisar de mais informações|
|---------------|--------------------------------|
|Preparou contas e grupos para o Office 365 ou o Azure Active Directory|[Preparar para o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|O Azure Rights Management está ativado|[Ativar o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|A aplicação de partilha Rights Management está implementada nos computadores dos utilizadores que executam o Windows|[Implementação automática da aplicação de partilha Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|Os utilizadores têm o Outlook do Office 2013|Se os utilizadores tiverem o Office 2010, substitua a captura de ecrã por uma versão equivalente para que a imagem corresponda ao que os utilizadores veem.|
|A subscrição do Azure RMS inclui o controlo de documentos|Se a sua subscrição do Azure RMS não incluir o controlo de documentos e a revogação, os utilizadores não conseguirão concluir todos os passos nas instruções de utilizador. Neste caso, compre uma subscrição que suporte estas funcionalidades ou modifique as instruções de utilizador para remover os passos que as utilizam.<br /><br />Para verificar o suporte da subscrição: [Comparação das Ofertas do Rights Management Services (RMS)](https://technet.microsoft.com/dn858608)|

## Instruções da documentação do utilizador
Utilizando o modelo seguinte, copie e cole as instruções de utilizador numa comunicação destinada aos utilizadores finais e efetue estas alterações para refletir o seu ambiente:

1.  Substitua *&lt;nome do tipo de documento do Office&gt;* pelo tipo de documento que os seus utilizadores enviarão. Utilize expressões específicas e familiares para os seus fluxos de trabalho, tais como “lista de preços”, “prazos de entrega” e “proposta de licitação”, em vez de “Documento do Word” e “Folha de cálculo do Excel”. A utilização de expressões mais específicas ajuda a aumentar a probabilidade de os utilizadores seguirem as instruções ao trabalhar com esses documentos.

2.  Substitua *&lt;detalhes de contacto&gt;* por instruções sobre como os utilizadores podem contactar o suporte técnico, tais como uma ligação para um site, um endereço de e-mail ou um número de telefone.

3.  **Modificações adicionais que poderá pretender efetuar:**

    -   No passo 2, sugerimos **Visualizador – Ver Apenas** para as permissões, o que torna o documento anexado (mas não o original) só de leitura para os destinatários. Se esta restrição não for adequada para a sua necessidade comercial, altere esta opção para outro conjunto de permissões, tal como **Revisor – Ver e Editar**.

    -   No passo 3, sugerimos **Revogar instantaneamente o acesso a estes documentos** para que não haja um atraso se os utilizadores revogarem o documento mais tarde. Contudo, a definição desta opção obriga a que o destinatário tenha sempre uma ligação à Internet para abrir o anexo. Este passo também requer que tenha uma subscrição que suporte o controlo de documentos e a revogação. Elimine este passo se não for adequado para os seus utilizadores.

    -   No passo 4, sugerimos a opção **Enviar-me um e-mail quando alguém tentar abrir este documento**. Se os utilizadores controlarem os documentos através do portal de controlo de documentos, poderá decidir que a notificação por e-mail não é necessária e eliminar este passo.

    -   Os passos não incluem a definição de uma data de expiração. Caso as informações não devam ser utilizadas após uma data específica, adicione outro passo para definir um prazo de expiração adequado, como 90 dias após o envio da mensagem de e-mail.

    > [!NOTE] Para mais informações sobre cada uma das opções que os utilizadores podem selecionar, consulte [Opções da caixa de diálogo para a aplicação de partilha Rights Management](https://technet.microsoft.com/library/dn574738.aspx)

4.  Efetue quaisquer modificações adicionais que pretenda a este conjunto de instruções e, em seguida, envie-o aos utilizadores.

A documentação de exemplo mostra que aspeto estas instruções poderão ter para os utilizadores depois das personalizações.

![Modelo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_UsersBanner.png)

### Como partilhar um &lt;nome do tipo de documento do Office&gt;

1.  Crie a sua mensagem de e-mail ao especificar o endereço ou os endereços de e-mail, escreva a mensagem e anexe o *&lt;nome do tipo de documento do Office&gt;* à mesma. Em seguida, no separador **MENSAGEM**, no grupo **RMS**, clique em **Partilhar Protegido** e, em seguida, clique em **Partilhar Protegido** novamente:

    ![Captura de ecrã de como partilhar um documento do Office através do Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Na caixa de diálogo **partilhar protegido**, selecione **Visualizador – Ver Apenas**:

    ![caixa de diálogo partilhar protegido – Visualizador – Ver Apenas](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Selecione **Revogar instantaneamente o acesso a estes documentos**:

    ![caixa de diálogo partilhar protegido – revogar instantaneamente](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Selecione **Enviar-me um e-mail quando alguém tentar abrir estes documentos**:

    ![caixa de diálogo partilhar protegido – enviar-me um e-mail](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Clique em **Enviar Agora**.

Quando as pessoas na linha **Para**, **CC** ou **Bcc** recebem este e-mail, veem uma mensagem com instruções sobre como ler o *&lt;nome do tipo de documento do Office&gt;* anexado. Podem ler o documento em vários dispositivos, incluindo iPads, iPhones, tablets e telemóveis Android, computadores Mac e computadores com o Windows.

Utilize o [portal de controlo de documentos](https://track.azurerms.com/) para controlar se e quando abrem o &lt;nome do tipo de documento do Office&gt; anexado. Considere contactá-las através de uma chamada telefónica de acompanhamento logo depois de confirmar que abriram o &lt;nome do tipo de documento do Office&gt;.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Proteger um ficheiro que partilha por e-mail](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [Controlar e revogar os documentos](https://technet.microsoft.com/library/dn986611.aspx)

-   Contactar o suporte técnico:

    -   *&lt;detalhes de contacto&gt;*

### Exemplo de documentação do utilizador personalizada
![Exemplo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Como partilhar uma lista de preços com o seu cliente

1.  Crie a sua mensagem de e-mail ao especificar o endereço ou os endereços de e-mail do cliente, escreva a mensagem e anexe a lista de preços mais recente à mesma. Em seguida, no separador **MENSAGEM**, no grupo **RMS**, clique em **Partilhar Protegido** e, em seguida, clique em **Partilhar Protegido** novamente:

    ![Captura de ecrã de como partilhar um documento do Office através do Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Na caixa de diálogo **partilhar protegido**, selecione **Visualizador – Ver Apenas**:

    ![caixa de diálogo partilhar protegido – Visualizador – Ver Apenas](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Selecione **Revogar instantaneamente o acesso a estes documentos**:

    ![caixa de diálogo partilhar protegido – revogar instantaneamente](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Selecione **Enviar-me um e-mail quando alguém tentar abrir estes documentos**:

    ![caixa de diálogo partilhar protegido – enviar-me um e-mail](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Clique em **Enviar Agora**.

Quando as pessoas na linha **Para**, **CC** ou **Bcc** recebem este e-mail, veem uma mensagem com instruções sobre como ler a lista de preços anexada. Podem ler o documento em vários dispositivos, incluindo iPads, iPhones, tablets e telemóveis Android, computadores Mac e computadores com o Windows.

Utilize o [portal de controlo de documentos](https://track.azurerms.com/) para controlar se e quando abrem a lista de preços anexada. Considere contactá-las através de uma chamada telefónica de acompanhamento logo depois de confirmar que abriram a lista de preços.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Proteger um ficheiro que partilha por e-mail](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [Controlar e revogar os documentos](https://technet.microsoft.com/library/dn986611.aspx)

-   Contactar o suporte técnico:

    -   E-mail: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO2-->


