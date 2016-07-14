---
title: Perguntas frequentes sobre o Azure Rights Management | Azure RMS
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
ms.sourcegitcommit: b73c83b91a6b00e44ff6c8fe7f8e954bd9713e34
ms.openlocfilehash: a3ed9e8de496741fae8904481edb1177762a12c0


---

# Perguntas frequentes sobre o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Algumas perguntas frequentes sobre o Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], também conhecido como Azure RMS:

## O que eu preciso para implantar o Azure RMS e como faço para prosseguir?
Primeiro, verifique os [Requisitos do Azure Rights Management](requirements-azure-rms.md), que tem informações sobre as opções de assinatura da nuvem, como você pode usar seus servidores locais com o Azure RMS, quais cenários de implantação não têm suporte atualmente, quais dispositivos e aplicativos dão suporte ao Azure RMS, e um link caso você necessite de uma lista de endereços IP e de nomes de domínio para firewalls ou para servidores de proxy. 

Verifique também os outros artigos na seção de **Introdução**, além da seção **Entender e explorar**, para obter um entendimento básico de como o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] pode ajudar a proteger os dados da organização, como ele funciona com aplicativos, como se compara à versão local do Active Directory Rights Management e compreender os termos e as abreviações específicos do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

Em seguida, para continuar, use o [roteiro de implantação do Azure Rights Management](../plan-design/deployment-roadmap.md).

## Os arquivos precisam estar na nuvem para serem protegidos pelo Azure RMS?
Não, isso é um equívoco comum. O serviço do Azure Rights Management (e a Microsoft) não vê nem armazena seus dados como parte do processo de proteção de informações. As informações que você protege nunca são enviadas ou armazenadas no Azure, a menos que as armazene explicitamente no Azure ou utilize outro serviço de nuvem que as armazene no Azure. 

Para saber mais, veja [Como funciona o Azure RMS? Nos bastidores](../understand-explore/how-does-it-work.md), para entender como uma fórmula de cola secreta criada e armazenada localmente é protegida pelo Azure RMS, mas permanece sendo local.

## Posso integrar o Azure RMS com meus servidores locais?
Sim. O Azure RMS pode ser integrado com seus servidores locais, como servidores de arquivos do Exchange Server, SharePoint e Windows. Para fazer isso, use o [conector do Rights Management](../deploy-use/deploy-rms-connector.md). Ou, se você estiver interessado apenas em usar a FCI (Infraestrutura de Classificação de Arquivos) com o Windows Server, você poderá usar os [cmdlets de Proteção do RMS](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). Você também pode sincronizar e federar seus controladores de domínio do Active Directory com o Azure AD para uma experiência de autenticação mais transparente para os usuários, por exemplo, usando o [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

O Azure RMS gera e gerencia automaticamente certificados XrML, conforme necessário, para que ele não use uma PKI local. Para saber mais sobre como o Azure RMS usa certificados, veja a seção [Passo a passo de como funciona o Azure RMS: primeiro uso, proteção de conteúdo, consumo de conteúdo](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) no artigo [Como funciona o Azure RMS?](../understand-explore/how-does-it-work.md)

## Onde posso encontrar informações sobre soluções de terceiros que se integram ao Azure RMS?

Muitos fornecedores de software já têm soluções ou estão implementando soluções que se integram ao Azure RMS — e a lista continua crescendo rapidamente. Talvez seja útil para verificar o [Blog de segurança e mobilidade corporativa](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) e obter as atualizações mais recentes de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) no Twitter. No entanto, se você tiver uma pergunta específica, envie uma mensagem de email para a equipe de proteção de informações: askipteam@microsoft.com.

## Há um pacote de gerenciamento ou mecanismo de monitoramento semelhante para o conector RMS?

Embora o conector do Rights Management registre informações, avisos e mensagens de erro no log de eventos, não há um pacote de gerenciamento que inclui monitoramento para esses eventos. No entanto, a lista de eventos e suas descrições, com mais informações para ajudá-lo a tomar uma medida corretiva é documentada em [Monitorar o conector do Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## Você precisa ser um administrador global para configurar o Azure RMS ou eu posso delegar a outros administradores?

Os administradores globais de um locatário do Office 365 ou locatário do Azure AD, obviamente, podem executar todas as tarefas administrativas do Azure RMS. No entanto, se você deseja atribuir permissões administrativas a outros usuários, você pode fazer isso usando o cmdlet do PowerShell do Azure RMS, [Add- AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx). Você pode atribuir essa função administrativa por conta de usuário ou por grupo. Há duas funções disponíveis: **Administrador global** e **Administrador do conector**. 

Como esses nomes de função sugerem, a primeira função concede permissões para executar todas as tarefas administrativas do Azure Rights Management (sem torná-los um administrador global para outros serviços de nuvem) e a segunda concede permissões para executar apenas o conector do Rights Management (RMS).

Algumas coisas a serem observadas:

- Somente os administradores globais do Office 365 e administradores globais do Azure AD podem usar os portais de gerenciamento (Centro de administração do Office 365 ou portal clássico do Azure) para configurar o Azure RMS. Os usuários aos quais você atribui a função de administrador global do Azure RMS devem usar comandos do PowerShell do Azure RMS para configurar o Azure RMS. Para ajudá-lo a localizar os cmdlets certos para tarefas específicas, consulte [Administrando o Azure Rights Management usando o Windows PowerShell](../deploy-use/administer-powershell.md).

- Se você tiver configurado [controles de integração](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), isso não afetará a capacidade de administrar o Azure RMS, exceto o conector RMS. Por exemplo, se você tiver configurado os controles de integração de modo que a capacidade de proteger o conteúdo fique restrita ao grupo "Departamento de TI", a conta que você usa para instalar e configurar o conector RMS deverá ser um membro desse grupo. 

- Nenhum administrador do Azure RMS (administrador global do locatário ou um administrador global do Azure RMS) pode remover automaticamente a proteção de documentos ou emails que foram protegidos pelo Azure RMS. Somente os usuários que receberam os superusuários do Azure RMS podem fazer isso e quando o recurso de superusuário estiver habilitado. No entanto, o administrador global do locatário e qualquer administrador global do Azure RMS podem atribuir usuários como superusuários, incluindo sua própria conta. Eles também podem habilitar o recurso de superusuário. Essas ações são registradas no log do administrador do Azure RMS. Para mais informações, consulte a seção de práticas recomendadas de segurança [Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou a recuperação de dados](../deploy-use/configure-super-users.md). 


## Eu tenho uma implantação híbrida do Exchange com alguns usuários no Exchange Online e com outros no Exchange Server — isto é compatível com o Azure RMS?
Com certeza, e o melhor é que os usuários serão capazes de proteger e consumir emails e anexos protegidos entre as duas implantações do Exchange. Para essa configuração, [ative o Azure RMS](../deploy-use/activate-service.md) e [habilite o IRM para o Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)e, em seguida, [implante e configure o conector RMS](../deploy-use/deploy-rms-connector.md) para o Exchange Server.

## Há instruções passo a passo para configurar o Exchange Online para usar o Azure RMS?

Sim. Consulte [Exchange Online: configuração de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) para ver um conjunto típico de comandos que permite que o Exchange Online use o Azure RMS, o motivo pelo qual o Outlook Web App não mostra imediatamente as opções de menu para **Definir permissões** e também o comando a ser executado se você alterar ou atualizar os modelos do Azure RMS. 

## Se eu implantar o Azure RMS em produção, a minha empresa fica então "bloqueada" na solução ou corre o risco de perder o acesso ao conteúdo que protegemos com o Azure RMS?
Não, você sempre permanece no controle de seus dados e pode continuar a acessá-los, mesmo se decidir não usar o Azure RMS. Para saber mais, veja [Encerramento e desativação do Azure Rights Management](../deploy-use/decommission-deactivate.md).

No entanto, antes de encerrar sua implantação do Azure RMS, gostaríamos de ouvi-lo para compreender por que tomou esta decisão. Se o Azure RMS não atender aos seus requisitos de negócios, verifique conosco se uma nova funcionalidade está planejada para um futuro próximo ou se existem alternativas. Envie um email para [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) e teremos todo o gosto em analisar seus requisitos técnicos e comerciais.

## É possível controlar quais dos meus usuários podem usar o Azure RMS para proteger o conteúdo?
Sim, o Azure RMS possui controles de integração do usuário para esse cenário. Para saber mais, veja a seção [Configuração de controles de integração para uma implantação em fases](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) no artigo [Ativação do Azure Rights Management](../deploy-use/activate-service.md).

## Posso impedir os usuários de compartilharem documentos protegidos com organizações específicas?
Um dos maiores benefícios do Azure RMS é que ele oferece suporte para colaboração de empresas sem precisar configurar confianças explícitas para cada organização parceira, pois o Azure AD cuida da autenticação para você.

Não há nenhuma opção de administração para impedir que os usuários compartilhem com segurança os documentos com organizações específicas. Por exemplo, você deseja bloquear uma organização que não confia ou que tenha uma empresa concorrente. Impedir que o Azure RMS envie documentos protegidos aos usuários dessas organizações não faz sentido, pois os usuários podem compartilhar seus documentos desprotegidos, o que é, provavelmente, a última coisa que você quer fazer neste cenário! Por exemplo, você não será capaz de identificar quem está compartilhando documentos confidenciais da empresa com os usuários dessas organizações, que pode ser feito quando o documento (ou email) for protegido pelo Azure RMS.

## Ao compartilhar um documento protegido com alguém fora da minha empresa, como o usuário é autenticado?
O Azure RMS sempre usa uma conta do Active Directory do Azure e um endereço de email associado para autenticação de usuário, o que torna a colaboração entre empresas perfeita para administradores. Se a outra organização usar os serviços do Azure, os usuários já terão contas no Active Directory do Azure, mesmo que essas contas sejam criadas e gerenciadas no local e, em seguida, sincronizadas no Azure. Se a organização tiver o Office 365, em segundo plano, esse serviço também usa o Active Directory do Azure para as contas de usuário. Se a organização não tiver contas gerenciadas no Azure, os usuários poderão se inscrever no [RMS para pessoas físicas](../understand-explore/rms-for-individuals.md), que cria um locatário do Azure não gerenciado e um diretório para a organização com uma conta de usuário, de forma que este usuário (e usuários subsequentes) possa ser autenticado no Azure RMS.

O método de autenticação para essas contas pode variar, dependendo de como o administrador na outra organização configurou as contas do Active Directory do Azure. Por exemplo, seria possível usar senhas que foram criadas para essas contas, Multi-Factor Authentication (MFA), federação ou senhas que foram criadas nos serviços de domínio do Active Directory e, em seguida, sincronizadas com o Active Directory do Azure.

## Posso adicionar usuários de fora da minha empresa aos modelos personalizados?
Sim. Ao criar modelos personalizados, onde os usuários finais (e os administradores) possam selecionar aplicativos, a aplicação de proteção de informações usando políticas predefinidas que você especifica torna-se um processo rápido e fácil. Uma das configurações no modelo é a de quem está autorizado a acessar o conteúdo, e você pode especificar usuários e grupos da sua organização e usuários fora da sua organização.

Para especificar usuários fora da sua organização, adicione-os como contatos a um grupo que você seleciona no portal clássico do Azure ao configurar seus modelos. Ou use o [Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md):

-   **Use um objeto de definição de direitos para criar ou atualizar um modelo**.    Especifique os endereços de email externos e seus direitos em um objeto de definição de direitos que você usará para criar ou atualizar um modelo. É possível especificar o objeto de definição de direitos usando o cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para criar uma variável e, em seguida, fornecer essa variável ao parâmetro -RightsDefinition com o cmdlet [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (para um novo modelo) ou o cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (se você estiver modificando um modelo existente). No entanto, se você está adicionando esses usuários a um modelo existente, precisará definir objetos de definição de direitos para os grupos existentes nos modelos e não apenas os usuários externos.

Para saber mais sobre modelos personalizados, veja [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

## O Azure RMS funciona com grupos dinâmicos no Azure AD?
Um recurso do Azure AD Premium permite que você configure a associação dinâmica de grupos especificando [regras baseadas em atributo](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quando você cria um grupo de segurança no Azure AD, esse tipo de grupo dá suporte à associação dinâmica, mas não oferece suporte a um endereço de email e, portanto, não pode ser usado com o Azure RMS. No entanto, agora você pode criar um novo tipo de grupo no Azure AD que dá suporte à associação dinâmica e é habilitado para email. Quando você adiciona um novo grupo no portal clássico do Azure, você pode escolher o **TIPO DE GRUPO** do **Office 365 "Visualização"**. Como esse grupo é habilitado para email, você pode usá-lo com o Azure RMS.

Como mostra claramente o nome da opção, esse novo tipo de grupo ainda está em visualização, e há a expectativa por outras funcionalidades e uma nova documentação. Enquanto isso, queremos confirmar que você pode usar esse novo tipo de grupo com o Azure RMS.


## A quais dispositivos e tipos de arquivos o Azure RMS oferece suporte?
Para obter uma lista de dispositivos com suporte, consulte [Requisitos do Azure RMS: dispositivos cliente com suporte para Azure RMS](../get-started/requirements-client-devices.md). Como nem todos os dispositivos com suporte podem atualmente dar suporte a todos os recursos RMS, verifique também a tabela [Requisitos do Azure RMS: aplicativos](../get-started/requirements-applications.md).

O Azure RMS oferece suporte a todos os tipos de arquivo. Para arquivos de texto, imagem, do Microsoft Office (Word, Excel, PowerPoint), .pdf e para tipos de arquivo de alguns outros aplicativos, o Azure RMS oferece proteção nativa que inclui criptografia e aplicação de direitos (permissões). Para todos os outros aplicativos e tipos de arquivo, a proteção genérica oferece encapsulamento de arquivos e autenticação para verificar se um usuário está autorizado a abrir o arquivo.

Para obter uma lista de extensões de nomes de arquivos que com suporte nativo pelo Azure RMS, veja a seção [Tipos de arquivos e extensões de nome de arquivos com suporte](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) no [guia de administrador do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-admin-guide.md). As extensões de nome de arquivo não listadas têm suporte através do uso do aplicativo de compartilhamento RMS, que automaticamente aplica a proteção genérica a esses arquivos.

## Ao abrir um documento do Office protegido pelo RMS, o arquivo temporário associado também ficará protegido pelo RMS?

Não. Nesse cenário, o arquivo temporário associado não contém dados do documento original, mas apenas o que o usuário insere enquanto o arquivo está aberto. Ao contrário do arquivo original, o arquivo temporário, obviamente, não se destina a compartilhamento e permanecerá no dispositivo, protegido por controles de segurança locais, como BitLocker e EFS.

## Quando você oferecerá suporte a migração do AD RMS?
Inicialmente, o Azure RMS não oferece suporte à migração de uma implantação local do Rights Management, como o AD RMS. Mas agora há suporte.

Para saber mais, confira [Migração do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## Nós desejamos muito usar o BYOK com o Azure RMS, mas sabemos que isso não é compatível com o Exchange Online. O que vocês sugerem?
Não deixe que essa limitação atual atrase a sua implantação do Azure RMS. Se você possui o Exchange Online e deseja usar sua própria chave (BYOK), recomenda-se implantar o Azure RMS no modo padrão de gerenciamento de chaves agora, em que a Microsoft gera e gerencia sua chave. Dessa forma, você obtém todos os benefícios de proteger seus arquivos importantes e emails agora, com a opção de mudar para BYOK posteriormente (por exemplo, quando o Exchange Online oferecer suporte a BYOK).

No entanto, se as políticas de sua empresa exigem que você use um módulo de segurança de hardware (HSM), o que bloquearia a implantação do Azure RMS, outra opção será implantar o Azure RMS com BYOK agora, com funcionalidade reduzida do RMS para o Exchange. Para saber mais, confira [Preços e restrições de BYOK](../plan-design/byok-price-restrictions.md) de [Planejamento e implementação de sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Um recurso que estou procurando não parece funcionar com as bibliotecas protegidas do SharePoint — o suporte para meu recurso está planejado?
Atualmente, o SharePoint oferece suporte aos documentos protegidos por RMS usando as bibliotecas protegidas por IRM que não oferecem suporte a modelos personalizados, rastreamento de documentos e outros recursos. Para saber mais, confira a seção [SharePoint Online e SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) no artigo [Serviços e aplicativos do Office](../understand-explore/office-apps-services-support.md).

Se você estiver interessado em uma funcionalidade específica que ainda não tem suporte, fique atento aos anúncios no [blog de Segurança e Mobilidade Corporativa](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## Como configurar o OneDrive for Business no SharePoint Online para que os usuários possam compartilhar com segurança seus arquivos com pessoas dentro e fora da empresa?
Por padrão, como um administrador do Ofice 365, você não configura isto, os usuários o fazem.

Da mesma forma que o administrador de site do SharePoint habilita e configura o IRM para uma biblioteca do SharePoint que ele tem, o OneDrive for Business é criado para os usuários habilitarem e configurarem o IRM para sua própria biblioteca do OneDrive for Business.  No entanto, usando o PowerShell, você pode fazer isso por eles. Para obter instruções, veja a seção [SharePoint Online e OneDrive for Business: configuração de IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) no artigo [Office 365: configuração de clientes e serviços online](../deploy-use/configure-office365.md).

## Você tem alguma dica ou truque para uma implantação bem-sucedida do RMS?
Após supervisionar muitas implantações e ouvir nossos clientes, parceiros, consultores e engenheiros de suporte – uma das maiores dicas que podemos passar por experiência: **Projetar e implantar políticas de direitos simples**.

Como o Azure RMS oferece suporte ao compartilhamento seguro com qualquer um, você pode se dar ao luxo de ser ambicioso com o alcance da sua proteção de informações. Mas seja conservador com suas políticas de direitos. Para muitas organizações, o maior impacto nos negócios vem da prevenção de vazamento de dados aplicando-se o modelo de política de direitos padrão que restringe o acesso às pessoas na organização. Obviamente, você pode obter muito mais granulares do que isso, se for necessário — impedir que pessoas imprimam, editem, etc. Mas mantenha as restrições mais granulares, como a exceção para documentos que realmente precisam de segurança de alto nível, e não implemente mais políticas restritivas no primeiro dia, apenas planeje uma abordagem mais gradual.

## Quais recursos podem ou não ser usados com as diferentes assinaturas do Azure RMS?
Para as assinaturas pagas que dão suporte ao Azure RMS (Office 365, Azure RMS Premium e Enterprise Mobility Suite), existem algumas diferenças nos recursos do RMS com suporte. Para obter uma lista delas, consulte [Comparação de Ofertas do Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

A assinatura gratuita que suporta o Azure RMS (RMS para pessoas físicas) suporta o consumo do conteúdo que foi protegido pelo Azure RMS. Para saber mais, confira [RMS para pessoas físicas e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## Onde posso obter informações técnicas sobre a assinatura gratuita do Azure RMS (RMS para pessoas físicas) — por exemplo, como ele realmente funciona, como assumir o controle das contas e quais domínios não podem ser usados?
Você encontrará respostas a essas perguntas em [RMS para indivíduos e Azure Rights Management](../understand-explore/rms-for-individuals.md) e artigos relacionados.

## Como podemos recuperar o acesso a arquivos que foram protegidos por um funcionário que saiu da organização?
Use o recurso de superusuário do Azure RMS, que permite que os usuários autorizados tenham direitos totais de proprietário para todas as licenças de uso que foram concedidas pelo locatário do RMS da sua organização. Esse mesmo recurso permite a serviços autorizados criarem índices e inspecionarem arquivos, conforme necessário.

Para mais informações, veja [Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou a recuperação de dados](../deploy-use/configure-super-users.md).

## O Rights Management pode prevenir capturas de tela?
Ao não conceder o [direito de uso](../deploy-use/configure-usage-rights.md) de **Cópia**, o Rights Management pode impedir capturas de tela de muitas das ferramentas de captura de tela comumente utilizados em plataformas Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) e Android. No entanto, dispositivos iOS e Mac não permitem que nenhum aplicativo impeça capturas de tela, e navegadores (por exemplo, quando usados com o Outlook Web App e Office Online) também não podem impedir capturas de tela.

A prevenção de capturas de tela pode ajudar a evitar a divulgação acidental ou negligente de informações confidenciais ou sigilosas. No entanto, há muitas maneiras que um usuário pode compartilhar dados que são exibidos em uma tela, e fazer uma captura de tela é apenas um método. Por exemplo, um usuário com intenção de compartilhar informações exibidas pode tirar uma foto dela usando a câmera do celular, digitando os dados novamente ou, simplesmente, retransmitindo-a verbalmente a alguém.

Como esses exemplos demonstram, mesmo se todas as plataformas e todo o software derem suporte às APIs do Rights Management para bloquear as capturas de tela, a tecnologia sozinha nem sempre poderá impedir que os usuários compartilhem dados que não deveriam. O Rights Management pode ajudar a proteger seus dados importantes usando autorização e políticas de uso, mas esta solução de gestão de direitos de empresa deve ser usada com outros controles. Por exemplo, implementar a segurança física, monitorar cuidadosamente as pessoas com acesso autorizado aos dados de sua organização e investir na educação do usuário para que eles entendam quais dados não devem ser compartilhados.

## Qual é a diferença entre um usuário proteger um email com Não Encaminhar e um modelo que não inclui o direito de Encaminhar?

Apesar do nome e da aparência, **Não Encaminhar** não é o oposto do direito de Encaminhar e não é um modelo. Na verdade, trata-se de um conjunto de direitos que inclui restrições de copiar, imprimir e salvar anexos, além restrições de encaminhamento de emails. Os direitos são aplicados dinamicamente aos usuários por meio dos destinatários escolhidos, e não estaticamente atribuídos pelo administrador. Para obter mais informações, consulte a seção [Opção Não Encaminhar para emails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) em [Configurando os direitos de uso do Azure Rights Management](../deploy-use/configure-usage-rights.md).

## Onde posso encontrar informações de suporte para o Azure RMS, tais como informações jurídicas, de conformidade e SLAs?
O Azure RMS oferece suporte a outros serviços e também se baseia em outros serviços. Se você estiver procurando por informações relacionadas ao Azure RMS, mas não sobre como usar o serviço Azure RMS, verifique os seguintes recursos:

**Informações jurídicas e de privacidade:**

-   Para obter informações sobre o contrato do Microsoft Azure: [Contrato do Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Para obter informações sobre a privacidade do Microsoft Azure: [Declaração de privacidade do Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Segurança, conformidade e auditoria:**

Veja a seção [Requisitos de segurança, conformidade e regulatórios](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) no artigo [Quais problemas o Azure RMS resolve?](../understand-explore/azure-rms-problems-it-solves.md) Além disso:

-   Para certificações externas do Azure RMS: [Central de confiabilidade do Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

-   Para obter informações sobre o FIPS 140: [Validação do FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

**Contratos de nível de serviço (SLA – Service Level Agreement):**

-   Contrato de nível de serviço para o Azure RMS, por região selecionada: [Download da página de pesquisa de Licenciamento do Produto](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - Por exemplo, clique em **OnlineSvcsConsolidatedSLA(WW)(English)(March2016)** para baixar o contrato de nível serviço de março de 2016 para a América do Norte.

-   Contrato de nível de serviço para o Active Directory do Azure: [Contratos de nível de serviço](http://azure.microsoft.com/support/legal/sla/)

**Documentação:**

-   Site de documentação do Active Directory do Azure: [Active Directory do Azure](http://azure.microsoft.com/documentation/services/active-directory/)

-   Biblioteca do Azure Active Directory: [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx)

-   Biblioteca do Office 365: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Ouvi dizer uma nova versão vai estar disponível em breve para o Azure RMS. Quando ela será lançada?

A documentação técnica não contém informações sobre versões futuras. Para obter esse tipo de informação e para ver anúncios sobre lançamentos, confira o [Blog de segurança e mobilidade corporativa](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) e veja as atualizações mais recentes de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) no Twitter. Se você tiver interesse em uma versão do Office, confira também o [blog do Office [(https://blogs.office.com/).

## O que eu faço se a minha pergunta não estiver aqui?
Use os links e recursos listados nas [Informações e suporte do Azure Rights Management](information-support.md).

Além disso, há perguntas frequentes projetadas para usuários finais:

-   [FAQ do aplicativo de compartilhamento do Rights Management para Windows](https://technet.microsoft.com/dn467883)

-   [Perguntas frequentes para os aplicativos de compartilhamento do Microsoft Rights Management para Plataformas Móveis e MAC](https://technet.microsoft.com/dn451248)

-   [Perguntas Frequentes para o Controle de documentos](http://go.microsoft.com/fwlink/?LinkId=523977)

Essa página de Perguntas Frequentes será atualizada regularmente, com novas adições listadas nos anúncios mensais de atualizações na documentação no [blog de Segurança e mobilidade corporativa](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).





<!--HONumber=Jul16_HO1-->


