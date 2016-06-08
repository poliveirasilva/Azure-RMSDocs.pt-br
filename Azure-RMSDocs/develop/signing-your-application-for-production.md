---
# required metadata

title: Assinando o aplicativo para produção | Azure RMS
description: Este tópico orienta você pelo processo de assinatura do aplicativo para o modo de produção.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 09BA148C-7D1E-43C8-92EA-24BBB6EFDB19
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
# Assinando o aplicativo para produção

Este tópico orienta você pelo processo de assinatura do aplicativo para o modo de produção.

## Assinar seu aplicativo habilitado para direitos

Essas etapas pressupõem que você já tenha assinado o seu aplicativo para uma hierarquia de pré-produção. Se você ainda não fez isso, percorra o processo descrito em [Testar seu aplicativo habilitado para direitos](running-your-first-application.md).

Depois de ter recebido o certificado de produção da Microsoft, você tem os seguintes arquivos com você:

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

Coloque-os no mesmo diretório que *GenManifest.exe* e o seu binário do aplicativo (.exe).

-   O processo abaixo conduz você pela criação de um novo arquivo MCF com certificado de produção:

    -   Crie um novo diretório e coloque arquivos nesse novo diretório. Use Notepad.exe para criar um arquivo MCF para seu aplicativo. O arquivo deve ter o conteúdo a seguir.

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   Execute o comando a seguir para assinar seu aplicativo:

        **genmanifest.exe -chain ProductionCertificate.xml** *NomeDoSeuAplicativo***.mcf** *NomeDoSeuAplicativo***.exe.man**

        Se Genmanifest for bem-sucedida, você verá apenas o seguinte texto:

        Se Genmanifest falhar, você verá uma mensagem de erro.

    -   O *NomeDoSeuAplicativo*.exe.man sempre deve ser colocado no mesmo diretório que *NomeDoSeuAplicativo*.exe.

## Tópicos relacionados

* [Como usar](how-to-use-msipc.md)
* [Testando seu aplicativo habilitado para direitos](running-your-first-application.md)
 

 





<!--HONumber=Jun16_HO1-->


