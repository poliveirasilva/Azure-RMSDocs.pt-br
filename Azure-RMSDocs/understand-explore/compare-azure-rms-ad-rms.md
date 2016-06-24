---
# required metadata

title: Comparando o Azure Rights Management e o AD RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Comparando o Azure Rights Management e o AD RMS

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Office 365*

Se você conhece ou já implantou o Active Directory Rights Management Services (AD RMS), você deve estar se perguntando como o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) se compara em termos de requisitos e funcionalidade. 

Algumas principais diferenças do Azure RMS:

- **Nenhuma infraestrutura de servidor necessária**: o Azure RMS não requer servidores adicionais e certificados PKI que o AD RMS precisa, porque o Microsoft Azure se encarrega disso por você. Isso torna esta solução de nuvem mais rápida de implantar e mais fácil de manter.

- **Autenticação baseada em nuvem**: o Azure RMS usa o Azure AD para autenticação - para usuários internos e usuários de outras organizações. Isso significa que os usuários móveis podem ser autenticados, mesmo quando não estão conectados à sua rede interna e é mais fácil compartilhar conteúdo protegido com usuários de outras organizações. Muitas organizações já têm contas de usuário no Azure AD, porque eles estão executando os serviços do Azure ou têm o Office 365. Mas se não, o RMS para pessoas físicas permite aos usuários criar uma conta gratuita. Para compartilhar o conteúdo protegido do AD RMS com outra organização, é necessário configurar relações de confiança explícitas com cada organização.

- **Suporte interno para dispositivos móveis**: nenhuma alteração de implantação é necessária para que o Azure RMS dê suporte a dispositivos móveis e computadores Mac. Para dar suporte a esses dispositivos com o AD RMS, instale a extensão do dispositivo móvel, configure o AD FS para federação e crie registros adicionais para o serviço DNS público.

- **Modelos padrão**: o Azure RMS cria dois modelos padrão assim que o serviço é ativado, o que facilita a proteção de dados importantes imediatamente. Não há nenhum modelo padrão para o AD RMS.

- **Modelos departamentais**: o Azure RMS dá suporte a modelos departamentais como uma definição de configuração para modelos adicionais que você cria. Essa configuração permite que você especifique quais usuários veem o modelo em seus aplicativos cliente (como aplicativos do Office), o que facilita a seleção da política correta que você define para diferentes grupos de usuários. O AD RMS não dá suporte a modelos departamentais.

- **Acompanhamento de documento, revogação e notificação por email**: o Azure RMS dá suporte a esses recursos com o aplicativo de compartilhamento RMS, ao passo que o AD RMS não.


Além disso, como o Azure RMS é um serviço de nuvem, ele pode fornecer novos recursos e correções mais rapidamente do que uma solução local baseada em servidor. Não há novos recursos planejados para AD RMS no Windows Server 2016.

Para obter mais detalhes e outras diferenças, use a tabela a seguir para uma comparação lado a lado dos recursos e benefícios do Azure RMS e AD RMS. Se você tiver dúvidas de comparação específicas de segurança, consulte a seção [Controles criptográficos para assinatura e criptografia](compare-azure-rms-ad-rms.md#cryptographic-controls-for-signing-and-encryption) neste artigo.

> [!NOTE]
> Para facilitar essa comparação, algumas informações aqui são repetidas de [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md). Use essa fonte para informações mais específicas de suporte e versão para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Azure RMS|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Suporta recursos de IRM (Gerenciamento de Direitos de Informação) em serviços da Microsoft Online, como o Exchange Online e o SharePoint Online, bem como o Office 365.<br /><br />Também dá suporte a produtos de servidor da Microsoft local, como o Exchange Server, SharePoint Server e servidores de arquivos que executam o Windows Server e o FCI (Infraestrutura de Classificação de Arquivos).|Dá suporte a produtos de servidor da Microsoft local, como o Exchange Server, SharePoint Server e servidores de arquivos que executam o Windows Server e o FCI (Infraestrutura de Classificação de Arquivos).|
|Proporciona confiança implícita entre as organizações e os usuários em qualquer organização. Isso significa que o conteúdo protegido pode ser compartilhado entre os usuários dentro da mesma organização ou entre organizações quando os usuários têm o [!INCLUDE[o365_1](../includes/o365_1_md.md)] ou o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], ou usuários inscritos para o RMS para indivíduos.|As relações de confiança devem ser explicitamente definidas em uma relação direta ponto-a-ponto entre duas organizações, usando TUDs (Domínios de Usuário Confiável) ou relações de confiança federadas que você cria usando os Serviços de Federação do Active Directory (AD FS).|
|Fornece dois modelos de política de direitos padrão que restringem o acesso do conteúdo a sua própria organização; um que fornece visualização de somente leitura de conteúdo protegido e outro modelo que fornece permissões de gravação ou modificação do conteúdo protegido.<br /><br />Você também pode criar seus próprios modelos personalizados, que incluam modelos de departamentos visíveis apenas para um subconjunto de usuários. Para obter mais informações, consulte [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).<br /><br />Além disso, os usuários podem definir seu próprio conjunto de permissões se os modelos não forem suficientes.|Não há modelos de política de direitos padrão. É necessário criá-los e distribuí-los. Para obter mais informações, consulte [Considerações sobre o modelo de política do AD RMS](http://go.microsoft.com/fwlink/?LinkId=154765).<br /><br />Além disso, os usuários podem definir seu próprio conjunto de permissões se os modelos não forem suficientes.|
|A versão mínima do Microsoft Office com suporte é o Office 2010, que requer o [aplicativo RMS sharing](../rms-client/sharing-app-windows.md).<br /><br />Microsoft Office para Mac:<br /><br />- Microsoft Office para Mac 2016: com suporte<br /><br />- Microsoft Office para Mac 2011: sem suporte|A versão mínima suportada do Microsoft Office é o Office 2007.<br /><br />Microsoft Office para Mac:<br /><br />- Microsoft Office para Mac 2016: com suporte<br /><br />- Microsoft Office para Mac 2011: com suporte|
|Dá suporte ao [aplicativo RMS sharing](../rms-client/sharing-app-windows.md) para computadores Windows, Mac e dispositivos móveis.<br /><br />Além disso, o aplicativo RMS sharing suporta o seguinte:<br /><br />- Compartilhamento com pessoas em outra organização.<br /><br />- Notificação por email que permite ao remetente saber quando alguém tenta abrir um anexo protegido.<br /><br />- Um site de acompanhamento de documentos para usuários que inclui a capacidade de revogar um documento.|Dá suporte ao [aplicativo RMS sharing](../rms-client/sharing-app-windows.md) para computadores Windows, Mac e dispositivos móveis. No entanto, o compartilhamento não suporta compartilhamento com pessoas em outra organização, notificação por email ou o site de rastreamento de documentos e a capacidade dos usuários para revogar documentos.|
|Todos os tipos de arquivo podem ser protegidos com [proteção nativa ou genérica quando você usa o aplicativo RMS sharing](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic).<br /><br />Para outros aplicativos, verifique a [tabela de recursos de dispositivos cliente](../get-started/requirements-client-devices.md#client-device-capabilities).|Todos os tipos de arquivo podem ser protegidos com [proteção nativa ou genérica quando você usa o aplicativo RMS sharing](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic).<br /><br />Para outros aplicativos, verifique a [tabela de recursos de dispositivos cliente](../get-started/requirements-client-devices.md#client-device-capabilities).|
|A versão mínima suportada do cliente Windows é o Windows 7.|A versão mínima suportada do cliente Windows é o Windows Vista Service Pack 2.|
|O suporte para dispositivos móveis inclui Windows Phone, Android, iOS e Windows RT.<br /><br />O suporte por email usando o Exchange ActiveSync IRM também é compatível com todas as plataformas de dispositivos móveis que suportam este protocolo.|O suporte aos dispositivos móveis inclui Windows Phone, Android, iOS e Windows RT e requer a [Extensão de Dispositivo Móvel do Active Directory Rights Management Services](http://technet.microsoft.com/library/dn673574.aspx).<br /><br />O suporte por email usando o Exchange ActiveSync IRM tem suporte em todas as plataformas de dispositivos móveis que suportam esse protocolo.|
|Oferece suporte a Multi-Factor Authentication (MFA) para computadores e dispositivos móveis.<br /><br />Para obter mais informações, consulte [MFA (Azure Multi-Factor Authentication) e Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms).|Oferece suporte à autenticação de cartão inteligente se o IIS estiver configurado para solicitar certificados.|
|Suporta o Modo de criptografia 2, sem configuração adicional, o que proporciona maior segurança para comprimentos de chave e algoritmos de criptografia.<br /><br />Para obter mais informações, consulte a seção [Controles criptográficos para assinatura e criptografia](#cryptographic-controls-for-signing-and-encryption) neste artigo e [Modos criptográficos do AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|Suporta o Modo de Criptografia 1 por padrão e requer configuração adicional para suportar o Modo de criptografia 2 para aumentar a segurança.<br /><br />Para obter mais informações, consulte a seção [Controles criptográficos para assinatura e criptografia](#cryptographic-controls-for-signing-and-encryption) neste artigo e [Modos criptográficos do AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|
|Dá suporte à migração do AD RMS e, se necessário, para o AD RMS:<br /><br />- [Migrando do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Descomissionamento e desativação do Azure Rights Management](../deploy-use/decommission-deactivate.md)|Dá suporte à migração do RMS Azure e para o Azure RMS:<br /><br />- [Descomissionamento e desativação do Azure Rights Management](../deploy-use/decommission-deactivate.md)<br /><br />- [Migrando do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|Requer uma licença de RMS para proteger conteúdo. Nenhuma licença de RMS é necessária para consumir o conteúdo que foi protegido pelo Azure RMS (inclui usuários de outra organização).<br /><br />Para obter mais informações, consulte [Assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).|Requer uma licença de RMS para proteger conteúdo e consumir o conteúdo que foi protegido pelo AD RMS.<br /><br />Para mais informações sobre o licenciamento do AD RMS, consulte [Licenças de acesso para cliente e gerenciamento de licenças](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) para obter informações gerais, mas entre em contato com seu parceiro Microsoft ou o representante da Microsoft para obter informações específicas.|

## Controles criptográficos para assinatura e criptografia
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] sempre usa o RSA 2048 para todas as criptografias de chave pública e SHA 256 para operações de assinatura. Em comparação, o AD RMS suporta RSA 1024 e RSA 2048, e SHA 1 ou SHA 256 para operações de assinatura.

Ambos o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e o AD RMS usam o AES 128 para criptografia simétrica.

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] é compatível com FIPS 140-2 quando sua chave de locatário é criada e gerenciada pela Microsoft (o padrão) ou se você gerenciar sua própria chave de locatário (conhecida como BYOK). Para obter mais informações sobre como gerenciar sua chave de locatário, consulte [Planejando e implementando sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Próximas etapas
Se você desejar migrar do AD RMS para o Azure RMS, consulte [Migrando do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)




<!--HONumber=May16_HO3-->


