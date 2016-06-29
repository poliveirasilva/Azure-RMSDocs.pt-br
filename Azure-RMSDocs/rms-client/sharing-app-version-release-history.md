---
# required metadata

title: Aplicação de partilha Rights Management&colon; histórico de lançamento de versões | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Aplicação de partilha Rights Management: histórico de lançamento de versões

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

A equipa do Rights Management atualiza regularmente a aplicação de partilha Rights Management com correções e novas funcionalidades. Utilize as seguintes informações para ver o que há de novo ou o que foi alterado num lançamento. A versão mais atual aparece em primeiro na lista.

As versões anteriores a 1 de janeiro de 2015 não estão listadas.

> [!NOTE]
> Se tiver comentários ou uma pergunta sobre a aplicação de partilha RMS, envie uma mensagem de e-mail para [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Versão 1.0.2004.0
**Lançada**: 11/12/2015

**Correções**:

-   Apenas o proprietário do ficheiro e as pessoas com níveis de permissões de **Coproprietário** podem desproteger ficheiros. Anteriormente, o proprietário e as pessoas com níveis de permissões de **Coautor** e **Coproprietário** podiam desproteger ficheiros.

-   Proteção nativa para ficheiros **.tif** (além de ficheiros .tiff), para produzir um ficheiro **.ptif** só de leitura protegido pelo RMS.

-   Melhoramentos nas mensagens de erro (precisão e clareza).

-   Melhoramentos de desempenho para a encriptação e desencriptação de conteúdo.

**Novas funcionalidades**:

-   Suporte para a instalação por não administradores, para que os utilizadores padrão possam instalar a aplicação de partilha RMS.

    Existem algumas restrições para os utilizadores padrão que executam o Office 2010. Para obter mais informações, consulte a secção [Se não for um administrador local e utilizar o Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) nas instruções do utilizador para [Transferir e instalar a aplicação de partilha Rights Management](install-sharing-app.md).

## Versão 1.0.1908.0
**Lançada**: 16/09/2015

**Correções**:

-   Suporte para a autenticação multifator (MFA) para o Azure RMS, que também remove a dependência do Assistente de Início de Sessão do Microsoft para as aplicações que utilizam autenticação moderna.

    Para obter mais informações, consulte a secção [Multi-Factor Authentication (MFA) e Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) em [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

## Versão 1.0.1784.0
**Lançada**: 30/07/2015

**Correções**:

-   O intervalo de atualização predefinido dos modelos de política de direitos foi reduzido de 7 dias para 1 dia.

-   Um pequeno número de regressões e erros secundários.

## Versão 1.0.1770.0
**Lançada**: 25/04/2015

**Correções**:

-   Agora, apenas o proprietário e os coproprietários podem remover a proteção. Os coautores não podem remover a proteção.

-   Agora, os ficheiros que se encontram numa partilha de rede podem ser protegidos.

**Novas funcionalidades**:

-   Suporte para revogação e controlo de documentos. Para obter mais informações, consulte [Controlar e revogar os documentos quando utiliza a aplicação de partilha RMS](sharing-app-track-revoke.md).

-   Suporte para modelos quando escolhe **Partilhar Protegido**:

    -   Agora, pode selecionar modelos.

    -   Em vez do controlo de deslize, verá uma caixa de listagem que inclui modelos e permissões personalizadas.

    -   Já não vê opções para **Permitir consumo em todos os dispositivos** e **Impor restrições de utilização**. Em vez disso, a **Proteção Genérica** é automaticamente selecionada, dependendo do tipo de ficheiro.

    Para obter mais informações, consulte [Opções da caixa de diálogo para a aplicação de partilha Rights Management](sharing-app-dialog-box.md).

## Versão 1.0.1667.0
**Lançada**: 19/01/2015

**Correções**:

-   Suporte para tipos de letra do idioma chinês no visualizador de PPDF da aplicação de partilha RMS.

-   Tratamento de erros e mensagens melhorados.

-   Correção de um problema com a notificação de atualização automática quando uma versão mais recente da aplicação está disponível para transferência.

**Novas funcionalidades**:

-   **Suporte para múltiplos domínios de e-mail dentro da sua organização**: se utilizar o AD RMS e os utilizadores da sua organização tiverem múltiplos domínios de e-mail, esta atualização permite que os seus utilizadores consumam conteúdo que foi protegido por utilizadores da sua organização noutros domínios. Para obter mais informações, consulte a secção [Apenas AD RMS: suporte para múltiplos domínios de e-mail dentro da sua organização](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization) no [Guia do administrador da aplicação de partilha Rights Management](sharing-app-admin-guide.md).



<!--HONumber=Apr16_HO4-->


