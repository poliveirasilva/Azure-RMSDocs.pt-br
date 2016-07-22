---
title: Perguntas mais frequentes sobre o Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 64b9cf141b755e4d54907424a7dcbd4ee14fadd7
ms.openlocfilehash: 758a603dde2c185767ba85229a397fd6e77b1c5b


---

# Perguntas mais frequentes sobre o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Algumas perguntas mais frequentes sobre o Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], também conhecido como Azure RMS:

## O que é necessário para implementar o Azure RMS e como posso começar a utilizá-lo?
Em primeiro lugar, consulte os [Requirements for Azure Rights Management (Requisitos do Azure Rights Management – em inglês)](requirements-azure-rms.md), que contêm informações sobre as opções de subscrição na nuvem, como pode utilizar os seus servidores no local com o Azure RMS, que cenários de implementação não são suportados atualmente, que dispositivos e aplicações suportam o Azure RMS e uma ligação se precisar de uma lista de endereços IP e nomes de domínio para firewalls ou servidores proxy. 

Também recomendamos que consulte os outros artigos na secção **Introdução**, bem como na secção **Compreender e Explorar**, para compreender como o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] pode ajudar a proteger os dados da sua organização, como funciona com aplicações, como se compara à versão no local do Active Directory Rights Management e compreender os termos e abreviaturas específicos do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

Em seguida, para avançar, utilize o [Plano de implementação do Azure Rights Management](../plan-design/deployment-roadmap.md).

## Os ficheiros têm de estar na nuvem para serem protegidos pelo Azure RMS?
Não, este é um equívoco comum. O serviço Azure Rights Management (e a Microsoft) não veem nem armazenam os seus dados como parte do processo de proteção das informações. As informações que protege nunca são enviadas para ou armazenadas no Azure, a menos que as armazene explicitamente no Azure ou utilize outro serviço em nuvem que as armazene no Azure. 

Para mais informações, consulte [How does Azure RMS work? (Como funciona o Azure RMS? Nos bastidores – em inglês)](../understand-explore/how-does-it-work.md) para compreender como uma fórmula de cola secreta criada e armazenada no local é protegida pelo Azure RMS mas permanece no local.

## Posso integrar o Azure RMS com os meus servidores no local?
Sim. O Azure RMS pode ser integrado com os seus servidores no local, como o Exchange Server, o SharePoint e servidores de ficheiros do Windows. Para tal, utilize o [conetor Rights Management](../deploy-use/deploy-rms-connector.md). Em alternativa, se estiver interessado em apenas utilizar a Infraestrutura de Classificação de Ficheiros (FCI) com o Windows Server, pode utilizar os [Cmdlets da Proteção RMS](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Também pode sincronizar e federar os seus controladores de domínio do Active Directory com o Azure AD para uma experiência de autenticação mais integrada para os utilizadores, por exemplo, ao utilizar o [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

O Azure RMS gera e faz a gestão dos certificados XrML automaticamente conforme necessário, pelo que não utiliza um PKI no local. Para mais informações sobre como o Azure RMS utiliza certificados, consulte a secção [Explicação passo a passo sobre como funciona o Azure RMS: primeira utilização, proteção de conteúdos, consumo de conteúdos](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) no artigo [Como funciona o Azure RMS?](../understand-explore/how-does-it-work.md).

## Onde posso encontrar informações sobre soluções de terceiros que se integram com o Azure RMS?

Vários fornecedores de software já têm soluções ou estão a implementar soluções que se integram com o Azure RMS — e a lista está a crescer muito rapidamente. Poderá considerar útil ler o [Blogue Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) e obter as atualizações mais recentes através de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) no Twitter. No entanto, se tiver uma questão específica, envie uma mensagem de e-mail à equipa de Proteção das Informações: askipteam@microsoft.com.

## Existe um pacote de gestão ou o mecanismo de monitorização semelhante para o conector de RMS?

Embora o conector do Rights Management registe mensagens de erro, aviso e informações no registo de eventos, não existe um pacote de gestão que inclua a monitorização destes eventos. No entanto, a lista de eventos e as suas descrições, com mais informações para ajudá-lo a aplicar as medidas corretivas está documentada em [Monitorizar o conector do Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## Tenho de ser um administrador global para configurar o Azure RMS ou posso delegar noutros administradores?

Os administradores globais de um inquilino do Office 365 ou inquilino do Azure AD podem obviamente executar todas as tarefas administrativas do Azure RMS. No entanto, se quiser atribuir permissões administrativas a outros utilizadores, pode fazê-lo utilizando o cmdlet do PowerShell do Azure RMS, [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx). Pode atribuir esta função administrativa por conta de utilizador ou por grupo. Existem duas funções disponíveis: **Administrador Global** e **Administrador do Conector**. 

Como estes nomes de função sugerem, a primeira função atribui permissões para executar todas as tarefas administrativas do Azure Rights Management (sem torná-los administrador global para outros serviços em nuvem) e a segunda função concede permissões para executar apenas o conector do Rights Management (RMS).

Factos a ter em conta:

- Apenas os administradores globais do Office 365 e os administradores globais do Azure AD podem utilizar os portais de gestão (centro de administração do Office 365 ou portal clássico do Azure) para configurarem o Azure RMS. Os utilizadores aos quais atribui a função de administrador global para o Azure RMS têm de utilizar os comandos do PowerShell do Azure RMS para configurarem o Azure RMS. Para ajudar a encontrar os cmdlets certos para tarefas específicas, consulte [Administrar o Azure Rights Management Utilizando o Windows PowerShell](../deploy-use/administer-powershell.md).

- Se tiver configurado [controlos de inclusão](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), isto não afeta a capacidade para administrar o Azure RMS, com exceção do conector do RMS. Por exemplo, se tiver configurado controlos de inclusão de para restringir a capacidade de proteger conteúdo ao grupo "Departamento de TI", a conta utilizada para instalar e configurar o conector do RMS tem de ser um membro desse grupo. 

- Nenhum administrador do Azure RMS (o administrador global do inquilino ou um administrador global do Azure RMS) pode remover automaticamente a proteção de documentos ou e-mails protegidos pelo Azure RMS. Apenas os utilizadores aos quais estão atribuídos superutilizadores para o Azure RMS podem fazê-lo, desde que a funcionalidade de superutilizador esteja ativada. No entanto, o administrador global do inquilino e qualquer administrador global do Azure RMS pode atribuir utilizadores como superutilizadores, incluindo a sua própria conta. Também pode ativar a funcionalidade de superutilizador. Estas ações são registadas no registo de administrador do Azure RMS. Para obter mais informações, consulte a secção de melhores práticas em [Configurar superutilizadores para o Azure Rights Management e serviços de deteção ou recuperação de dados](../deploy-use/configure-super-users.md). 


## Tenho uma implementação híbrida do Exchange com alguns utilizadores no Exchange Online e outros no Exchange Server. Isto é suportado pelo Azure RMS?
Absolutamente. Além disso, a vantagem é que os utilizadores poderão proteger e consumir de forma totalmente integrada e-mails e anexos protegidos nas duas implementações do Exchange. Para esta configuração, [ative o Azure RMS](../deploy-use/activate-service.md) e [ative a IRM para o Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx) e, em seguida, [implemente e configure o conetor RMS](../deploy-use/deploy-rms-connector.md) para o Exchange Server.

## Existem instruções passo a passo para configurar o Exchange Online para utilizar o Azure RMS?

Sim. Consulte [Exchange Online: configuração da IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) para ver um conjunto de comandos típico que permite ao Exchange Online utilizar o Azure RMS, por que motivo o Outlook Web App não mostra imediatamente as opções do menu **Definir permissões** e o comando a executar se alterar ou atualizar os modelos do Azure RMS. 

## Se implementar o Azure RMS em produção, a minha empresa fica presa a essa solução ou arrisca-se a perder o acesso aos conteúdos que protegemos com o Azure RMS?
Não, permanece sempre no controlo dos seus dados e pode continuar a aceder aos mesmos, mesmo se optar por deixar de utilizar o Azure RMS. Para mais informações, consulte [Desativar o Azure Rights Management](../deploy-use/decommission-deactivate.md).

No entanto, antes de desativar a implementação do Azure RMS, gostaríamos de ouvir o seu feedback e compreender por que motivo tomou esta decisão. Se o Azure RMS não satisfazer os seus requisitos empresariais, contacte-nos no caso de estarmos a planear novas funcionalidades para um futuro próximo ou no caso de existirem alternativas. Envie uma mensagem de e-mail para [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) e teremos todo o gosto em debater os seus requisitos técnicos e empresariais.

## Posso controlar que utilizadores podem aceder ao Azure RMS para proteger o conteúdo?
Sim, o Azure RMS tem controlos de inclusão do utilizador para este cenário. Para mais informações, consulte a secção [Configuring onboarding controls for a phased deployment (Configurar os controlos de inclusão para uma implementação faseada – em inglês)](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) no artigo [Activating Azure Rights Management (Ativar o Azure Rights Management – em inglês)](../deploy-use/activate-service.md).

## Posso impedir que os utilizadores partilhem documentos protegidos com organizações específicas?
Uma das grandes vantagens do Azure RMS é que suporta a colaboração entre empresas sem ter de configurar confianças explícitas para cada organização parceira, porque o Azure AD processa a autenticação automaticamente.

Não existe uma opção de administração para impedir que os utilizadores partilhem documentos de forma segura com organizações específicas. Por exemplo, imagine que pretende bloquear uma organização na qual não confia ou que tem uma empresa concorrente. Não faria sentido impedir o Azure RMS de enviar documentos protegidos aos utilizadores nessas organizações, porque os seus utilizadores iriam partilhar os seus documentos desprotegidos, que é provavelmente a última coisa que quer que aconteça neste cenário! Por exemplo, não poderia identificar quem está a partilhar documentos confidenciais da empresa com os utilizadores nessas organizações, o que pode fazer quando o documento (ou e-mail) é protegido pelo Azure RMS.

## Quando partilho um documento protegido com alguém fora da minha empresa, como é que esse utilizador é autenticado?
O Azure RMS utiliza sempre uma conta do Azure Active Directory e um endereço de e-mail associado para a autenticação do utilizador, o que torna a colaboração entre empresas totalmente integrada para os administradores. Se a outra organização utilizar serviços do Azure, os utilizadores já terão contas no Azure Active Directory, mesmo que estas contas tenham sido criadas e geridas no local e, em seguida, sincronizadas com o Azure. Se a organização tiver o Office 365, nos bastidores, este serviço também utiliza o Azure Active Directory para as contas de utilizador. Se a organização do utilizador não tiver contas geridas no Azure, os utilizadores podem inscrever-se no [RMS para indivíduos](../understand-explore/rms-for-individuals.md), que cria um diretório e um inquilino do Azure não gerido para a organização com uma conta para o utilizador, para que este utilizador (e utilizadores subsequentes) possa ser autenticado para o Azure RMS.

O método de autenticação para estas contas pode variar, dependendo da forma como o administrador na outra organização configurou as contas do Azure Active Directory. Por exemplo, podem utilizar palavras-passe que foram criadas para estas contas, autenticação multifator (MFA), federação ou palavras-passe que foram criadas nos Serviços de Domínio do Active Directory e, em seguida, sincronizadas com o Azure Active Directory.

## Posso adicionar utilizadores externos à minha empresa aos modelos personalizados?
Sim. Criar modelos personalizados que os utilizadores finais (e os administradores) podem selecionar a partir de aplicações torna mais rápido e fácil aplicar a proteção de informações, com políticas predefinidas especificadas por si. Uma das definições no modelo é quem pode aceder aos conteúdos. Pode especificar os utilizadores e os grupos da sua organização e os utilizadores externos à sua organização.

Para especificar os utilizadores a partir de fora da sua organização, adicioná-los como contactos a um grupo que selecionou no portal clássico do Azure quando configurar os seus modelos. Ou utilize o [Módulo Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md):

-   **Utilize um objeto de definição de direitos para criar ou atualizar um modelo**.    Especifique os endereços de e-mail externos e os seus direitos num objeto de definição de direitos, que utilizará para criar ou atualizar um modelo. Especifique o objeto de definição de direitos com o cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para criar uma variável e, em seguida, fornecer esta variável ao parâmetro -RightsDefinition com o cmdlet [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (para um novo modelo) ou o cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (se estiver a modificar um modelo existente). No entanto, se estiver a adicionar estes utilizadores a um modelo existente, terá de definir os objetos de definição de direitos para os grupos existentes nos modelos e não apenas os utilizadores externos.

Para mais informações sobre modelos personalizados, consulte [Configurar modelos personalizados para o Azure Rights Management](../deploy-use/configure-custom-templates.md).

## O Azure RMS funciona com grupos dinâmicos no Azure AD?
Uma funcionalidade do Azure AD Premium permite-lhe configurar a associação dinâmica para grupos ao especificar [regras baseadas em atributos](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quando cria um grupo de segurança no Azure AD, este tipo de grupo suporta a associação dinâmica mas não suporta um endereço de e-mail e, por isso, não pode ser utilizado com o Azure RMS. No entanto, agora pode criar um novo tipo de grupo no Azure AD que suporte a associação dinâmica e tenha capacidade de correio. Quando adiciona um novo grupo no portal clássico do Azure, pode escolher o **TIPO DE GRUPO** do **Office 365 "Preview"**. Como este grupo tem capacidade de correio, pode utilizá-lo com o Azure RMS.

Como a opção de nome mostra claramente, este novo tipo de grupo ainda está no modo de pré-visualização e esperam-se funcionalidades adicionais e nova documentação. Entretanto, queremos confirmar que pode utilizar este novo tipo de grupo com o Azure RMS.


## Que dispositivos e que tipos de ficheiro são suportados pelo Azure RMS?
Para obter uma lista dos dispositivos suportados, consulte [Dispositivos cliente que suportam o Azure RMS](../get-started/requirements-client-devices.md). Uma vez que nem todos os dispositivos suportados conseguem atualmente suportar todas as funcionalidades de RMS, certifique-se de que também consulta a tabela [Requisitos do Azure RMS: Aplicações](../get-started/requirements-applications.md).

O Azure RMS suporta todos os tipos de ficheiro. Para texto, imagem, ficheiros do Microsoft Office (Word, Excel, PowerPoint), ficheiros .pdf e outros tipos de ficheiro de aplicação, o Azure RMS fornece proteção nativa que inclui encriptação e imposição dos direitos (permissões). Para todas as outras aplicações e tipos de ficheiro, a proteção genérica fornece autenticação e encapsulamento de ficheiro para verificar se um utilizador tem autorização para abrir o ficheiro.

Para obter uma lista de extensões de nome de ficheiro que são suportadas nativamente pelo Azure RMS, consulte a secção [Supported file types and file name extensions (Tipos de ficheiro e extensões de nome de ficheiro suportados – em inglês)](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) do [Rights Management sharing application administrator guide (Guia do administrador da aplicação de partilha Rights Management – em inglês)](../rms-client/sharing-app-admin-guide.md). As extensões de nome de ficheiro que não estiverem indicadas são suportadas com a aplicação de partilha RMS que aplica automaticamente proteção genérica a estes ficheiros.

## Quando abro um documento do Office protegido por RMS, o ficheiro temporário associado também fica protegido por RMS?

Não. Neste cenário, o ficheiro temporário associado não contém dados do documento original, mas apenas o que o utilizador introduz enquanto o ficheiro está aberto. Ao contrário do ficheiro original, o ficheiro temporário não foi concebido para partilha e permaneceria no dispositivo, protegido por controlos de segurança locais, como o BitLocker e o EFS.

## Quando irão suportar a migração a partir do AD RMS?
Inicialmente, o Azure RMS não suportava a migração a partir de uma implementação no local do Rights Management, como o AD RMS. Agora já suporta.

Para mais informações, consulte [Migrar do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## Queremos utilizar o BYOK (Bring Your Own Key – Traga a Sua Própria Chave) com o Azure RMS, mas descobrimos que não é compatível com o Exchange Online. O que aconselham?
Não permita que esta limitação atual atrase a sua implementação do Azure RMS. Se tiver o Exchange Online e quiser utilizar o BYOK (Bring Your Own Key – Traga a Sua Própria Chave), recomendamos que implemente agora o Azure RMS no modo de gestão de chaves predefinido, em que a Microsoft gera e faz a gestão da sua chave. Dessa forma, obtém todas as vantagens de proteger os seus ficheiros e e-mails importantes, com a opção de mudar para o BYOK mais tarde (por exemplo, quando o Exchange Online suporta o BYOK).

No entanto, se as políticas da sua empresa exigirem que utilize um módulo de hardware de segurança (HSM) e isto bloquear a sua implementação do Azure RMS, outra opção é implementar o Azure RMS com o BYOK agora, com funcionalidade de RMS reduzida para o Exchange. Para mais informações, consulte [Preços e restrições do BYOK](../plan-design/byok-price-restrictions.md) em [Planear e implementar a sua chave de inquilino do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## A funcionalidade que procuro não funciona com bibliotecas protegidas do SharePoint. Planeiam oferecer suporte para a minha funcionalidade?
Atualmente, o SharePoint suporta documentos protegidos do RMS com bibliotecas protegidas da IRM, que não suportam modelos personalizados, controlo de documentos e outras funcionalidades. Para mais informações, consulte a secção [SharePoint Online e SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) no artigo [Office applications and services (Aplicações e serviços do Office – em inglês)](../understand-explore/office-apps-services-support.md).

Se estiver interessado numa funcionalidade específica que ainda não é suportada, certifique-se de que fica atento aos anúncios no [Blogue do Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## Como posso configurar o OneDrive para Empresas no SharePoint Online, para que os utilizadores possam partilhar os seus ficheiros de forma segura com pessoas dentro e fora da empresa?
Por predefinição, enquanto administrador do Office 365, não lhe cabe a si configurar isto, mas sim aos utilizadores.

Tal como um administrador do site do SharePoint ativa e configura a IRM para uma biblioteca do SharePoint que possui, o OneDrive para Empresas é concebido para os utilizadores ativarem e configurarem a IRM para as suas próprias bibliotecas do OneDrive para Empresas.  No entanto, com o PowerShell, pode fazê-lo pelos utilizadores. Para obter instruções, consulte a secção [SharePoint Online and OneDrive for Business: IRM Configuration (SharePoint Online e OneDrive para Empresas: configuração de IRM – em inglês)](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) no artigo [Office 365: Configuration for clients and online services (Office 365: configuração para clientes e serviços online – em inglês)](../deploy-use/configure-office365.md).

## Tem sugestões ou truques para uma implementação do RMS com êxito?
Após supervisionar várias implementações e ouvir os nossos clientes, parceiros, consultores e engenheiros de suporte – uma das maiores sugestões que podemos transmitir da nossa experiência: **Crie e implemente políticas de direitos simples**.

Como o Azure RMS suporta a partilha segura com todas as pessoas, pode ser ambicioso com o alcance da proteção das suas informações. No entanto, seja conservador com as suas políticas de direitos. Para muitas organizações, o maior impacto comercial provém de impedir a fuga de dados ao aplicar o modelo de política de direitos predefinido que restringe o acesso a pessoas na sua organização. Claro que, se for necessário, pode ser muito mais granular e impedir que as pessoas imprimam, editem, etc. No entanto, as restrições mais granulares devem ser a exceção, para documentos que precisam de um alto nível de segurança. Não implemente estas políticas mais restritas no primeiro dia, mas planeie uma abordagem mais faseada.

## Que funcionalidades podem ou não ser utilizadas com as diferentes subscrições do Azure RMS?
Para as subscrições pagas que suportam o Azure RMS (Office 365, Azure RMS Premium e Enterprise Mobility Suite), existem algumas diferenças nas funcionalidades do RMS que são suportadas. Para obter uma lista, consulte [Comparação de Ofertas de Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

A subscrição gratuita que suporta o Azure RMS (RMS para utilizadores autónomos) suporta o consumo de conteúdos protegidos pelo Azure RMS. Para mais informações, consulte [RMS para indivíduos e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## Onde posso obter informações técnicas sobre a subscrição gratuita do Azure RMS (RMS para utilizadores autónomos), por exemplo, como funciona realmente, como assumir o controlo das contas e que domínios não podem ser utilizados?
Encontrará as respostas a estas perguntas em [RMS for individuals and Azure Rights Management (RMS para utilizadores autónomos e Azure Rights Management – em inglês)](../understand-explore/rms-for-individuals.md) e artigos relacionados.

## Como recuperamos o acesso a ficheiros que foram protegidos por um funcionário que saiu da organização?
Utilize a funcionalidade de superutilizador do Azure RMS, que permite que os utilizadores autorizados tenham direitos de proprietário totais para todas as licenças de utilização que foram concedidas pelo inquilino do RMS da sua organização. Esta mesma funcionalidade permite que os serviços autorizados indexem e inspecionem ficheiros, conforme necessário.

Para mais informações, consulte [Configurar superutilizadores para o Azure Rights Management e serviços de deteção ou recuperação de dados](../deploy-use/configure-super-users.md).

## O Rights Management pode impedir capturas de ecrã?
Ao não conceder direitos de **cópia**[utilização](../deploy-use/configure-usage-rights.md), o Rights Management pode impedir capturas de ecrãs de muitas das ferramentas de captura de ecrã utilizadas normalmente em plataformas com Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) e Android. No entanto, os dispositivos iOS e Mac não permitem que as aplicações impeçam capturas de ecrã e os browsers (por exemplo, quando são utilizados com o Outlook Web App e o Office Online) também não podem impedir capturas de ecrã.

Impedir capturas de ecrã pode ajudar a evitar a divulgação por acidente ou por negligência de informações confidenciais. No entanto, existem várias formas de um utilizador partilhar os dados apresentados num ecrã e tirar uma captura de ecrã é apenas um dos métodos possíveis. Por exemplo, um utilizador que esteja determinado em partilhar as informações apresentadas pode tirar uma fotografia com a câmara do telemóvel, reescrever os dados ou simplesmente dizê-las a alguém.

Conforme estes exemplos demonstram, mesmo que todas as plataformas e todos os softwares suportassem as APIs do Rights Management para bloquear as capturas de ecrã, a tecnologia por si só nem sempre pode impedir os utilizadores de partilharem dados que não deviam. O Rights Management pode ajudar a salvaguardar os seus dados importantes com políticas de utilização e autorização, mas esta solução de gestão de direitos de empresa deve ser utilizada em conjunto com outros controlos. Por exemplo, implementar segurança física, monitorizar cuidadosamente as pessoas que têm acesso autorizado aos dados da sua organização e investir na educação do utilizadores para que estes compreendam que os dados não devem ser partilhados.

## Qual a diferença entre um utilizador que protege um e-mail com Não Reencaminhar e um modelo que não inclui o direito de Reencaminhar?

Apesar do nome e do aspeto, **Não Reencaminhar** não é o oposto do direito de Reencaminhar nem um modelo. Na realidade, é um conjunto de direitos que incluem restringir a cópia, impressão e gravação de anexos, para além de restringir o reencaminhamento de e-mails. Os direitos são aplicados dinamicamente aos utilizadores através de destinatários escolhidos e não estaticamente atribuídos pelo administrador. Para obter mais informações, consulte a secção [Opção Não Reencaminhar para e-mails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) em [Configurar os direitos de utilização do Azure Rights Management](../deploy-use/configure-usage-rights.md).

## Onde posso encontrar informações de suporte para o Azure RMS, como informações legais, sobre conformidade e SLAs?
O Azure RMS suporta outros serviços e também depende de outros serviços. Se estiver à procura de informações relacionadas com o Azure RMS mas não sobre como utilizar o serviço Azure RMS, consulte os seguintes recursos:

**Informações legais e privacidade:**

-   Para obter informações sobre o contrato do Microsoft Azure: [Contrato do Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Para obter informações sobre a privacidade do Microsoft Azure: [Declaração de Privacidade do Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Segurança, conformidade e auditoria:**

Consulte a secção [Requisitos de segurança, conformidade e regulamentação](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) no artigo [Que problemas resolve o Azure RMS?](../understand-explore/azure-rms-problems-it-solves.md). Além disso:

-   Para obter certificados externos para o Azure RMS: [Centro de Fidedignidade do Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

-   Para obter informações sobre a norma FIPS 140: [FIPS 140 Validation (Validação da Norma FIPS 140 – em inglês)](https://technet.microsoft.com/library/security/cc750357.aspx)

**Contratos de nível de serviço:**

-   Contrato de nível de serviço para o Azure RMS, por região selecionada: [Transferir a partir da página Pesquisa de Licenciamento de Produtos](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - Por exemplo, clique em **OnlineSvcsConsolidatedSLA(WW)(inglês)(março de2016)** para transferir o contrato de nível de serviço de março de 2016 da América do Norte.

-   Contrato de nível de serviço para o Azure Active Directory: [Contratos de Nível de Serviço](http://azure.microsoft.com/support/legal/sla/)

**Documentação:**

-   Site de Documentação do Azure Active Directory: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Biblioteca do Azure Active Directory: [Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Biblioteca do Office 365: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Já ouvi falar numa nova versão vai estar disponível em breve para o Azure RMS — quando será lançada?

A documentação técnica não contêm informações sobre os lançamentos futuros. Para obter este tipo de informação e ter acesso aos anúncios de lançamento, leia o [Blogue Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) e obter as atualizações mais recentes através de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) no Twitter. Se estiver interessado numa versão do Office, consulte também o [blogue do Office [(https://blogs.office.com/).

## O que posso fazer se a minha pergunta não estiver aqui?
Utilize as ligações e os recursos indicados em [Informações e suporte para o Azure Rights Management](information-support.md).

Além disso, existem FAQs criadas para utilizadores finais:

-   [FAQ for Rights Management Sharing Application for Windows (FAQ acerca da Aplicação de Partilha Rights Management para Windows – em inglês)](https://technet.microsoft.com/dn467883)

-   [FAQ for Rights Management Sharing Application for Mobile and Mac Platforms (FAQ acerca da Aplicação de Partilha Rights Management para Plataformas Móveis e Mac – em inglês)](https://technet.microsoft.com/dn451248)

-   [FAQ for Document Tracking (FAQ acerca do Controlo de Documentos – em inglês)](http://go.microsoft.com/fwlink/?LinkId=523977)

Esta página de FAQ será atualizada regularmente, com novas adições indicadas nos anúncios de atualização de documentação mensal no [Blogue do Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).





<!--HONumber=Jun16_HO5-->


