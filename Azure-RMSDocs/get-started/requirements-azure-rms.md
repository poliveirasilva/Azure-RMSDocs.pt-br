---
title: Requisitos para o Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2fab331a26e18730e9cc64a24c0501b7ae21aa1b
ms.openlocfilehash: f225d8579e2440d2eb00a4f821a78727b6442fdd


---

# Requisitos para o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*


Para implantar o Azure RMS (Microsoft Azure Rights Management) em sua organização, certifique-se de ter os pré-requisitos a seguir. Então, você poderá usar o [Roteiro de implantação do Azure Rights Management](../plan-design/deployment-roadmap.md) para implantar o Rights Management para a sua organização.

|Requisito|Mais informações|
|---------------|--------------------|
|Uma assinatura de nuvem para o RMS|Sua organização deve ter uma assinatura de nuvem que ofereça suporte ao RMS.<br /><br />Para informações de licenciamento, consulte [Assinaturas de nuvem que dão suporte ao Azure RMS](requirements-subscriptions.md).|
|Diretório do AD do Azure|Sua organização deve ter um diretório do AD do Azure para oferecer suporte à autenticação de usuário para o RMS. Além disso, se você quiser usar as contas de usuário do seu diretório local (AD DS), também será necessário configurar a integração do diretório.<br /><br />O MFA (Multi-Factor Authentication) tem suporte com o Azure RMS quando você tem o software cliente necessário e a infraestrutura de suporte do MFA configurada corretamente.<br /><br />Para obter mais informações, consulte o [diretório do Azure AD](requirements-azure-ad.md).|
|Dispositivos cliente|Os usuários devem ter um dispositivo cliente (computador ou dispositivo móvel) que execute um sistema operacional que suporte o RMS.<br /><br />Para obter mais informações, consulte [Dispositivos cliente que dão suporte ao Azure RMS](requirements-client-devices.md).|
|Aplicativos|Os usuários devem executar aplicativos que suportem o RMS.<br /><br />Para obter mais informações, consulte [Aplicativos que dão suporte ao Azure RMS](requirements-applications.md).|
|Infraestrutura que oferece suporte à conectividade com a Internet e serviços em nuvem dependentes|Se você tem um firewall ou dispositivos de rede de intervenção similares que devem ser configurados para permitir conexões específicas, consulte as informações para **Azure Rights Management (RMS)** na seção [Portal do Office 365 e compartilhado](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) do seguinte artigo do Office: [URLs e intervalos de endereços IP do Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Use as instruções neste artigo do Office para se manter atualizado em relação às alterações dessas informações, inscrevendo-se em um RSS feed.<br /><br />Além das informações no artigo do Office, há outras especificações para o Azure RMS:<br /><br />- Não encerre a conexão cliente/serviço TLS (por exemplo, fazer inspeção no nível de pacote). Isso interrompe a fixação de certificado que os clientes RMS usam com CAs gerenciados pela Microsoft para ajudar a proteger suas comunicações com o Azure RMS.<br /><br />- Se você usar um proxy Web que requer autenticação, deverá configurá-lo para usar a autenticação integrada do Windows com as credenciais de logon de usuário do Active Directory.|

Se quiser usar o Azure RMS com servidores locais, os seguintes produtos são compatíveis:

-   Exchange Server

-   SharePoint Server

-   Servidores de arquivos Windows Server que suportem FCI (Infraestrutura de Classificação de Arquivos)

Para obter informações sobre os requisitos adicionais do Azure RMS para este cenário, consulte [Servidores locais que dão suporte ao Azure RMS](requirements-servers.md).

> [!IMPORTANT]
> Não há suporte para o cenário de implantação a seguir:
> 
> -   Execução do AD RMS e do Azure RMS lado a lado na mesma organização, exceto durante a migração, conforme descrito em [Migrando do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Há um caminho de migração com suporte [do AD RMS para o Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) e do [Azure RMS para AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Se você implantar o Azure RMS e depois decidir que não quer mais usar esse serviço de nuvem, consulte [Encerramento e desativação do Azure Rights Management](../deploy-use/decommission-deactivate.md).






<!--HONumber=Jul16_HO3-->


