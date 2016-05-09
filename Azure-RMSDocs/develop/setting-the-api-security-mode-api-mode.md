---
# required metadata

title: Configurando o modo de segurança de API | Azure RMS
description: Escolha o modo de segurança em que o seu aplicativo de API de arquivo é executado.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b3acfcd5-1af5-4f3a-912b-962198c59103

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
# Configurando o modo de segurança de API

Você pode escolher em que modo de segurança seu aplicativo de API do arquivo é executado usando a função [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

Para inicializar o aplicativo para que seja executado no *modo de servidor*, chame a função [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) e defina o modo de segurança como [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER). Por padrão, o aplicativo será executado *modo cliente*, **IPC\_API\_MODE\_CLIENT**.

Para obter mais informações sobre *modo de servidor*, consulte [Tipos de aplicativos](application-types.md).

**Importante**  O modo de segurança deve ser definido antes que qualquer outra função do Rights Management Services SDK 2.1 seja chamada. Depois que o modo de segurança tiver sido definido, ele não pode ser alterado para o processo atual.

 

### Tópicos relacionados

* [Tipos de aplicativo](application-types.md)
* [Conceitos de desenvolvedor](ad-rms-concepts-nav.md)
* [**Valores do modo de API**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 





<!--HONumber=Apr16_HO3-->


