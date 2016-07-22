---
title: "Procedimentos sobre como trabalhar com definições de encriptação | Azure RMS"
description: "Este artigo descreve os nossos pacotes de encriptação"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 29e856e3e9990f81a791c533ddad5a332093d5d3
ms.openlocfilehash: 82903eff43ee2dee7ef64e618171225a06013d99


---

# Procedimentos: trabalhar com definições de encriptação

Este tópico descreve os nossos pacotes de encriptação e mostra como é possível utilizar alguns recortes de código.

## Suporte para AES 256, a nova predefinição

Nenhum código adicional é necessário para utilizar a encriptação baseada em *AES 256*, dado que se trata da nova predefinição, partindo do princípio de que compila com o SDK RMS 2.1, atualização de março de 2015, ou posterior. Aconselhamo-lo a considerar a atualização das suas aplicações com esta versão devido às vantagens de segurança adicionais da *AES 256*.

> [!IMPORTANT]
> O suporte para consumo de ficheiros protegidos por *AES 256* já existia desde a [versão de outubro de 2014](release-notes-rtm.md). Se estiver a executar aplicações criadas com uma versão do SDK anterior à de outubro de 2014, esta atualização irá interromper a sua aplicação. Certifique-se de que os clientes das aplicações que está a criar estão a utilizar o SDK atualizado ou estão dispostos a atualizar imediatamente para a versão mais recente da aplicação.

 
## Suporte de encriptação de API

A partir da [atualização de março de 2015](release-notes-rtm.md), incorporamos os três sinalizadores seguintes na nossa API e nos respetivos pacotes de encriptação associados:

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (também conhecido como Algoritmos Preteridos)

Os sinalizadores de pacote de encriptação (consulte [**Encriptação Preferencial**](/rights-management/sdk/2.1/api/win/constants#msipc_preferred_encryption)) podem ser utilizados em conjunto com o nosso novo sinalizador de Propriedade da Licença **IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE**.

Seguem-se alguns fragmentos de código simples que demonstram como utilizar a nova propriedade de licença.

## Algoritmos Preteridos

Já não expomos o sinalizador **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** na nossa API. Isto significa que as aplicações futuras vão deixar de compilar se fizerem referência a este sinalizador, mas as aplicações já criadas que o utilizam vão continuar a funcionar, uma vez que respeitamos o sinalizador em privado no código de API.

Para aproveitar ainda as vantagens do sinalizador de algoritmos de encriptação preterido antigo, basta alterar um sinalizador. Consulte os seguintes fragmentos de código para obter exemplos.

## Proteger Ficheiros com AES 256 CBC4K

Não são necessárias alterações no código, *AES 256* CBC4K é a predefinição.

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## Proteger Ficheiros com AES 128 CBC4K

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## Proteger Ficheiros com AES-128 ECB (Algoritmos Preteridos)

Este exemplo mostra também a nova forma de suportar *algoritmos preteridos*.

    C++
    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);

 

 



<!--HONumber=Jun16_HO4-->


