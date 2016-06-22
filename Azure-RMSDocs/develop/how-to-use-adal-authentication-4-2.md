---
# required metadata

title: Usar o Portal do Azure para configurar para autenticação do RMS | Azure RMS
description: Descreve o processo de autenticação com ADAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como usar o Portal do Azure para configurar para autenticação do RMS

Autenticação com o Azure RMS para seu aplicativo usando o ADAL (Azure Active Directory Authentication Library).

Usar essa abordagem requer que seu aplicativo gerencie a própria autenticação OAuth. Com essa abordagem, o cliente RMS usará um retorno de chamada definido pelo aplicativo quando a autenticação for necessária.

## Configurar por meio do portal do Azure
Comece seguindo este guia para configurar por meio do portal do Azure, [Configurar o Azure RMS para autenticação de ADAL](adal-auth.md). Certifique-se de copiar e salvar a *ID do Cliente* e o *URI de Redirecionamento* desse processo para uso posterior.

## Exemplos de código
Aqui está uma captura de código do exemplo maior para o código de cliente móvel para habilitar o ADAL do Azure. Para obter mais informações, consulte o exemplo completo em [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## Tópicos relacionados

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [Configurar o Azure RMS para autenticação de ADAL](adal-auth.md)


<!--HONumber=Jun16_HO2-->


