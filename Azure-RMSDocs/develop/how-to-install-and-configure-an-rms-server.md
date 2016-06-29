---
# required metadata

title: Procedimentos para instalar, configurar e testar com um servidor RMS | Azure RMS
description: Instale e configure e Servidor RMS para testar a sua aplicação com capacidade para direitos.
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

# Procedimentos: instalar, configurar e testar com um servidor RMS

Este tópico inclui os passos para ligação a um servidor RMS ou ao Azure RMS para fins de testar da sua aplicação com permissão para direitos.
 
## Instruções

### Passo 1: configurar o servidor RMS

Os seguintes passos descrevem a configuração do servidor RMS e incluem:

-   Instalar o servidor
-   Inscrever o servidor

1.  **Instalar o servidor**

    Os Serviços de Gestão de Direitos do Active Directory (AD RMS) são compostos por componentes de cliente e servidor separados. O componente de servidor é implementado como um conjunto de serviços Web que podem ser utilizados para administrar uma infraestrutura de RMS, emitir licenças para consumidores e publicadores de conteúdo e emitir certificados para computadores e utilizadores.

    A partir do Windows Server 2008, os componentes de cliente e servidor estão incluídos no sistema operativo. Pode transferir os componentes de servidor para sistemas operativos anteriores a partir da seguinte localização.

    -   [Servidor RMS v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Para configurar o componente de servidor no Windows Server 2008, tem de instalar a função de AD RMS. Se estiver a desenvolver aplicações num sistema operativo do servidor anterior, configure o registo após a instalação do RMS Server v1.0 SP2, mas antes do aprovisionamento do serviço RMS.

2.  **Inscrever o servidor**

    Tem de inscrever um servidor dos Serviços de Gestão de Direitos (RMS) para o identificar na hierarquia de Pré-produção ou de Produção. O processo de inscrição deixa um certificado de licenciante para servidor no computador do servidor. Este certificado encadeia novamente para uma raiz de fidedignidade da Microsoft. O modo como inscreve o servidor depende da versão RMS que está a utilizar.

    -   **Autoinscrição**

        A partir do Windows Server 2008, é possível inscrever um servidor RMS na hierarquia adequada sem enviar informações à Microsoft. Ao instalar a função de RMS, um certificado de autoinscrição e a chave privada também são instalados. Estes são utilizados para criar automaticamente o certificado de licenciante para servidor. Nenhuma informação é trocada com a Microsoft.

    -   **Inscrição online**

        Se estiver a utilizar o AD RMS v1.0 SP2, pode inscrever o servidor online. A Inscrição decorre em segundo plano durante o processo de aprovisionamento, mas tem de ter uma ligação à Internet.

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **Teste com o RMS Server**

    Para efetuar testes com um servidor RMS, configure a deteção do lado do servidor ou do lado do cliente para permitir que o Rights Management Service Client 2.1 detete e estabeleça comunicação com o seu servidor RMS.

    > [!Note] Os testes com o Azure RMS não necessitam de configuração de deteção.

  - Na deteção do lado do servidor, um administrador regista um ponto de ligação de serviço (SCP) para o cluster de raiz RMS com o Active Directory e o cliente consulta o Active Directory para detetar o SCP e estabelecer uma ligação com o servidor.
  - Na deteção do lado do cliente, configura as definições de Deteção do Serviço RMS no registo do computador onde está a executar o RMS Client 2.1. Estas definições apontam o RMS Client 2.1 para o servidor RMS a utilizar. Quando estiverem presentes, a deteção do lado do servidor não é efetuada.

  Para configurar a deteção do lado do cliente, pode definir as seguintes chaves de registo para que apontem para o servidor RMS. Para obter informações sobre como configurar a deteção do lado do serviço, consulte as [Notas de Implementação do RMS Client 2.0](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx).

1. **EnterpriseCertification**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterpriseCertification

  **Value**: (Predefinição): [**http|https**]://RMSClusterName/**_wmcs/Certification**

2. **EnterprisePublishing**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterprisePublishing **Value**: (Predefinição): [**http|https**]://RMSClusterName/**_wmcs/Licensing**

>[!NOTE] Por predefinição, estas chaves não existem no registo e têm de ser criadas.

>[!IMPORTANT] Se estiver a executar uma aplicação de 32 bits numa versão de 64 bits do Windows, tem de definir estas chaves na seguinte localização da chave:<p>
  ```    
  HKEY_LOCAL_MACHINE
    SOFTWARE
      Wow6432Node
        Microsoft
          MSIPC
            ```

 

 


<!--HONumber=Jun16_HO2-->


