---
title: Configurar o Visual Studio | Azure RMS
description: "Instruções sobre como configurar um projeto do Visual Studio para utilizar o SDK RMS 2.1."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 872bb0c20db2ef8d661d321598a2b1fe61d69316
ms.openlocfilehash: 9747c39742c66735b9619036cb77a914563ecf29


---

# Configurar o Visual Studio

Este tópico contém instruções sobre como configurar um projeto do Visual Studio para utilizar o SDK Rights Management Services 2.1.

## Pré-requisitos

-   [Instalar o SDK](install-the-rms-sdk.md)

**Instruções**

### Passo 1: configurar um projeto do Visual Studio para utilizar o SDK RMS 2.1

Estas instruções são específicas para o Microsoft Visual Studio 2010. Se estiver a utilizar uma versão diferente do Microsoft Visual Studio, as caixas de diálogo das definições podem ter um aspeto ligeiramente diferente.

Estas instruções aplicam-se à criação de uma aplicação de 32 bits nativa.

1.  Adicione o diretório de inclusão do SDK RMS 2.1 ao projeto do Visual Studio 2010.

    Em **Propriedades de Configuração**, selecione **VC++ Directories** e adicione o diretório de inclusão do SDK RMS 2.1, **$(MSIPCSDKDIR)\\inc** ao campo **Incluir Diretórios**.

    ![Campo de diretórios de inclusão das propriedades de configuração](../media/include_directories.png)

2.  Adicione o diretório de bibliotecas do SDK RMS 2.1 ao projeto do Visual Studio 2010.

    Em **Propriedades de Configuração**, selecione **VC++ Directories** e adicione o diretório de bibliotecas do SDK RMS 2.1 ao campo **Biblioteca de Diretórios** da sua plataforma.

    -   Para o Win32, utilize **$(MSIPCSDKDIR)\\lib**
    -   Para o x64, utilize **$(MSIPCSDKDIR)\\lib\\x64**

    ![Campo de diretórios de bibliotecas das propriedades de configuração](../media/library_directories.png)

3.  Adicione os ficheiros de biblioteca do SDK RMS 2.1 como dependências do Visual Studio 2010.

    Em **Linker**, selecione **Entrada** e adicione os ficheiros de biblioteca do SDK RMS 2.1 **Msipc.lib** e **Msipc\_s.lib** ao campo **Dependências Adicionais**.

    ![Campo de dependências da biblioteca do linker](../media/additional_dependencies.png)

4.  Adicione o ficheiro DLL (Dynamic-Link Library) do SDK RMS 2.1 como um DLL carregado com atraso.

    Em **Linker**, selecione **Entrada** e adicione o ficheiro DLL do SDK RMS 2.1 **Msipc.dll** ao campo **DLL Carregado com Atraso**.

    ![Campo de bibliotecas carregadas com atraso do linker](../media/delay_loaded.png)

5.  Crie informações da versão para o binário resultante.

    Em **Explorador de Soluções**, selecione **Ficheiros de Recurso** e adicione o nome binário ao campo **NomeFicheiroOriginal**.

    ![Campo de ficheiros de recurso do explorador de soluções](../media/original_file_name.png)

## Tópicos relacionados

* [Instalar o SDK](install-the-rms-sdk.md)
 

 



<!--HONumber=Jun16_HO4-->


