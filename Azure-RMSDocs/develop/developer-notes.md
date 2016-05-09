---
# required metadata

title: Notas do desenvolvedor | Azure RMS
description: Este tópico aborda as diretrizes específicas para vários cenários de desenvolvimento importantes. 
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 65c2f3d1-0852-41fa-a95a-53dcec787680

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Notas do desenvolvedor

Esta seção aborda as diretrizes específicas para vários cenários de desenvolvimento importantes. Os cenários nesta seção são específicos para esta versão do Rights Management Services SDK 2.1 e podem ser alterados em versões subsequentes.

- [Adicionar direitos explícitos de proprietário](add-explicit-owner-rights.md) - seu aplicativo deve adicionar direitos de &quot;Proprietário&quot; explicitamente ao criar do zero uma licença ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [Condições de erro comuns e soluções](common-error-conditions-and-solutions.md) - as mensagens de erro mais comuns que você pode encontrar ao usar as ferramentas de desenvolvedor do RMS SDK 2.1.
- [Habilitando a notificação por email](how-to-enable-email-notification.md) - a notificação por email permite que um proprietário de conteúdo protegido seja notificado quando seu conteúdo for acessado.
- [Configuração da API do arquivo](file-api-configuration.md) - o comportamento da API do arquivo pode ser configurado por meio das configurações no Registro.
- [IPCHelloWorld - um aplicativo de exemplo](how-to-build-your-first-application.md) - este tópico contém instruções para criar um aplicativo de exemplo habilitado para direitos.
- [Configurando o modo de segurança da API](setting-the-api-security-mode-api-mode.md) - você pode escolher em que modo de segurança seu aplicativo de API do arquivo é executado usando a função [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Formatos de arquivo com suporte](supported-file-formats.md) - a API do arquivo dá suporte aos formatos pfile e nativo.
- [Acompanhando o conteúdo](tracking-content.md) - este tópico aborda as diretrizes básicas para implementar o rastreamento de documentos em conteúdo protegido com o RMS SDK 2.1.
- [Trabalhando com criptografia](working-with-encryption.md) - este tópico orienta você sobre nossos pacotes de criptografia e mostra alguns trechos de código para o uso desses pacotes.

 

## Tópicos relacionados ##
* [Visão geral](ad-rms-overview.md)
* [Como usar](how-to-use-msipc.md)
 

 


<!--HONumber=Apr16_HO3-->


