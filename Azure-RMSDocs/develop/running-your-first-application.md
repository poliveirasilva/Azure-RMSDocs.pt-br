---
# required metadata

title: Testar seu aplicativo habilitado para direitos | Azure RMS
description: Descreve as etapas que precisam ser concluídas para testar seu aplicativo habilitado para direitos do RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 43b611a8-2cc0-49a8-9db9-e81321c38f7a

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
# Testar seu aplicativo habilitado para direitos

Este tópico descreve as etapas que precisam ser concluídas para testar seu aplicativo habilitado para direitos do Rights Management Services SDK 2.1.

Para publicar e consumir conteúdo protegido, um aplicativo do RMS (Rights Management Services) usa vários tipos diferentes de certificados e licenças, cada uma delas composta por uma cadeia de certificados que leva, em última análise, a uma autoridade de certificação da Microsoft. A Microsoft fornece as seguintes hierarquias:

-   A hierarquia de Pré-produção pode ser usada para desenvolver e testar aplicativos.
-   A hierarquia de Produção deve ser usada por aplicativos lançados

Recomendamos o uso da hierarquia de Pré-produção ao desenvolver um aplicativo. Ao fazer isso, você pode trabalhar sem assinar um Contrato de Licença de Produção com a Microsoft.

> [!IMPORTANT]
> É uma prática recomendada testar seu aplicativo do RMS SDK 2.1 primeiro com o ambiente de pré-produção do RMS no servidor RMS. Em seguida, caso deseje que seu cliente tenha a capacidade de usar o aplicativo com o serviço do Azure RMS, teste com esse ambiente. Para obter mais informações, veja [Habilite seu aplicativo de serviço para funcionar com o RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

 

### Pré-requisitos

-   Uma configuração de ambiente de desenvolvimento do RMS SDK 2.1. Para saber mais, confira [Configuração do ambiente de desenvolvimento de pré-produção](how-to-set-up-the-pre-production-development-environment.md)
-   Para obter um exemplo de aplicativo, confira [IPCHelloWorld - um de exemplo aplicativo](how-to-build-your-first-application.md).

Instruções

### Etapa 1:

Criar e compilar um aplicativo habilitado para direitos Consulte a seção Pré-requisitos acima para conhecer as opções.

### Etapa 2: Gerar um manifesto de aplicativo usando a cadeia de certificados de pré-produção

Você deve gerar um manifesto para seu aplicativo antes de executá-lo.

**Observação** Se o seu aplicativo usar o modo de API do servidor (**IPC\_API\_MODE\_SERVER**), não será necessário usar um manifesto de aplicativo. Você pode testar o aplicativo em um servidor de produção do AD RMS sem precisar obter uma licença de produção ao alternar para o ambiente de produção. Para saber mais sobre aplicativos no modo de servidor, confira [Tipos de aplicativos](application-types.md).

 

Esse processo também é conhecido como assinar seu aplicativo. Você pode gerar o manifesto usando uma cadeia de certificados de produção ou a cadeia de certificados de pré-produção que é instalada com o SDK. Recomendamos o uso da cadeia de certificados de pré-produção durante o desenvolvimento.

Para saber mais sobre chaves e cadeias de certificados, confira [Noções básicas sobre cadeias de certificados](understanding-certificate-chains.md).

Para saber mais sobre como assinar um aplicativo com uma cadeia de certificados de produção, veja [Como alternar para o ambiente de produção](switching-to-the-production-environment.md).

Para gerar o manifesto do aplicativo usando a cadeia de certificados de pré-produção, execute estas etapas no computador de desenvolvimento:

1.  Copie os seguintes arquivos de seus diretórios de instalação para a mesma pasta que o seu aplicativo.

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\NomeDoSeuAplic.isv.mcf

2.  Na pasta de seu aplicativo, renomeie o arquivo de configuração do manifesto, NomeDoSeuAplic.isv.mcf, com o nome de seu aplicativo com a extensão de nome de arquivo .mcf anexada. Por exemplo se o seu aplicativo chamar MeuAplic.exe, renomeie NomeDoSeuAplic.isv.mcf para MeuAplic.exe.mcf.

3.  Use um editor de texto para adicionar o aplicativo ao arquivo de configuração do manifesto. Para fazer isso, substitua o texto de espaço reservado &lt;NomeDoSeuAplicativo&gt;.exe na lista de módulos em seu arquivo .mcf pelo nome de seu aplicativo; por exemplo, MeuAplic.exe.

    O processo de assinatura gerará um erro se o arquivo .mcf for usado sem modificação.

4.  Execute Genmanifest.exe para gerar o manifesto do aplicativo. Isso também é conhecido como assinar seu aplicativo. A saída dessa operação deve ser um arquivo .man. Por exemplo, se o seu aplicativo chamar MeuAplic.exe e seu arquivo de configuração de manifesto chamar MeuAplic.exe.mcf, execute o seguinte comando:

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MeuAplic.exe.mcf MeuAplic.exe.man**

### Etapa 3: Executar seu aplicativo

Você pode executar o aplicativo de qualquer diretório, mas o manifesto do aplicativo (MeuAplic.exe.man) deve estar no mesmo diretório que o executável (MeuAplic.exe).

-   **Como usar o Ambiente de uma caixa do RMS**

    Se você estiver usando o ambiente de uma caixa do RMS para testar seu aplicativo, copie o executável do aplicativo e o manifesto do aplicativo para qualquer diretório no ambiente de uma caixa e, depois, execute o aplicativo.

    Para saber mais sobre o ambiente de uma caixa do RMS, confira [Configurar o ambiente de teste](how-to-set-up-your-test-environment.md).

-   **Como usar uma configuração de servidor de pré-produção**

    Se você estiver testando seu aplicativo em um servidor RMS configurado para pré-produção, configure o Active Directory Rights Management Services Client 2.1 no computador onde o aplicativo será executado; por exemplo, no computador de desenvolvimento. Em seguida, certifique-se de que o executável do aplicativo e o manifesto do aplicativo estejam no mesmo diretório no computador e execute o aplicativo.

    Para saber mais sobre como configurar o cliente, veja [Configuração do cliente](how-to-configure-the-ad-rms-client-2-0.md) Para saber mais sobre como instalar um servidor RMS, veja [Instalação e configuração do servidor](how-to-install-and-configure-an-rms-server.md).

### Tópicos relacionados

* [Como usar](how-to-use-msipc.md)
* [Configuração do cliente](how-to-configure-the-ad-rms-client-2-0.md)
* [Instalação e configuração do servidor](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - um exemplo de aplicativo](how-to-build-your-first-application.md)
* [Configurando o ambiente de desenvolvimento de pré-produção](how-to-set-up-the-pre-production-development-environment.md)
* [Alternando para o ambiente de produção](switching-to-the-production-environment.md)
* [Configurar o ambiente de teste](how-to-set-up-your-test-environment.md)
* [Noções básicas sobre cadeias de certificados](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


