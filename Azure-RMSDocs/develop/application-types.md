---
# required metadata

title: Tipos de aplicativos | Azure RMS
description: Este tópico aborda os tipos de aplicativos que você pode escolher criar como habilitado para direitos.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 749146d4-a49d-47dc-a43a-d37d96310e18

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Tipos de aplicativo


Este tópico aborda os tipos de aplicativos que você pode escolher criar como habilitado para direitos.

Os seguintes tipos de aplicativo têm suporte no momento no Rights Management Services SDK 2.1

## Aplicativos simples

Um aplicativo simples pode ser uma ferramenta de linha de comando criada para criptografar um arquivo fornecido. Para obter um exemplo de um aplicativo simples habilitado para direitos, consulte [IPCHelloWorld - um de aplicativo de exemplo](how-to-build-your-first-application.md).

### Aplicativos de modo de servidor


*Modo de servidor* é destinado para aplicativos não interativos que consomem, protegem ou processam o conteúdo protegido por RMS. Um exemplo seria um aplicativo de *Prevenção de Perda de Dados* executado como um serviço em um servidor de arquivos e que protege automaticamente documentos confidenciais. Consulte o [exemplo de IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d) para obter um exemplo desse tipo de aplicativo.

Se seu aplicativo usar o *modo de servidor*, ele deverá autenticar para o servidor RMS silenciosamente. Diferente do *modo cliente*, o RMS SDK 2.1 não abrirá uma solicitação de credenciais quando falhar em autenticar silenciosamente. Além disso, quando executado no *modo de servidor*, não é necessário nenhum manifesto do aplicativo.

Para obter mais informações sobre como definir o modo de segurança de API, consulte [Configurando o modo de segurança de API](setting-the-api-security-mode-api-mode.md).

### Aplicativos cliente avançado

Um aplicativo cliente avançado permite aos usuários exibir e manipular dados por meio de uma GUI (interface gráfica do usuário). Normalmente, os dados apresentados nessa GUI têm alto valor e são sensível a roubo ou exposição acidental. O suporte à proteção de informações normalmente aprimora cenários existentes, mas não é a principal motivação para desenvolver o aplicativo.

Usar o RMS SDK 2.1 com aplicativos cliente avançados ajuda a:

-   Certificar-se de que esses dados estejam sempre criptografados.

-   Impedir que os usuários extraiam dados para um formato desprotegido (por exemplo, impeça o uso da área de transferência para copiar e colar).

O Bloco de Notas da Microsoft é um aplicativo cliente avançado simples. O Microsoft Office é um aplicativo cliente avançado mais complexo.

Para obter mais informações sobre como proteger seu aplicativo, consulte [Noções básicas sobre restrições de uso](understanding-usage-restrictions.md).

### Tópicos relacionados

* [Conceitos de desenvolvedor](ad-rms-concepts-nav.md)
* [Exemplo de IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
* [IPCHelloWorld - um aplicativo de exemplo](how-to-build-your-first-application.md)
* [Configurando o modo de segurança de API](setting-the-api-security-mode-api-mode.md)
* [Noções básicas sobre restrições de uso](understanding-usage-restrictions.md)
 

 





<!--HONumber=Apr16_HO3-->


