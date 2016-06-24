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
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Implantar na pré-produção


Este tópico descreve opções de implantação para seu aplicativo habilitado para direitos e orienta você sobre elas.

## Solicitar um Contrato de Licença de Produção

 Antes de você poder lançar um aplicativo desenvolvido com o Rights Management Services SDK 2.1, você deve se inscrever para um Contrato de licença de produção a fim de obter um certificado de produção.

> [!IMPORTANT]
> Se você for executar o aplicativo cliente com o RMS baseado no Azure, será necessário criar seus próprios locatários. Para obter mais informações, consulte [Requisitos do Azure RMS: assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).
> Para saber mais sobre como executar com o Azure RMS, confira [Permitir que seu aplicativo de serviço funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

Você pode obter o certificado por meio da inscrição em um Contrato de licença de produção.

Envie uma mensagem de email para [RMLA@microsoft.com](mailto:rmla@microsoft.com) e inclua as seguintes informações:

- Nome completo da empresa
- Endereços físico da empresa (inclua a cidade, estado, país ou região e CEP ou código postal)
- Endereços de correspondência da empresa (inclua a cidade, estado, país ou região e CEP ou código postal)
- Números de telefone e de fax da empresa
- URL da empresa
- País ou região de incorporação
- Nome do aplicativo ou produto
- Nome e sobrenome do solicitante
- Cargo ou a posição do solicitante
- Endereço de email do solicitante

Embora uma conta de email não seja rigorosamente exigida, o processo de inscrição normalmente depende da comunicação por email. Você pode obter uma conta de email gratuita no Microsoft Outlook.com. Se você não tiver uma conta e não quiser uma, envie uma inscrição impressa para o endereço a seguir:

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

Ao solicitar uma contrato, faça o seguinte:
- Envie as informações, em inglês, como devem aparecer no contrato.
- Envie todas as informações solicitadas. Informações incompletas ou ausentes podem atrasar o processamento da solicitação.

A equipe do ADRMLA (Contrato de licenciamento do Active Directory Rights Management) responderá à sua solicitação por email em até três dias úteis, ou em mais tempo se você enviou a solicitação usando um serviço postal. A resposta incluirá o formulário do contrato de licença e instruções adicionais. Leia, assine e devolva todas as páginas do contrato para a equipe do ADRMLA. Não altere as fontes ou reformate os parágrafos do contrato de licença.

Siga as instruções recebidas da equipe do ADRMLA. As instruções listam os itens de informações digitais necessários para atender à sua solicitação de certificado. Seguindo as instruções passo a passo, você reduzirá qualquer atraso.

A equipe do ADRMLA encaminhará o certificado de produção para você após sua criação. Observe que pode demorar até 15 dias úteis para a equipe do ADRMLA responder com seu certificado por email, ou mais tempo se a comunicação for pelo serviço postal.


## Opções e requisitos de instalação do Rights Management Service Client 2.1

Considerando que você utilizou o RMS SDK 2.1, será necessário implantar o Active Directory Rights Management Services Client 2.1 no computador do usuário final.

### RMS Client 2.1

O RMS Client 2.1 é um software projetado para seus computadores cliente para ajudar a proteger o acesso e uso das informações que passam por aplicativos que usam o RMS, seja instalado no seu local ou em um datacenter da Microsoft.

O RMS Client 2.1 não é um componente do sistema operacional Windows. O RMS Client 2.1 é enviado com um download opcional que pode ser, com a confirmação e aceitação do seu contrato de licença, distribuído gratuitamente com o software de terceiros para permitir ao cliente acessar o conteúdo que tenha sido protegidos por direitos pelo uso e a implantação de servidores RMS em seu ambiente.


> [!IMPORTANT] O AD RMS Client 2.1 é específico à arquitetura e deve corresponder à arquitetura de seu sistema operacional de destino.


## Opções de instalação do RMS Client 2.1

-   **Redistribuição do RMS Client 2.1**

    A abordagem recomendada é incluir o pacote do instalador do RMS Client com seu aplicativo ou solução usando sua tecnologia de instalação preferida. O RMS Client pode ser redistribuído livremente e agrupado com outros aplicativos e soluções de TI.

    Você pode optar por instalar o RMS Client 2.1 de forma interativa iniciando o instalador do RMS Client 2.1 ou instalando-o silenciosamente. As etapas de integração serão:

    -   Baixar o instalador do RMS Client 2.1
    -   Integrar a execução do instalador do RMS Client 2.1 com o instalador de seu aplicativo

    Dois bons exemplos de integração do RMS Client 2.1 com seu aplicativo são os pacotes de instalador do RMS SDK 2.1 e do Explorador de Pasta Protegido por Direitos. Tente instalá-los por conta para entender a abordagem.

-   **Tornar o RMS Client 2.1 um pré-requisito para a instalação do aplicativo**

    Nesse caso, você criará um pré-requisito, de modo que a instalação do aplicativo falhará se o RMS Client 2.1 não estiver presente no computador do usuário final.

    Se o cliente não estiver presente, forneça uma mensagem de erro informando ao usuário onde ele poderá baixar uma cópia do RMS Client 2.1

    Se o cliente estiver presente, continue com a instalação do aplicativo.

## Habilitação do Azure Rights Management Services com seu aplicativo

> [!NOTE]
> Se você tiver migrado para o novo modelo do ADAL para autenticação, não será necessário instalar o SIA. Para saber mais, consulte [Autenticação ADAL para seu aplicativo habilitado para RMS](adal-auth.md).
> Além disso, você pode **Certificar seu aplicativo para Windows 10** - Ao atualizar seu aplicativo para usar a autenticação de ADAL em vez do Assistente de Conexão do Microsoft Online, você e seus clientes poderão: utilizar a autenticação multifator e instalar o RMS Client 2.1 sem exigir privilégios administrativos do computador


Para que seu usuário final tire proveito dos Azure Rights Management Services, você deve implantar o *SIA (Assistente de Conexão) do Online Services*. Como desenvolvedor de aplicativos, você não sabe se o usuário final usará RMS (local) ou o Azure Rights Management Services (serviço de nuvem).


> [!IMPORTANT]
> A execução do aplicativo cliente do RMS SDK 2.1 com o Azure RMS exige que você crie seus próprios locatários. Para obter mais informações, consulte [Requisitos do Azure RMS: assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).

-   Baixe o [Assistente de Conexão do Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) do Centro de Download da Microsoft.
-   Certifique-se de que a implantação de um aplicativo habilitado para direitos inclua uma verificação de pré-requisitos para a seleção de serviço.
-   Para seus próprios testes e para o uso do serviço online por seus usuários finais, veja o tópico da TechNet, [Configuring Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx) (Configuração do Rights Management).

Para saber mais sobre como permitir que seu aplicativo use o RMS para o Azure Rights Management Services, confira [Permitir que seu aplicativo funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Tópicos relacionados

* [Assistente de Conexão do Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configurando o Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Permitir que seu aplicativo funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md)
 

 


<!--HONumber=Jun16_HO2-->


