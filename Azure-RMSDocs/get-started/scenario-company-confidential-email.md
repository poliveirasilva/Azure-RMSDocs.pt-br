---
title: "Cenário - Enviar um email confidencial da empresa | Azure RMS"
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
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: b6f3b06485dda81be2a36035fea7477f4061a8e9


---

# Cenário - Enviar um email confidencial da empresa

*Aplica-se a: Azure Rights Management, Office 365*

Esse cenário e a documentação de suporte ao usuário usam o Azure Rights Management para que qualquer usuário na organização possa enviar com segurança comunicações por email que não possam ser lidas fora da organização. Por exemplo, se alguém encaminha a mensagem de email para outra pessoa em outra organização ou para uma conta de email pessoal. Os emails e anexos serão protegidos pelo Azure Rights Management e por um modelo que os usuários selecionam no cliente de email.

A maneira mais simples de habilitar esse cenário é usar um dos modelos internos padrão que restringem automaticamente o acesso a todos os usuários em sua organização. Mas, se for necessário, você pode tornar isso ainda mais restritivo por meio da criação de um modelo personalizado que, por exemplo, restringe o acesso a um subconjunto de usuários, ou que tenha outras restrições, como somente leitura ou uma data de expiração, ou ainda desabilite o botão Avançar no cliente de email.

> [!IMPORTANT]
> Nesse cenário, embora seja possível remover o direito **Forward** (Encaminhar) de um modelo personalizado configurado por você, e isso desabilitará o botão Avançar no cliente de email, essa configuração não impede que os usuários compartilhem o email com outro usuário autorizado. O destinatário pode salvar o email (e todos os anexos) e compartilhar as informações por meio de outros mecanismos de compartilhamento.
> 
> Por exemplo, Vinícius envia um email para Alice usando um modelo personalizado que aplica os direitos personalizados Salvar Arquivo e Editar Conteúdo para o grupo Marketing, e não inclui o direito Forward. Apesar de Alice não poder encaminhar o email para outras pessoas, ela pode salvar a mensagem de email e os anexos em uma unidade USB ou compartilhamento de servidor de arquivo, que qualquer membro do grupo Marketing pode ler e editar se puderem acessar esses arquivos. Os usuários que não estão no grupo Marketing não poderão abrir o conteúdo.

As instruções são adequadas para o seguinte conjunto de circunstâncias:

-   Qualquer usuário na organização deseja compartilhar informações com outras pessoas da organização, mas essas informações não devem ser compartilhadas fora da organização.

-   As informações a serem compartilhadas podem estar dentro da mensagem de email ou do anexo.

-   Os usuários devem selecionar manualmente o modelo de dentro de seu cliente de email.

## Instruções de implantação
![Instruções do administrador para implantação rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Verifique se os requisitos a seguir estão satisfeitos antes de prosseguir para a documentação do usuário.

## Requisitos para este cenário
Para que as instruções desse cenário funcionem, deve ser feito o seguinte:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|Você preparou contas e grupos do Office 365 ou o Azure Active Directory|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Sua chave de locatário do Azure Rights Management é gerenciada pela Microsoft. Você não está usando BYOK|[Planejando e implementando sua chave de locatário do Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Um das seguintes condições:<br /><br />- O Exchange Online está habilitado para o Azure Rights Management<br /><br />- O conector RMS está instalado e configurado para o Exchange local|Para o Exchange Online: confira a seção **Exchange Online: configuração do IRM** de [Configuração de aplicativos para o Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx).<br /><br />Para o Exchange local: [Implantação do conector do Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx).|
|Você não arquivou o modelo padrão do Azure Rights Management **&lt;organização&gt; - Confidencial**. Ou, você configurou um modelo personalizado para essa finalidade, pois precisa de configurações mais restritivas, ou apenas um subconjunto de usuários na organização deve ser capaz de ler os emails protegidos.|[Configurando modelos personalizados do Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)<br /><br />Dica: se você precisar de configurações de política de uso mais restritivas, mas para todos os usuários na organização, copie e edite os modelos padrão, em vez de criar um modelo a partir do zero.<br /><br />Os modelos atualizados não são atualizados imediatamente para os clientes de email nesse cenário. Confira a seção [Atualização de modelos para usuários](https://technet.microsoft.com/library/dn642472.aspx) no artigo de configuração de modelos para saber mais.|
|Os usuários que enviam email protegido têm o Outlook 2013 ou 2016 ou o Outlook Web Access.<br /><br />Os usuários que receberem o e-mail têm um cliente de email que oferece suporte ao Azure Rights Management.|Você pode usar o Outlook 2010, mas deve [instalar o aplicativo de compartilhamento do Rights Management para Windows](https://technet.microsoft.com/library/dn339003.aspx) e ajustar as instruções do usuário adequadamente.<br /><br />Para obter uma lista de clientes de email que oferecem suporte ao Azure Rights Management, veja a coluna **Email** na tabela [Recurso de dispositivos do cliente](https://technet.microsoft.com/library/dn655136.aspx), de [Requisitos do Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx)|

## Instruções sobre a documentação do usuário
Usando o modelo a seguir, copie e cole as instruções do usuário em uma comunicação para seus usuários finais e faça com que essas modificações reflitam o seu ambiente:

1.  Substitua todas as instâncias de *&lt;nome da organização&gt;* pelo nome de sua organização.

2.  Substitua todas as instâncias de *&lt;nome da organização - Confidencial&gt;* pelo nome do modelo personalizado ou padrão.

3.  Substitua as capturas de tela para que elas mostrem os nomes de modelo de sua organização.

4.  Substitua *&lt;detalhes de contato&gt;* por instruções de como os usuários podem entrar em contato com o suporte técnico, como um link de site, endereço de email ou número de telefone.

5.  **Modificações adicionais que talvez você queira fazer:**

    -   Se for prático limitar as instruções para um cliente de email apenas, considere fazer isso para manter a simplicidade e exclua o outro conjunto de instruções.

    -   Se você usar um modelo personalizado em vez do modelo padrão sugerido, revise as palavras adequadamente:

        -   Torne o título mais específico.

        -   Especifique os usuários ou grupos para seleção na etapa 1.

        -   Especifique o nome do modelo personalizado na etapa 2.

        -   Modifique o parágrafo final para explicar as restrições que os destinatários terão.

6.  Faça outras modificações que deseje para este conjunto de instruções e, em seguida, envie-o para esses usuários.

7.  Como alguns clientes não oferecem suporte ao Rights Management, talvez seja necessário fornecer orientações e recomendações para os destinatários dessas mensagens de email protegido. Essas informações terão base nos dispositivos e aplicativos de email usados em sua organização e em quaisquer preferências que você tenha. Por exemplo, recomendamos que os usuários do iOS leiam os emails protegidos com o Outlook para iPad e iPhone, em vez do cliente de email para iOS nativo .

    Para saber mais sobre os clientes de email, veja a coluna **Email** na tabela [Recurso de dispositivos do cliente](https://technet.microsoft.com/library/dn655136.aspx), de [Requisitos do Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx)

A documentação de exemplo mostra como essas instruções pode parecer para os usuários, após as personalizações.

![Documentação de usuário do modelo para implantação rápida de RMS do Azure](../media/AzRMS_UsersBanner.png)

### Como enviar emails que contêm informações confidenciais da empresa usando o Outlook

1.  No Outlook, crie uma nova mensagem de email, adicione os anexos que quiser incluir e selecione os usuários ou grupos de *&lt;nome da organização&gt;*.

2.  Na guia **OPÇÕES**, clique em **Permissão** e selecione **&lt;nome da organização - Confidencial&gt;**:

    ![Captura de tela de como enviar emails que contêm informações confidenciais da empresa usando o Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envie a mensagem.

### Como enviar emails que contêm informações confidenciais da empresa usando o Outlook Web App

1.  No Outlook Web App, crie uma nova mensagem de email, adicione todos os anexos que você quiser incluir e, em seguida, selecione usuários ou grupos de *&lt;nome da organização&gt;* do catálogo de endereços.

2.  Clique em **...**, clique em **Definir permissões**, e, em seguida, selecione **&lt;nome da organização - Confidencial&gt;**:

    ![Captura de tela de como enviar emails que contêm informações confidenciais da empresa usando o Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envie a mensagem.

Quando alguém na linha **Para**, **Cc**, ou **Cco** recebe o email, pode ser solicitado a autenticar antes de lerem a mensagem, para verificar se são um usuário de *&lt;nome da organização&gt;*. Outras vezes, os usuários não recebem essa solicitação, pois já estão autenticados.

As pessoas para as quais você envia o email poderão encaminhá-lo para outras pessoas, mas apenas os usuários de *&lt;nome da organização&gt;* conseguirão lê-lo. Se você anexar um documento do Office, ele terá a mesma proteção, mesmo se esse anexo for salvo com um nome diferente, em outro local. No entanto, os usuários autenticados com êxito poderão copiar e colar do email ou anexo, ou imprimir a partir dele. Se precisar de uma proteção mais restritiva que impeça ações como essas, entre em contato com o suporte técnico.

**Precisa de ajuda?**

-   Entre em contato com o suporte técnico:

    -   *&lt;detalhes de contato&gt;*

### Documentação do usuário personalizada de exemplo
![Documentação de usuário de exemplo para implantação rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Como enviar emails que contêm informações confidenciais da empresa usando o Outlook

1.  No Outlook, crie uma nova mensagem de email, adicione os anexos que quiser incluir e selecione os usuários ou grupos da VanArsdel do catálogo de endereços

2.  Na guia **OPÇÕES** clique em **Permissões** e selecione **VanArsdel, Ltd - Confidencial**:

    ![Captura de tela de como enviar emails que contêm informações confidenciais da empresa usando o Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envie a mensagem.

#### Como enviar emails que contêm informações confidenciais da empresa usando o Outlook Web App

1.  No Outlook Web App, crie uma nova mensagem de email, adicione os anexos que quiser incluir e selecione os usuários ou grupos da VanArsdel do catálogo de endereços

2.  Clique em **…**, clique em **Definir permissões** e selecione **VanArsdel, Ltd - Confidential**:

    ![Captura de tela de como enviar emails que contêm informações confidenciais da empresa usando o Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envie a mensagem.

Quando alguém na linha **Para**, **Cc** ou **Cco** receber o email, poderá receber uma solicitação de autenticação antes de poder ler a mensagem, a fim de verificar se são usuários da VanArsdel, Ltd. Outras vezes, os usuários não recebem essa solicitação, pois já estão autenticados.

As pessoas para as quais você envia seu email poderão encaminhá-lo a outras pessoas, mas apenas os usuários de VanArsdel conseguirão lê-lo. Se você anexar um documento do Office, ele terá a mesma proteção, mesmo se esse anexo for salvo com um nome diferente, em outro local. No entanto, os usuários autenticados com êxito poderão copiar e colar do email ou anexo, ou imprimir a partir dele. Se precisar de uma proteção mais restritiva que impeça ações como essas, entre em contato com o suporte técnico.

**Precisa de ajuda?**

-   Entre em contato com o suporte técnico:

    -   Email: helpdesk@vanarsdelltd.com




<!--HONumber=Jun16_HO4-->


