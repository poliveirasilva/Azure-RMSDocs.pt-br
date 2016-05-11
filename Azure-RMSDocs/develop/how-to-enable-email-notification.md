---
# required metadata

title: Habilitar a notificação por email | Azure RMS
description: A notificação por email permite que um proprietário de conteúdo protegido seja notificado quando seu conteúdo for acessado.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: fcaa5643-64a9-4181-b29b-90211fce7ab5

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
# Habilitar a notificação por email

A notificação por email permite que um proprietário de conteúdo protegido seja notificado quando seu conteúdo for acessado.

Para configurar a notificação por email para uma licença determinada, use [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) com o parâmetro de tipo de propriedade, *dwPropID*, como [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA) e os campos de dados de aplicativo formatados como [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list).

## C++

    ...
    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {&quot;MS.Conetent.Name&quot;, 0, &quot;FinancialReport.docx&quot;};
    propertyValuePairs[1] = {&quot;MS.Notify.Enabled&quot;,0 , &quot;true&quot;};
    propertyValuePairs[2] = {&quot;MS.Notify.Culture&quot;,0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
    ...    

A tabela a seguir contém os campos de dados do aplicativo, pares de nome e valor da propriedade, para notificação por email do RMS.


|Nome da propriedade | Tipo de dados | Exemplo de valor | Anotações |
|--------------|-----------|---------------|-------|
|MS.Content.Name|cadeia de caracteres|"FinancialReport.docx"|Esse é um identificador associado ao conteúdo protegido.<br><br> Para arquivos protegidos, esse valor deve ser o nome do arquivo sem qualquer informação de caminho.<br><br> Para outros tipos de conteúdo, como uma mensagem de email, pode ser o assunto do email ou pode estar vazio.|
|MS.Notify.Enabled|cadeia de caracteres|“true” &#124; “false”|Se esse valor for definido como "true", uma notificação de email será enviado ao proprietário da licença de publicação quando alguém tentar usá-la para obter uma licença de usuário final.|
|MS.Notify.Culture|cadeia de caracteres|“pt-BR”| **Fonte:** System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>Esse valor é usado para determinar o idioma localizado do email de notificação, e a data/hora e a formatação de número que devem ser usadas na mensagem de email.<br><br>Ele deve ser definido com base nas configurações do usuário da máquina na qual a licença de publicação será criada, ou com base na cultura preferencial do proprietário da licença de publicação.|
|MS.Notify.TZID|cadeia de caracteres|“Hora padrão do Pacífico”|**Fonte:** TimeZoneInfo.Local.Id - ID do fuso horário do Windows.<br><br>Esse valor é o identificador de fuso horário do sistema operacional Microsoft Windows, descrevendo um determinado fuso horário e suas características.|
|MS.Notify.TZO|cadeia de caracteres|“-480”|Esse é o deslocamento de fuso horário do proprietário de licença de publicação em relação aos minutos da hora UTC.<br><br>Se um valor válido de TZID for fornecido, o deslocamento do fuso horário especificado por ele será usado e este valor será ignorado.<br><br>Há uma probabilidade muito grande de esse valor ser usado por plataformas de publicação que não são baseadas no Windows e que não têm acesso à lista de valores de ID de fuso horário do sistema operacional Windows.<br><br>Caso um valor de TZID não seja fornecido, esse valor será usado para calcular o deslocamento de tempo em mensagens de notificação, e o TZSN será usado (independentemente do valor de fuso horário) para indicar o nome do fuso horário. Isso resultará em um fuso horário fixo, sem uma atualização para o horário de verão quando for aplicável.<br><br>Por exemplo:<br><br>Se o TXID estiver em branco, e o TZ0 for definido como "-420", e o TZSN for definido como "Horário de Verão do Pacífico", todos os valores mostrados no email de notificação serão ajustados para "Horário de Verão do Pacífico" e exibidos dessa forma, mesmo se o horário de verão não estiver mais em vigor no momento.<br><br>Por outro lado, se um TZID for fornecido junto com o TZSN e o TZDN, as horas especificadas no email de notificação serão ajustadas e exibidas com base na exibição da data e hora no modo Horário de verão ou Padrão.|
|MS.Notify.TZSN|cadeia de caracteres|“Hora padrão do Pacífico”|**Fonte:** TimeZoneInfo.Local.StandardName - Nome do fuso horário padrão.<br><br>Esse deve ser o nome localizado do fuso horário padrão.|
|MS.Notify.TZDN|cadeia de caracteres|"Horário de Verão do Pacífico"|**Fonte:** TimeZoneInfo.Local.DaylightName - Nome do Fuso horário de verão.<br><br>Esse deve ser o nome localizado do horário de verão do fuso horário. Pode ser igual ao nome padrão, se o fuso horário não oferecer suporte ao horário de verão.|

## Tópicos relacionados

* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
* [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)
* [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)
 

 


<!--HONumber=Apr16_HO3-->


