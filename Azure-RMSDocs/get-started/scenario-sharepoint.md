---
# required metadata

title: Cenário – Manter o controlo de documentos armazenados no SharePoint | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cenário – Manter o controlo de documentos armazenados no SharePoint

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação do utilizador associada utilizam o Azure Rights Management para garantir que os documentos do Office armazenados no SharePoint permanecem sob o seu controlo através da utilização de bibliotecas protegidas. Por exemplo, os documentos são automaticamente protegidos contra fugas acidentais ou intencionais por parte dos utilizadores e pode bloquear o acesso ao conteúdo mesmo depois de este ser transferido ou sincronizado. Os ficheiros que pretende proteger podem destinar-se à colaboração interna em documentos ou planos de conceção ou podem ser outros tipos de material a entregar. Quando configura bibliotecas protegidas para o SharePoint, os ficheiros do Office armazenados nas mesmas são protegidos pelo Azure Rights Management.

As instruções aplicam-se às seguintes circunstâncias:

-   Os empregados partilham e colaboram em documentos do Office armazenados numa biblioteca do SharePoint.

-   Os empregados não precisam de definir ou alterar as permissões que um administrador define ao nível da biblioteca.

-   Os empregados não precisam de partilhar estes documentos com pessoas fora da sua organização.

## Instruções de implementação
![Instruções do administrador para a Implementação Rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Certifique-se de que os seguintes requisitos e procedimentos de suporte estão em vigor antes de avançar para a documentação do utilizador.

## Requisitos para este cenário
Para que este cenário funcione, é necessário que os seguintes aspetos estejam implementados:

|Requisito|Se precisar de mais informações|
|---------------|--------------------------------|
|Preparou contas e grupos para o Office 365 ou o Azure Active Directory|[Preparar para o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|O Azure Rights Management está ativado|[Ativar o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Se pretender utilizar o SharePoint Server: implemente o conector RMS e configure-o para o SharePoint|[Implementar o conector Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Configurar permissões para o site do SharePoint a proteger|[Gerir permissões para uma lista, biblioteca, pasta, documento ou item da lista](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[Aplicar a Gestão de Direitos de Informação a uma lista ou biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|Configurar o SharePoint para IRM e bibliotecas protegidas|[Configurar a Gestão de Direitos de Informação (IRM) no centro de administração do SharePoint](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Aplicar a Gestão de Direitos de Informação a uma lista ou biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

### Para configurar a biblioteca do SharePoint para definições de IRM

1.  Depois de configurar o SharePoint para utilizar o serviço de IRM, navegue para a biblioteca do SharePoint que pretende proteger com o Azure RMS. Na página **Definições** &gt; **Gestão de Direitos de Informação (IRM)** do site, além de selecionar **Restringir as permissões nesta biblioteca durante a transferência** e especificar um título da política para os administradores e uma descrição da política para os utilizadores, clique em **MOSTRAR OPÇÕES**.

2.  Selecione o seguinte:

    -   **Não permitir que os utilizadores carreguem documentos que não suportam a IRM**

    -   Opcional: **Permitir proteção de grupo. Grupo predefinido** e, em seguida, especifique o nome de um grupo adicional que poderá ter de colaborar em documentos armazenados nesta biblioteca, mas fora do SharePoint. Por exemplo, o grupo Vendas tem permissões de Edição no site e uma pessoa deste grupo transfere um documento, guarda-o no disco e envia-o por e-mail para uma colega de trabalho que não faz parte do grupo Vendas. Se a colega de trabalho fizer parte do grupo especificado aqui, herda automaticamente as mesmas permissões que estão configuradas para o site e pode editar o documento.

        Sem esta opção, apenas os utilizadores que têm acesso à biblioteca do SharePoint podem colaborar nestes documentos e apenas se os transferirem diretamente do SharePoint. Em muitos casos, esta restrição é adequada.

## Instruções da documentação do utilizador
Não existem instruções sobre procedimentos a dar aos utilizadores para este cenário, uma vez que as bibliotecas protegidas não requerem qualquer ação especial por parte deles. Os documentos são automaticamente protegidos durante a transferência, de acordo com as permissões definidas por um administrador do SharePoint para o site. No entanto, deve informar os utilizadores sobre esta alteração para que saibam o que esperar. Do mesmo modo, deve indicar ao suporte técnico quais são as bibliotecas que estão protegidas e como esta proteção pode restringir a utilização dos documentos. Por exemplo, devido às limitações atuais, estes documentos podem ser visualizados, mas não editados, em dispositivos móveis. Se tiver configurado a proteção de grupo, indique aos utilizadores quais são os grupos que podem aceder e editar documentos fora do SharePoint.

Utilizando o modelo seguinte, copie e cole o anúncio numa comunicação destinada aos utilizadores finais e efetue estas alterações para refletir o seu ambiente:

1.  Substitua cada instância de *&lt;nome da biblioteca do SharePoint&gt;* pelo nome e a ligação da biblioteca do SharePoint que configurou para o Azure Rights Management. Se esta comunicação se destinar a mais do que uma biblioteca protegida, altere as instruções em conformidade.

2.  Se tiver configurado a opção **Permitir proteção de grupo. Grupo predefinido**, substitua *&lt;nome do grupo&gt;* pelo nome do grupo que configurou e forneça o motivo – &lt;motivo pelo qual este grupo tem permissões de acesso para colaborar nos ficheiros, mas não através da biblioteca do SharePoint&gt;. Se não tiver configurado esta opção, elimine esta frase.

3.  Substitua *&lt;detalhes de contacto&gt;* por instruções sobre como os utilizadores podem contactar o suporte técnico, tais como uma ligação para um site, um endereço de e-mail ou um número de telefone.

4.  Efetue quaisquer modificações adicionais que pretenda ao anúncio e, em seguida, envie-o aos utilizadores.

A documentação de exemplo mostra que aspeto este anúncio poderá ter para os utilizadores depois das personalizações.

![Modelo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_UsersBanner.png)

### Anúncio de TI: alterações ao site de &lt;nome da biblioteca do SharePoint&gt;
O site do SharePoint, **&lt;nome da biblioteca do SharePoint&gt;**, está agora configurado para colaboração segura. Agora, apenas os membros do &lt;nome do grupo&gt; podem abrir estes documentos a partir deste site, mesmo que os guarde localmente ou envie por e-mail para outra pessoa. A exceção é que pode partilhá-los com os membros do &lt;nome do grupo&gt; depois de transferir os documentos, para que &lt;motivo pelo qual este grupo tem permissões de acesso para colaborar nos ficheiros, mas não através da biblioteca do SharePoint&gt;. Ao editar os ficheiros, é apresentada uma faixa de informações amarela na parte superior do documento para informá-lo de que tem esta proteção e sobre quem pode aceder.

Esta alteração ajuda a manter os nossos dados confidenciais da empresa protegidos das pessoas que não os devem ver. Se utilizar um dispositivo móvel para aceder a estes documentos protegidos, pode visualizá-los. No entanto, se pretender editá-los, tem de utilizar um dispositivo de ambiente de trabalho.

Não poderá carregar documentos para o site &lt;nome de site do SharePoint&gt; se estes não suportarem a colaboração segura.

**Precisa de ajuda?**

-   Contacte o suporte técnico: &lt;detalhes de contacto&gt;

### Exemplo de documentação do utilizador
![Exemplo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Anúncio de TI: alterações ao site de Previsões de Vendas e Relatórios
O site do SharePoint, **Previsões de Vendas e Relatórios**, está agora configurado para colaboração segura. Agora, apenas os membros da nossa equipa de Vendas e Marketing podem abrir estes documentos a partir deste site, mesmo que os guarde localmente ou envie por e-mail para outra pessoa. A exceção é que pode partilhá-los com os membros da equipa de Finanças depois de transferir os documentos, para que eles possam extrair os valores das previsões mensais. Ao editar os ficheiros, é apresentada uma faixa de informações amarela na parte superior do documento para informá-lo de que tem esta proteção e sobre quem pode aceder.

Esta alteração ajuda a manter os nossos dados confidenciais da empresa protegidos das pessoas que não os devem ver. Se utilizar um dispositivo móvel para aceder a estes documentos protegidos, pode visualizá-los. No entanto, se pretender editá-los, tem de utilizar um dispositivo de ambiente de trabalho.

Não poderá carregar documentos para o site Previsões de Vendas e Relatórios se estes não suportarem a colaboração segura.

**Precisa de ajuda?**

-   Contacte o suporte técnico: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO2-->


