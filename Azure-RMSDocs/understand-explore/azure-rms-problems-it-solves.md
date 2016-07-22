---
title: Que Problemas Resolve o Azure RMS | Azure RMS
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


# Que problemas resolve o Azure RMS?

*Aplica-se a: Azure Rights Management, Office 365*

Utilize a tabela seguinte para identificar os requisitos ou os problemas empresariais que a sua organização pode ter e de que forma o Azure RMS os pode resolver.

|Requisito ou problema|Resolvido pelo Azure RMS|
|--------------------------|-----------------------|
|Proteger todos os tipos de ficheiros|√ Na implementação anterior do Rights Management, apenas era possível proteger ficheiros do Office, através da proteção nativa. Agora, com a [proteção genérica](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection-) significa que todos os tipos de ficheiros são suportados.|
|Proteger ficheiros em qualquer lugar|√ Quando um ficheiro é guardado numa localização ([proteger no local](../rms-client/sharing-app-protect-in-place.md)), a proteção mantém-se com o ficheiro, mesmo que seja copiado para armazenamento que não esteja sob o controlo de TI, tal como um serviço de armazenamento na nuvem.|
|Partilhar ficheiros de forma segura por e-mail|√ Quando um ficheiro é partilhado por e-mail ([partilhar protegido](../rms-client/sharing-app-protect-by-email.md)), o ficheiro está protegido como um anexo a uma mensagem de e-mail, com instruções sobre como abrir o anexo protegido. O texto do e-mail não é encriptado, pelo que o destinatário pode sempre ler estas instruções. No entanto, dado que o documento anexado está protegido, apenas os utilizadores autorizados poderão abri-lo, mesmo que o e-mail ou o documento seja reencaminhado para outras pessoas.|
|Auditoria e monitorização|√ Pode [auditar e monitorizar a utilização](../deploy-use/log-analyze-usage.md) dos seus ficheiros protegidos, mesmo depois de estes ficheiros saírem das imediações da sua organização.<br /><br />Por exemplo, trabalha para a Contoso, Ltd. Está a trabalhar num projeto conjunto com 3 pessoas da Fabrikam, Inc. Envia a estas 3 pessoas um documento por e-mail que protege e restringe para só de leitura. A auditoria do Azure RMS pode facultar as seguintes informações:<br /><br />- Se as pessoas que especificou na Fabrikam abriram o documento e quando.<br /><br />- Se outras pessoas que não especificou tentaram (e não conseguiram) abrir o documento, talvez porque foi reencaminhado ou guardado numa localização partilhada à qual outros utilizadores podiam aceder.<br /><br />- Se qualquer uma das pessoas especificadas tentou (e não conseguiu) imprimir ou alterar o documento.|
|Suporte para todos os dispositivos utilizados mais frequentemente, não apenas computadores Windows|√ [Os dispositivos suportados](../get-started/requirements-client-devices.md) incluem:<br /><br />- Computadores e telemóveis Windows<br /><br />- Computadores Mac<br /><br />- Telemóveis e tablets iOS<br /><br />- Telemóveis e tablets Android|
|Suporte para colaboração empresa-empresa|√ Porque o Azure RMS é um serviço em nuvem, não é necessário configurar explicitamente fidedignidades com outras organizações para poder partilhar conteúdo protegido com as mesmas. Se estas já possuírem um Office 365 ou um diretório do Azure AD, a colaboração entre as organizações é suportada automaticamente. Caso contrário, os utilizadores podem inscrever-se na subscrição gratuita do [RMS para indivíduos](rms-for-individuals.md).|
|Suporte para serviços no local e Office 365|√ Para além de trabalhar [de forma totalmente integrada com o Office 365](office-apps-services-support.md), também pode utilizar o Azure RMS com os seguintes serviços no local quando implementar o [conector RMS](../deploy-use/deploy-rms-connector.md):<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- Windows Server a executar a Infraestrutura de Classificação de Ficheiros|
|Ativação fácil|√ [A ativação do serviço Rights Management](../deploy-use/activate-service.md) para os utilizadores requer apenas alguns cliques no portal clássico do Azure.|
|Capacidade de dimensionamento na sua organização, conforme necessário|√ Uma vez que o Azure RMS é executado como um serviço em nuvem com a elasticidade da Azure para aumentar verticalmente e horizontalmente, não tem de aprovisionar ou implementar mais servidores no local.|
|Capacidade para criar políticas simples e flexíveis|√ [Os modelos de políticas de direitos personalizados](../deploy-use/configure-custom-templates.md) proporcionam uma solução rápida e fácil para os administradores aplicarem políticas e para os utilizadores aplicarem o nível correto de proteção a cada documento e restringirem o acesso a pessoas dentro da organização.<br /><br />Por exemplo, para um documento estratégico à escala da empresa ser partilhado com todos os funcionários, pode aplicar uma política só de leitura a todos os empregados internos. Em seguida, para um documento mais confidencial, tal como um relatório financeiro, pode restringir o acesso a apenas executivos.|
|Suporte abrangente de aplicações|√ O Azure RMS tem uma integração total com as aplicações e serviços do Microsoft Office e expande o suporte a outras aplicações através da aplicação de partilha RMS.<br /><br />√ O [SDK Microsoft Rights Management](../develop/developers-guide.md#software-development-kits) proporciona aos programadores internos e aos fornecedores de software APIs para que escrevam aplicações personalizadas que suportam o Azure RMS.<br /><br />Para obter mais informações, consulte [Outras aplicações que suportam as APIs do RMS](api-support.md).|
|O departamento de TI tem de manter o controlo dos dados|√ As organizações podem optar por gerir as suas próprias chaves de inquilino e utilizar a solução “[Traga a Sua Própria Chave](../plan-design/plan-implement-tenant-key.md)” (BYOK) e armazenar a respetiva chave de inquilino nos Módulos de Hardware de Segurança (HSMs).<br /><br />√ Suporte para auditoria e [registo de utilização](../deploy-use/log-analyze-usage.md) para poder analisar informações empresariais, monitorizar abusos e (se tiver uma fuga de informação) proceder à análise forense.<br /><br />√ O acesso delegado através da [funcionalidade de superutilizador](../deploy-use/configure-super-users.md) garante que o departamento de TI pode sempre aceder a conteúdo protegido, mesmo que um documento tenha sido protegido por um funcionário que, entretanto, saia da organização. Em comparação, as soluções de encriptação ponto a ponto arriscam a perda de acesso aos dados da empresa.<br /><br />√ Sincronize [apenas os atributos do diretório de que o Azure RMS necessita](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) para suportar uma identidade comum para as suas contas do Active Directory no local, ao utilizar uma [ferramenta de sincronização de diretórios](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison), como o Azure AD Connect.<br /><br />√ Ative o início de sessão único sem replicar as palavras-passe na nuvem, utilizando o AD FS.<br /><br />√ As organizações têm sempre a opção de deixar de utilizar o Azure RMS sem perderem o acesso a conteúdo que foi anteriormente protegido pelo Azure RMS. Para mais informações acerca das opções de desativação, consulte [Encerrar e desativar o Azure Rights Management](../deploy-use/decommission-deactivate.md). Além disso, as organizações que implementaram os Serviços de Gestão de Direitos do Active Directory (AD RMS) podem [migrar para o Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md) sem perderem o acesso aos dados que foram anteriormente protegidos pelo AD RMS.|
> [!TIP]
> Se está familiarizado com a versão no local do Rights Management e do Active Directory Rights Management Services (AD RMS), a tabela de comparação apresentada em [Comparar o Azure Rights Management e o AD RMS](compare-azure-rms-ad-rms.md) poderá interessar-lhe.

## Requisitos de segurança, conformidade e regulamentação
O Azure RMS suporta os seguintes requisitos de segurança, conformidade e regulamentação:

√ Utilização de criptografia de norma da indústria e suporte da certificação FIPS 140-2. Para obter mais informações, consulte [Controlos criptográficos utilizados pelo Azure RMS: comprimentos de chave e algoritmos](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Suporte de Módulos de Hardware de Segurança (HSMs) da Thales para armazenar a sua chave de inquilino nos centros de dados do Microsoft Azure. O Azure RMS utiliza universos de segurança separados nos seus centros de dados na América do Norte, EMEA (Europa, Médio Oriente e África) e Ásia, para que as suas chaves possam ser utilizadas apenas na sua região.

√ Possui as seguintes certificações:

-   Norma ISO/IEC 27001:2013 (inclui a norma [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Certificados SOC 2 SSAE 16/ISAE 3402

-   BAA HIPAA

-   Cláusula Modelo da UE

-   FedRAMP como parte da certificação do Azure Active Directory no Office 365, Autoridade Operativa da Agência FedRAMP emitida pelos HHS

-   PCI DSS de Nível 1

Para obter mais informações acerca destas certificações externas, consulte o [Centro de Fidedignidade do Azure](http://azure.microsoft.com/support/trust-center/compliance/).

## Passos seguintes

Para ver o aspeto do Azure RMS do ponto de vista de administradores e utilizadores, consulte [O Azure RMS em ação](what-admins-users-see.md).

Para obter mais informações técnicas sobre o funcionamento do Azure RMS, consulte [Como funciona o Azure RMS?](how-does-it-work.md) 


<!--HONumber=Jun16_HO4-->


