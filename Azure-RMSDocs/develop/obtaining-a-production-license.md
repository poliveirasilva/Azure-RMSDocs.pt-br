---
# required metadata

title: Obtenção de uma licença de produto | Azure RMS
description: O lançamento de um aplicativo desenvolvido com o SDK 2.1 do RMS, exige um Contrato de licença de produção.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013f9d75-0b66-44a8-9b01-d05b44a5ea0c

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
# Obtenção de uma licença de produto

Antes de você poder lançar um aplicativo desenvolvido com o Rights Management Services SDK 2.1, você deve se inscrever para um Cato de licença de produção a fim de obter um certificado de produção.

> [!IMPORTANT]
> Se você for executar o aplicativo cliente com o RMS baseado no Azure, será necessário solicitar um locatário do Azure RMS. Envie um email para <rmcstbeta@microsoft.com> e inclua sua solicitação de locatário.

Para saber mais sobre como executar com o Azure RMS, confira [Permitir que seu aplicativo de serviço funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).


O certificado de produção e o certificado de pré-produção executam uma função semelhante, mas servem para ambientes diferentes. Os dois contêm uma cadeia de certificados com um certificado de CA (autoridade de certificação) da Microsoft na raiz da confiança, mas o certificado de pré-produção é usado apenas durante o desenvolvimento de um aplicativo RMS. O certificado de produção é usado em ambientes pós-lançamento. O certificado de produção e a chave privada associada são usados para criar e assinar um manifesto que identifica os arquivos que podem ou devem ser carregados no espaço de processo de seu aplicativo, e aqueles que não devem ser carregados.

Para saber mais sobre chaves, confira [Testar seu aplicativo habilitado para direitos](running-your-first-application.md).

Você pode obter o certificado por meio da inscrição em um Contrato de licença de produção.

## Solicitação de um Contrato de licença de produção

![](../media/wedge.gif)

-   Envie uma mensagem de email para [RMLA@microsoft.com](mailto:rmla@microsoft.com) e inclua as seguintes informações:

    -   Nome completo da empresa

    -   Endereços físico da empresa (inclua a cidade, estado, país ou região e CEP ou código postal)
    -   Endereços de correspondência da empresa (inclua a cidade, estado, país ou região e CEP ou código postal)
    -   Números de telefone e de fax da empresa
    -   URL da empresa
    -   País ou região de incorporação
    -   Nome do aplicativo ou produto
    -   Nome e sobrenome do solicitante
    -   Cargo ou a posição do solicitante
    -   Endereço de email do solicitante

    Embora uma conta de email não seja rigorosamente exigida, o processo de inscrição normalmente depende da comunicação por email. Você pode obter uma conta de email gratuita no Microsoft Outlook.com. Se você não tiver uma conta e não quiser uma, envie uma inscrição impressa para o endereço a seguir:

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    Ao solicitar uma contrato, faça o seguinte:

    -   Envie as informações, em inglês, como devem aparecer no contrato.
    -   Envie todas as informações solicitadas. Informações incompletas ou ausentes podem atrasar o processamento da solicitação.

    A equipe do ADRMLA (Contrato de licenciamento do Active Directory Rights Management) responderá à sua solicitação por email em até três dias úteis, ou em mais tempo se você enviou a solicitação usando um serviço postal. A resposta incluirá o formulário do contrato de licença e instruções adicionais. Leia, assine e devolva todas as páginas do contrato para a equipe do ADRMLA. Não altere as fontes ou reformate os parágrafos do contrato de licença.

    Siga as instruções recebidas da equipe do ADRMLA. As instruções listam os itens de informações digitais necessários para atender à sua solicitação de certificado. Seguindo as instruções passo a passo, você reduzirá qualquer atraso.

    A equipe do ADRMLA encaminhará o certificado de produção para você após sua criação. O certificado é criado com base no contrato de licença e nas informações digitais (incluindo uma chave pública) fornecidas por você. Observe que pode demorar até 15 dias úteis para a equipe do ADRMLA responder com seu certificado por email, ou mais tempo se a comunicação for pelo serviço postal.

## Tópicos relacionados

* [Como usar](how-to-use-msipc.md)
* [Testar seu aplicativo habilitado para direitos](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO3-->


