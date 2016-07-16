---
title: Como&#58; habilitar o log de desempenho e de erro | Azure RMS
description: "O Microsoft Rights Management SDK 4.2 gerencia o upload de logs de desempenho e de diagnóstico por meio da propriedade de um único dispositivo."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79e58b8092ea7cb057229d4c464d79f3694296e6
ms.openlocfilehash: 5faea360de8aa9ecb82abf25b5c1392d52d0afad


---

# Como: habilitar o log de desempenho e de erro
O Microsoft Rights Management SDK 4.2 gerencia o upload de logs de desempenho e de diagnóstico por meio da propriedade de um único dispositivo.

## Visão geral ##
Você pode melhorar a experiência de seus usuários e solução de problemas habilitando o diagnóstico automático e o upload do log de desempenho para a Microsoft. Para respeitar a privacidade do usuário, você, como o desenvolvedor do aplicativo, deve solicitar o consentimento do usuário antes de habilitar o registro em log automático.

Você gerenciará o controle de log por meio de duas propriedades.

-   Habilite o registro em log por meio da propriedade **IpcCustomerExperienceDataCollectionEnabled**. A configuração é persistente entre reinicializações do dispositivo.
-   Controlar o nível de log por meio da propriedade **IpcLogLevel** usando as configurações a seguir.

    * 1 - Detalhado
    * 2 - Informativo
    * 3 - Aviso
    * 4 - Erro
    * 5 - Crítico

Em cada um dos trechos de código de exemplo a seguir, o aplicativo de chamada pode definir ou consultar a propriedade.

### Android ###
Habilitar registro em log automático

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Obter a configuração do sinalizador de controle de log atual

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
Habilitar registro em log automático

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

Obter a configuração do sinalizador de controle de log atual

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

Definir o controle de nível de log

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

Obter configuração de controle de nível de log

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## Windows ##
Habilitar registro em log automático

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Para obter mais informações sobre as configurações opcionais, consulte [CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions).

Obter a configuração do sinalizador de controle de log atual

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Observação** - os trechos de código do Windows acima estão em C++. Para C\#, atualize a sintaxe com ‘.’ em vez de ‘::’.

**Linux/C++** - este SDK tem algum registro em log básico que não é tão grande quanto o encontrado em outras plataformas. Para obter mais informações, consulte a seção **Solução de problemas** de "README.md" no [RMS SDK para C++ móvel](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

 

 



<!--HONumber=Jun16_HO4-->


