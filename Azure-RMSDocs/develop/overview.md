---
# required metadata

title: Descrição geral | Azure RMS
description: O AD RMS e o Azure RMS são uma tecnologia de proteção de informações que ajudam a salvaguardar as informações digitais contra a utilização não autorizada.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8A13494E-C1D7-407D-BCD1-A406915EA578
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Descrição Geral


O Microsoft Rights Management Services (AD RMS e Azure RMS) é uma tecnologia de proteção de informações que ajuda a salvaguardar as informações digitais contra a utilização não autorizada. Através das aplicações com capacidade para direitos, os proprietários de conteúdo conseguirão definir quem pode abrir, modificar, imprimir, reencaminhar ou efetuar outras ações no conteúdo.

O SDK Microsoft Rights Management 4.2 está disponível para várias plataformas e é uma arquitetura ou um SDK (Software Development Kit), que foi concebido para computadores cliente e dispositivos para ajudar a proteger o acesso e utilização das informações que circulam pelas aplicações com “capacidade para direitos”. Os SDKs para estas plataformas fornecem uma API simples para um programador de aplicações proteger ou consumir conteúdos digitais, obter modelos e adquirir políticas de um servidor e outras tarefas de gestão de direitos relacionados.

Para obter mais informações sobre as plataformas atualmente suportadas, consulte o nosso portal de documentação para programadores do [SDK Microsoft Rights Management](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md).

Seguem-se alguns dos possíveis cenários:

-   Uma firma de advogados pretende impedir que as mensagens de e-mail confidenciais sejam impressas ou reencaminhadas num dispositivo móvel.
-   Os programadores do projeto assistido por computador e software de fabrico pretendem limitar o acesso de desenho a um pequeno grupo de utilizadores dentro da divisão de pesquisa sem a necessidade da utilização de palavras-passe.
-   Os proprietários de uma aplicação móvel de design gráfico pretendem utilizar uma única licença que permita a livre visualização de cópias de baixa resolução das suas imagens, mas requer o pagamento para o acesso a versões de alta resolução.
-   Os proprietários de uma biblioteca de documentos online pretendem ativar direitos para ver, imprimir ou editar documentos com base na identidade do utilizador quando os documentos são transferidos para um dispositivo móvel.
-   Uma empresa pretende publicar informações confidenciais sobre os funcionários num Web site interno que restringe a visualização e edição de privilégios a determinados utilizadores.

O SDK MS RMS 4.2 pode ser transferido, com o reconhecimento e a aceitação do respetivo contrato de licença, distribuído gratuitamente com o seu software de terceiros para permitir o acesso de cliente ao conteúdo que foi protegido por direitos através da utilização e implementação de servidores AD RMS no seu ambiente ou serviços do Azure RMS. Para obter mais informações, consulte [Introdução](get-started.md).

## Destaques do SDK


O SDK MS RMS 4.2 oferece algumas funcionalidades novas que incluem o seguinte:

-   **API reformulada** – a API do SDK MS RMS 4.2 foi reformulada para uma simplicidade máxima para que os programadores possam desfrutar de uma API de encriptação e desencriptação simples e transparente, que forneça comportamentos de RMS consistentes com esforços mínimos.
-   **Suporte híbrido para o AD RMS e o Azure RMS** – uma única aplicação com suporte RMS pode consumir e proteger conteúdo do servidor AD RMS (utilizando a extensão do dispositivo móvel do AD RMS) e do serviço do Azure RMS. O SDK MS RMS 4.2 deteta de forma transparente o ponto final relevante que os administradores de TI podem configurar.
-   **Traga a sua própria biblioteca de autenticação** – como um programador de aplicações, pode escolher que biblioteca de autenticação é utilizada com o SDK MS RMS 4.2. Quer seja a [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx) ou a biblioteca personalizada da sua organização, o SDK MS RMS 4.2 divide a pilha de autorização para que possa escolher a biblioteca que mais se adequa às suas necessidades.
-   **Traga a sua própria interface de utilizador** – o SDK MS RMS 4.2 agora permite-lhe implementar a sua interface de utilizador personalizada. Desde proteger conteúdo e escolher modelos, a mostrar e alterar as permissões enquanto é consumido conteúdo protegido, o SDK MS RMS 4.2 não impõe qualquer IU incorporada nas suas aplicações. Se quiser, no entanto, pode utilizar bibliotecas da IU do Microsoft RMS para todas as plataformas através da nossa [Conta do GitHub](https://github.com/AzureAD/).
-   **Aceder aos conteúdos protegidos offline** – o SDK MS RMS 4.2 permite aos utilizadores de aplicações aceder aos conteúdos protegidos, mesmo quando não existe acesso à Internet. O SDK MS RMS 4.2 coloca em cache as políticas de consumo dos conteúdos protegidos em segurança para que os utilizadores possam aceder aos dados protegidos do RMS offline.

Utilize o guia de [Introdução](get-started.md) para iniciar o projeto de aplicação do dispositivo de informações protegidas.

## Tópicos relacionados

* [SDK Microsoft Rights Management](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [Introdução](get-started.md)
* [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx)
* [Conta do GitHub](https://github.com/AzureAD/)
 

 





<!--HONumber=Apr16_HO4-->


