---
# required metadata

title: O que os administradores e os usuários veem? | Azure RMS
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


# O Azure RMS em ação: O que administradores e usuários veem

*Aplica-se a: Azure Rights Management, Office 365*

Este artigo mostra alguns exemplos comuns de como administradores e usuários veem e podem usar o Azure RMS (Azure Rights Management) para ajudar a proteger informações confidenciais.

> [!NOTE] Em todos esses exemplos em que o Azure RMS protege os dados, o proprietário do conteúdo continua com acesso completo aos dados (arquivo ou email), mesmo que a proteção aplicada conceda permissões a um grupo do qual o proprietário não seja um membro ou mesmo que a proteção aplicada inclua uma data de validade.
>
> Da mesma forma, a TI sempre pode acessar os dados protegidos sem restrições, usando o recurso de superusuário do gerenciamento de direitos que concede acesso delegado a usuários autorizados ou serviços que você especificar. Além disso, a TI pode controlar e monitorar o uso de dados que foi protegido — por exemplo, quem está acessando os dados e quando.

Para outras capturas de tela e vídeos que mostram o RMS em ação, confira o [portal dos serviços do Microsoft Rights Management](http://www.microsoft.com/rms) e o [Blog da equipe do Microsoft RMS (Rights Management)](http://blogs.technet.com/b/rms)

## Ativando e configurando o Rights Management
Embora você possa usar o Windows PowerShell para ativar e configurar o Azure RMS, é mais fácil no portal de gerenciamento. Assim que o serviço é ativado, você tem dois modelos padrão que os administradores e os usuários podem selecionar para aplicar rapidamente e facilmente a proteção de informações nos arquivos. Mas você também pode criar seus próprios modelos personalizados para opções adicionais e configurações.

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 1](../media/AzRMS_StoryboardActivate_small1.png)


**O QUE OS ADMINISTRADORES VEEM NA ETAPA 1:** você pode usar o centro de administração do Office 365 (primeira imagem) ou o portal clássico do Azure (segunda imagem) para ativar o RMS.<br /><br />Basta um clique para ativar e outro clique para confirmar; assim a proteção de informações está habilitada para administradores e usuários em sua organização.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 2](../media/AzRMS_TemplatesPortal_small.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 2:** após a ativação, dois modelos de política de direitos ficam disponíveis automaticamente para sua organização. Um modelo é somente leitura (**Somente Exibição Confidencial** aparece no nome) e o outro é para acesso de leitura e modificação (**Confidencial**).

Quando esses modelos são aplicados aos arquivos ou emails, eles restringem o acesso a usuários em sua organização. Essa é uma maneira muito fácil e rápida de ajudar a impedir que os dados da empresa vazem para pessoas fora da sua organização.

> [!TIP]
> Você pode reconhecer facilmente esses modelos padrão, pois eles são automaticamente precedidos pelo nome da sua organização. Em nosso exemplo, **VanArsdel, Ltd**.

Se não quiser que os usuários vejam esses modelos ou se quiser criar seus próprios modelos, será possível fazer isso no Portal clássico do Azure. Como mostra a imagem, um assistente o guiará durante o processo de criação de modelo personalizado.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 3](../media/AzRMS_TemplatesSettings3.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 3:** acesso offline, configurações de expiração e publicação imediata do modelo (torná-lo visível em aplicativos que dão suporte ao Rights Management) serão algumas das definições de configuração disponíveis se você optar por criar seus próprios modelos.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 4](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 4:** como resultado da publicação desses modelos, os usuários podem selecioná-los agora em aplicativos como Microsoft Word e o Explorador de Arquivos:

- Um usuário pode escolher o modelo padrão, **VanArsdel, Ltd – Confidencial**. Em seguida, somente os funcionários da organização VanArsdel podem abrir e usar este documento, mesmo que enviado por email posteriormente para alguém fora da organização ou salvo em um local público.

- Um usuário pode escolher o modelo personalizado criado pelo administrador, **Vendas e Marketing – Somente Leitura e Impressão**. Assim, o arquivo não é somente protegido das pessoas fora da organização, mas ele também é restrito aos funcionários do departamento de Vendas e Marketing. Além disso, esses funcionários não possuem direitos totais para o documento, somente leitura e impressão. Por exemplo, eles não podem modificá-lo ou copiá-lo.

---

**Mais informações sobre esse cenário:**

- Para obter instruções passo a passo, confira [Ativando o Azure Rights Management](../deploy-use/activate-service.md) e [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

- Para ajudar os usuários a proteger arquivos importantes da empresa, confira [Ajudando os usuários a proteger arquivos usando o Azure Rights Management](../deploy-use/help-users.md).

Em seguida, veja alguns exemplos de como os administradores podem aplicar os modelos para configurar automaticamente a proteção de informações para arquivos e emails.

## Protegendo automaticamente arquivos em servidores de arquivos que executam o Windows Server e a infraestrutura de classificação de arquivos

Este exemplo mostra como você pode usar o Azure RMS para proteger automaticamente os arquivos em servidores de arquivos que executam pelo menos o Windows Server 2012 e que estão configurados para usar a infraestrutura de classificação de arquivos.

Há várias maneiras de aplicar os valores de classificação aos arquivos. Por exemplo, você pode inspecionar o conteúdo dos arquivos e portanto aplicar classificações internas como confidencialidade e informações de identificação pessoal. No entanto, neste exemplo, um administrador cria uma classificação personalizada do **Marketing** que é aplicada automaticamente a todos os documentos do usuário que foram salvos na pasta **Promoções de Marketing** . Embora essa pasta seja protegida com permissões NTFS que restringem o acesso aos membros do grupo Marketing, o administrador sabe que essas permissões podem ser perdidas se alguém desse grupo se mudar ou enviar os arquivos por email. Em seguida, as informações nos arquivos podem ser acessadas por usuários não autorizados.

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 1](../media/AzRMS_FCI_ConnectorSmall.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 1:** os administradores instalam e configuram o conector do RMS (Rights Management), que atua como um retransmissor entre servidores locais e o Azure RMS.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 2](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 2:** no servidor de arquivos, o administrador configura as regras de classificação e tarefas para que todos os arquivos do usuário na pasta **Promoções de Marketing** sejam automaticamente classificadas como **Marketing** e protegidas com criptografia RMS.

Ela seleciona o modelo de RMS personalizado que foi criado no primeiro exemplo, que restringe o acesso a membros dos departamentos de Vendas e de Marketing: **Vendas e Marketing – Somente Leitura e Impressão**.

Como resultado, todos os documentos nessa pasta são automaticamente configurados com a classificação de Marketing e protegidos pelo modelo RMS Vendas e Marketing.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 3](../media/AzRMS_FCI_EmailSmall.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 3:** como o RMS ajuda a evitar o vazamento de dados às pessoas que não devem ter acesso a informações confidenciais:

- Janet, de Marketing, envia email de um relatório confidencial da pasta Promoções de Marketing. Esse relatório contém as características do novo produto e os planos de propaganda, e isso é solicitado por um colega de trabalho que está viajando atualmente a negócios. No entanto, Janet por engano envia por email para a pessoa errada — ela nem notou que selecionou acidentalmente um destinatário com um nome semelhante, em outra empresa.<br><br>
O destinatário não pode ler o relatório confidencial porque ele não é um membro do grupo de Vendas e Marketing.

---

**Mais informações sobre esse cenário:**

- Para obter instruções passo a passo, confira [Deploying the Azure Rights Management connector (Implantando o conector do Azure Rights Management)](../deploy-use/deploy-rms-connector.md).

## Proteger automaticamente emails com o Exchange Online e políticas de prevenção de perda de dados

O exemplo anterior mostrou como você poderia proteger automaticamente os arquivos que contêm informações confidenciais, mas e se as informações não estiverem em um arquivo, mas sim em uma mensagem de email? É aí em que as políticas de prevenção de perda de dados (DLP) do Exchange Online entram em ação, seja solicitando aos usuários que apliquem a proteção de informações (usando as Dicas de política) ou aplicando-a automaticamente (usando regras de transporte).

Nesse exemplo, o administrador configura uma política para ajudar a manter a organização em conformidade com nos regulamentos dos EUA para proteção de dados de informações de identificação pessoal, mas as regras também podem ser configuradas para outras regulamentações de conformidade ou regras personalizadas que você definir.

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 1](../media/AzRMS_DLPExample1.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 1:** no centro de administração do Exchange, o modelo do Exchange chamado ** Dados de PII (Informações de Identificação Pessoal) dos EUA** é usado pelo administrador para criar e configurar uma nova política DLP. Esse modelo procura informações como números de previdência social e números da carteira de motorista nas mensagens de email.

As regras são configuradas para que as mensagens de email que contêm essas informações e enviadas fora da organização automaticamente tenham proteção de direitos aplicada usando um modelo de RMS que restringe o acesso apenas aos funcionários da empresa.

Aqui, a regra está configurada para usar um dos modelos padrão, **VanArsdel, Ltd – Confidencial**, do nosso primeiro exemplo. Mas você também pode ver como a escolha de modelos inclui quaisquer modelos personalizados que você criou e uma opção **Não Encaminhar** que é específica para o Exchange.

> [!NOTE]
> Se as opções de configuração que você vê forem ligeiramente diferentes daquelas na imagem, pode ser necessário primeiro selecionar **Mais opções** ao configurar a regra. Então você pode selecionar **Modificar a segurança da mensagem** > **Aplicar proteção dos direitos** e, em seguida, selecione o modelo de RMS.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 2](../media/AzRMS_DLPUnprotectedEmail_small.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 2:** o gerente de contratação escreve uma mensagem de email contendo o número de previdência social de um funcionário contratado recentemente. Ele envia essa mensagem de email para Sherrie no departamento de Recursos Humanos.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 3](../media/AzRMS_DLPProtectedEmail_small.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 3:** se essa mensagem de email for enviada ou encaminhada para alguém fora da organização, a regra DLP aplicará automaticamente a proteção de direitos.

O email é criptografado quando ele sai da infra-estrutura da organização, para que o número de previdência social na mensagem de email não possa ser lido em trânsito ou na caixa de entrada do destinatário. O destinatário não poderá ler a mensagem, a menos que ele seja um funcionário VanArsdel.

---

**Mais informações sobre esse cenário:**

-   Para saber mais sobre como o Azure RMS funciona com o Exchange Online, confira a seção sobre o [Exchange Online e o Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) de [How applications support Azure Rights Management (Como os aplicativos dão suporte ao Azure Rights Management)](applications-support.md).

-   Para obter instruções passo a passo sobre como configurar o Exchange Online para o Azure RMS, confira [Exchange Online: IRM Configuration (Exchange Online: configuração do IRM)](../deploy-use/configure-office365.md#exchange-online-irm-configuration) de [Configuring applications for Azure Rights Managemen (Configurando aplicativos para o Azure Rights Management)](../deploy-use/configure-applications.md).

## Protegendo automaticamente os arquivos com SharePoint Online e bibliotecas protegidas

Isso mostra como você pode proteger facilmente documentos quando usa o SharePoint Online e as bibliotecas protegidas.

Nesse exemplo, o administrador do SharePoint para Contoso criou uma biblioteca para cada departamento que eles usam para armazenar centralmente e consultar os documentos para controle de versão e edição. Por exemplo, há uma biblioteca para Vendas, uma para Marketing, uma para Recursos Humanos e assim por diante. Quando um novo documento for carregado ou criado em uma dessas bibliotecas protegidas, esse documento herda a proteção da biblioteca (sem necessidade de selecionar um modelo de política de direitos) e esse documento é protegido automaticamente e permanece protegido, mesmo que ele seja movido para fora da biblioteca do SharePoint.

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 1](../media/AzRMS_StoryboardSPO_small1.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 1:** a administradora ativa o Information Rights Management para o site do SharePoint.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 2](../media/AzRMS_StoryboardSPO_small2.png)

**O QUE OS ADMINISTRADORES VEEM NA ETAPA 2:** ela habilita o Rights Management para uma biblioteca. Embora existam opções adicionais, essa configuração simples geralmente é tudo o que é necessário.

Agora, quando os documentos são baixados desta biblioteca, eles são automaticamente protegidos pelo Rights Management, herdando a proteção que está configurada para a biblioteca.

---

![O QUE OS ADMINISTRADORES VEEM NA ETAPA 3](../media/AzRMS_StoryboardSPO_small3.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 3:** quando alguém do departamento de vendas verifica esse relatório de vendas na biblioteca, eles podem ver claramente da faixa de informações na parte superior que se trata de um documento protegido com acesso restrito.

O documento permanece protegido, mesmo se o usuário o renomear, salvá-lo em outro local ou compartilhá-lo por email. Não importa qual arquivo é nomeado, onde ele está armazenado ou se ele é compartilhado por email, somente os membros do departamento de vendas podem lê-lo.

---

**Mais informações sobre esse cenário:**

-   Para saber mais sobre como o Azure RMS funciona com o SharePoint, confira a seção sobre o [SharePoint Online e o SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) de [How applications support Azure Rights Management (Como os aplicativos dão suporte ao Azure Rights Management)](applications-support.md).

-   Para obter instruções passo a passo sobre como configurar o SharePoint para o Azure RMS, confira a seção [SharePoint Online e OneDrive for Business: configuração do IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) de [Configurando aplicativos para o Azure Rights Management](../deploy-use/configure-applications.md).

## Os usuários compartilham com segurança anexos com usuários móveis

Os exemplos anteriores mostraram como os administradores podem aplicar automaticamente a proteção de informações para dados confidenciais. Mas haverá algumas ocasiões em que os usuários talvez precisem aplicar essa proteção sozinhos. Por exemplo, eles estão colaborando com parceiros em outra organização, eles precisam de permissões personalizadas ou configurações que não são definidas nos modelos ou em situações ad hoc que não estão cobertas pelos exemplos anteriores. Nessas situações, os usuários podem aplicar os modelos de RMS sozinhos ou configurar permissões personalizadas.

Este exemplo mostra como os usuários podem facilmente compartilhar um documento com alguém que está colaborando com outra empresa, mas ainda proteger o documento e ter certeza de que o destinatário possa lê-lo mesmo de um dispositivo móvel popular. Esse cenário usa o aplicativo de compartilhamento Rights Management, que pode ser automaticamente implantado em computadores com Windows em sua organização. Ou, os usuários podem instalá-lo sozinhos.

Neste exemplo, Alice da Contoso, envia email de um documento confidencial do Word para Bob, na Fabrikam. Ele lê o documento em seu iPad, mas poderia lê-lo facilmente em um iPhone, um tablet Android ou telefone, um computador Mac, um Windows phone ou computador.

![O QUE OS USUÁRIOS VEEM NA ETAPA 1](../media/AzRMS_StoryboardEmail_small1.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 1:** no seu PC com Windows, Alice cria uma mensagem de email padrão e anexa um documento.

Ela clica em **Compartilhamento protegido** na faixa de opções, que carrega a caixa de diálogo **compartilhamento protegido** no aplicativo de RMS sharing.

Alice quer restringir Bob à visualização e edição do documento, e não deseja que ele copie ou imprima; assim, ela seleciona **REVISOR - Ver e Editar**. Ela também quer receber um e-mail quando alguém tentar abrir o documento e tem a capacidade de revogar o documento mais tarde, se necessário e sabe que a revogação entrará em vigor imediatamente.

---

![O QUE OS USUÁRIOS VEEM NA ETAPA 2](../media/AzRMS_StoryboardEmail_small2.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 2:** Vinícius vê o email em seu iPad.

Além de mensagens e anexos de Alice, há instruções que ele segue para inscrever-se e instalar o aplicativo de compartilhamento do RMS no seu iPad.

---

![O QUE OS USUÁRIOS VEEM NA ETAPA 3](../media/AzRMS_StoryboardEmail_small3.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 3:** Vinícius agora pode abrir o anexo. Primeiro, é solicitado que efetue logon para confirmar que ele é o destinatário pretendido.

Quando Bob exibe o documento, ele também vê as informações de acesso restrito que informam que ele pode exibir e editar o documento, mas não copiar ou imprimir.

---

![O QUE OS USUÁRIOS VEEM NA ETAPA 4](../media/AzRMS_StoryboardEmail_small4.png)

**O QUE OS USUÁRIOS VEEM NA ETAPA 4:** Alice recebe uma mensagem de email informando que Vinícius abriu o documento que ela enviou com êxito e a data e hora em ele acessou o documento.

Se Bob encaminhar seu email com o anexo ou salvá-lo onde outros usuários possam acessá-lo ou isso será interceptado na rede, outras pessoas não poderão ler o documento.

---

**Mais informações sobre esse cenário:**

- Para saber mais, confira [Protect a file that you share by email (Proteger um arquivo que você compartilha por emai)l](../rms-client/sharing-app-protect-by-email.md) e [View and use files that have been protected (Exibir e usar arquivos que foram protegidos)](../rms-client/sharing-app-view-use-files.md) do [Rights Management sharing application user guide (Guia de usuário do aplicativo de compartilhamento Rights Management)](../rms-client/sharing-app-user-guide.md).

- O [Quick start tutorial for Azure Rights Management (Tutorial de início rápido para o Azure Rights Management)](../get-started/quick-start-tutorial.md) inclui instruções passo a passo para esse cenário.

## Próximas etapas

Agora você viu alguns exemplos do que o Azure RMS pode fazer, você pode estar interessado em saber como ele faz isso. Para obter informações técnicas sobre como funciona o Azure RMS, confira [How does Azure RMS work? (Como funciona o Azure RMS?)](how-does-it-work.md)


<!--HONumber=Jun16_HO2-->


