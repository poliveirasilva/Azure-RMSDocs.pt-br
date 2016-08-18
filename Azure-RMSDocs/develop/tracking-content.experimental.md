---
title: "Como habilitar o acompanhamento e a revogação de documentos | Azure RMS"
description: "Orientações básicas para implementar o acompanhamento de documento"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experiment_id: priyamo-test-20160729
translationtype: Human Translation
ms.sourcegitcommit: fe167a6bb22c4d07847ed1bbf390dd19aaada23a
ms.openlocfilehash: d3b343b8c1b28c47bb76171e032e9fffca3844c9


---

# Como habilitar o rastreamento e a revogação de documentos

Este tópico aborda as diretrizes básicas para implementar o rastreamento de documentos de conteúdo e inclui um código de exemplo de atualizações de metadados e de criação de um [**botão Acompanhar Uso**](#add-a-track-usage-button-to-your-app) para o aplicativo.

## Etapas para implementar o rastreamento de documentos

As etapas 1 e 2 permitem que o documento seja rastreado. A etapa 3 permite que os usuários de seu aplicativo acessem o site de rastreamento de documentos para rastrear e revogar seus documentos protegidos.

1. Adicionar metadados de rastreamento de documentos
2. Registrar o documento no serviço RMS
3. Adicionar o botão Acompanhar Uso ao seu aplicativo

Veja os detalhes de implementação para essas etapas.

## 1. Adicionar metadados de rastreamento de documentos

O rastreamento de documentos é um recurso do sistema do Rights Management. Ao adicionar metadados específicos durante o processo de proteção do documento, um documento pode ser registrado com o portal de serviço de acompanhamento que fornece várias opções para o rastreamento.

Use essas APIs para adicionar/atualizar uma licença de conteúdo com metadados de rastreamento de documentos.


Operacionalmente, somente as propriedades **nome do conteúdo** e o **tipo de notificação** são necessárias para o rastreamento de documentos.


- [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
- [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

  Esperamos que defina todas as propriedades de metadados. Aqui estão elas, listadas por tipo.

  Para obter mais informações, consulte [Tipos de propriedade de metadados de licença](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types).

  - **IPC_MD_CONTENT_PATH**

    Use para identificar o documento rastreado. Em casos nos quais um caminho completo não é possível, forneça apenas o nome do arquivo.

  - **IPC_MD_CONTENT_NAME**

    Use para identificar o nome do documento rastreado.

  - **IPC_MD_NOTIFICATION_TYPE**

    Use para especificar quando a notificação será enviada. Para obter mais informações, consulte Tipo de notificação.

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    Use para especificar o tipo de notificação. Para obter mais informações, consulte Preferência de notificação.

  - **IPC_MD_DATE_MODIFIED**

    Sugerimos que você defina essa data sempre que o usuário clicar em Salvar.

  - **IPC_MD_DATE_CREATED**

    Use para a definir a data de criação do arquivo

- [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

Use aquela adequada dentre estas APIs para adicionar os metadados para o arquivo ou fluxo.

- [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
- [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

Por fim, use essa API para registrar seu documento rastreado no sistema de rastreamento.

- [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)


## 2. Registrar o documento no serviço RMS

Aqui está um trecho de código que mostra um exemplo de configuração de metadados de rastreamento e a chamada a registrar com o sistema de rastreamento.

      C++
      HRESULT hr = S_OK;
      LPCWSTR wszOutputFile = NULL;
      wstring wszWorkingFile;
      IPC_LICENSE_METADATA md = {0};

      md.cbSize = sizeof(IPC_LICENSE_METADATA);
      md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
      md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
      //file origination date, current time for this example
      md.ftDateCreated = GetCurrentTime();
      md.ftDateModified = GetCurrentTime();

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

     /* This will contain the serialized license */
     PIPC_BUFFER pSerializedLicense;

     /* the context to use for the call */
     PCIPC_PROMPT_CTX pContext;

     wstring wstrContentName(“MyDocument.txt”);
     bool sendLicenseRegistrationNotificationEmail = FALSE;

     hr = IpcRegisterLicense( pSerializedLicense,
                        0,
                        pContext,
                        wstrContentName.c_str(),
                        sendLicenseRegistrationNotificationEmail);

## Adicionar um botão **Acompanhar Uso** ao seu aplicativo

Adicionar um item de interface do usuário para **Acompanhar Uso** ao seu aplicativo é tão simples quanto usar um dos seguintes formatos de URL:

- Usando a ID de Conteúdo
  - Obtenha a ID de conteúdo usando [IpcGetLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetlicenseproperty) ou [IpcGetSerializedLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetserializedlicenseproperty) se a licença for serializada e use a propriedade de licença **IPC_LI_CONTENT_ID**. Para saber mais, confira [Tipos de propriedade da licença](/rights-management/sdk/2.1/api/win/constants#msipc_license_property_types).
  - Com os metadados **ContentId** e **Issuer**, use o seguinte formato: `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    Exemplo: `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- Se não tiver acesso aos metadados (ou seja, se estiver examinando a versão desprotegida do documento), você poderá usar **Content_Name** no seguinte formato: `https://track.azurerms.com/#/?q={ContentName}`

  Exemplo - https://track.azurerms.com/#/?q=Secret!.txt

O cliente precisa apenas abrir um navegador com a URL apropriada. O portal de Rastreamento de Documentos do RMS cuida da autenticação e de qualquer redirecionamento necessário.

## Tópicos relacionados

* [Tipos de propriedade de metadados de licença](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)
* [Preferência de notificação](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [Tipo de notificação](/rights-management/sdk/2.1/api/win/constants#msipc_notification_type)
* [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

 



<!--HONumber=Jul16_HO5-->


