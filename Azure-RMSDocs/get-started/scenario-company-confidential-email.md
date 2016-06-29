---
# required metadata

title: Cenário – enviar um e-mail confidencial da empresa | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 950799e9-2289-48c7-b95a-f54a8ead520a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cenário – enviar um e-mail confidencial da empresa

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação de apoio do utilizador utilizam o Azure Rights Management para que qualquer utilizador na organização possa enviar em segurança comunicações por e-mail que não podem ser lidas fora da organização. Por exemplo, se alguém reencaminhar a mensagem de e-mail para alguém noutra organização ou para uma conta de e-mail pessoal. As mensagens de e-mail e quaisquer anexos serão protegidos pelo Azure Rights Management e por um modelo que os utilizadores selecionam no cliente de e-mail.

A forma mais simples para ativar este cenário é utilizar um dos modelos predefinidos incorporados que automaticamente restringem o acesso a todos os utilizadores na sua organização. Porém, se necessário, pode tornar isto mais restritivo ao criar um modelo personalizado que, por exemplo, restringe o acesso a um subconjunto de utilizadores ou que tenha outras restrições, tais como só de leitura ou uma data de validade, ou desativa o botão Reencaminhar no cliente de e-mail.

> [!IMPORTANT]
> Neste cenário, embora possa remover o direito **Reencaminhar** de um modelo personalizado que configurou (este procedimento desativará o botão Reencaminhar no cliente de e-mail), esta configuração não impede que os utilizadores partilhem o e-mail com outro utilizador autorizado. O destinatário pode guardar o e-mail (e quaisquer anexos) e, em seguida, partilhar as informações através de outros mecanismos de partilha.
> 
> Por exemplo, João envia um e-mail a Adriana através de um modelo personalizado que aplica os direitos personalizados Guardar Ficheiro e Editar Conteúdo ao grupo de Marketing e não inclui o direito Reencaminhar. Embora Adriana não possa reencaminhar o e-mail a outras pessoas, pode guardar a mensagem de e-mail e quaisquer anexos numa pen USB ou numa partilha de servidor de ficheiros, que, posteriormente, qualquer membro do grupo de Marketing pode ler e editar se conseguir aceder a estes ficheiros. Os utilizadores que não estão no grupo de Marketing não poderão abrir o conteúdo.

As instruções aplicam-se às seguintes circunstâncias:

-   Qualquer utilizador da organização pretende partilhar informações com outras pessoas dentro da organização, mas essas informações não devem ser partilhadas fora da organização.

-   As informações a serem partilhadas podem estar dentro da mensagem de e-mail ou do anexo.

-   Os utilizadores têm de selecionar manualmente o modelo no cliente de e-mail.

## Instruções de implementação
![Instruções do administrador para a Implementação Rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Certifique-se de que os seguintes requisitos estão em vigor antes de avançar para a documentação do utilizador.

## Requisitos para este cenário
Para que as instruções para este cenário funcionem, é necessário o seguinte:

|Requisito|Se precisar de mais informações|
|---------------|--------------------------------|
|Preparou contas e grupos para o Office 365 ou o Azure Active Directory|[Preparar para o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|A chave de inquilino do Azure Rights Management é gerida pela Microsoft; não está a utilizar o BYOK|[Planear e implementar a chave de inquilino do Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|O Azure Rights Management está ativado|[Ativar o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Um dos seguintes:<br /><br />- O Exchange Online está ativado para o Azure Rights Management<br /><br />- O conetor RMS está instalado e configurado para o Exchange no local|Para o Exchange Online: consulte a secção **Exchange Online: configuração de IRM** em [Configurar aplicações do Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx).<br /><br />Para o Exchange no local: [Implementar o conetor Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Não arquivou o modelo do Azure Rights Management predefinido **&lt;organização&gt; – Confidencial**. Ou configurou um modelo personalizado para este fim porque precisa de definições mais restritivas ou apenas um subconjunto de utilizadores da organização deve ter capacidade para ler os e-mails protegidos.|[Configurar modelos personalizados para o Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)<br /><br />Sugestão: se forem necessárias definições de política de utilização mais restritivas, mas para todos os utilizadores na organização, copie e edite um dos modelos predefinidos, em vez de criar um modelo do zero.<br /><br />Os modelos atualizados não são imediatamente atualizados para os clientes de e-mail neste cenário. Consulte a secção [Atualizar modelos para utilizadores](https://technet.microsoft.com/library/dn642472.aspx) no artigo de configuração de modelos para obter informações.|
|Os utilizadores que enviem o e-mail protegido têm o Outlook 2013, o Outlook 2016 ou o Outlook Web Access.<br /><br />Os utilizadores que recebem o e-mail têm um cliente de e-mail que suporta o Azure Rights Management.|Pode utilizar o Outlook 2010, mas tem de [instalar a aplicação de partilha Rights Management para Windows](https://technet.microsoft.com/library/dn339003.aspx) e ajustar as instruções de utilizador em conformidade.<br /><br />Para obter uma lista de clientes de e-mail que suportam o Azure Rights Management, consulte a coluna **E-mail** na tabela [Capacidade dos dispositivos cliente](https://technet.microsoft.com/library/dn655136.aspx) de [Requisitos do Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx)|

## Instruções da documentação do utilizador
Utilizando o modelo seguinte, copie e cole as instruções de utilizador numa comunicação destinada aos utilizadores finais e efetue estas alterações para refletir o seu ambiente:

1.  Substitua todas as instâncias de *&lt;nome da organização&gt;* pelo nome da sua organização.

2.  Substitua todas as instâncias de *&lt;nome da organização – Confidencial&gt;* pelo nome do modelo personalizado ou predefinido.

3.  Substitua as capturas de ecrã para mostrarem os nomes dos modelos da organização.

4.  Substitua os *&lt;detalhes de contacto&gt;* por instruções sobre como os utilizadores podem contactar o suporte técnico, tais como uma ligação para um Web site, um endereço de e-mail ou um número de telefone.

5.  **Modificações adicionais que poderá pretender efetuar:**

    -   Se for prático limitar as instruções apenas a um cliente de e-mail, considere fazê-lo para simplificar e elimine o outro conjunto de instruções.

    -   Se utilizar um modelo personalizado em vez do modelo predefinido sugerido, reveja as palavras utilizadas em conformidade:

        -   Torne o título mais específico.

        -   Especifique os utilizadores ou grupos a selecionar no passo 1.

        -   Especifique o nome do modelo personalizado no passo 2.

        -   Modifique o parágrafo final para explicar as restrições que os destinatários terão.

6.  Efetue as modificações adicionais que pretender a este conjunto de instruções e, em seguida, envie-o para os utilizadores.

7.  Uma vez que alguns clientes não suportam o Rights Management, poderá ter de fornecer orientações e recomendações aos destinatários destas mensagens de e-mail protegidas. Estas informações serão baseadas nos dispositivos e aplicações de e-mail que estarão em utilização na sua organização e nas preferências que tiver. Por exemplo, recomendamos que os utilizadores do iOS leiam os e-mails protegidos com o Outlook para iPad e iPhone, em vez do cliente de correio iOS nativo.

    Para obter mais informações sobre os clientes de e-mail, consulte a coluna **E-mail**, na tabela [Capacidade dos dispositivos cliente](https://technet.microsoft.com/library/dn655136.aspx) de [Requisitos do Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx).

A documentação de exemplo mostra o aspeto que estas instruções poderão ter para os utilizadores depois das personalizações.

![Modelo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_UsersBanner.png)

### Como enviar e-mails que contêm informações confidenciais da empresa através do Outlook

1.  No Outlook, crie uma nova mensagem de correio, adicione os anexos que pretende incluir e, em seguida, selecione os utilizadores ou os grupos da *&lt;nome da organização&gt;*.

2.  No separador **OPÇÕES**, clique em **Permissão** e, em seguida, selecione **&lt;nome da organização – Confidencial&gt;**:

    ![Captura de ecrã de como enviar e-mails que contêm informações confidenciais da empresa através do Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envie a mensagem.

### Como enviar e-mails que contêm informações confidenciais da empresa através do Outlook Web App

1.  No Outlook Web App, crie uma nova mensagem de correio, adicione os anexos que pretende incluir e, em seguida, selecione os utilizadores ou os grupos da *&lt;nome da organização&gt;* no livro de endereços.

2.  Clique em **…**, clique em **Definir permissões** e, em seguida, selecione **&lt;nome da organização – Confidencial&gt;**:

    ![Captura de ecrã de como enviar e-mails que contêm informações confidenciais da empresa através do Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envie a mensagem.

Quando os indivíduos na linha **Para**, **Cc** ou **Bcc** recebem este e-mail, poderá ser pedida a sua autenticação antes de poderem ler a mensagem para confirmar se são utilizadores da *&lt;nome da organização&gt;*. Noutros casos, a autenticação não é solicitada porque estes já estão autenticados.

As pessoas a quem enviar o e-mail poderão reencaminhá-lo para outras pessoas, mas apenas os utilizadores da *&lt;nome da organização&gt;* poderão lê-lo. Se anexar um documento do Office, terá a mesma proteção, mesmo que esse anexo seja guardado com um nome diferente e noutra localização. No entanto, os utilizadores autenticados com êxito podem copiar e colar a partir do e-mail ou anexo ou imprimir a partir do mesmo. Se precisar de uma proteção mais restritiva que impeça ações como estas, contacte o suporte técnico.

**Precisa de ajuda?**

-   Contactar o suporte técnico:

    -   *&lt;detalhes de contacto&gt;*

### Exemplo de documentação do utilizador personalizada
![Exemplo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Como enviar e-mails que contêm informações confidenciais da empresa através do Outlook

1.  No Outlook, crie uma nova mensagem de correio, adicione os anexos que pretende incluir e, em seguida, selecione os utilizadores ou os grupos da VanArsdel no livro de endereços.

2.  No separador **OPÇÕES**, clique em **Permissão** e, em seguida, selecione **VanArsdel, Lda. – Confidencial**:

    ![Captura de ecrã de como enviar e-mails que contêm informações confidenciais da empresa através do Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envie a mensagem.

#### Como enviar e-mails que contêm informações confidenciais da empresa através do Outlook Web App

1.  No Outlook Web App, crie uma nova mensagem de correio, adicione os anexos que pretende incluir e, em seguida, selecione os utilizadores ou os grupos da VanArsdel no livro de endereços.

2.  Clique em **…**, clique em **Definir permissões** e, em seguida, selecione **VanArsdel, Lda. – Confidencial**:

    ![Captura de ecrã de como enviar e-mails que contêm informações confidenciais da empresa através do Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envie a mensagem.

Quando os indivíduos na linha **Para**, **Cc** ou **Bcc** recebem este e-mail, poderá ser pedida a sua autenticação antes de poderem ler a mensagem para confirmar se são utilizadores da VanArsdel, Ltd. Noutros casos, a autenticação não é solicitada porque estes já estão autenticados.

As pessoas a quem enviar o e-mail poderão reencaminhá-lo para outras pessoas, mas apenas os utilizadores da VanArsdel poderão lê-lo. Se anexar um documento do Office, terá a mesma proteção, mesmo que esse anexo seja guardado com um nome diferente e noutra localização. No entanto, os utilizadores autenticados com êxito podem copiar e colar a partir do e-mail ou anexo ou imprimir a partir do mesmo. Se precisar de uma proteção mais restritiva que impeça ações como estas, contacte o suporte técnico.

**Precisa de ajuda?**

-   Contactar o suporte técnico:

    -   E-mail: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO3-->


