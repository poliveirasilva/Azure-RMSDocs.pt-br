---
# required metadata

title: Tipos de aplicações | Azure RMS
description: Este tópico inclui os tipos de aplicações que pode escolher para criar com capacidade para direitos.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Tipos de aplicações


Este tópico inclui os tipos de aplicações que pode escolher para criar com capacidade para direitos.

Os tipos de aplicações que se seguem são atualmente suportados pelo SDK Rights Management Services 2.1

## Aplicações simples

Uma aplicação simples pode ser uma ferramenta de linha de comandos criada para encriptar um ficheiro fornecido. Para obter um exemplo de uma aplicação simples e com capacidade para direitos, consulte [IPCHelloWorld – uma aplicação de exemplo](how-to-build-your-first-application.md).

### Aplicações de modo de servidor

O *modo de servidor* destina-se às aplicações não interativas que consomem, protegem ou processam conteúdo protegido por RMS. Um exemplo seria uma aplicação de *Prevenção de Perda de Dados* que é executada como um serviço num servidor de ficheiros e protege automaticamente documentos confidenciais. Consulte o [Exemplo de IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d) para obter um exemplo deste tipo de aplicação.

Se a sua aplicação utilizar o *modo de servidor*, deve autenticar para o servidor do RMS silenciosamente. Ao contrário do *modo de cliente*, o SDK RMS 2.1 não irá abrir um pedido de credenciais quando não conseguir autenticar silenciosamente. Além disso, quando executar no *modo de servidor*, não é necessário nenhum manifesto de aplicação.

Para obter mais informações sobre a definição do modo de segurança da API, consulte [Definir o modo de segurança de API](setting-the-api-security-mode-api-mode.md).

### Aplicações de clientes avançados

Uma aplicação de cliente avançado permite que os utilizadores visualizem e manipulem dados através de uma interface gráfica (GUI). Os dados apresentados nesta GUI são frequentemente de elevado valor e passíveis de roubo ou exposição acidental. O suporte para proteção de informações normalmente melhora os cenários existentes; no entanto, não é a motivação primária para o desenvolvimento da aplicação.

Utilizar o SDK RMS 2.1 com aplicações de cliente avançado ajuda-o a:

-   Garantir que estes dados são sempre encriptados.

-   Impedir que os utilizadores extraiam dados num formato não protegido (por exemplo, impedir a utilização da área de transferência para copiar e colar).

O Bloco de Notas da Microsoft é uma aplicação simples de cliente avançado. O Microsoft Office é uma aplicação de cliente avançado mais complexa.

Para obter mais informações acerca de como proteger a sua aplicação, consulte [Compreender as restrições de utilização](understanding-usage-restrictions.md).

## Tópicos relacionados

* [Exemplo de IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
* [IPCHelloWorld – uma aplicação de exemplo](how-to-build-your-first-application.md)
* [Definir o modo de segurança de API](setting-the-api-security-mode-api-mode.md)
* [Compreender as restrições de utilização](understanding-usage-restrictions.md)


<!--HONumber=Jun16_HO2-->


