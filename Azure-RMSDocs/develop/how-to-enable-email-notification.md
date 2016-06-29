---
# required metadata

title: Ativar notificação por e-mail | Azure RMS
description: A notificação por e-mail permite que um proprietário de conteúdo protegido seja notificado quando o respetivo conteúdo for acedido.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedimentos: ativar notificação por e-mail

A notificação por e-mail permite que um proprietário de conteúdo protegido seja notificado quando o respetivo conteúdo for acedido.

Para configurar a notificação por e-mail para uma determinada licença, utilize [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) com o parâmetro de tipo de propriedade *dwPropID* como [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA) e os campos de dados da aplicação formatados como [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list).

    C++

    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {&quot;MS.Conetent.Name&quot;, 0, &quot;FinancialReport.docx&quot;};
    propertyValuePairs[1] = {&quot;MS.Notify.Enabled&quot;,0 , &quot;true&quot;};
    propertyValuePairs[2] = {&quot;MS.Notify.Culture&quot;,0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
        

A tabela seguinte contém os campos de dados da aplicação, o nome da propriedade e os pares de valor para a notificação por e-mail do RMS.


|Nome da Propriedade | Tipo de Dados | Valor de Exemplo | Notas |
|--------------|-----------|---------------|-------|
|MS.Content.Name|cadeia|“FinancialReport.docx”|Este é um identificador associado ao conteúdo protegido.<br><br> Para ficheiros protegidos, este valor deverá ser o nome do ficheiro sem quaisquer informações de caminho.<br><br> Para outros tipos de conteúdo, tal como uma mensagem de e-mail, poderá ser o assunto do e-mail ou poderá estar vazio.|
|MS.Notify.Enabled|cadeia|“true” &#124; “false”|Se este valor for definido como “true”, será enviado um e-mail de notificação para o proprietário da licença de publicação quando alguém tenta utilizá-la para obter uma licença de utilizador final.|
|MS.Notify.Culture|cadeia|“pt-PT”| **Origem:** System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>Este valor é utilizado para determinar o idioma localizado do e-mail de notificação e a formatação de números e data/hora que devem ser utilizados na mensagem de e-mail.<br><br>Deve ser definido com base nas definições do utilizador do computador no qual a licença publicada é criada ou com base na cultura preferencial do proprietário da licença publicada.|
|MS.Notify.TZID|cadeia|“Hora Padrão do Pacífico”|**Origem:** TimeZoneInfo.Local.Id – ID de fuso horário do Windows.<br><br>Este valor é o identificador de fuso horário do sistema operativo do Microsoft Windows que descreve um fuso horário específico e as respetivas caraterísticas.|
|MS.Notify.TZO|cadeia|“-480”|Este é o desvio de fuso horário do proprietário da licença publicada em termos de minutos da hora UTC.<br><br>Se um valor de TZID válido for fornecido, o desvio do fuso horário especificado pelo mesmo será utilizado e este valor será ignorado.<br><br>O mais provável é que este valor seja utilizado por plataformas de publicação não baseadas no Windows que não têm acesso à lista de valores de ID de fuso horário do sistema operativo Windows.<br><br>Se um valor TZID não for fornecido, este valor será utilizado para calcular o desvio do tempo nas mensagens de notificação e o TZSN será utilizado (independentemente do valor de fuso horário) para indicar o nome do fuso horário. Isto fará com que o fuso horário seja fixo e não atualize para a hora de verão quando for aplicável.<br><br>Por exemplo:<br><br>Se TXID estiver em branco, TZ0 estiver definido como “-420” e TZSN estiver definido como “Hora de Verão do Pacífico”, todos os valores apresentados no e-mail de notificação serão ajustados para “Hora de Verão do Pacífico” e apresentados como tal, mesmo que a hora de Verão já não esteja atualmente em vigor.<br><br>Por outro lado, se um TZID for fornecido juntamente com TZSN e TZDN, as horas especificadas no e-mail de notificação serão ajustadas e apresentadas com base na apresentação da data e hora no Modo de verão ou Modo padrão.|
|MS.Notify.TZSN|cadeia|“Hora Padrão do Pacífico”|**Origem:** TimeZoneInfo.Local.StandardName – nome do Fuso Horário Padrão.<br><br>Isto deve ser o nome localizado do nome do fuso horário padrão do fuso horário.|
|MS.Notify.TZDN|cadeia|“Hora de Verão do Pacífico”|**Origem:** TimeZoneInfo.Local.DaylightName – nome do Fuso Horário de Verão.<br><br>Isto deve ser o nome localizado do nome da hora de verão do fuso horário. Pode ser igual ao nome padrão se o fuso horário não suportar a hora de verão.|

## Tópicos relacionados

* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
* [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)
* [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)
 

 


<!--HONumber=Jun16_HO2-->


