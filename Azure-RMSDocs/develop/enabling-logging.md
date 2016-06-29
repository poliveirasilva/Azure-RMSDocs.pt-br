---
# required metadata

title: Como&#58; ativar registo de erros e de desempenho | Azure RMS
description: O SDK Microsoft Rights Management 4.2 gere o carregamento de registos de diagnóstico e de desempenho através de uma propriedade de único dispositivo.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como: ativar registo de erros e de desempenho
O SDK Microsoft Rights Management 4.2 gere o carregamento de registos de diagnóstico e de desempenho através de uma propriedade de único dispositivo.

## Descrição Geral ##
Pode melhorar a experiência dos seus utilizadores e a resolução de problemas ao ativar o carregamento de diagnósticos automáticos e do registo de desempenho para a Microsoft. Para honrar a privacidade do utilizador, na qualidade de programador da aplicação, deve pedir consentimento ao utilizador antes de ativar o registo automático.

Irá gerir o controlo de registo através de duas propriedades.

-   Ative o registo através da propriedade **IpcCustomerExperienceDataCollectionEnabled**. A definição resiste às reposições do dispositivo.
-   Controle o nível de registo através da propriedade **IpcLogLevel** ao utilizar as seguintes definições.

    * 1 – Verboso
    * 2 – Informativo
    * 3 – Aviso
    * 4 – Erro
    * 5 – Crítico

Em cada um dos fragmentos de código de exemplo que se seguem, a aplicação de chamada pode definir ou consultar a propriedade.

### Android ###
Ativar o registo automático

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Obter a definição atual do sinalizador de controlo de registo

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
Ativar o registo automático

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

Obter a definição atual do sinalizador de controlo de registo

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

Definir o controlo do nível de registo

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

Obter a definição de controlo do nível de registo

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## Windows ##
Ativar o registo automático

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Para obter mais informações sobre definições opcionais, consulte [CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions).

Obter a definição atual do sinalizador de controlo de registo

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Nota** – Os recortes de código Windows acima são em C++. Para C\#, atualize a sintaxe com ‘.’ em vez de ‘::’.

**Linux/C++** – Este SDK possui algum registo básico que não é tão extensivo como o de outras plataformas. Para mais informações, consulte a secção **Resolução de problemas** do “LEIAME.md” em [SDK RMS para Portable C++](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

 

 


<!--HONumber=Apr16_HO4-->


