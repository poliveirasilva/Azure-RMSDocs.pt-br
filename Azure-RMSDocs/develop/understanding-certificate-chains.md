---
# required metadata

title: Noções básicas sobre cadeias de certificados | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 14694cb0-adc4-4c2f-aff5-22aa132777df

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Noções básicas sobre cadeias de certificados

Desenvolvendo um aplicativo habilitado para direitos requer um par de chaves públicas e uma cadeia de certificados que leve de volta a um certificado da Microsoft na raiz de confiança.

## Tipos de certificado

Cada licença e o certificado usados em um ambiente do RMS (Rights Management Services) consistem em uma cadeia de certificados que leva de volta para um certificado de AC (autoridade de certificação) da Microsoft. A Microsoft fornece duas cadeias nas quais uma licença ou certificado pode ser aninhado, uma cadeia de certificados de pré-produção e uma cadeia de produção. É recomendável que você use a hierarquia de pré-produção ao desenvolver um aplicativo para que você possa trabalhar sem assinar um *Contrato de licença de produção* com a Microsoft. Observe que o servidor RMS também deve ser configurado para pré-produção.

Você deve alternar para uma cadeia de produção antes de lançar seu aplicativo. O conteúdo protegido por um certificado de pré-produção é menos seguro do que aquele protegido por um certificado de produção.

As chaves públicas e privadas e o certificado de pré-produção são incluídos no SDK nos arquivos a seguir, localizados na pasta `%MsipcSDKDir%\Bin`.

- **ISVTier5AppSigningPrivKey.dat** contém a chave privada usada para assinar um manifesto para uso durante o desenvolvimento de aplicativo.
- **ISVTier5AppSigningPubKey.dat** contém a chave pública conectada à hierarquia do certificado de pré-produção.
- **ISVTier5AppSignSDK_Client.xml** contém o certificado de pré-produção usado para gerar um manifesto para uso durante o desenvolvimento de aplicativo.

 

Você usa o certificado e a chave privada para criar e assinar um manifesto que identifica os arquivos que podem ou devem ser carregados no espaço de processo de seu aplicativo, e aqueles que não devem ser carregados. O manifesto, em seguida, é carregado pela plataforma.

Independentemente de você ter usado um certificado de pré-produção durante o desenvolvimento de aplicativos, quando você estiver pronto para lançar o aplicativo, deverá gerar um novo par de chaves, adquirir um certificado de produção da Microsoft e usar a nova chave particular e o certificado para criar e assinar um manifesto de aplicativo.

Para obter mais informações sobre como trabalhar com cadeias de certificados e a assinatura de aplicativos, consulte [Alternando para o ambiente de produção](switching-to-the-production-environment.md).

### Tópicos relacionados

* [Conceitos de desenvolvedor](ad-rms-concepts-nav.md)
* [Alternando para o ambiente de produção](switching-to-the-production-environment.md)
 

 


<!--HONumber=Apr16_HO3-->


