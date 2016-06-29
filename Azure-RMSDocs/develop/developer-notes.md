---
# required metadata

title: Informações e documentação de orientação para programadores | Azure RMS
description: Este tópico inclui orientações específicas para vários cenários de desenvolvimento importantes.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Informações e documentação de orientação para programadores

Esta secção inclui documentação de orientação específica para diversos cenários de desenvolvimento importantes, bem como informações gerais sobre a desenvolvimento este SDK. Os cenários nesta secção são específicos desta versão do SDK Rights Management Services 2.1 e poderão ser alterados em versões posteriores.
- [Procedimentos: utilizar a autenticação ADAL](how-to-use-adal-authentication.md) - Autenticação com o Azure RMS para a sua aplicação com o ADAL (Azure Active Directory Authentication Library).
- [Procedimentos: Adicionar direitos de proprietário explícitos](add-explicit-owner-rights.md) – A aplicação deve adicionar explicitamente direitos de &quot;Proprietário&quot; quando cria uma licença de raiz ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [Procedimentos: depurar uma aplicação com permissão para direitos](debugging-applications-that-use-ad-rms.md) - Este tópico mostra como depurar a aplicação e utilizar o Registo de Eventos do Windows.
- [Procedimentos: ativar o controlo e a revogação de documentos](tracking-content.md) -Este tópico inclui a documentação de orientação básica para implementação do controlo de documento do conteúdo, bem como código de exemplo para atualizações de metadados e criação de um botão **Controlar Utilização** para a sua aplicação.
- [Procedimentos: ativar a notificação por e-mail](how-to-enable-email-notification.md) – A notificação por e-mail permite que um proprietário de conteúdo protegido seja notificado quando esse conteúdo for acedido.
- [Procedimentos: permitir que a aplicação de serviço funcione com o RMS baseado na nuvem](how-to-use-file-api-with-aadrm-cloud.md) – Este tópico descreve os passos para configurar a sua aplicação de serviço para utilizar o Azure Rights Management.
- [Procedimentos: instalar e configurar um servidor RMS](how-to-install-and-configure-an-rms-server.md) - Este tópico inclui os passos para ligação a um Servidor RMS ou ao Azure RMS para fins de testar da sua aplicação com permissão para direitos.
- [Procedimentos: definir o modo de segurança da API](setting-the-api-security-mode-api-mode.md) – Pode escolher em que modo de segurança a sua aplicação de API de Ficheiros é executada utilizando a função [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Procedimentos: trabalhar com definições de encriptação](working-with-encryption.md) – Este tópico descreve os nossos pacotes de encriptação e mostra alguns fragmentos de código para utilização.
- [Tipos de aplicação](application-types.md) – Este tópico inclui os tipos de aplicações que pode escolher para criar com capacidade para direitos.
- [Configuração da API de ficheiros](file-api-configuration.md) – O comportamento da API de ficheiros pode ser configurado através de definições no registo.
- [Formatos de ficheiro suportados](supported-file-formats.md) – A API de Ficheiros suporta formatos nativos e Pfile
- [Plataformas suportadas](supported-platforms.md) - Este tópico identifica as plataformas de cliente e de servidor suportadas pelo SDK RMS 2.1.
- [Compreender restrições de utilização](understanding-usage-restrictions.md) – Todas as aplicações com suporte RMS têm de impor restrições de utilização.
- [Referência de restrição da utilização](usage-restriction-reference.md) - As restrições de utilização são definidas pelas constantes listadas neste tópico.

 
## Tópicos relacionados ##
* [Descrição Geral](ad-rms-overview.md)
 

 


<!--HONumber=Jun16_HO2-->


