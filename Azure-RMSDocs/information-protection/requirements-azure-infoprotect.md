---
title: Requisitos do Azure Information Protection | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fe19726959bc16384120b610183c392031519813
ms.openlocfilehash: ff322e4ff0914ca29c7fe937a41936cb15d9a913


---

# Requisitos do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Para avaliar a versão de visualização do Azure Information Protection, certifique-se de que você tenha os seguintes pré-requisitos. 

|Requisito|Mais informações|
|---------------|--------------------|
|Uma assinatura de nuvem que inclui o Azure RMS|Sua organização deve ter uma assinatura de nuvem que dê suporte ao Rights Management.<br /><br />Para obter mais informações e links para avaliações gratuitas, consulte [Assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).|
|Diretório do AD do Azure|Sua organização deve ter um diretório do Azure AD para dar suporte à autenticação do usuário para o Azure RMS e o Azure Information Protection. Além disso, se você quiser usar as contas de usuário do seu diretório local (AD DS), também será necessário configurar a integração do diretório.<br /><br />O MFA (Multi-Factor Authentication) tem suporte com o Azure RMS quando você tem o software cliente necessário e a infraestrutura de suporte do MFA configurada corretamente.<br /><br />Para obter mais informações, consulte [Diretório do Azure AD](../get-started/requirements-azure-ad.md), em que as informações para o Azure RMS também se aplicam ao Azure Information Protection.|
|Dispositivos cliente|Os dispositivos cliente a seguir têm suporte para essa visualização:<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />Quando você protege os dados, eles podem ser consumidos pelos mesmos dispositivos (Windows, Mac, iOS, Android) que dão suporte ao Azure Rights Management. Para obter detalhes sobre esses dispositivos e as versões com suporte, consulte [Requisitos do Azure RMS: dispositivos cliente que dão suporte ao Azure RMS](../get-started/requirements-client-devices.md).|
|Aplicativos|Para a versão de visualização e na GA (disponibilidade geral), o Azure Information Protection dá suporte à rotulação e à proteção dos arquivos e emails criados pelos seguintes aplicativos do Office: **Word**, **Excel**, **PowerPoint** e **Outlook** dos seguintes pacotes o Office:<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 com Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Após a disponibilidade geral, procure um comunicado no [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de segurança e mobilidade corporativa) sobre quando o Azure Information Protection dará suporte a tipos de arquivo adicionais, como arquivos PDF, de áudio, de vídeo e de imagem.|
|Infraestrutura que oferece suporte à conectividade com a Internet e serviços em nuvem dependentes|Se você tem um firewall ou dispositivos de rede de intervenção similares que devem ser configurados para permitir conexões específicas, consulte as informações para **RMS (Azure Rights Management)** na seção [Portal do Office 365 e compartilhado](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) do seguinte artigo do Office: [URLs e intervalos de endereços IP do Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)<br /><br />Além disso:<br /><br />- Permitir o tráfego em TCP 443 para **rmsibizaapiprod.cloudapp.net**.<br /><br />- Não encerre a conexão cliente/serviço TLS (por exemplo, fazer inspeção no nível de pacote). <br /><br />- Se você usar um proxy Web que requer autenticação, deverá configurá-lo para usar a autenticação integrada do Windows com as credenciais de logon de usuário do Active Directory.|

## Próximas etapas

Se você atender a esses requisitos, experimente nossa demonstração autoguiada para configurar e testar o Azure Information Protection sozinho: [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Jul16_HO5-->


