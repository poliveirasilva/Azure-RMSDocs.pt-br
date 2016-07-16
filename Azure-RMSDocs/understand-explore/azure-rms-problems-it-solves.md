---
title: Quais problemas o Azure RMS resolve | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/02/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e84de6afd80196d4237499718af45c64788c408d
ms.openlocfilehash: 2863c98390b8fda528c4fe3a1b2ebce3510763b4


---


# Quais problemas o Azure RMS resolve?

*Aplica-se a: Azure Rights Management, Office 365*

Use a tabela a seguir para identificar os requisitos ou problemas empresariais que sua organização pode ter e como o Azure RMS pode solucioná-los.

|Requisito ou problema|Resolvido pelo Azure RMS|
|--------------------------|-----------------------|
|Proteger todos os tipos de arquivos|√ Na implementação anterior do Rights Management, só era possível proteger arquivos do Office usando a proteção nativa. Agora, [proteção genérica](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection-) significa que todos os tipos de arquivo têm suporte.|
|Proteger arquivos em qualquer lugar|√ Quando um arquivo é salvo em um local ([proteção in-loco](../rms-client/sharing-app-protect-in-place.md)), a proteção permanece com o arquivo, mesmo que ele seja copiado para o armazenamento que não está sob o controle da TI, como um serviço de armazenamento de nuvem.|
|Compartilhar arquivos por email com segurança|√ Quando um arquivo é compartilhado por email ([compartilhamento protegido](../rms-client/sharing-app-protect-by-email.md)), o arquivo é protegido como um anexo a uma mensagem de email, com instruções de como abrir o anexo protegido. O texto do email não é criptografado, então o destinatário sempre pode ler essas instruções. No entanto, como o documento anexo é protegido, somente usuários autorizados podem abri-lo, mesmo que o email ou o documento seja encaminhado para outras pessoas.|
|Auditoria e monitoramento|√ Você pode [auditar e monitorar o uso](../deploy-use/log-analyze-usage.md) dos seus arquivos protegidos, mesmo depois que eles saírem dos limites da sua organização.<br /><br />Por exemplo, você trabalha para a Contoso, Ltd. Você está trabalhando em um projeto conjunto com 3 pessoas da Fabrikam, Inc. Você envia um e-mail para essas 3 pessoas um documento que proteger e restringir a somente leitura. A auditoria do Azure RMS pode fornecer as seguintes informações:<br /><br />– Se as pessoas da Fabrikam que você especificou abriram o documento e quando o fizeram.<br /><br />– Se outras pessoas que você não especificou tentaram (e não conseguiram) abrir o documento: talvez porque ele foi encaminhado ou salvo em um local compartilhado ao qual outras pessoas têm acesso.<br /><br />– Se alguma das pessoas especificadas tentou (e não conseguiu) imprimir ou alterar o documento.|
|Suporte a todos os dispositivos mais usados e não apenas a computadores Windows|√ [Os dispositivos com suporte](../get-started/requirements-client-devices.md) incluem:<br /><br />– Computadores e celulares Windows<br /><br />– Computadores Mac<br /><br />– Tablets e celulares iOS<br /><br />– Tablets e celulares Android|
|Suporte à colaboração entre empresas|√ Como o Azure RMS é um serviço de nuvem, você não precisa configurar relações de confiança com outras organizações explicitamente para poder compartilhar conteúdo protegido com elas. Se elas já tiverem um Office 365 ou um diretório do AD do Azure, a colaboração entre organizações terá suporte automaticamente. Se eles não tiverem, os usuários poderão se inscrever para a assinatura do [RMS para pessoas físicas](rms-for-individuals.md) gratuita.|
|Suporte para serviços locais, bem como para o Office 365|√ Além de funcionar [perfeitamente com o Office 365](office-apps-services-support.md), você também pode usar o Azure RMS com os seguintes serviços locais ao implantar o [conector RMS](../deploy-use/deploy-rms-connector.md):<br /><br />– Exchange Server<br /><br />– SharePoint Server<br /><br />– Windows Server executando a Infraestrutura de Classificação de Arquivos|
|Ativação fácil|√ [Ativar o serviço Rights Management](../deploy-use/activate-service.md) para os usuários requer apenas alguns cliques no Portal clássico do Azure.|
|Escalabilidade para toda a sua organização, conforme necessário|√ Como o Azure RMS é executado como um serviço de nuvem com a elasticidade do Azure para escalar verticalmente e horizontalmente, não é necessário provisionar ou implantar servidores locais adicionais.|
|Capacidade de criar políticas simples e flexíveis|√ [Os modelos personalizados de políticas de direitos](../deploy-use/configure-custom-templates.md) oferecem uma solução rápida e fácil que permite aos administradores aplicar políticas, além de permitir que os usuários atribuam o nível correto de proteção a cada documento e restrinjam o acesso somente a pessoas dentro da sua organização.<br /><br />Por exemplo, para que um documento de estratégia pertinente a toda a empresa seja compartilhado com todos os funcionários, você pode aplicar uma política somente leitura a todos os funcionários internos. Já para um documento confidencial, como um relatório financeiro, pode restringir o acesso somente aos diretores da empresa.|
|Amplo suporte a aplicativos|√ O Azure RMS tem sólida integração com os aplicativos e serviços do Microsoft Office e amplia o suporte a outros aplicativos usando o aplicativo de compartilhamento do RSM.<br /><br />√ O [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) oferece aos seus fornecedores de software e desenvolvedores internos, APIs para programar aplicativos personalizados compatíveis com o Azure RMS.<br /><br />Para obter mais informações, consulte [Outros aplicativos que dão suporte às APIs do RMS](api-support.md).|
|A TI deve manter o controle dos dados|√ Organizações podem optar por gerenciar sua própria chave de locatário e usar a solução “[Traga a sua própria chave](../plan-design/plan-implement-tenant-key.md)” (BYOK) e armazenar a chave de locatário em HSMs (Módulos de Segurança de Hardware).<br /><br />√ Derem suporte para auditoria e [log de uso](../deploy-use/log-analyze-usage.md) para que você possa analisar ideias de negócios, monitorar abuso e (se você tiver um vazamento de informação) executar a análise forense.<br /><br />√ Acesso delegado usando o [recurso de superusuário](../deploy-use/configure-super-users.md) garante que a TI possa sempre acessar o conteúdo protegido, mesmo se um documento foi protegido por um funcionário que deixou a organização. Por outro lado, as soluções de criptografia ponto a ponto apresentam o risco de perda de acesso aos dados da empresa.<br /><br />√ Sincronizar [somente os atributos do diretório que o Azure RMS precisa](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) para dar suporte a uma identidade comum para suas contas do Active Directory locais, usando uma [ferramenta de sincronização de diretório](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison), como Azure AD Connect.<br /><br />√ Habilitar o logon único sem replicar senhas para a nuvem, usando o AD FS.<br /><br />√ Organizações sempre têm a opção de parar de usar o Azure RMS sem perder o acesso ao conteúdo anteriormente protegido pelo Azure RMS. Para obter informações sobre as opções de encerramento, consulte [Encerramento e desativação do Azure Rights Management](../deploy-use/decommission-deactivate.md). Além disso, as organizações que implantaram o Active Directory Rights Management Services (AD RMS) podem [migrar para o Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md) sem perder o acesso aos dados anteriormente protegidos pelo AD RMS.|
> [!TIP]
> Se você tem familiaridade com a versão local do Rights Management, o Active Directory Rights Management Services (AD RMS), talvez tenha interesse na tabela de comparação disponível em [Comparando o Azure Rights Management e o AD RMS](compare-azure-rms-ad-rms.md).

## Requisitos de segurança, conformidade e regulamentos
O Azure RMS oferece suporte aos seguintes requisitos de segurança, conformidade e regulamentos:

√ Uso de criptografia padrão do setor e suporte ao FIPS 140-2. Para obter mais informações, consulte a informação [Controles criptográficos utilizados pelo Azure RMS: algoritmos e comprimentos de chave](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Suporte a HSMs (Módulos de Segurança de Hardware) da Thales para armazenar sua chave de locatário nos data centers do Microsoft Azure. O Azure RMS usa ambientes de segurança separados para os data centers na América do Norte, na EMEA (Europa, Oriente Médio e África) e na Ásia, garantindo que suas chaves só possam ser usadas na sua região.

√ Certificado para:

-   ISO/IEC 27001:2013 (inclui [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Atestados SSAE 16/ISAE 3402 do SOC 2

-   BAA do HIPAA

-   Cláusula de modelo da UE

-   FedRAMP como parte do Active Directory do Azure na certificação do Office 365, ATO da agência FedRAMP emitido pelo HSS

-   PCI DSS nível 1

Para obter mais informações sobre essas certificações externas, consulte o [Azure Trust Center](http://azure.microsoft.com/support/trust-center/compliance/).

## Próximas etapas

Para ver a aparência do Azure RMS para administradores e usuários, consulte [Azure RMS em ação](what-admins-users-see.md).

Se você estiver interessado em mais informações técnicas sobre como funciona o Azure RMS, confira [Como funciona o Azure RMS?](how-does-it-work.md) 


<!--HONumber=Jun16_HO4-->


