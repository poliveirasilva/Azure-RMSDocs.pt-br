---
# required metadata

title:
How-to: install, configure and test with an RMS server | Azure RMS
description: Install and configure and RMS Sever for testing your rights-enabled application.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como instalar, configurar e testar com um Servidor RMS

Este tópico aborda as etapas de conexão a um Servidor RMS ou ao Azure RMS para testar seu aplicativo habilitado para direitos.
 
## Instruções

### Etapa 1: Configurar seu servidor RMS

As etapas a seguir orientarão você pela configuração de seu servidor RMS e incluem:

-   Instalação do servidor
-   Registro do servidor

1.  **Instalação do servidor**

    O Active Directory Rights Management Services (AD RMS) é composto por componentes de servidor e de cliente separados. O componente de servidor é implementado como um conjunto de serviços Web que podem ser usados para administrar uma infraestrutura de RMS, emitir licenças para os consumidores e editores de conteúdo e emitir certificados para computadores e usuários.

    A partir do Windows Server 2008, os componentes de cliente e de servidor estão incluídos no sistema operacional. Você pode baixar os componentes do servidor para sistemas operacionais mais antigos no seguinte local.

    -   [RMS Server v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Para configurar o componente de servidor no Windows Server 2008, você deve instalar a função AD RMS. Se você estiver desenvolvendo aplicativos com base em um sistema operacional mais antigo, configure o Registro após a instalação do servidor RMS v1.0 SP2, mas antes de provisionar o serviço RMS.

2.  **Registro do servidor**

    Você deve registrar um servidor RMS (Rights Management Services) para identificá-lo na Hierarquia de pré-produção ou de produção. O processo de registro deixa um certificado de licenciante para servidor no computador do servidor. Esse certificado é associado a uma raiz de confiança da Microsoft. O modo como você registra o servidor depende de qual versão do RMS você está usando.

    -   **Autorregistro**

        A partir do Windows Server 2008, você pode registrar um servidor RMS na hierarquia apropriada sem enviar informações à Microsoft. Quando você instala a função RMS, um certificado de autorregistro e uma chave privada também são instalados. Eles são usados para criar automaticamente o certificado de licenciante para servidor. Nenhuma informação é trocada com a Microsoft.

    -   **Registro online**

        Se você estiver usando o AD RMS v 1.0 SP2, poderá registrar o servidor online. O registro ocorre em segundo plano durante o processo de provisionamento, mas você precisa ter uma conexão com a Internet.

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **Teste com o Servidor RMS**

    Para fazer testes com um Servidor RMS, configure a descoberta no lado do servidor ou a descoberta no lado do cliente para permitir que o Rights Management Service Client 2.1 descubra e estabeleça a comunicação com o Servidor RMS.

    >[OBSERVAÇÃO] Testar com o Azure RMS não requer configuração de descoberta.

  - Na descoberta do lado do servidor, um administrador registra um ponto de conexão de serviço (SCP) para o cluster RMS raiz com o Active Directory, e o cliente consulta o Active Directory para descobrir o SCP e estabelecer uma conexão com o servidor.
  - Na descoberta no lado do cliente, você define as configurações de Descoberta do Serviço RMS no Registro no computador no qual o RMS Client 2.1 está em execução. Essas configurações apontam o RMS Client 2.1 para uso do servidor RMS. Quando estiverem presentes, a descoberta no lado do servidor não será executada.

  Para configurar a descoberta no lado do cliente, você pode definir as seguintes chaves do Registro para apontarem para seu Servidor RMS. Para saber mais sobre como configurar a descoberta no lado do serviço, confira [Notas de implantação do RMS Client 2.0](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx).

1. **EnterpriseCertification**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterpriseCertification

  **Valor**: (padrão): [**http|https**]://RMSClusterName/**_wmcs/Certification**

2. **EnterprisePublishing**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterprisePublishing **Value**: (Default): [**http|https**]://RMSClusterName/**_wmcs/Licensing**

>[!NOTE] Por padrão, essas chaves não existem no Registro e devem ser criadas.

>[!IMPORTANT] Se você estiver executando um aplicativo de 32 bits em uma versão de 64 bits do Windows, defina essas chaves no seguinte local de chave:<p>
  ```    
  HKEY_LOCAL_MACHINE
    SOFTWARE
      Wow6432Node
        Microsoft
          MSIPC
            ```

 

 


<!--HONumber=Jun16_HO2-->


