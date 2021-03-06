---
title: Como depurar um aplicativo habilitado para direitos | Azure RMS
description: "O tópico a seguir mostra como depurar seu aplicativo e usar o Log de Eventos do Windows."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 29e856e3e9990f81a791c533ddad5a332093d5d3
ms.openlocfilehash: c00ce9829ce4150cfef74ecd972450b3d787f312


---

# Como depurar um aplicativo habilitado para direitos

O tópico a seguir mostra como depurar seu aplicativo e usar o Log de Eventos do Windows.

## Depurando seu aplicativo

No Rights Management Services SDK 2.1, as verificações antidepuração na versão de desenvolvedor do nosso tempo de execução estão desabilitadas.

Você pode ativar o rastreamento de depuração usando a chave do Registro a seguir. (Para desligar o rastreamento de depuração, altere o valor para 0.) Não é necessário mais nada para depuração nesta versão.


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### Log de aplicativo usando o Log de Eventos do Windows

O nome do log de eventos é "Microsoft-RMS-MSIPC/Debug". Isso significa que, no Visualizador de Eventos do Windows, o log aparece como "Logs de Aplicativos e Serviços\\Microsoft\\RMS\\MSIPC\\Debug".

**Observação**  O log é habilitado por padrão e definido para o nível de detalhamento 3.

 

Para alterar as configurações do recurso de registro em log, você pode usar a interface do usuário do Visualizador de Eventos do Windows ou Wevtutil, uma ferramenta de linha de comando interna do Windows.

Por meio da interface Wevtutil, você pode controlar o nível de detalhamento de seu log.

Neste momento, damos suporte a 3 níveis de registro em log:

-   Nível 2 - Erro
-   Nível 3 - Aviso
-   Nível 4 - Informações

Por exemplo, o comando a seguir habilitará o log de eventos do MSIPC e definirá o nível de detalhamento para informações.

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**Observação**  No Visualizador de Eventos do Windows no menu **exibição**, selecione **Mostrar logs analíticos e de depuração** para tornar visível o log de depuração do MSIPC.

 

## Tópicos relacionados

 

 



<!--HONumber=Jun16_HO4-->


