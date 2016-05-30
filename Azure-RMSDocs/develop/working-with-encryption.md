---
# required metadata

title: Trabalhando com criptografia | Azure RMS
description: orienta você para nossos pacotes de criptografia
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabalhando com criptografia

Este tópico orienta você sobre nossos pacotes de criptografia e mostra alguns trechos de código para o uso desses pacotes.

## Suporte a AES 256, o novo padrão

Nenhum código adicional é necessário para usar o *AES 256* baseado em criptografia visto que este é o novo padrão, supondo que você crie na atualização de março de 2015 ou posterior do RMS SDK 2.1. Incentivamos você a considerar seriamente atualizar seus aplicativos com esta versão para os benefícios de segurança adicionais do *AES 256*.

> [!IMPORTANT]
> O suporte para consumo de arquivos protegidos por *AES 256* existe desde a [versão de outubro de 2014](release-notes-rtm.md). Se você estiver executando aplicativos criados com uma versão do SDK anterior a outubro de 2014, essa atualização interromperá seu aplicativo. Verifique se os clientes dos aplicativos que você está compilando estão usando o SDK atualizado ou estão dispostos a atualizar imediatamente para a versão mais recente do seu aplicativo.

 
## Suporte à criptografia de API

Da [atualização de março de 2015](release-notes-rtm.md) em diante, nós incorporamos três sinalizadores em nossa API e seus pacotes de criptografia associados:

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (também conhecidos como algoritmos preteridos)

Os sinalizadores de pacote de criptografia, consulte [**Criptografia preferencial**](/rights-management/sdk/2.1/api/win/constants#msipc_preferred_encryption), podem ser usados em conjunto com nosso novo sinalizador de Propriedade de Licença **IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE**.

A seguir estão alguns trechos de código simples que demonstram como usar a nova propriedade de licença.

## Algoritmos preteridos

Não estamos mais expondo o sinalizador **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** na nossa API. Isso significa que aplicativos futuros não serão mais compilados se eles fizerem referência a esse sinalizador, mas os aplicativos já compilados utilizando-o continuarão a funcionar, já que respeitamos o sinalizador em particular no código de API.

Ainda é possível obter o benefício do sinalizador de algoritmos de criptografia antigo preterido simplesmente alterando um sinalizador. Consulte os trechos de código a seguir para um exemplo.

## Proteger arquivos com AES 256 CBC4K

Nenhuma alteração no código necessária, *AES 256* CBC4K é o padrão.

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    

## Proteger arquivos com AES-128 CBC4K

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    
    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K; 
    
    hr = IpcSetLicenseProperty(pLicenseHandle, 
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);
    

## Proteger arquivos com o AES-128 ECB (algoritmos preteridos)

Este exemplo também mostra a nova maneira de dar suporte a *algoritmos preteridos*.

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    
    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;
    
    hr = IpcSetLicenseProperty(pLicenseHandle, 
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE, 
                           &amp;dwEncryptionMode);
    
 

 





<!--HONumber=May16_HO2-->


