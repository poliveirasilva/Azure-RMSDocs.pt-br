---
# required metadata

title: Utilize o Portal do Azure para configurar a autenticação RMS | Azure RMS
description: Descreve o processo para a autenticação com a ADAL
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

# Procedimentos: utilize o Portal do Azure para configurar a autenticação RMS

Autenticação com o Azure RMS para a sua aplicação com o ADAL (Azure Active Directory Authentication Library).

Utilizar esta abordagem requer que a aplicação efetue a gestão da sua própria autenticação OAuth. Com esta abordagem, o cliente RMS irá exercer uma chamada de retorno definida pela aplicação quando a autenticação for necessária.

## Configurar através do portal do Azure
Comece por seguir este guia para configurar através do portal do Azure, [Configurar o Azure RMS para a autenticação da ADAL](adal-auth.md). Certifique-se de que copia e guarda o *ID de cliente* e o *URI de Redirecionamento* a partir deste processo para uma utilização posterior.

## Exemplo de código
Eis um recorte de código do maior exemplo para o código de cliente móvel para ativar o ADAL do Azure. Para obter mais informações, consulte o exemplo completo em [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)

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
- [Configurar o Azure RMS para a autenticação ADAL](adal-auth.md)


<!--HONumber=Jun16_HO2-->


