---
# required metadata

title: Configuração do cliente | Azure RMS
description: Instruções sobre como configurar o Active Directory Rights Management Services Client 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58051d42-5a0a-4b65-9e02-bcdbf17d3262

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
# Configuração do cliente

Este tópico contém instruções sobre como configurar o Active Directory Rights Management Services Client 2.1.

**Importante** Se você testar seu aplicativo executando-o no ambiente ISV do RMS de uma caixa, não será necessário configurar o AD RMS Client 2.1. Para saber mais, confira [Testar seu aplicativo habilitado para direitos](running-your-first-application.md).

 

### Pré-requisitos

-   Você deve ter o AD RMS Client 2.1 instalado no computador no qual você testará seu aplicativo.

    -   Se você for testar seu aplicativo no computador de desenvolvimento, você já deve ter instalado o Rights Management Services SDK 2.1. O AD RMS Client 2.1 já terá sido instalado silenciosamente.

        Para saber mais sobre como instalar o SDK 2.1 do RMS, confira [Instalação do SDK](create-your-first-rights-aware-application.md).

    -   Se você for testar seu aplicativo em um computador diferente do computador de desenvolvimento, instale o AD RMS Client 2.1 no computador a partir da [página de download do AD RMS Client 2.1](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
        **Observação** Se o seu aplicativo usar o modo de API do servidor (**IPC\_API\_MODE\_SERVER**), não será necessário usar um manifesto de aplicativo. Você pode testar o aplicativo em um servidor de produção RMS sem precisar obter uma licença de produção ao alternar para o ambiente de produção. Para saber mais sobre aplicativos no modo de servidor, confira [Tipos de aplicativos](application-types.md).

         

-   Você deve ter um servidor RMS instalado e configurado para trabalhar no ambiente de pré-produção. Para saber mais, confira [Instalação e configuração do servidor](how-to-install-and-configure-an-rms-server.md).

Instruções

### Etapa 1: Como configurar o RMS Client 2.1 para a hierarquia de certificados de pré-produção

As etapas a seguir descrevem como instalar o tempo de execução do desenvolvedor, configurar o cliente a fim de usar a hierarquia de certificados do ISV (pré-produção) e configurar a descoberta de serviços no cliente.

1.  Copie o tempo de execução do desenvolvedor, Ipcsecproc\_isv.dll, from %MSIPCSDKDIR%\\bin\\x86 (para versões de 32 bits do Windows) ou %MSIPCSDKDIR\\bin\\x64 (para versões de 64 bits do Windows), em C:\\Arquivos de Programas\\Active Directory Rights Management Services Client 2.1.

    **Importante** Se você estiver executando um aplicativo de 32 bits em uma versão de 64 bits do Windows, copie Ipcsecproc\_isv.dll from %MSIPCSDKDIR%\\bin\\x86 para C:\\Arquivos de Programas(x86)\\Active Directory Rights Management Services Client 2.1.

     

2.  Configure o AD RMS Client 2.1 a fim de usar a hierarquia de certificados de ISV (pré-produção), definindo o valor da chave do Registro **Hierarchy** como 1.

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    **Observação** Sem o valor de **Hierarchy** presente no Registro é o mesmo, funcionalmente, a ter seu valor definido como 0 (zero), o que significa que o SDK 2.1 do RMS operará no modo de produção. Para saber mais sobre chaves e cadeias de certificados, confira [Noções básicas sobre cadeias de certificados](understanding-certificate-chains.md).

    **Importante**  
    Se você estiver executando um aplicativo de 32 bits em uma versão de 64 bits do Windows, defina o valor de **Hierarchy** no seguinte local de chave:

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  Configure a descoberta no lado do servidor ou a descoberta no lado do cliente para permitir que o AD RMS Client 2.1 descubra e estabeleça a comunicação com o servidor RMS de pré-produção.

    -   Na descoberta do lado do servidor, um administrador registra um ponto de conexão de serviço (SCP) para o cluster RMS raiz de pré-produção com o Active Directory, e o cliente consulta o Active Directory para descobrir o SCP e estabelecer uma conexão com o servidor.
    -   Na descoberta no lado do cliente, você define as configurações de Descoberta do Serviço RMS no Registro no computador no qual o AD RMS Client 2.1 está em execução. Essas configurações apontam o AD RMS Client 2.1 para uso do servidor RMS. Quando estiverem presentes, a descoberta no lado do servidor não será executada.

    Para configurar a descoberta no lado do cliente, você pode definir as seguintes chaves do Registro para apontarem para seu servidor RMS de pré-produção. Para saber mais sobre como configurar a descoberta no lado do serviço, confira [Notas de implantação do RMS Client 2.0](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx).

|Chave|Valor|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|(Padrão):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Certification**|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|(Padrão):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Licensing**|


**Observação**  Por padrão, essas chaves não existem no Registro e devem ser criadas.
     
**Importante**  
    Se você estiver executando um aplicativo de 32 bits em uma versão de 64 bits do Windows, defina essas chaves no seguinte local de chave:


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### Comentários

As diretrizes neste tópico não são abrangentes. Para saber mais sobre como configurar a o AD RMS Client 2.1, confira [RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx) (Notas de implantação do RMS Client 2.1).

### Tópicos relacionados


* [Como usar](how-to-use-msipc.md)
* [Notas de Implantação do RMS Client 2.0](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [Instalar o SDK](create-your-first-rights-aware-application.md)
* [Instalação e configuração do servidor](how-to-install-and-configure-an-rms-server.md)
* [Testar seus aplicativos habilitados para direitos](running-your-first-application.md)
* [Noções básicas sobre cadeias de certificados](understanding-certificate-chains.md)
 

 


<!--HONumber=Apr16_HO3-->


