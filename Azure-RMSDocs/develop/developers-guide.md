---
# required metadata

title: Guia do desenvolvedor | Azure RMS
description: Visão geral do uso de ferramentas de desenvolvedor; SDKs, bibliotecas adicionais e exemplos de código.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guia do desenvolvedor

## Visão geral ##
Três gerações do Rights Management SDK estão disponíveis: **Microsoft Rights Management SDK 4.2** para Android, iOS/OS X, dispositivos Windows e Linux, **Microsoft Rights Management SDK 2.1** para Windows Desktop Client e o **AD RMS SDK**, que foi substituído.

## Software Development Kits ##
| SDK | Descrição |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Um conjunto de ferramentas simplificado e de última geração, que fornece uma experiência de desenvolvimento leve para habilitar seus aplicativos de dispositivos Android, iOS, Mac OS X, Windows Phone/RT e Linux/C++ com proteção de informações por meio dos Microsoft Rights Management services |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Uma oferta de SDK poderosa para os desenvolvedores de aplicativos de área de trabalho do Windows e provedores de soluções baseadas em servidor para habilitar seus produtos para o gerenciamento de direitos|
|[SDK do AD RMS](https://msdn.microsoft.com/en-us/library/cc530379(v=vs.85).aspx)|** OBSERVAÇÃO ** - o AD RMS SDK, que aproveita a funcionalidade exposta pelo cliente em Msdrm.dll, está disponível para uso no Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 e Windows Vista. Ele poderá ser alterado ou ficar indisponível em versões subsequentes. Em seu lugar, use o Microsoft Rights Management Services SDK 2.1, que aproveita a funcionalidade exposta pelo cliente em Msipc.dll.|
|[API de Scripts do AD RMS](https://msdn.microsoft.com/en-us/library/bb968797(v=vs.85).aspx)| Usada para criar scripts para administrar uma instalação do AD RMS|

## Exemplos de código e ferramentas
Esta coleção de exemplos de código do Microsoft RMS e ferramentas de suporte developer fornecidos abrange todos os sistemas operacionais com suporte: Android, iOS/OS X, Windows Phone e Windows Desktop; além disso, é atualizada periodicamente para manter a compatibilidade com o SDK ao qual dá suporte.

### Android

Os itens relacionados a seguir são executados no Android com suporte pelo [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versões posteriores do SDK 4.x.

- [Aplicativo de exemplo e a biblioteca de interface do usuário](https://github.com/AzureAD/rms-sdk-ui-for-android) no GitHub, de modo que você possa começar rapidamente e reutilizar nossa interface do usuário padrão em seus aplicativos.
- [Cenários de uso do Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) em Java representam cenários de desenvolvimento importantes para você se acostumar com o RMS SDK. Exemplos incluem o uso do formato de Arquivo Protegido da Microsoft, formatos de arquivo protegidos personalizados e controles de interface do usuário personalizados.

### iOS/OS X

Os itens a seguir são executados em iOS/OS X com suporte pelo [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versões posteriores do SDK 4.x.

- [Cenários de uso do iOS/OS X](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) em Objective C representam cenários de desenvolvimento importantes para você se acostumar com o RMS SDK. Exemplos incluem o uso do formato de Arquivo Protegido da Microsoft, formatos de arquivo protegidos personalizados e controles de interface do usuário personalizados.
- [Aplicativo de exemplo e a biblioteca de interface do usuário](https://github.com/AzureAD/rms-sdk-ui-for-ios) no GitHub, de modo que você possa começar rapidamente e reutilizar nossa interface do usuário padrão em seus aplicativos. Com suporte **somente pelo iOS**.

### Área de trabalho do Windows

Os itens a seguir são executados no Windows Desktop com suporte pelo [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) e por versões posteriores do SDK 2.x.

- [Ler PDF protegido por arquivo PFILE](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) é um exemplo de código simples no nosso blog do Espaço do desenvolvedor RMS, que usa a API de arquivo MSIPC para descriptografar e abrir um documento PDF protegido por arquivo PFILE.
- [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) é uma representação do .NET (C#) do RMS SDK 2.1 para facilitar a habilitação do seu aplicativo gerenciado para RMS.
- [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) é um aplicativo de exemplo habilitado para RMS que o guiará durante as etapas básicas que cada aplicativo habilitado para RMS deve realizar para proteger e consumir conteúdo restrito.
- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) é um aplicativo de exemplo de DPL (Proteção Contra Vazamento de Dados) habilitado para RMS que o guiará durante as etapas básicas que cada aplicativo habilitado para RMS deverá realizar para proteger e consumir conteúdo restrito.
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) é um exemplo que demonstra como usar o RMS SDK no aplicativo do Azure para proteger os dados no Armazenamento de Blobs do Azure.
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) é uma ferramenta que pode fornecer informações sobre qualquer arquivo RMS protegido, como ids de conteúdo ou direitos do usuário.
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) é um exemplo que demonstra como compilar um aplicativo do Windows que observa diretórios no sistema de arquivos e aplica as políticas de proteção por RMS a cada alteração, por exemplo, a cada arquivo adicionado ou modificado.

### Windows Store e Windows Phone

- [Biblioteca de Interface do Usuário para Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) - uma biblioteca da interface do usuário para o Microsoft RMS SDK v4.1 para aplicativos da Windows Store. Essa biblioteca é opcional e um desenvolvedor pode optar por compilar sua própria interface do usuário ao usar o Microsoft RMS SDK v4.1

- [Biblioteca de Interface do Usuário para Windows Phone](https://github.com/AzureAD/rms-sdk-ui-for-winphone) - uma biblioteca da interface do usuário para o Microsoft RMS SDK v4.1 para aplicativos do Windows Phone. Essa biblioteca é opcional e um desenvolvedor pode optar por compilar sua própria interface do usuário ao usar o Microsoft RMS SDK v4.1

- [Aplicativo de exemplo](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore) - o exemplo do Microsoft RMS SDK v4.1 para aplicativos da Windows Store fornece um exemplo básico de consumo de documento para a plataforma.


<!--HONumber=Apr16_HO3-->


