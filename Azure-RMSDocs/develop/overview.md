---
title: "Visão geral | Azure RMS"
description: "O AD RMS e o Azure RMS são uma tecnologia de proteção de informações que ajuda a proteger informações digitais do uso não autorizado."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8A13494E-C1D7-407D-BCD1-A406915EA578
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 417888c5445d702b1f700a8e717fbb746593efc6


---

# Visão geral


O AD RMS e o Azure RMS (Microsoft Rights Management Services) são uma tecnologia de proteção de informações que ajuda a proteger informações digitais do uso não autorizado. Por meio de seus aplicativos habilitados para direitos, os proprietários de conteúdo poderão definir quem pode abrir, modificar, imprimir, encaminhar ou executar outras ações em seu conteúdo.

Microsoft Rights Management SDK 4.2 está disponível para várias plataformas e é um SDK (Kit de desenvolvedor de software), ou estrutura, projetado para computadores e dispositivos cliente com o objetivo de ajudar a proteger o acesso e o uso de informações que passam por aplicativos "habilitados para direitos". Os SDKs para essas plataformas fornecem uma API simples para um desenvolvedor de aplicativos proteger ou consumir conteúdo digital, recuperar modelos e adquirir políticas de um servidor, além de outras tarefas de gerenciamento de direitos relacionadas.

Para saber mais sobre as plataformas com suporte no momento, consulte nosso portal de documentação do desenvolvedor para o [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md).

Veja a seguir alguns cenários possíveis:

-   Uma firma de advocacia quer impedir que mensagens de email confidenciais sejam impressas ou encaminhadas em um dispositivo móvel.
-   Os desenvolvedores de projetos auxiliados por computador e softwares de fabricação desejam limitar o acesso ao desenho a um grupo pequeno de usuários dentro da divisão de pesquisa, sem exigir o uso de senhas.
-   Os proprietários de um aplicativo móvel de design gráfico desejam usar uma única licença que permita a visualização livre de cópias de baixa resolução das imagens, mas que exija o pagamento para acessar as versões em alta resolução.
-   Os proprietários de uma biblioteca de documentos online desejam habilitar direitos para exibir, imprimir ou editar documentos com base na identidade do usuário, quando os documentos são baixados em um dispositivo móvel.
-   Uma empresa deseja publicar informações confidenciais de funcionários em um site interno que restrinja os privilégios de visualização e edição para determinados usuários.

O MS RMS SDK 4.2 pode ser baixado, mediante confirmação e aceitação do seu contrato de licença, distribuído gratuitamente com o software de terceiros para permitir ao cliente acessar o conteúdo que tenha sido protegidos por direitos pelo uso e implantação de servidores do AD RMS em seu ambiente ou pelos Serviços do Azure RMS. Para saber mais, confira [Introdução](get-started.md).

## Destaques do SDK


O SDK do MS RMS SDK 4.2 oferece alguns recursos novos e interessantes que incluem o seguinte:

-   **API reprojetada** – A API do MS RMS SDK 4.2 foi reformulada para manter a simplicidade máxima, de modo que os desenvolvedores possam aproveitar uma API simples e transparente de criptografia e descriptografia que forneça comportamentos consistentes de RMS com o mínimo de esforço.
-   **Suporte híbrido para AD RMS e Azure RMS** – um único aplicativo habilitado para RMS pode consumir e proteger o conteúdo do servidor do AD RMS (usando a extensão de dispositivo móvel do AD RMS) e do serviço do Azure RMS. O MS RMS SDK 4.2 descobre de forma transparente o ponto de extremidade relevante que os administradores de TI podem configurar.
-   **Traga sua própria biblioteca de autenticação** – como desenvolvedor de aplicativos você pode escolher qual biblioteca de autenticação é usada com o MS RMS SDK 4.2. Quer seja a [Biblioteca de Autenticação do Azure AD](https://msdn.microsoft.com/library/jj573266.aspx) ou a biblioteca personalizada de sua organização, o MS RMS SDK 4.2 separa a pilha de autenticação para que você possa escolher a biblioteca mais adequada às suas necessidades.
-   **Traga sua própria interface de usuário** - agora, o MS RMS SDK 4.2 permite que você implemente a interface de usuário personalizada. Desde a proteção do conteúdo e escolha dos modelos até a exibição e alteração de permissões ao consumir conteúdo protegido, o MS RMS SDK 4.2 não impõe qualquer interface interna em seus aplicativos. No entanto, se você quiser, use as bibliotecas de interface de usuário do Microsoft RMS para todas as plataformas por meio de nossa [conta do GitHub](https://github.com/AzureAD/).
-   **Acessar o conteúdo protegido offline** – O MS RMS SDK 4.2 permite que os usuários de seu aplicativo acessem o conteúdo protegido, mesmo quando não houver conectividade com a internet. O MS RMS SDK 4.2 armazena com segurança em cache as políticas de consumo de conteúdo protegido, para que os usuários possam acessar dados protegido do RMS no modo offline.

Use o guia de [Introdução](get-started.md) para iniciar seu projeto de aplicativo para dispositivo com informações protegidas.

## Tópicos relacionados

* [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [Introdução](get-started.md)
* [Biblioteca de Autenticação do Azure AD](https://msdn.microsoft.com/en-us/library/jj573266.aspx)
* [Conta do GitHub](https://github.com/AzureAD/)
 

 






<!--HONumber=Jul16_HO2-->


