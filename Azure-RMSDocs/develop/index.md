---
title: Guia do desenvolvedor do RMS | Azure RMS
description: "Agora, há três gerações do Rights Management SDK disponíveis."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0510ead4-2fe7-4269-885b-fe16bcc69888
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 6f8a475907347e545eb3ea46fecc04013fa74c5e


---

# Guia do desenvolvedor do RMS

## Visão geral ##
Três gerações do Rights Management SDK estão disponíveis: **Microsoft Rights Management SDK 4.2** para Android, iOS/OS X, dispositivos Windows e Linux, **Microsoft Rights Management SDK 2.1** para Windows Desktop Client e o **AD RMS SDK**, que foi substituído.

## Software Development Kits ##
| SDK | Descrição |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Um conjunto de ferramentas simplificado e de última geração, que fornece uma experiência de desenvolvimento leve para habilitar seus aplicativos de dispositivos Android, iOS, Mac OS X, Windows Phone/RT e Linux/C++ com proteção de informações por meio dos serviços Microsoft Rights Management |
| [SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) | Uma oferta de SDK poderosa para os desenvolvedores de aplicativos da área de trabalho do Windows e os provedores de soluções baseadas em servidor para habilitar seus produtos para o gerenciamento de direitos|
|[SDK do AD RMS]()|** OBSERVAÇÃO ** - O AD RMS SDK que aproveita a funcionalidade exposta pelo cliente em Msdrm.dll, está disponível para uso no Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 e Windows Vista. Ele poderá ser alterado ou ficar indisponível em versões subsequentes. Em seu lugar, use o Microsoft Rights Management Services SDK 2.1, que aproveita a funcionalidade exposta pelo cliente em Msipc.dll.|
|[API de scripts do AD RMS]()| Usada para criar scripts para administrar uma instalação do AD RMS|

## Exemplos de código e ferramentas ##
Esta coleção de exemplos de código do Microsoft RMS e ferramentas de suporte de desenvolvedor fornecidos abrange todos os sistemas operacionais com suporte: Android, iOS/OS X, Windows Phone e Windows Desktop; além disso, é atualizada periodicamente para manter a compatibilidade com o SDK ao qual dá suporte.

| Item | Sistema operacional | Suporte à versão do SDK | Descrição |
|------|------------------|------------------------|-------------|
| [Ler PDF protegido por arquivo PFILE](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) | Área de trabalho do Windows| [SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x | **Ler PDF protegido por arquivo PFILE** é um exemplo de código simples no nosso blog do Espaço do desenvolvedor RMS, que usa a API de arquivo MSIPC para descriptografar e abrir um documento PDF protegido por arquivo PFILE.|
| [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Área de trabalho do Windows | [SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x | **IpcManagedAPI** é uma representação do .NET (C#) do SDK 2.1 do RMS para facilitar a reabilitação do seu aplicativo gerenciado para RMS.|
| [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) | Área de trabalho do Windows | [SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x| **IPCNotepad** é um aplicativo de exemplo habilitado para RMS que o guiará durante as etapas básicas que cada aplicativo habilitado para RMS deve realizar para proteger e consumir conteúdo restrito.|
| [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms)|Área de trabalho do Windows|[SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x|**IpcDlp** é um aplicativo de exemplo de DPL (Proteção Contra Vazamento de Dados) habilitado para RMS que o guiará durante as etapas básicas que cada aplicativo habilitado para RMS deverá realizar para proteger e consumir conteúdo restrito.|
| [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Área de trabalho do Windows|[SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x|**IpcAzureApp** é um exemplo que demonstra como usar o RMS SDK no aplicativo do Azure para proteger os dados no Armazenamento de Blobs do Azure.|
| [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Área de trabalho do Windows|[SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x|**RmsDocumentInspector** é uma ferramenta que pode fornecer informações sobre qualquer arquivo RMS protegido, como ids de conteúdo ou direitos do usuário.|
| [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Área de trabalho do Windows|[SDK 2.1 do RMS](microsoft-information-protection-and-control-client-portal.md) e versões posteriores do SDK 2.x|**RmsFileWatcher** é um exemplo que demonstra como compilar um aplicativo do Windows que observa diretórios no sistema de arquivos e aplica as políticas de proteção por RMS a cada alteração, por exemplo, a cada arquivo adicionado ou modificado.|
| [Cenários de uso do iOS/OS X](https://msdn.microsoft.com/library/dn758307(v=vs.85).aspx) |iOS / OS X|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versões posteriores do SDK 4.x|Os exemplos de código em **Objective C** representam cenários importantes de desenvolvimento para você se acostumar ao RMS SDK. Exemplos incluem o uso do formato de Arquivo Protegido da Microsoft, formatos de arquivo protegidos personalizados e controles de interface do usuário personalizados.|
| [Aplicativo de exemplo e biblioteca de interface do usuário](https://github.com/AzureAD/rms-sdk-ui-for-ios) |iOS|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versões posteriores do SDK 4.x|**Aplicativo de exemplo e bibliotecas de interface do usuário para iOS** no GitHub, de modo que você possa começar rapidamente e reutilizar nossa interface do usuário padrão em seus aplicativos.|
| [Aplicativo de exemplo e biblioteca de interface do usuário](https://github.com/AzureAD/rms-sdk-ui-for-android) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versões posteriores do SDK 4.x|**Aplicativo de exemplo e bibliotecas de interface do usuário para Android** no GitHub, de modo que você possa começar rapidamente e reutilizar nossa interface do usuário padrão em seus aplicativos.|
| [Cenários de uso do Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versões posteriores do SDK 4.x|**Os exemplos de código em Java** representam cenários importantes de desenvolvimento para você se acostumar ao RMS SDK. Exemplos incluem o uso do formato de Arquivo Protegido da Microsoft, formatos de arquivo protegidos personalizados e controles de interface do usuário personalizados.|



<!--HONumber=Jul16_HO3-->


