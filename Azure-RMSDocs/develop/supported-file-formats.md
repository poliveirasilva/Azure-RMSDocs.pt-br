---
# required metadata

title: Formatos de arquivo com suporte | Azure RMS
description: A versão atual da API do arquivo dá suporte à proteção nativa para arquivos do Microsoft Office, PDF e proteção PFile para todos os outros formatos de arquivo.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Este conteúdo do SDK não é atual. Por um curto período, encontre a [versão atual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) da documentação no MSDN. **
# Formatos de arquivo com suporte

A API do arquivo dá suporte aos formatos nativo e Pfile.

## Formatos de arquivo com suporte

A versão atual da API do arquivo dá suporte à proteção nativa para arquivos do Microsoft Office, arquivos PDF e proteção PFile para todos os outros formatos de arquivo. Arquivos PDF podem, opcionalmente, ter a proteção PFile aplicada.

-   **Proteção nativa**. Proteção nativa, o arquivo é criptografado para um formato de arquivo AD RMS baseado em seu tipo MIME (extensão de nome de arquivo). Arquivos que são protegidos nativamente usando a API do arquivo são consistentes com o formato esperado por aplicativos habilitados para AD RMS que usam proteção nativa; por exemplo, Office 2010, Office 2013 e leitor de PDF FoxIt. A proteção nativa tem suporte apenas em arquivos do Office, arquivos PDF e um número seleto de outros tipos de arquivo. Para obter mais informações sobre os tipos de arquivo nos quais há suporte para proteção nativa, consulte [Configuração da API do arquivo](file-api-configuration.md).
-   **Proteção PFile**. Na proteção PFile, os arquivos são criptografados usando o formato PFile (Arquivo Protegido) AD RMS. O arquivo está criptografado em um arquivo com a extensão. pfile. Proteção por PFile tem suporte para todos os formatos de arquivo, exceto arquivos do Office.

Os administradores podem definir chaves do Registro para configurar se e como os arquivos devem ser protegidos com base em sua extensão de nome de arquivo. Para obter mais informações sobre como configurar a proteção de arquivo ao usar a API do arquivo, consulte [Configuração da API do arquivo](file-api-configuration.md).

## Tópicos relacionados

* [Notas do desenvolvedor](developer-notes.md)
* [Configuração da API do arquivo](file-api-configuration.md)
 

 





<!--HONumber=Jun16_HO1-->


