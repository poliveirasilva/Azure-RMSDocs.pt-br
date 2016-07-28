---
title: "Perguntas frequentes sobre a visualização do Azure Information Protection | Azure Information Protection"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e60cd910a8e995a2681d7eb87a13f815183d9124
ms.openlocfilehash: 846578a84df383821a64d32ce6dd69290a5fdee9


---

# Perguntas frequentes sobre a visualização do Azure Information Protection

*Aplica-se a: visualização do Azure Information Protection*

Tem alguma pergunta sobre a versão de visualização do Azure Information Protection?  Veja se ela foi respondida aqui. 

Espere que esta lista seja atualizada com frequência, uma vez que algumas informações são movidas para a documentação principal e incluímos novas perguntas que ouvimos dos clientes. 

## O que posso fazer com a versão de visualização do Azure Information Protection e quais são as limitações atuais?

Esta versão de visualização adiciona uma barra do Information Protection aos aplicativos do Microsoft Office que permite que você exiba e modifique os rótulos de classificação atribuídos aos dados. A classificação pode ser feita manualmente, de forma recomendada para você ou aplicada automaticamente. Para as classificações que você especificar, os dados podem ser protegidos usando um modelo do Azure Rights Management.  

O comportamento e os rótulos de classificação são configurados no Portal do Azure. Você pode usar as políticas internas padrão para avaliar rapidamente o Azure Information Protection ou personalizar totalmente suas próprias políticas. Você pode alterar as cores, os nomes e a ordem dos rótulos de classificação que os usuários veem. Você também pode configurar as dicas de ferramentas e marcações visuais de classificação, como o cabeçalho, o rodapé ou uma marca-d'água.

Experimente nosso tutorial de início rápido para ver isso funcionando em apenas alguns minutos: [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md).

Observe que a visualização permite que você experimente o novo **plano de serviço Premium P2** e que alguns recursos avançados, como a rotulação automática e recomendada, podem não estar disponíveis para você no seu plano atual na disponibilidade geral. Para obter informações sobre os diferentes planos de serviço (Azure Information Protection Premium P1 e Azure Information Protection Premium P2), consulte a seguinte postagem do blog: [Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/) (Apresentando a mobilidade corporativa + segurança).

Essa versão de visualização tem as limitações a seguir. Esteja atento aos comunicados no [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de segurança e mobilidade corporativa) e em nosso [site do Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para quando recursos e funcionalidades adicionais forem disponibilizados:

- Não há nenhum log centralizado para classificação e rotulagem.

- Nomes de rótulo e dicas de ferramentas têm suporte apenas em inglês.

- As condições para a classificação automática devem ser frases ou padrões.

- Os arquivos não podem ser classificados do Explorador de Arquivos do Windows.

- Os aplicativos do Office para dispositivos móveis (iOS e Android) e computadores Mac e os aplicativos Web do Office (Office Online) não têm suporte ainda.

- Sem integração com o Exchange Online ou SharePoint Online.

- O SDK para parceiros e desenvolvedores não está disponível.

## De qual assinatura eu preciso para testar o Azure Information Protection?

Para a versão de visualização, você pode usar qualquer assinatura que inclua o Azure Rights Management. O Azure Information Protection está disponível em todas as regiões. Para obter mais informações sobre as assinaturas disponíveis e os links para avaliações gratuitas, consulte [Requisitos do Azure RMS: assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).

Para configurar as políticas do Azure Information Protection no Portal do Azure, você deve ter uma assinatura do Azure. Se você ainda não tiver uma assinatura do Azure para sua organização, poderá obtê-la se inscrevendo em uma avaliação gratuita: vá para a página [Introdução ao Azure](https://account.windowsazure.com/organization) e siga as instruções.

Todas as alterações nos requisitos de assinatura serão anunciadas no [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de segurança e mobilidade corporativa).

## Se o Azure Information Protection agora está em visualização pública, por que não consigo encontrá-lo no Portal do Azure?

No momento, é necessário usar esse link para ver o Azure Information Protection no portal: https://portal.azure.com/?Microsoft_Azure_InformationProtection=true

Em seguida, no menu hub, clique em **Procurar** e comece a digitar “Information Protection” na caixa de filtro. Nos resultados, selecione **Azure Information Protection**.

## É necessário ser um administrador global para experimentar a visualização do Azure Information Protection?

Apenas para a versão de visualização, qualquer usuário autenticado pelo Azure poderá ver e configurar sua política do Azure Information Protection de locatário no Portal do Azure.

Se você selecionar a opção para instalar a política de demonstração, ao instalar o [cliente do Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), não precisa nem entrar no portal para experimentar a visualização. A política de demonstração instala localmente a política padrão para o Azure Information Protection, portanto, é possível tentar rotular documentos e emails, mas não é possível alterar ou adicionar novos rótulos sem entrar no Portal do Azure. 

Se você quiser proteger os documentos e emails classificados e rotulados e ainda não tiver ativado o Azure Rights Management, o processo de ativação exigirá permissões de administrador especiais. Para obter mais informações, consulte [Você precisa ser um administrador global para configurar o Azure RMS ou eu posso delegar a outros administradores?](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)


## O Azure Information Protection dá suporte a cenários locais e híbridos?

O Azure Information Protection é uma solução baseada em nuvem. Se você tiver interesse em cenários híbridos, entre em contato com a equipe do Information Protection enviando um email para askipteam@microsoft.com.

## Quais plataformas de cliente e aplicativos têm suporte no Azure Information Protection?

Agora isso está documentado e será atualizado em [Requisitos do Azure Information Protection](requirements-azure-infoprotect.md).


## Como os computadores obtêm as informações da política do Azure Information Protection e com que frequência elas são atualizadas?

Sempre que um usuário abre um aplicativo do Office, o cliente do Azure Information Protection verifica se há uma versão mais recente da política do Azure Information Protection. Se houver uma versão mais recente, o cliente a baixa usando um link HTTPS para proteger os dados. 

Se o aplicativo já estiver carregado quando uma política do Azure Information Protection for atualizada, será necessário fechar e reabrir o aplicativo para obter a versão mais recente da política.

## Onde é possível armazenar arquivos para usar o Azure Information Protection? 

Como o Azure Information Protection aplica proteção e rótulos persistentes aos arquivos e emails, não importa onde os arquivos são armazenados.

## Posso classificar somente dados novos ou posso classificar dados existentes também?

As ações de política do Azure Information Protection entram em vigor quando os documentos são salvos e os emails são enviados, tanto para o conteúdo novo como para as alterações no conteúdo existente. 

Se você salvou os arquivos que deseja classificar, basta abri-los e salvá-los em seu aplicativo do Office. 

Atualmente, não é possível verificar e aplicar a classificação em massa e é necessário abrir e salvar cada documento no aplicativo do Office. 

## Posso usar o Azure Information Protection apenas para classificação, sem impor a criptografia e restringir direitos de uso?

Sim. Você pode configurar uma política do Azure Information Protection que se aplique a apenas um rótulo. Na verdade, esperamos que esse seja o caso da maioria para redes de implantação em que é necessário proteger apenas um subconjunto de documentos ou emails que exigem o gerenciamento de dados especial.

## Como a classificação automática funciona?

No Portal do Azure, você pode usar padrões predefinidos, como "Números de cartão de crédito" ou "Número do seguro social dos EUA". Ou, você pode definir uma cadeia de caracteres personalizada ou padrão como uma condição para a classificação automática.

Você verá um exemplo disso no [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md). 

A precisão da classificação depende de como você configurar a regra de classificação, que é baseada em condições. Atualmente, as condições dão suporte a expressões regulares e padrões de texto. Para obter uma explicação de cada uma das opções disponíveis durante a visualização, com alguns exemplos sugeridos para teste, consulte a postagem do Yammer [Description of content matching for our pre-define Information types](https://www.yammer.com/askipteam/#/Threads/show?threadId=737163344) (Descrição do conteúdo correspondente para nossos tipos de informações predefindos). A detecção é executada quando o documento é salvo ou um email é enviado.

Para a melhor experiência do usuário e para garantir a continuidade dos negócios, é recomendável que você comece com ações de recomendação de usuário, em vez de ações totalmente automáticas. Isso oferece aos usuários a capacidade de aceitar a ação de proteção ou rotulação ou substituir estas sugestões.   

## O Azure Information Protection pode solicitar que os próprios usuários classifiquem os arquivos em vez de usar a classificação automática? 

Sim. Use o Portal do Azure para configurar se deseja usar a classificação automática ou fazer uma recomendação para os usuários, definindo a opção **Select how this label is applied: automatically or recommended to user** (Selecionar como este rótulo é aplicado: automaticamente ou recomendado para o usuário) como **Recomendado**.

Você verá um exemplo disso no [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md).

## Posso forçar todos os documentos a serem classificados?

Sim. Se você exige que os usuários classifiquem todos os arquivos que salvarem, no Portal do Azure, defina a opção **All documents and emails must have a label** (Todos os documentos e emails devem ter um rótulo) como **Ativado**. 

## Posso remover a classificação de um arquivo?

Sim. Para remover a classificação de um arquivo, abra o arquivo no aplicativo do Office, clique no ícone **Editar rótulo** na barra do Information Protection, clique no ícone **Remover rótulo** e clique em **OK** para confirmar sua ação. 


## Posso solicitar que os usuários justifiquem por que eles estão alterando o nível de classificação?

Sim. Para garantir que os usuários justifiquem a alteração de classificação, no Portal do Azure, defina a opção **Users must provide justification when lowering the sensitivity level** (Os usuários devem fornecer uma justificativa ao reduzir o nível de confidencialidade) como **Ativado**. Ao fazer isso, sua ação e justificativa são registradas no log de eventos do Windows local: **Aplicativo** > **Microsoft Azure Information Protection**.

## Como posso proteger automaticamente o conteúdo após ele ser classificado?

No portal do Azure, você pode selecionar um modelo do Azure Rights Management para proteger o conteúdo automaticamente, de acordo com o nível de classificação especificado.

Você verá um exemplo disso no [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md).

## Um arquivo pode ser classificado com duas classificações diferentes?

Se necessário, você pode criar sub-rótulos para descrever melhor as subcategorias para um rótulo de confidencialidade específico. Por exemplo, o rótulo principal **Segredo** pode conter sub-rótulos como **Segredo – Legal** e **Segredo – Finanças**. Você pode aplicar marcas visuais de classificação diferentes e modelos do Rights Management diferentes aos diferentes sub-rótulos.

Embora atualmente você possa definir marcas visuais, proteção e condições nos dois níveis, ao usar subníveis, configure essas definições apenas no subnível. Se você configurar as mesmas definições no rótulo pai e seu subnível, as definições no subnível terão precedência.

## Como outros aplicativos e soluções DLP se integram ao Azure Information Protection?

Como o Azure Information Protection usa metadados persistentes para a classificação, que incluem um rótulo de texto não criptografado, essas informações podem ser lidas por soluções DLP e outros aplicativos. Em arquivos, esses metadados são armazenados nas propriedades personalizadas; nos emails, essas informações estão nos cabeçalhos de email.

## Como o rastreamento de documentos e a revogação funcionam para o Azure Information Protection?

O rastreamento de documentos para os arquivos que você classifica e protege usando o Azure Information Protection funciona da mesma forma que atualmente para o Azure Rights Management. Para obter mais informações, consulte [Rastreie e revogue seus documentos ao usar o aplicativo RMS sharing](../rms-client/sharing-app-track-revoke.md).

## Como o Azure Information Protection impõe as políticas que eu configuro?

Quando um documento é protegido usando um modelo do Azure Rights Management, o usuário é autenticado primeiro para garantir que tem direitos para o arquivo e, em seguida, a política de direitos de uso é imposta pelo aplicativo. 

## Como o Azure Information Protection usa o Azure Active Directory?

O Azure Information Protection usa o Azure Active Directory para autenticação de usuário.

## Posso controlar quais usuários podem usar o Azure Information Protection para classificar e proteger o conteúdo?

Você pode restringir quais usuários classificam e protegem dados controlando a distribuição do cliente do Azure Information Protection. 

Arquivos e emails que são classificadas pelo Azure Information Protection podem ser consumidos ou editados por qualquer usuário, com ou sem o cliente do Azure Information Protection instalado. 

## Como relatar um problema ou enviar comentários para essa visualização?

Se você encontrar um problema ao usar a versão de visualização, em seu aplicativo do Office, na guia **Página Inicial**, no grupo **Proteção**, clique em **Proteger** e em **Ajuda e comentários**. Na caixa de diálogo **Microsoft Azure Information Protection**, clique em **Enviar comentários**. Isso envia um email para a equipe do Information Protection e anexa automaticamente os arquivos de log do seu computador para ajudar a diagnosticar o problema. 

Se você tiver perguntas ou comentários, use o [site do Yammer do Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). 

## O que eu faço se a minha pergunta não estiver aqui?

Primeiro, verifique se sua pergunta não está incluída no [comunicado da visualização do Azure Information Protection](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/), no Enterprise Mobility and Security Blog (Blog de segurança e mobilidade corporativa).

Em seguida, visite nosso [site do Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) para ver se alguém fez a mesma pergunta. Se não, poste sua pergunta lá.







<!--HONumber=Jul16_HO3-->


