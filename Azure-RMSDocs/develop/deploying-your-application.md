---
title: "Implementar a aplicação | Azure RMS"
description: "Este tópico descreve e serve de orientação nas opções de implementação da sua aplicação com capacidade para direitos"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 982021a2e972023b04e6483348a7c27aa029e198
ms.openlocfilehash: 8308e2db84e13c6b8c85a1a3ae6c01fc0aabee75


---

# Implementar em produção


Este tópico descreve e serve de orientação nas opções de implementação da sua aplicação com capacidade para direitos.

## Pedir um Contrato de Licença de Produção

 Para lançar uma aplicação desenvolvida utilizando o SDK Rights Management Services 2.1, tem de solicitar um Contrato de Licença de Produção para obter um certificado de produção.

> [!IMPORTANT]
> Se executar a aplicação cliente com o RMS baseado no Azure, terá de solicitar os seus próprios inquilinos. Para mais informações, consulte [Requisitos do Azure RMS: Subscrições na nuvem que suportam o Azure RMS](../get-started/requirements-subscriptions.md).
> Para obter mais informações sobre a execução com o Azure RMS, consulte [Permitir que a aplicação do serviço funcione com o RMS baseado na nuvem](how-to-use-file-api-with-aadrm-cloud.md).

Pode obter o certificado ao solicitar um Contrato de Licença de Produção.

Envie uma mensagem de e-mail para [RMLA@microsoft.com](mailto:rmla@microsoft.com) e inclua as seguintes informações:

- Nome da empresa completo
- Endereço físico da empresa (inclua a cidade, o estado, o país ou a região e o código postal)
- Morada de correio postal da empresa (inclua a cidade, o estado, o país ou a região e o código postal)
- Números de telefone e fax da empresa
- URL da empresa
- País ou região de constituição
- Nome da aplicação ou produto
- Nome próprio e apelido do autor do pedido
- Título ou cargo do autor do pedido
- Endereço de e-mail do autor do pedido

Embora uma conta de e-mail não seja estritamente necessária, o processo de candidatura normalmente depende do e-mail para a comunicação. Pode obter uma conta de e-mail gratuita em Microsoft Outlook.com. Se não tiver uma conta e não pretender uma, pode enviar uma candidatura datilografada para o seguinte endereço:

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

Quando solicitar um contrato, efetue o seguinte:
- Submeta as informações em inglês, conforme deve aparecer no contrato.
- Envie todas as informações necessárias. As informações em falta ou incompletas podem atrasar o processamento do pedido.

A equipa do Contrato de Licença do Active Directory Rights Management (ADRMLA) responderá ao seu pedido por e-mail no prazo de três dias úteis ou superior se enviar o pedido utilizando um serviço postal. A resposta irá incluir o formulário do contrato de licença e mais instruções. Leia, assine e devolva todas as páginas do contrato à equipa do ADRMLA. Não altere os tipos de letra nem reformate os parágrafos do contrato de licença.

Certifique-se de que segue as instruções que recebe da equipa do ADRMLA. As instruções listam os itens de informações digitais necessários para satisfazer o pedido de certificado. Ao seguir as instruções passo a passo, reduzirá os atrasos.

A equipa do ADRMLA irá reencaminhar o certificado de produção para si depois de ser criado. Tenha em atenção que poderá demorar até 15 dias úteis para a equipa do ADRMLA responder com o certificado por e-mail ou mais se a comunicação for pelo serviço postal.


## Opções de instalação e requisitos do Rights Management Service Client 2.1

Dado que utilizou o SDK RMS 2.1, será necessário que o Cliente dos Serviços de Gestão de Direitos do Active Directory 2.1 seja implementado no computador do utilizador final.

### RMS Client 2.1

O RMS Client 2.1 é um software concebido para computadores cliente para ajudar a proteger o acesso e a utilização de informações que circulam nas aplicações que utilizam o RMS, independentemente de estar instalado no local ou num centro de dados Microsoft.

O RMS Client 2.1 não é um componente de sistema operativo Windows. O RMS Client 2.1 é incluído como uma transferência opcional que pode ser, com o reconhecimento e a aceitação do respetivo contrato de licença, distribuída gratuitamente com o seu software de terceiros para permitir o acesso de cliente a conteúdo que foi protegido por direitos através da utilização e implementação de servidores RMS no seu ambiente.


> [!IMPORTANT]
> O Cliente de AD RMS 2.1 é de arquitetura específica e tem de corresponder à arquitetura do seu sistema operativo de destino.


## Opções de instalação do RMS Client 2.1

-   **Redistribuir o RMS Client 2.1**

    A abordagem recomendada é agrupar o pacote instalador do Cliente do RMS com a sua aplicação ou solução utilizando a sua tecnologia de instalação preferencial. O Cliente do RMS pode ser livremente redistribuído e agrupado com outras aplicações e soluções de TI.

    Pode optar por instalar o RMS Client 2.1 de forma interativa ao iniciar o instalador do RMS Client 2.1 ou ao instalá-lo silenciosamente. Os passos de integração serão:

    -   Transferir o instalador do Cliente do RMS 2.1
    -   Integrar o instalador do RMS Client 2.1 executado com o instalador da sua aplicação

    Dois bons exemplos de integração do RMS Client 2.1 com a sua aplicação são o pacote instalador SDK RMS 2.1 e o pacote do Right Protected Folder Explorer. Tente instalá-los por si para compreender a abordagem.

-   **Tornar o RMS Client 2.1 um pré-requisito para a instalação da sua aplicação**

    Neste caso, irá criar um pré-requisito de forma que a instalação da aplicação falhe se o RMS Client 2.1 não estiver presente no computador do utilizador final.

    Se o cliente não estiver presente, forneça uma mensagem de erro a informar o utilizador onde pode transferir uma cópia do RMS Client 2.1

    Se o cliente estiver presente, prossiga com a instalação da aplicação.

## Ativar Serviços de Gestão de Direitos do Azure com a sua aplicação

> [!NOTE]
> Se tiver migrado para o novo modelo da ADAL para autenticação, não tem de instalar o SIA. Para obter mais informações, consulte [Autenticação ADAL para a aplicação com suporte RMS](adal-auth.md).
> Além disso, pode **certificar a sua aplicação para o Windows 10** - através da atualização da sua aplicação para utilizar a autenticação ADAL em vez do Assistente de Início de Sessão do Microsoft Online, o utilizador e os seus clientes poderão: utilizar a autenticação multifator Instale o RMS Client 2.1 sem necessidade de privilégios administrativos para a máquina


Para o utilizador final tirar partido dos serviços de Gestão de Direitos do Azure, tem de implementar o *Assistente de Início de Sessão do Online Services (SIA)*. Na qualidade de programador da aplicação, não sabe se o utilizador final irá utilizar o RMS (no local) ou os serviços de Gestão de Direitos do Azure (serviço em nuvem).


> [!IMPORTANT]
> Executar a aplicação de cliente SDK RMS 2.1 com o Azure RMS exige a criação dos seus próprios inquilinos. Para mais informações, consulte [Requisitos do Azure RMS: Subscrições na nuvem que suportam o Azure RMS](../get-started/requirements-subscriptions.md).

-   Transfira o [Assistente de Início de Sessão do Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) do Centro de Transferências da Microsoft.
-   Certifique-se de que a implementação de uma aplicação com capacidade para direitos inclui uma verificação de pré-requisitos para esta seleção de serviço.
-   Para os seus próprios testes e para a utilização do serviço online por parte dos utilizadores finais, consulte o tópico da TechNet [Configurar o Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx).

Para obter mais informações sobre como permitir que a aplicação utilize o RMS para serviços de Gestão de Direitos do Azure, consulte [Permitir que a aplicação funcione com o RMS baseado na nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Tópicos relacionados

* [Assistente de Início de Sessão do Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configurar o Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Permitir que a aplicação funcione com o RMS baseado na nuvem](how-to-use-file-api-with-aadrm-cloud.md)
 

 



<!--HONumber=Jul16_HO1-->


