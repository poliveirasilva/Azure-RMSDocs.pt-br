---
# required metadata

title: Informações e diretrizes para desenvolvedores | Azure RMS
description: Este tópico aborda as diretrizes específicas para vários cenários de desenvolvimento importantes.
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

# Informações e diretrizes para desenvolvedores

Esta seção aborda as diretrizes específicas para vários cenários de desenvolvimento importantes, bem como informações gerais sobre o desenvolvimento com este SDK. Os cenários nesta seção são específicos para esta versão do Rights Management Services SDK 2.1 e podem ser alterados em versões subsequentes.
- [Como fazer usar a autenticação de ADAL](how-to-use-adal-authentication.md) - autenticação com o Azure RMS para seu aplicativo usando o ADAL (Azure Active Directory Authentication Library).
- [Como adicionar direitos explícitos de proprietário](add-explicit-owner-rights.md) – seu aplicativo deve adicionar direitos de &quot;Proprietário&quot; explicitamente ao criar do zero uma licença ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [ Como depurar um aplicativo habilitado para direitos](debugging-applications-that-use-ad-rms.md) – este tópico a seguir mostra como depurar seu aplicativo e usar o Log de Eventos do Windows.
- [Como habilitar o rastreamento e a revogação de documentos](tracking-content.md) – este tópico aborda as diretrizes básicas para implementar o rastreamento de documentos do conteúdo e inclui um código de exemplo das atualizações metadados de e criar um botão **Acompanhar Uso** para seu aplicativo.
- [Como habilitar a notificação por email](how-to-enable-email-notification.md) - a notificação por email permite que um proprietário de conteúdo protegido seja notificado quando seu conteúdo for acessado.
- [Como habilitar o serviço de aplicativo para trabalhar com a nuvem com base em RMS](how-to-use-file-api-with-aadrm-cloud.md) - esse tópico descreve as etapas para configurar seu aplicativo de serviço para usar o Azure Rights Management.
- [Como instalar e configurar um Servidor RMS](how-to-install-and-configure-an-rms-server.md) – este tópico aborda as etapas de conexão a um Servidor RMS ou ao Azure RMS para testar seu aplicativo habilitado para direitos.
- [Como configurar o modo de segurança da API](setting-the-api-security-mode-api-mode.md) - você pode escolher em que modo de segurança seu aplicativo de API do arquivo é executado usando a função [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Como trabalhar com configurações de criptografia](working-with-encryption.md) - este tópico orienta você sobre nossos pacotes de criptografia e mostra alguns trechos de código para o uso desses pacotes.
- [Tipos de aplicativo](application-types.md) - este tópico aborda os tipos de aplicativos que você pode escolher criar como habilitados para direitos.
- [Configuração da API do arquivo](file-api-configuration.md) - o comportamento da API do arquivo pode ser configurado por meio das configurações no Registro.
- [Formatos de arquivo com suporte](supported-file-formats.md) - a API do arquivo dá suporte aos formatos pfile e nativo
- [Plataformas com suporte](supported-platforms.md): este tópico identifica as plataformas de cliente e servidor do RMS SDK 2.1 com suporte.
- [Noções básicas sobre restrições de uso](understanding-usage-restrictions.md) - todos os aplicativos habilitados para RMS devem impor restrições de uso.
- [Referência de restrição de uso](usage-restriction-reference.md) – as restrições de uso são definidas pelas constantes listadas neste tópico.

 
## Tópicos relacionados ##
* [Visão geral](ad-rms-overview.md)
 

 


<!--HONumber=Jun16_HO2-->


