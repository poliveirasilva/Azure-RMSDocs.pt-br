---
# required metadata

title: Implantação de seu aplicativo | Azure RMS
description: Este tópico descreve opções de implantação para seu aplicativo habilitado para direitos e orienta você sobre elas
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 08cb33e0-7df5-4855-a05b-159e6532f3ca

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
# Implantação de seu aplicativo


Este tópico descreve opções de implantação para seu aplicativo habilitado para direitos e orienta você sobre elas.

> [!IMPORTANT]
> É uma prática recomendada testar seu aplicativo do Rights Management Services SDK 2.1 primeiro com o ambiente de pré-produção do RMS no servidor RMS. Em seguida, caso deseje que seu cliente tenha a capacidade de usar o aplicativo com o serviço do Azure RMS, teste com esse ambiente. Para obter mais informações, veja [Habilite seu aplicativo de serviço para funcionar com o RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

 

## Opções de instalação do Active Directory Rights Management Services Client 2.1

Depois de criar o arquivo de manifesto usando um certificado de produção, o aplicativo estará pronto para ser implantado. Considerando que você utilizou o RMS SDK 2.1, será necessário implantar o Active Directory Rights Management Services Client 2.1 no computador do usuário final.

### AD RMS Client 2.1

O AD RMS Client 2.1 é um software projetado para seus computadores cliente para ajudar a proteger o acesso e uso das informações que passam por aplicativos que usam o RMS, seja instalado no seu local ou em um datacenter da Microsoft.

O AD RMS Client 2.1 não é um componente do sistema operacional Windows. O AD RMS Client 2.1 é enviado com um download opcional que pode ser, com a confirmação e aceitação do seu contrato de licença, distribuído gratuitamente com o software de terceiros para permitir ao cliente acessar o conteúdo que tenha sido protegidos por direitos pelo uso e a implantação de servidores RMS em seu ambiente.

> [!IMPORTANT]
> O AD RMS Client 2.1 é específico à arquitetura e deve corresponder à arquitetura de seu sistema operacional de destino.


## Opções de instalação do AD RMS Client 2.1

-   **Redistribuição do AD RMS Client 2.1**

    A abordagem recomendada é incluir o pacote do instalador do RMS Client com seu aplicativo ou solução usando sua tecnologia de instalação preferida. O RMS Client pode ser redistribuído livremente e agrupado com outros aplicativos e soluções de TI.

    Você pode optar por instalar o AD RMS Client 2.1 de forma interativa iniciando o instalador do AD RMS Client 2.1 ou instalando-o silenciosamente. As etapas de integração serão:

    -   Baixar o instalador do RMS Client 2.1
    -   Integrar a execução do instalador do AD RMS Client 2.1 com o instalador de seu aplicativo

    Dois bons exemplos de integração do AD RMS Client 2.1 com seu aplicativo são os pacotes de instalador do RMS SDK 2.1 e do Explorador de Pasta Protegido por Direitos. Tente instalá-los por conta para entender a abordagem.

-   **Tornar o AD RMS Client 2.1 um pré-requisito para a instalação do aplicativo**

    Nesse caso, você criará um pré-requisito, de modo que a instalação do aplicativo falhará se o AD RMS Client 2.1 não estiver presente no computador do usuário final.

    Se o cliente não estiver presente, forneça uma mensagem de erro informando ao usuário onde ele poderá baixar uma cópia do AD RMS Client 2.1

    Se o cliente estiver presente, continue com a instalação do aplicativo.

## Habilitação do Azure Rights Management Services com seu aplicativo

> [!NOTE]
> Se você tiver migrado para o novo modelo do ADAL para autenticação, não será necessário instalar o SIA. Para saber mais, veja a autenticação ADAL para seu aplicativo habilitado para RMS.

- **Certifique seu aplicativo para o Windows 10**: ao atualizar seu aplicativo para usar a autenticação ADAL em vez do Assistente de Conexão do Microsoft Online, você e seus clientes poderão:
  - Usar a autenticação multifator
  - Instalar o cliente do RMS 2.1 sem exigir privilégios administrativos no computador
 
  Para que seu usuário final tire proveito dos Azure Rights Management Services, você deve implantar o *Assistente de Conexão do Online Services*. Como desenvolvedor de aplicativos, você não sabe se o usuário final usará RMS (local) ou o Azure Rights Management Services (serviço de nuvem).

> [!IMPORTANT]
> A execução do aplicativo cliente do RMS SDK 2.1 com o Azure RMS exige que você solicite um Locatário do Azure RMS. Envie um email para <rmcstbeta@microsoft.com> e inclua sua solicitação de locatário.

-   Baixe o [Assistente de Conexão do Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) do Centro de Download da Microsoft.
-   Certifique-se de que a implantação de um aplicativo habilitado para direitos inclua uma verificação de pré-requisitos para a seleção de serviço.
-   Para seus próprios testes e para o uso do serviço online por seus usuários finais, veja o tópico da TechNet, [Configuring Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx) (Configuração do Rights Management).

Para saber mais sobre como permitir que seu aplicativo use o RMS para o Azure Rights Management Services, confira [Permitir que seu aplicativo funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Tópicos relacionados

* [Como usar](how-to-use-msipc.md)
* [Assistente de Conexão do Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configurando o Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Permitir que seu aplicativo funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Apr16_HO3-->


