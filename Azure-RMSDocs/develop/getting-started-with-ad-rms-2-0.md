---
# required metadata

title: Introdução | Azure RMS
description: A plataforma do RMS SDK 2.1 permite aos desenvolvedores compilar aplicativos que aproveitam a proteção de informações do RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Introdução

A plataforma do Rights Management Services SDK 2.1 permite aos desenvolvedores compilar aplicativos que aproveitam a proteção de informações do RMS por meio de um Servidor RMS ou do Azure RMS. A plataforma lida com as práticas de segurança complexas, como processamento de descriptografia, criptografia e gerenciamento de chaves, e oferece uma API simplificada para fácil desenvolvimento de aplicativos.

## Introdução ao RMS SDK 2.1

Este tópico o orientará durante o processo de configuração e execução do seu aplicativo habilitado para direitos em um ambiente de teste. Os tópicos a seguir abordam como configurar seu ambiente de desenvolvimento e são listados de modo a sugerir uma ordem para execução das tarefas.

## Nestas seções

| Tópico | Descrição |
|-------|-------------|
| [Notas de versão](release-notes-rtm.md) | Este tópico contém informações importantes sobre esta versão e sobre versões anteriores do RMS SDK 2.1.|
| [Instalar o SDK](install-the-rms-sdk.md) | Este tópico o orientará durante a instalação das ferramentas de desenvolvedor.|
| [Configurar o Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | Este tópico contém instruções sobre como configurar um projeto do Visual Studio para usar o RMS SDK 2.1.|
| [Desenvolvendo seu aplicativo](developing-your-application.md) | Este tópico contém orientações essenciais sobre os principais aspectos de um aplicativo habilitado para RMS e pode servir como a base do desenvolvimento de seu próprio aplicativo.|
| [Testando seu aplicativo](running-your-first-application.md) |Este tópico contém instruções sobre a configuração dos testes para seu aplicativo.|
| [Implantar na produção](deploying-your-application.md) |Este tópico orienta você quanto à opções de implantação para seu aplicativo habilitado para direitos.|

Depois de ter começado usar, confira alguns dos nossos outros [exemplos de RMS](samples.md). Em seguida, mantenha-se atualizado por meio de nosso [Blog do Desenvolvedor do RMS](http://blogs.msdn.com/b/rms/).


Tente usar o RMS SDK 2.1 seguindo as diretrizes nestes tópicos:

-   [Instalar o SDK](install-the-rms-sdk.md)
-   [Testando seu aplicativo habilitado para direitos](running-your-first-application.md)
-   [IPCHelloWorld - um aplicativo de exemplo](how-to-build-your-first-application.md)

### Por que usar o RMS SDK 2.1 para proteger seu conteúdo

Para os desenvolvedores que desejam adicionar suporte RMS para seus aplicativos novos e existentes, o RMS SDK 2.1 ajuda a tornar mais fácil:

-   Aplicativos gerenciáveis pelo autor, compatíveis e robustos que reconhecem o RMS.
-   Criptografe dados de usuário de maneira persistente. Os dados permanecem criptografados independentemente do ambiente, do dispositivo ou do sistema operacional.
-   Imponha um rico conjunto de restrições de uso, como impedir a capturas de tela de seus dados confidenciais.
-   Dê suporte a políticas de proteção gerenciadas pela empresa.
-   Dê suporte a novos mecanismos de autenticação e algoritmos de criptografia assim que eles ficarem disponíveis.

O RMS SDK 2.1 dá suporte a uma variedade de importantes plataformas de cliente e servidor. Para obter mais informações, consulte [Plataformas com suporte](supported-platforms.md).

## Princípios básicos

**Simplicidade** – padrões de uso e comentários para AD RMS SDK 1.0 foram analisados e esses dados foram usados para simplificar ou automatizar as tarefas de programação mais difícil. Aplicativos RMS criados usando o RMS SDK 2.1 normalmente exigem de cinco a dez menos linhas de código RMS que aplicativos RMS escritos usando o AD RMS SDK 1.0.
**Escreva uma vez**— os aplicativos RMS SDK 2.1 não precisam de alteração ou recompilação de código para funcionarem com os recursos mais recentes do RMS. Novos recursos do RMS estarão disponíveis em seu aplicativo existente conforme são adicionados ao servidor RMS.
**Consistência**— o RMS SDK 2.1 ajuda a tornar mais fácil escrever aplicativos que cumpram consistentemente configurações diferentes do RMS. Ele também reduzem significativamente a quantidade da interface do usuário do RMS que você, como desenvolvedor do aplicativo, precisa criar, incentivando uma aparência consistente e reduzindo a necessidade de treinamento do usuário.

## Tópicos relacionados

* [Exemplos do AD RMS](samples.md)
* [Blog do Desenvolvedor do AD RMS](http://blogs.msdn.com/b/rms/)
* [Instalar o SDK](install-the-rms-sdk.md)
* [IPCHelloWorld - um aplicativo de exemplo](how-to-build-your-first-application.md)
* [Visão geral](ad-rms-overview.md)
* [Plataformas com suporte](supported-platforms.md)
 

 


<!--HONumber=Jun16_HO2-->


