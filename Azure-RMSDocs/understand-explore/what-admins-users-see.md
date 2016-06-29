---
# required metadata

title: O Que Veem os Administradores e Utilizadores? | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013e0eb4-49a7-4e81-9e4d-f56c0ceb017f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# O Azure RMS em ação: o que veem os administradores e utilizadores

*Aplica-se a: Azure Rights Management, Office 365*

Este artigo mostra alguns exemplos típicos de como os administradores e utilizadores veem e podem utilizar o Azure Rights Management (Azure RMS) para ajudar a proteger as informações confidenciais.

> [!NOTE] Em todos estes exemplos, nos quais o Azure RMS protege os dados, o proprietário dos conteúdos continua a ter acesso total aos dados (ficheiro ou e-mail), mesmo que a proteção aplicada conceda permissões a um grupo a que o proprietário não pertença como membro ou mesmo que a proteção aplicada inclua uma data de expiração.
>
> Da mesma forma, a equipa de TI pode aceder sempre aos dados protegidos sem restrições, através da funcionalidade de superutilizador do Rights Management que concede acesso de delegado aos utilizadores ou serviços autorizados especificados por si. Além disso, a equipa de TI pode controlar e monitorizar a utilização dos dados protegidos; por exemplo, quem está a aceder aos dados e quando.

Para ter acesso a outras capturas de ecrã e vídeos que mostram o RMS em ação, consulte o [Microsoft Rights Management services portal (Portal de serviços do Microsoft Rights Management – em inglês)](http://www.microsoft.com/rms) e o [Microsoft Rights Management (RMS) Team Blog (Blogue da Equipa do Microsoft Rights Management (RMS) – em inglês)](http://blogs.technet.com/b/rms).

## Ativar e configurar o Rights Management
Apesar de poder utilizar o Windows PowerShell para ativar e configurar o Azure RMS, é mais fácil fazê-lo a partir do portal de gestão. Assim que o serviço é ativado, dispõe de dois modelos predefinidos que os administradores e os utilizadores podem selecionar para aplicar a proteção de informações aos ficheiros de uma forma rápida e fácil. No entanto, também pode criar os seus próprios modelos personalizados para disponibilizar opções e definições adicionais.

![O QUE VEEM OS ADMINISTRADORES NO PASSO 1](../media/AzRMS_StoryboardActivate_small1.png)


**O QUE VEEM OS ADMINISTRADORES NO PASSO 1:** pode utilizar o centro de administração do Office 365 (primeira imagem) ou o portal clássico do Azure (segunda imagem) para ativar o RMS.<br /><br />Basta um clique para ativar e outro para confirmar, e a proteção de informação estará ativada para administradores e utilizadores da sua organização.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 2](../media/AzRMS_TemplatesPortal_small.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 2:** após a ativação, são automaticamente disponibilizados dois modelos de política de direitos para a sua organização. Um modelo permite o acesso só de leitura (inclui a designação **Apenas Visualização Confidencial** no nome), o outro concede acesso de leitura e modificação (**Confidencial**).

Quando estes modelos são aplicados a ficheiros ou mensagens de e-mail, restringem o acesso aos utilizadores da sua organização. Esta é uma forma muito rápida e fácil de ajudar a impedir a fuga de dados da sua empresa para pessoas fora da sua organização.

> [!TIP]
> Estes modelos predefinidos são facilmente reconhecidos, uma vez que lhes é automaticamente adicionado o nome da sua organização como prefixo. No nosso exemplo, **VanArsdel, Ltd**

Se não quiser que estes modelos sejam apresentados aos utilizadores ou preferir criar os seus próprios modelos, pode fazê-lo a partir do portal clássico do Azure. Como mostra a imagem, terá a ajuda de um assistente que o orienta ao longo do processo de criação do modelo personalizado.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 3](../media/AzRMS_TemplatesSettings3.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 3:** acesso offline, definições de expiração e eventuais instruções para publicar o modelo imediatamente (torná-lo visível em aplicações que suportam o Rights Management) são algumas das definições de configuração disponíveis se optar por criar os seus próprios modelos.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 4](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 4:** na sequência da publicação destes modelos, os utilizadores passam a poder selecioná-los em aplicações como o Explorador de Ficheiros e o Microsoft Word:

- Um utilizador poderia escolher o modelo predefinido, **VanArsdel, Ldt – Confidencial**. Desta forma, apenas os funcionários da organização VanArsdel podem abrir e utilizar este documento, mesmo que mais tarde seja enviado por e-mail a alguém fora da organização ou guardado numa localização pública.

- Um utilizador poderia escolher o modelo personalizado criado pelo administrador, **Vendas e Marketing – Apenas Leitura e Impressão**. Desta forma, além de estar protegido de pessoas fora da organização, o ficheiro está igualmente restringido aos funcionários do departamento de Vendas e Marketing. Além disso, estes funcionários não têm direitos totais sobre o documento, apenas de leitura e impressão. Por exemplo, não podem modificá-lo nem copiar trechos do mesmo.

---

**Para mais informações relativas a este cenário:**

- Para obter instruções passo a passo, consulte [Activating Azure Rights Management (Ativar o Azure Rights Management – em inglês)](../deploy-use/activate-service.md) e [Configuring custom templates for Azure Rights Management (Configurar modelos personalizados para o Azure Rights Management – em inglês)](../deploy-use/configure-custom-templates.md).

- Para ajudar os utilizadores a proteger ficheiros importantes da empresa, consulte [Helping users to protect files by using Azure Rights Management (Ajudar os utilizadores a proteger ficheiros com o Azure Rights Management – em inglês)](../deploy-use/help-users.md).

Em seguida, veja alguns exemplos que ilustram a forma como os administradores podem aplicar os modelos para configurar automaticamente a proteção de informações de ficheiros e mensagens de e-mail.

## Proteger automaticamente os ficheiros em servidores de ficheiros com o Windows Server e a Infraestrutura de Classificação de Ficheiros

Este exemplo mostra como pode utilizar o Azure RMS para proteger automaticamente os ficheiros em servidores de ficheiros que têm, pelo menos, o Windows Server 2012 e estão configurados para utilizar a Infraestrutura de Classificação de Ficheiros.

Existem várias formas de aplicar valores de classificação aos ficheiros. Por exemplo, pode inspecionar os conteúdos dos ficheiros e aplicar as classificações incorporadas que se adequem, tal como Confidencialidade e Informações Pessoais. No entanto, neste exemplo, um administrador cria uma classificação personalizada, **Marketing**, que é aplicada automaticamente a todos os documentos de utilizador guardados na pasta **Promoções de Marketing**. Apesar de esta pasta estar protegida com permissões de NTFS que restringem o acesso aos membros do grupo de Marketing, o administrador sabe que estas permissões podem ser perdidas se alguém desse grupo mover ou enviar os ficheiros por e-mail. Nessa situação, as informações contidas nos ficheiros poderiam ser acedidas por utilizadores não autorizados.

![O QUE VEEM OS ADMINISTRADORES NO PASSO 1](../media/AzRMS_FCI_ConnectorSmall.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 1:** os administradores instalam e configuram o conector Rights Management (RMS), que funciona como um reencaminhador entre os servidores no local e o Azure RMS.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 2](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 2:** no servidor de ficheiros, o administrador configura as tarefas e regras de classificação de modo a que todos os ficheiros de utilizador contidos na pasta **Promoções de Marketing** sejam automaticamente classificados como **Marketing** e protegidos com a encriptação do RMS.

Seleciona o modelo personalizado do RMS criado no primeiro exemplo, que restringe o acesso aos membros dos departamentos de Vendas e Marketing: **Vendas e Marketing – Apenas Leitura e Impressão**.

Como resultado, todos os documentos contidos nessa pasta são automaticamente configurados com a classificação de Marketing e protegidos pelo modelo de Vendas e Marketing do RMS.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 3](../media/AzRMS_FCI_EmailSmall.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 3:** forma como o RMS ajuda a impedir a fuga de dados para pessoas que não devem ter acesso a informações confidenciais:

- A Júlia, do departamento de Marketing, envia um relatório confidencial da pasta Promoções de Marketing por e-mail. Este relatório contém novas funcionalidades do produto e planos de publicidade e foi pedido por um colega de trabalho que está atualmente numa viagem de negócios. No entanto, a Júlia envia-o por engano à pessoa errada, pois não reparou que selecionou acidentalmente um destinatário com um nome semelhante, mas de outra empresa.<br><br>
O destinatário não poderá ler o relatório confidencial porque não é um membro do grupo de Vendas e Marketing.

---

**Para mais informações relativas a este cenário:**

- Para obter instruções passo a passo, consulte [Deploying the Azure Rights Management connector (Implementar o conector Azure Rights Management – em inglês)](../deploy-use/deploy-rms-connector.md).

## Proteger automaticamente a mensagens de e-mail com o Exchange Online e políticas de prevenção de perda de dados

O exemplo anterior mostrou como pode proteger automaticamente ficheiros que contêm informações confidenciais, mas o que acontece se as informações não estiverem num ficheiro e sim numa mensagem de e-mail? É aqui que as políticas de prevenção de perda de dados (DLP) do Exchange Online entram em ação, seja através de pedidos aos utilizadores no sentido de aplicarem a proteção de informações (por intermédio de Sugestões de Política) seja através da sua aplicação automática (por intermédio de regras de transporte).

Neste exemplo, o administrador configura uma política para ajudar a manter a organização em conformidade com as normas dos E.U.A. no que se refere à proteção de dados de informações pessoais, mas também é possível configurar as regras para outras normas de conformidade ou regras personalizadas definidas por si.

![O QUE VEEM OS ADMINISTRADORES NO PASSO 1](../media/AzRMS_DLPExample1.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 1:** no centro de administração do Exchange, o modelo do Exchange com o nome ** Dados de Informação Identificativa (PII) dos E.U.A.** é utilizado pelo administrador para criar e configurar uma nova política de DLP. Este modelo procura informações como números de segurança social e números de cartas de condução nas mensagens e-mail.

As regras são configuradas de modo a que a proteção de direitos seja automaticamente aplicada às mensagens de e-mail que contêm estas informações e que são enviadas para fora da organização, através de um modelo de RMS que restringe o acesso exclusivamente aos funcionários da empresa.

Aqui, a regra está configurada para utilizar um dos modelos predefinidos, **VanArsdel, Ltd – Confidencial**, do primeiro exemplo. Porém, também pode ver que o leque de modelos inclui todos os modelos personalizados que criou, bem como uma opção **Não Reencaminhar** específica do Exchange.

> [!NOTE]
> Se as opções de configuração que vê são ligeiramente diferentes da imagem, poderá ter de selecionar primeiro **Mais opções** ao configurar a regra. Em seguida, pode selecionar **Modificar a mensagem segurança** > **Aplicar proteção de direitos** e, em seguida, selecione o modelo do RMS.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 2](../media/AzRMS_DLPUnprotectedEmail_small.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 2:** o gestor de contratações escreve uma mensagem de e-mail que contém o número de segurança social de um funcionário contratado recentemente. Em seguida, envia a mensagem de e-mail para a Sofia, do departamento de Recursos Humanos.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 3](../media/AzRMS_DLPProtectedEmail_small.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 3:** se esta mensagem de e-mail for enviada ou reencaminhada para alguém fora da organização, a regra de DLP aplica automaticamente a proteção de direitos.

A mensagem de e-mail é encriptada quando sai da infraestrutura da organização, para que o número de segurança social nela contido não possa ser lido enquanto se encontra em trânsito ou na caixa de entrada do destinatário. O destinatário só conseguirá ler a mensagem se for um funcionário da VanArsdel.

---

**Para mais informações relativas a este cenário:**

-   Para mais informações sobre a interação do Azure RMS com o Exchange Online, consulte a secção [Exchange Online e Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) em [How applications support Azure Rights Managemen (Como é que as aplicações suportam o Azure Rights Management – em inglês)](applications-support.md).

-   Para obter instruções passo a passo com vista à configuração do Exchange Online para o Azure RMS, consulte a secção [Exchange Online: IRM Configuration (Exchange Online: Configuração da IRM – em inglês)](../deploy-use/configure-office365.md#exchange-online-irm-configuration) em [Configuring applications for Azure Rights Management (Configurar aplicações para o Azure Rights Management – em inglês)](../deploy-use/configure-applications.md).

## Proteger automaticamente os ficheiros com o SharePoint Online e as bibliotecas protegidas

Este tópico mostra como é fácil proteger documentos com o SharePoint Online e as bibliotecas protegidas.

Neste exemplo, o administrador do SharePoint da Contoso criou uma biblioteca para cada departamento, que utiliza para armazenar e dar saída de documentos de forma centralizada para fins de edição e controlo de versões. Por exemplo, existe uma biblioteca para o departamento de Vendas, outra para o de Marketing, outra para o de Recursos Humanos e assim sucessivamente. Sempre que é carregado ou criado um novo documento numa destas bibliotecas protegidas, esse documento herda a proteção da biblioteca (sem ter de selecionar um modelo de política de direitos), sendo automaticamente protegido e permanecendo protegido, mesmo que seja movido para fora da biblioteca do SharePoint.

![O QUE VEEM OS ADMINISTRADORES NO PASSO 1](../media/AzRMS_StoryboardSPO_small1.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 1:** o administrador ativa a Gestão de Direitos de Informação para o site do SharePoint.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 2](../media/AzRMS_StoryboardSPO_small2.png)

**O QUE VEEM OS ADMINISTRADORES NO PASSO 2:** em seguida, ativa o Rights Management para uma biblioteca. Apesar de existirem opções adicionais, esta definição simples é, muitas vezes, tudo o que precisa.

A partir desse momento, sempre que forem transferidos documentos a partir desta biblioteca, estarão automaticamente protegidos pelo Rights Management, herdando a proteção configurada para a biblioteca.

---

![O QUE VEEM OS ADMINISTRADORES NO PASSO 3](../media/AzRMS_StoryboardSPO_small3.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 3:** quando alguém do departamento de vendas der saída deste relatório de vendas a partir da biblioteca, verá claramente na faixa de informações localizada na parte superior que se trata de um documento protegido com acesso restrito.

O documento permanece protegido mesmo que o utilizador lhe mude o nome, o guarde noutra localização ou o partilhe por e-mail. Independentemente do nome do ficheiro, do local onde está armazenado ou da partilha por e-mail, os membros do departamento de vendas serão as únicas pessoas que o poderão ler.

---

**Para mais informações relativas a este cenário:**

-   Para mais informações sobre a interação do Azure RMS com o SharePoint, consulte a secção [SharePoint Online and SharePoint Server (SharePoint Online e SharePoint Server – em inglês)](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) em [How applications support Azure Rights Management (Como é que as aplicações suportam o Azure Rights Management – em inglês)](applications-support.md).

-   Para obter instruções passo a passo com vista à configuração do SharePoint para o Azure RMS, consulte a secção [SharePoint Online and OneDrive for Business: IRM Configuration (SharePoint Online e OneDrive para Empresas: Configuração da IRM – em inglês)](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) em [Configuring Applications for Azure Rights Management (Configurar Aplicações para o Azure Rights Management – em inglês)](../deploy-use/configure-applications.md).

## Os utilizadores partilham anexos de forma segura com os utilizadores móveis

Os exemplos anteriores demonstraram como os administradores podem aplicar a proteção de informações aos dados confidenciais de forma automática. No entanto, pode haver ocasiões em que os utilizadores poderão precisar de aplicar esta proteção pessoalmente. Por exemplo, se estiverem a colaborar com parceiros noutra organização, precisarem de definições ou permissões personalizadas que não estão definidas nos modelos ou outras situações ad-hoc que não são abrangidas pelos exemplos anteriores. Nestas situações, os utilizadores podem aplicar os modelos de RMS pessoalmente ou configurar permissões personalizadas.

Este exemplo mostra como os utilizadores podem partilhar facilmente um documento com uma pessoa de outra empresa com quem estejam a colaborar, sem descurar a proteção do documento e com a certeza de que o destinatário o conseguirá ler, mesmo a partir de um dispositivo móvel popular. Este cenário utiliza a aplicação de partilha Rights Management, que pode implementar automaticamente nos computadores Windows da sua organização. Em alternativa, os utilizadores podem instalá-la pessoalmente.

Neste exemplo, a Adriana, da Contoso, envia um documento do Word confidencial por e-mail para o Artur, da Fabrikam. Este lê o documento no seu iPad, mas também poderia fazê-lo facilmente num iPhone, num telemóvel ou tablet Android, num computador Mac ou num computador ou telemóvel com Windows.

![O QUE VEEM OS UTILIZADORES NO PASSO 1](../media/AzRMS_StoryboardEmail_small1.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 1:** num PC com Windows, a Inês cria uma mensagem de e-mail padrão e anexa um documento.

A seguir, clica em **Partilhar Protegido** no friso, o que carrega a caixa de diálogo **partilha protegida** da aplicação de partilha RMS.

A Inês quer restringir as ações do Artur à visualização e edição do documento; além disso, não quer que este o copie ou imprima, por isso seleciona **REVISOR – Ver e Editar**. Também quer receber uma mensagem por e-mail quando alguém tentar abrir o documento, bem como ter a capacidade de revogar o documento mais tarde, se for necessário, com a certeza de que a revogação entrará em vigor imediatamente.

---

![O QUE VEEM OS UTILIZADORES NO PASSO 2](../media/AzRMS_StoryboardEmail_small2.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 2:** o Artur vê a mensagem de e-mail no seu iPad.

Para além da mensagem e do anexo enviados pela Inês, encontra instruções para se inscrever e instalar a aplicação de partilha RMS no seu iPad.

---

![O QUE VEEM OS UTILIZADORES NO PASSO 3](../media/AzRMS_StoryboardEmail_small3.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 3:** o Artur pode agora abrir o anexo. Em primeiro lugar, é-lhe pedido que inicie sessão a fim de confirmar que é o destinatário pretendido.

Quando o Artur vê o documento, vê também as informações de acesso restrito com a indicação de que pode ver e editar o documento, mas não o pode copiar ou imprimir.

---

![O QUE VEEM OS UTILIZADORES NO PASSO 4](../media/AzRMS_StoryboardEmail_small4.png)

**O QUE VEEM OS UTILIZADORES NO PASSO 4:** a Inês recebe uma mensagem de e-mail a indicar que o Artur abriu o documento que ela lhe enviou com êxito, indicando também quando foi feito o acesso ao documento.

Se o Artur reencaminhar a mensagem de e-mail com o anexo, se a guardar num local onde outros utilizadores lhe podem aceder ou se esta for intercetada na rede, mais ninguém conseguirá ler o documento.

---

**Para mais informações relativas a este cenário:**

- Para obter instruções passo a passo, consulte [Protect a file that you share by email (Proteger um ficheiro partilhado por e-mail – em inglês)](../rms-client/sharing-app-protect-by-email.md) e [View and use files that have been protected (Ver e utilizar ficheiros que foram protegidos – em inglês)](../rms-client/sharing-app-view-use-files.md) do [Rights Management sharing application user guide (Guia de utilizador da aplicação de partilha Rights Management – em inglês)](../rms-client/sharing-app-user-guide.md).

- O [Quick start tutorial for Azure Rights Management (Tutorial de introdução ao Azure Rights Management – em inglês)](../get-started/quick-start-tutorial.md) inclui instruções passo a passo para este cenário.

## Passos seguintes

Agora que viu alguns exemplos das capacidades do Azure RMS, poderá estar interessado na aplicação prática das mesmas. Para obter informações técnicas sobre o funcionamento do Azure RMS, consulte [How does Azure RMS work? (Como funciona o Azure RMS? – em inglês)](how-does-it-work.md)


<!--HONumber=Jun16_HO2-->


