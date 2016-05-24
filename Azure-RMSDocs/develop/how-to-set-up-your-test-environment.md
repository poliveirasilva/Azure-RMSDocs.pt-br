---
# required metadata

title: Configuração do ambiente de teste | Azure RMS
description: O aplicativo habilitado para direitos pode ser testado com diferentes opções de servidor.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurar o ambiente de teste

O aplicativo habilitado para direitos pode ser testado com diferentes opções de servidor.

**Importante**: é uma prática recomendada testar seu aplicativo do Rights Management Services SDK 2.1 primeiro com o ambiente de pré-produção do AD RMS no servidor de AD RMS. Em seguida, caso deseje que seu cliente tenha a capacidade de usar o aplicativo com o serviço do Azure RMS, teste com esse ambiente. Para obter mais informações, veja [Habilite seu aplicativo de serviço para funcionar com o RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

 

### Pré-requisitos

-   [Instalar o SDK](create-your-first-rights-aware-application.md)

Instruções

### Etapa 1: configure seu ambiente de teste

Para testar seu aplicativo habilitado para direitos, você deve executá-lo em um servidor RMS configurado para pré-produção. Um servidor RMS de pré-produção usa a hierarquia de pré-produção/certificados ISV para criptografar e descriptografar arquivos.

Para obter mais informações sobre a hierarquia de certificados do AD RMS, consulte [Noções básicas sobre cadeias de certificados](understanding-certificate-chains.md).

Há duas opções disponíveis para testar seu aplicativo em um servidor RMS:

-   **Você pode executar seu aplicativo no ambiente do AD RMS ISV de uma caixa**. Se você estiver executando o Windows Server 2012, Windows Server 2008 R2 ou Windows Server 2008 e tiver o Hyper-V instalado, poderá implantar o ambiente do AD RMS ISV de uma caixa criando uma máquina virtual usando o AD RMS de uma caixa VHD. O ambiente do AD RMS ISV de uma caixa fornece um servidor RMS configurado para pré-produção e também o Active Directory Rights Management Services Client 2.1 instalado. As configurações do Registro para o servidor RMS e do cliente já estão configuradas. Para testar seu aplicativo, execute-o na máquina virtual na qual o ambiente de uma caixa está implantado.
-   **Você pode executar o aplicativo em um servidor RMS configurado para pré-produção e que está implantado em sua rede**. Nesse caso, você também deve instalar e configurar o AD RMS Client 2.1 no computador no qual o aplicativo será executado. Para obter informações sobre como fazer isso, consulte [Configuração de cliente](how-to-configure-the-ad-rms-client-2-0.md). Para obter informações sobre como implantar um servidor RMS e configurá-lo para pré-produção, consulte [Instalação e configuração do servidor](how-to-install-and-configure-an-rms-server.md).

## Tópicos relacionados

* [Como usar](how-to-use-msipc.md)
* [Página de download de material de referência do AD RMS SDK Webinar](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [Configuração do cliente](how-to-configure-the-ad-rms-client-2-0.md)
* [Instalar o SDK](create-your-first-rights-aware-application.md)
* [Instalar e configurar o servidor](how-to-install-and-configure-an-rms-server.md)
* [Noções básicas sobre cadeias de certificados](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO4-->


