---
# required metadata

title: Como adicionar direitos de proprietário explícitos | Azure RMS
description: Seu aplicativo deve adicionar explicitamente direitos de "Proprietário" ao criar uma licença do zero.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como adicionar direitos de proprietário explícitos

Seu aplicativo deve adicionar explicitamente direitos de "Proprietário" ao criar uma licença desde o início ([**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).

## Pré-requisitos

Quando seu aplicativo estiver criando um identificador de licença usando [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch), ele também deverá conceder o proprietário todos os direitos (permissões) explicitamente.

>[!NOTE] Configurar um usuário como "proprietário" usando [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) com a propriedade **IPC\_LI\_OWNER** não concede ao proprietário permissões completas.

O código de exemplo a seguir mostra somente as etapas envolvidas na criação e adição de direitos específicos para uma determinada licença.

## Instruções
 
## Etapa 1: Cenário de exemplo

Neste exemplo, direitos necessários são adicionados a uma licença criada com [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch). O exemplo mostra a criação e atribuição de direitos a licença por meio de uma lista de direitos.

Estes dois direitos são adicionados a esses usuários:

-   Permissões de *Leitura* atribuídas a joe@contoso.com
-   Permissões *Totais* atribuídas a mary\_kay@contoso.com

        // Create User Rights structure
        IPC_USER_RIGHTS ownerRightForOwner = {0};

        // Create rights
        LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure
        ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
        ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
        ownerRightForOwner.rgwszRights = rgwszOwnerRights;
        ownerRightForOwner.cRights = 1;

        // Create User Rights structure for Joe with Read permissions
        IPC_USER_RIGHTS joeReadRight = {0};
        LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

        // Assign values to members of Rights structure for Joe
        joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
        joeReadRight.User.wszID = "joe@contoso.com";
        joeReadRight.rgwszRights = rgwszReadRights;
        joeReadRight.cRights = 1;

        // Create User Rights structure for Mary Kay with Full permissions
        IPC_USER_RIGHTS mary_kayFullRight = {0};
        LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure for Mary Kay
        mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
        mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
        mary_kayFullRight.rgwszRights = rgwszFullRights;
        mary_kayFullRight.cRights = 1;

        // Create User Rights List and assign the above rights
        size_t uNoOfUserRights = 3;
        PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
        pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
        (new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

        if(pUserRightsList == NULL)
        {
          // Handle error
        }

        // Assign values to members of Rights List structure for Joe and Mary Kay
        (*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
        (*pUserRightsList).cUserRights = uNoOfUserRights;
        (*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
        (*pUserRightsList).rgUserRights[1] = joeReadRight;
        (*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

        // Set the Rights List property on the license via its handle
        // hLicense is a license handle created with IpcCreateLicenseFromScratch
        hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

        if(FAILED(hr))
        {
          // Handle the error
        }



## Tópicos relacionados

* [Notas do desenvolvedor](developer-notes.md)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
 

 


<!--HONumber=Jun16_HO2-->


