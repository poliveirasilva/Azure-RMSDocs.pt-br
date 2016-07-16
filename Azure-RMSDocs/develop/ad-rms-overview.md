---
title: "Visão geral | Azure RMS"
description: "O RMS (Rights Management Services) é uma tecnologia de proteção de informações que ajuda a proteger informações digitais contra uso não autorizado."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 37f3bc2308caaa8fd5e5c7fc8c56b6dc4d076b97


---

# Visão geral

O RMS (Rights Management Services) é uma tecnologia de proteção de informações que ajuda a proteger informações digitais contra uso não autorizado. Por meio do aplicativo habilitado para direitos, os proprietários de conteúdo poderão definir quem pode abrir, modificar, imprimir, encaminhar ou executar outras ações no conteúdo.

## Visão geral

O AD RMS consiste em dois componentes de [servidor](ad-rms-server.md) e [cliente](ad-rms-client.md). O servidor, em execução no Azure ou no Windows Server, consiste em diversos serviços Web.

O componente do [cliente](ad-rms-client.md) pode ser executado em um cliente ou servidor de sistema operacional e contém funções que permitem a um aplicativo criptografar e descriptografar o conteúdo, recuperar modelos e listas de revogação, adquirir licenças e certificados de um servidor e outras tarefas relacionadas ao gerenciamento de direitos.

Para saber mais, confira [Tipos de aplicativo](application-types.md).

A seguir estão apenas alguns dos cenários ao qual os aplicativos criados com o Rights Management Services SDK 2.1 podem ser aplicados.

-   Uma firma de advocacia quer impedir que mensagens de email confidenciais sejam impressas ou encaminhadas.
-   Os desenvolvedores de projetos auxiliados por computador e softwares de fabricação desejam limitar o acesso ao desenho a um grupo pequeno de usuários dentro da divisão de pesquisa, sem exigir o uso de senhas.
-   Os proprietários de um site de design gráfico desejam usar uma única licença que permita a visualização livre de cópias de baixa resolução das imagens, mas que exija o pagamento para acessar as versões em alta resolução.
-   Os proprietários de uma biblioteca de documentos online desejam habilitar direitos exibir, imprimir ou editar documentos com base na identidade do usuário.
-   Uma empresa deseja publicar informações confidenciais de funcionários em um site interno que restrinja os privilégios de visualização e edição para determinados usuários.

Para obter mais informações sobre o servidor AD RMS, o cliente AD RMS e sua funcionalidade, consulte o conteúdo do TechNet para [Documentação do profissional de TI para AD RMS](https://TechNet.Microsoft.Com/library/cc771234.aspx).

Os tópicos restantes nesta seção abordam a Arquitetura do RMS e suas implementações.

## Nesta seção

| Tópico | Descrição |
|-------|-------------|
|[Cliente](ad-rms-client.md) |Este tópico descreve a finalidade e a função do Rights Management Services Client 2.1 |
|[Servidor](ad-rms-server.md) | Este tópico descreve o a finalidade e as funções do Servidor RMS para Azure e Windows Server.|


## Tópicos relacionados

* [Conceitos do RMS](application-types.md)
* [Introdução](getting-started-with-ad-rms-2-0.md)
* [Documentação do IT Pro para AD RMS](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
 

 



<!--HONumber=Jul16_HO2-->


