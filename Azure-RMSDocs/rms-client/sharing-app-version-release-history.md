---
title: "Aplicativo de compartilhamento Rights Management&colon; Histórico de lançamento de versão | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: b19eadd408837ebcd77b3ae2f9520f5286fcf41f
ms.openlocfilehash: cad9d01735d8e649875bc6bba73d29573891e1d8


---

# Aplicativo de compartilhamento do Rights Management: histórico de lançamento de versão

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

A equipe do Rights Management atualiza o aplicativo Rights Management sharing regularmente para correções e novas funcionalidades. Use as informações a seguir para ver o que há de novo ou o que foi alterado em uma versão. A versão mais recente é listada primeiro.

As versões anteriores a 1º de janeiro de 2015 não são listadas.

> [!NOTE] Se você tiver comentários ou uma pergunta sobre o aplicativo RMS sharing, envie uma mensagem de email para [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Versão 1.0.2191.0
**Lançada em**: 16/06/2016

**Correções**:

- O site de acompanhamento do documento agora mostra o número correto de modos de exibição para cada documento acompanhado.

- Modelos para todas as localidades agora são exibidos como disponíveis para os usuários.

- Depois de usar o compartilhamento protegido para um arquivo do PowerPoint, as alterações na versão local do arquivo são salvas corretamente.

- Pequeno número de bugs secundários e melhorias para mensagens de erro.


## Versão 1.0.2004.0
**Lançada**: 11/12/2015

**Correções**:

-   Somente o proprietário do arquivo e as pessoas com níveis de permissões de **Coproprietário** podem desproteger os arquivos. Anteriormente, o proprietário e as pessoas com os níveis de permissões **Coautor** e **Coproprietário** podiam desproteger arquivos.

-   Proteção nativa para arquivos **.tif** (além de arquivos .tiff), para produzir um arquivo **.ptif** protegido por RMS e somente leitura.

-   Melhorias para as mensagens de erro (precisão e clareza).

-   Melhorias de desempenho para criptografar e descriptografar conteúdo.

**Novos recursos**:

-   Suporte para instalação de não-administrador, para que os usuários padrão possam instalar o aplicativo RMS sharing.

    Existem algumas restrições para usuários padrão que executam o Office 2010. Para obter mais informações, consulte a seção [Se você não for um administrador local e usar o Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) nas instruções para o usuário [Baixar e instalar o aplicativo de compartilhamento Rights Management](install-sharing-app.md).

## Versão 1.0.1908.0
**Lançada**: 16/9/2015

**Correções**:

-   Suporte para Multi-Factor Authentication (MFA) para o Azure RMS, que também remove a dependência do assistente de conexão da Microsoft que usa autenticação moderna.

    Para obter mais informações, consulte a seção [Multi-Factor Authentication (MFA) e Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) de [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

## Versão 1.0.1784.0
**Lançada**: 30/7/2015

**Correções**:

-   O intervalo de atualização padrão para modelos de política de direitos foi reduzido de 7 dias para 1 dia.

-   Pequeno número de bugs menores e regressões.

## Versão 1.0.1770.0
**Lançada**: 25/4/2015

**Correções**:

-   Agora, somente o proprietário e os coproprietários podem remover a proteção. Co-autores não podem remover a proteção.

-   Os arquivos que estão em um compartilhamento de rede agora podem ser protegidos.

**Novos recursos**:

-   Suporte para rastreamento e revogação de documentos. Para obter mais informações, consulte [Rastrear e revogar seus documentos ao usar o aplicativo RMS sharing](sharing-app-track-revoke.md).

-   Suporte de modelo quando você escolhe **Compartilhamento protegido**:

    -   Agora você pode selecionar modelos.

    -   Em vez do controle deslizante, você verá uma caixa de listagem que inclui modelos e permissões personalizadas.

    -   Você não verá mais opções para **Permitir consumo em todos os dispositivos** e **Impor restrições de uso**. Em vez disso, **Proteção genérica** é selecionada automaticamente, dependendo do tipo de arquivo.

    Para obter mais informações, consulte [Opções de caixa de diálogo para o aplicativo de compartilhamento Rights Management](sharing-app-dialog-box.md).

## Versão 1.0.1667.0
**Lançada**: 19/1/2015

**Correções**:

-   Suporte a fontes do idioma chinês no visualizador PPDF do aplicativo RMS sharing.

-   Melhor manipulação de erros e mensagens.

-   Correção para um problema com a notificação de atualização automática quando uma versão mais recente do aplicativo está disponível para download.

**Novos recursos**:

-   **Suporte para vários domínios de email dentro de sua organização**: se você usa o AD RMS e os usuários em sua organização têm vários domínios de email, essa atualização permite que os usuários consumam conteúdo protegido por usuários em sua organização em outros domínios. Para obter mais informações, consulte a seção [Somente AD RMS: suporte para vários domínios de email dentro de sua organização](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization) no [guia de administrador do aplicativo de compartilhamento Rights Management](sharing-app-admin-guide.md).




<!--HONumber=Jun16_HO3-->


