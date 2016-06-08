---
# required metadata

title: Instalação e configuração do servidor | Azure RMS
description: Instale e configure o servidor RMS para testar seu aplicativo habilitado para direitos.
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
** Este conteúdo do SDK não é atual. Por um curto período, encontre a [versão atual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) da documentação no MSDN. **
# Instalar e configurar o servidor

Este tópico aborda as etapas de instalação e configuração do servidor RMS para testar seu aplicativo habilitado para direitos.

**Importante** Se você estiver testando seu aplicativo por meio da execução no ambiente ISV do RMS de uma caixa, não será necessário instalar um Servidor RMS, pois já existe um instalado e configurado no ambiente de uma caixa.
Para saber mais sobre o ambiente ISV do AD RMS de uma caixa, confira [Configurar o ambiente de teste](how-to-set-up-your-test-environment.md).

 

## Instruções

### Etapa 1: Configurar seu servidor RMS

As etapas a seguir orientarão você pela configuração de seu servidor RMS e incluem:

-   Configuração do Registro
-   Instalação do servidor
-   Registro do servidor

1.  **Configuração do Registro**

    Para especificar que você está usando a hierarquia de certificados de pré-produção, defina os seguintes valores do Registro.

    **Observação** Se você estiver usando o Windows Server 2008 R2 ou o Windows Server 2008, defina os valores do Registro antes de instalar o serviço AD RMS.

    Se você estiver usando o AD RMS no Windows Server 2008 R2, será necessário definir o valor **REG\_DWORD** a seguir. Altere esse valor para 0 (zero) a fim de alternar para a hierarquia de produção.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    Se você estiver usando o AD RMS no Windows Server 2008 R2 e outro serviço AD RMS já estiver implantado no Active Directory como um serviço de pré-produção, adicione o seguinte valor de cadeia de caracteres vazia ao Registro.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    Se você estiver usando o AD RMS no Windows Server 2008, será necessário definir o valor **REG\_DWORD** a seguir. Altere esse valor para 0 (zero) a fim de alternar para a hierarquia de produção.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    Se você estiver usando o AD RMS no Windows Server 2008 e outro serviço AD RMS já estiver implantado no Active Directory como um serviço de pré-produção, adicione o seguinte valor de cadeia de caracteres vazia ao Registro.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **Instalação do servidor**

    O Active Directory Rights Management Services (AD RMS) é composto por componentes de servidor e de cliente separados. O componente de servidor é implementado como um conjunto de serviços Web que podem ser usados para administrar uma infraestrutura de RMS, emitir licenças para os consumidores e editores de conteúdo e emitir certificados para computadores e usuários.

    A partir do Windows Server 2008, os componentes de cliente e de servidor estão incluídos no sistema operacional. Você pode baixar os componentes do servidor para sistemas operacionais mais antigos no seguinte local.

    -   [RMS Server v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Para configurar o componente de servidor no Windows Server 2008, você deve instalar a função AD RMS. No entanto, antes de fazer isso, configure o Registro para especificar que você usará a Hierarquia de certificados de pré-produção, em vez de a Hierarquia de produção. Se, entretanto, você estiver desenvolvendo aplicativos com base em um sistema operacional mais antigo, configure o Registro após a instalação do servidor RMS v1.0 SP2, mas antes de provisionar o serviço RMS.

    Para saber mais, consulte a etapa anterior, Etapa 1, "Configuração do Registro".

3.  **Registro do servidor**

    Você deve registrar um servidor RMS (Rights Management Services) para identificá-lo na Hierarquia de pré-produção ou de produção. O processo de registro deixa um certificado de licenciante para servidor no computador do servidor. Esse certificado é associado a uma raiz de confiança da Microsoft. O modo como você registra o servidor depende de qual versão do RMS você está usando.

    -   **Autorregistro**

        A partir do Windows Server 2008, você pode registrar um servidor RMS na hierarquia apropriada sem enviar informações à Microsoft. Quando você instala a função RMS, um certificado de autorregistro e uma chave privada também são instalados. Eles são usados para criar automaticamente o certificado de licenciante para servidor. Nenhuma informação é trocada com a Microsoft.

    -   **Registro online**Se você estiver usando o AD RMS v 1.0 SP2, poderá registrar o servidor online. O registro ocorre em segundo plano durante o processo de provisionamento, mas você deve ter uma conexão com a Internet e especificar o valor apropriado do Registro para identificar em qual hierarquia você está registrando o servidor. Para registrar-se na Hierarquia de pré-produção, adicione o valor **REG\_SZ** a seguir e provisione o servidor. Para registrar-se na Hierarquia de produção, limpe esse valor e provisione o servidor.

        Para saber mais, consulte a etapa anterior, Etapa 1, "Configuração do Registro".

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

## Tópicos relacionados

* [Como usar](how-to-use-msipc.md)
 

 





<!--HONumber=Jun16_HO1-->


