---
# required metadata

title: Visão geral | Azure RMS
description: O RMS (Rights Management Services) é uma tecnologia de proteção de informações que ajuda a proteger informações digitais contra uso não autorizado.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a58894d5-3271-46d7-bb1c-fbd22eae8530

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
# Visão geral

O RMS (Rights Management Services) é uma tecnologia de proteção de informações que ajuda a proteger informações digitais contra uso não autorizado. Por meio do aplicativo habilitado para direitos, os proprietários de conteúdo poderão definir quem pode abrir, modificar, imprimir, encaminhar ou executar outras ações no conteúdo.

## Visão geral

O AD RMS consiste em dois componentes de [servidor](ad-rms-server.md) e [cliente](ad-rms-client.md). Os componentes de servidor incluem vários serviços Web executados em um servidor Windows, como o Windows Server 2008 R2 ou por meio da nuvem por meio de serviços da web do RMS no Azure. O componente do cliente pode ser executado em um cliente ou servidor de sistema operacional e contém funções que permitem a um aplicativo criptografar e descriptografar o conteúdo, recuperar modelos e listas de revogação, adquirir licenças e certificados de um servidor e outras tarefas relacionadas de gerenciamento de direitos.

Para saber mais, confira [Tipos de aplicativo](application-types.md).

A seguir estão apenas alguns dos cenários ao qual os aplicativos criados com o Rights Management Services SDK 2.1 podem ser aplicados.

-   Uma firma de advocacia quer impedir que mensagens de email confidenciais sejam impressas ou encaminhadas.
-   Os desenvolvedores de projetos auxiliados por computador e softwares de fabricação desejam limitar o acesso ao desenho a um grupo pequeno de usuários dentro da divisão de pesquisa, sem exigir o uso de senhas.
-   Os proprietários de um site de design gráfico desejam usar uma única licença que permita a visualização livre de cópias de baixa resolução das imagens, mas que exija o pagamento para acessar as versões em alta resolução.
-   Os proprietários de uma biblioteca de documentos online desejam habilitar direitos exibir, imprimir ou editar documentos com base na identidade do usuário.
-   Uma empresa deseja publicar informações confidenciais de funcionários em um site interno que restrinja os privilégios de visualização e edição para determinados usuários.

Para obter mais informações sobre o servidor AD RMS, o cliente AD RMS e sua funcionalidade, consulte o conteúdo do TechNet para [Documentação do profissional de TI para AD RMS](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx).

Para iniciar, consulte [Introdução](getting-started-with-ad-rms-2-0.md).

## Tópicos relacionados

* [Conceitos do AD RMS](application-types.md)
* [Diferenças entre o AD RMS e o AD RMS 2.1](differences-between-ad-rms-and-ad-rms-2-0.md)
* [Introdução](getting-started-with-ad-rms-2-0.md)
* [Documentação do IT Pro para AD RMS](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
* [servidor](ad-rms-server.md)
* [cliente](ad-rms-client.md)
 

 





<!--HONumber=Apr16_HO3-->


