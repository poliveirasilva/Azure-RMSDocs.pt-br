---
# required metadata

title: Requisitos do Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Requisitos do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*


Para implementar o Microsoft Azure Rights Management (Azure RMS) na sua organização, certifique-se de que cumpre os seguintes pré-requisitos. Em seguida, pode utilizar o [Plano de implementação do Azure Rights Management](../plan-design/deployment-roadmap.md) para implementar o Rights Management para a sua organização.

|Requisito|Mais informações|
|---------------|--------------------|
|Uma subscrição na nuvem do RMS|A sua organização tem de ter uma subscrição na nuvem que suporte RMS.<br /><br />Para obter informações de licenciamento, consulte [Subscrições na nuvem que suportam o Azure RMS](requirements-subscriptions.md).|
|Diretório do Azure AD|A sua organização tem de ter um diretório do Azure AD para suportar a autenticação de utilizador para RMS. Além disso, se pretender utilizar as contas de utilizador do seu diretório no local (AD DS), tem também de configurar a integração de diretórios.<br /><br />A Multi-Factor Authentication (MFA) é suportada com o Azure RMS quando tem o software de cliente necessário e a infraestrutura de suporte de MFA corretamente configurada.<br /><br />Para obter mais informações, consulte [Diretório do Azure AD](requirements-azure-ad.md).|
|Dispositivos cliente|Os utilizadores têm de ter dispositivos cliente (computador ou dispositivo móvel) com um sistema operativo que suporte RMS.<br /><br />Para obter mais informações, consulte [Dispositivos cliente que suportam o Azure RMS](requirements-client-devices.md).|
|Aplicações|Os utilizadores têm de executar aplicações que suportem RMS.<br /><br />Para obter mais informações, consulte [Aplicações que suportam o Azure RMS](requirements-applications.md).|
|Infraestrutura que suporta a conetividade à Internet e a serviços em nuvem dependentes|Se tiver uma firewall ou dispositivos de rede intervenientes semelhantes que devem ser configurados para permitir ligações específicas, consulte [Intervalos de endereços IP e URLs do Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />A lista de URLs e endereços IP nas secções **Portal do Office 365 e partilhado** e **Identidade e autenticação do Office 365** aplica-se ao portal do Office 365, aos recursos do Azure Active Directory e ao Azure Rights Management. Utilize as instruções neste artigo para se manter atualizado em relação às alterações a estas informações ao subscrever um feed RSS.<br /><br />Além das informações no artigo do Office, específico para o Azure RMS:<br /><br />- Não termine a ligação cliente para serviço TLS (por exemplo, para fazer uma inspeção ao nível do pacote). Se o fizer, quebrará a afixação de certificado que os clientes de RMS utilizam com as AC geridas pela Microsoft para ajudar a proteger as comunicações com o Azure RMS.<br /><br />- Se utilizar um proxy Web que requer autenticação, tem de o configurar para utilizar a autenticação integrada do Windows com as credenciais de início de sessão do utilizador do Active Directory.|

Se pretender utilizar o Azure RMS com servidores no local, são suportados os seguintes produtos:

-   Exchange Server

-   SharePoint Server

-   Servidores de ficheiros do Windows Server que suportam a Infraestrutura de Classificação de Ficheiros

Para obter informações acerca dos requisitos adicionais do Azure RMS para este cenário, consulte a secção [Servidores no local que suportam o Azure RMS](requirements-servers.md).

> [!IMPORTANT] O cenário de implementação seguinte não é suportado:
> 
> -   Executar o AD RMS e o Azure RMS lado a lado na mesma organização, exceto durante a migração, conforme descrito em [Migrar do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Existe um caminho de migração suportado do [AD RMS para o Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) e do [Azure RMS para o AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Se implementar o Azure RMS e, em seguida, decidir que já não pretende utilizar este serviço em nuvem, consulte [Encerrar e Desativar o Azure Rights Management](../deploy-use/decommission-deactivate.md).





<!--HONumber=May16_HO3-->


