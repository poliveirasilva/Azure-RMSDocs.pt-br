---
# required metadata

title: Configuração do Visual Studio | Azure RMS
description: Instruções sobre como configurar um projeto do Visual Studio para usar o RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurar o Visual Studio

Este tópico contém instruções sobre como configurar um projeto do Visual Studio para usar o Rights Management Services SDK 2.1.

## Pré-requisitos

-   [Instalar o SDK](install-the-rms-sdk.md)

**Instruções**

### Etapa 1: configurar um projeto do Visual Studio para usar o RMS SDK 2.1

Essas instruções são específicas para o Microsoft Visual Studio 2010. Se você estiver usando uma versão diferente do Microsoft Visual Studio, suas caixas de diálogo de configurações poderão ser ligeiramente diferentes.

Essas instruções se aplicam à criação de um aplicativo nativo de 32 bits.

1.  Adicione o diretório de inclusão do RMS SDK 2.1 ao seu projeto do Visual Studio 2010.

    Em **Propriedades de Configuração** Selecione **Diretórios VC ++** e adicione o diretório de inclusão do RMS SDK 2.1, **$(MSIPCSDKDIR)\\inc**, no campo **Diretórios de Inclusão**.

    ![Configuração do campo de diretórios de inclusão de propriedades](../media/include_directories.png)

2.  Adicione o diretório da biblioteca do RMS SDK 2.1 ao seu projeto do Visual Studio 2010.

    Em **Propriedades de Configuração** Selecione **Diretórios VC ++** e adicione o diretório de biblioteca do RMS SDK 2.1, no campo **Diretórios de Biblioteca** da sua plataforma.

    -   Para Win32, use **$(MSIPCSDKDIR)\\lib**
    -   Para x64, use **$(MSIPCSDKDIR)\\lib\\x64**

    ![Configuração do campo de diretórios de biblioteca de propriedades](../media/library_directories.png)

3.  Adicione os arquivos da biblioteca do RMS SDK 2.1 como dependências do Visual Studio 2010.

    Em **Vinculador**, selecione **Entrada** e adicione os arquivos de biblioteca do RMS SDK 2.1; **Msipc.lib** e **Msipc\_s.lib**, no campo **Dependências Adicionais**.

    ![Campo de dependências de biblioteca do vinculador](../media/additional_dependencies.png)

4.  Adicione a DLL (Dynamic Link Library) do RMS SDK 2.1 como uma DLL carregada com atraso.

    Em **Vinculador**, selecione **Entrada**, e adicione o arquivo DLL do RMS SDK 2.1, **Msipc.dll**, no campo **Atrasar DLLs Carregadas**.

    ![Campo das bibliotecas carregadas com atraso do vinculador](../media/delay_loaded.png)

5.  Crie informações de versão para o binário resultante.

    Em **Gerenciador de Soluções** selecione **Arquivos de Recurso** e adicione seu nome binário ao campo **OriginalFileName**.

    ![Campo de arquivos de recurso do Gerenciador de Soluções](../media/original_file_name.png)

## Tópicos relacionados

* [Instalar o SDK](install-the-rms-sdk.md)
 

 


<!--HONumber=Jun16_HO2-->


