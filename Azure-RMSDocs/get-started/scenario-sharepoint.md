---
# required metadata

title: Cenário: reter controle de documentos armazenados no SharePoint | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
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

# Cenário: reter controle de documentos armazenados no SharePoint
Esse cenário e a documentação do usuário de suporte usam o Azure Rights Management para garantir que os documentos do Office armazenados no SharePoint permaneçam sob seu controle usando bibliotecas protegidas. Por exemplo, os documentos são protegidos automaticamente contra vazamento acidental ou pretendido pelos usuários, e você pode bloquear o acesso ao conteúdo mesmo depois que ele é baixado ou sincronizado. Os arquivos que você deseja proteger podem ser para colaboração interna em planos ou documentos de design ou para outros resultados. Quando você configurar bibliotecas protegidas para o SharePoint, os arquivos do Office armazenados nelas estarão protegidos pelo Azure Rights Management.

As instruções são adequadas para o seguinte conjunto de circunstâncias:

-   Os funcionários compartilham e colaboram com documentos do Office que estão em uma biblioteca do SharePoint.

-   Os funcionários não precisam definir ou alterar as permissões que um administrador define no nível da biblioteca.

-   Os funcionários não precisam compartilhar esses documentos com pessoas fora da sua organização.

## Instruções de implantação
![](../media/AzRMS_AdminBanner.png)

Tenha os seguintes requisitos e os procedimentos de suporte prontos antes de ir para a documentação do usuário.

## Requisitos para este cenário
Para que este cenário funcione, o seguinte deve ser feito:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|Você preparou contas e grupos do Office 365 ou o Azure Active Directory|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Se você pretende usar o SharePoint Server: Implante o conector RMS e configure-o para o SharePoint|[Implantando o conector do Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Configurar permissões para o site do SharePoint a fim de proteger|[Gerencie permissões para uma lista, biblioteca, pasta, documento ou item de lista](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[Aplicar o Gerenciamento de Direitos de Informação a uma lista ou biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|Configurar o SharePoint para o IRM e bibliotecas protegidas|[Configurar o Gerenciamento de Direitos de Informação (IRM) no centro de administração do SharePoint](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Aplicar o Gerenciamento de Direitos de Informação a uma lista ou biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

### Para configurar a biblioteca do SharePoint de acordo com as configurações IRM

1.  Depois de configurar o SharePoint para usar o serviço IRM, navegue até a biblioteca do SharePoint para protegê-la com o Azure RMS. Na página **Configurações** &gt; **IRM (Gerenciamento de Direitos de Informação)** no site, além de selecionar **Restringir permissões nesta biblioteca no download** e especificar um título de política para administradores e descrições uma política para os usuários, clique em **MOSTRAR OPÇÕES**.

2.  Selecione os seguintes valores:

    -   **Não permite que usuários carreguem documentos que não dão suporte a IRM**

    -   Opcional: **permitir a proteção de grupo. Grupo padrão** e especifique o nome de um grupo adicional que precise colaborar com documentos armazenados na biblioteca, mas fora do SharePoint. Por exemplo, o grupo Vendas tem permissões de edição para o site e alguém desse grupo faz o download de um documento, salva em disco e envia por email para uma colega de trabalho que não está no grupo Vendas. Se o colega de trabalho estiver no grupo que você especificar aqui, ela herdará automaticamente as mesmas permissões que são configuradas para o site e será capaz de editar o documento.

        Sem essa opção, somente os usuários que têm acesso à biblioteca do SharePoint poderão colaborar nesses documentos e somente baixando-os diretamente do SharePoint. Em muitos casos, essa restrição é adequada.

## Instruções sobre a documentação do usuário
Não há instruções procedimentais específicas para dar aos usuários para esse cenário porque as bibliotecas protegidas não exigem ações especiais dos usuários. Os documentos são automaticamente protegidos no download, de acordo com as permissões que um administrador do SharePoint define para o site. No entanto, informe os usuários sobre essa alteração para que eles saibam o que esperar e informe ao Suporte Técnico quais bibliotecas são protegidas e como isso pode restringir o uso dos documentos. Por exemplo, devido a limitações atuais, os documentos podem ser exibidos, mas não editados com dispositivos móveis. Se você tiver configurado a proteção do grupo, informe aos usuários quais grupos podem acessar e editar documentos fora do SharePoint.

Usando o modelo a seguir, copie e cole o anúncio em uma comunicação para seus usuários finais e faça com que essas modificações reflitam o seu ambiente:

1.  Substitua cada ocorrência do *&lt;nome da biblioteca do SharePoint&gt;* pelo nome e link da biblioteca do SharePoint que você configurou para o Azure Rights Management. Se essa comunicação for para mais de uma biblioteca protegida, altere as instruções adequadamente.

2.  Se você tiver configurado o **Permitir a proteção de grupo. Opção Grupo padrão**, substitua *&lt;nome do grupo&gt;* pelo nome do grupo configurado e forneça a &lt;razão por que esse grupo tem permissões de acesso para colaborar nos arquivos, mas não usando a biblioteca do SharePoint&gt;. Se você não configurou essa opção, exclua essa frase.

3.  Substitua os *&lt;detalhes de contato&gt;* por instruções sobre como os usuários podem entrar em contato com o suporte técnico, como um link de site, endereço de email ou número de telefone.

4.  Faça modificações adicionais no anúncio, se desejar, e envie-o para esses usuários.

A documentação de exemplo mostra como esse anúncio pode parecer para os usuários depois das personalizações.

![](../media/AzRMS_UsersBanner.png)

### Anúncio de TI: mudanças no site &lt;nome da biblioteca do SharePoint&gt;
O site do SharePoint, **&lt;nome da biblioteca do SharePoint&gt;**, agora está configurado para colaboração segura. Agora, somente membros do &lt;nome do grupo&gt; podem abrir esses documentos neste site, mesmo se você salvá-los localmente ou enviá-los para outra pessoa. A exceção é que você pode compartilhá-los com membros do &lt;nome do grupo&gt; depois de baixar os documentos, para que &lt;motivo por que esse grupo tem permissões de acesso para colaborar nos arquivos, mas não usando a biblioteca do SharePoint&gt;. Quando editar os arquivos, você verá um banner de informações amarelo na parte superior do documento, para que possa saber que tem essa proteção e quem pode acessá-los.

Essa alteração ajuda a manter os dados confidenciais de nossa empresa protegidos de pessoas que não deveriam vê-los. Se usa um dispositivo móvel para acessar esses documentos protegidos, você pode visualizá-los, mas deve usar um dispositivo de desktop para editá-los.

Você não pode carregar documentos para o site &lt;nome do site do SharePoint&gt; se eles não dão suporte a colaboração segura.

**Precisa de ajuda?**

-   Entre em contato com o suporte técnico: &lt;detalhes de contato&gt;

### Documentação do usuário de exemplo
![](../media/AzRMS_ExampleBanner.png)

#### Anúncio de TI: Alterações no site de Relatórios e Previsões de Vendas
O site do SharePoint, **Relatórios e Previsões de Vendas**, agora está configurado para colaboração segura. Agora, somente membros de nossas equipes de vendas e marketing podem abrir esses documentos neste site, mesmo se você salvá-los localmente ou enviá-los para outra pessoa. A exceção é que você pode compartilhá-los com os membros da equipe de finanças depois de ter baixado os documentos, assim eles podem extrair os números de previsão mensais. Quando editar os arquivos, você verá um banner de informações amarelo na parte superior do documento, para que possa saber que tem essa proteção e quem pode acessá-los.

Essa alteração ajuda a manter os dados confidenciais de nossa empresa protegidos de pessoas que não deveriam vê-los. Se usa um dispositivo móvel para acessar esses documentos protegidos, você pode visualizá-los, mas deve usar um dispositivo de desktop para editá-los.

Você não pode carregar documentos para o site de previsões de vendas e relatórios se eles não oferecem suporte a colaboração segura.

**Precisa de ajuda?**

-   Contate o suporte técnico: helpdesk@vanarsdelltd.com



<!--HONumber=Apr16_HO4-->


