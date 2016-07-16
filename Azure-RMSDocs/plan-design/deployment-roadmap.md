---
title: "Roteiro de implantação do Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7f8a4d53665dd79a6d0e02d340b0e7a09d995e00
ms.openlocfilehash: 96ee0aa3151ede8b8a263f3ce6c3d2e5b8ec9c81


---

# Roteiro de implantação do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use as seguintes etapas para se preparar para implementar e gerenciar o Azure Rights Management (Azure RMS) para a sua organização.

No entanto, se quiser testar rapidamente o Azure RMS para si mesmo, em vez de distribuí-lo em um ambiente de produção, consulte [Tutorial de início rápido para o Azure Rights Management](../get-started/quick-start-tutorial.md).

Para obter uma lista de cenários específicos e etapas de configuração associados e documentação do usuário final, consulte o [Guia de implantação rápida para o Azure Rights Management](../get-started/rapid-deployment-guide.md).

> [!IMPORTANT]
> Antes de realizar estas etapas, certifique-se de ter revisado os [Requisitos para o Azure Rights Management](../get-started/requirements-azure-rms.md).

## Etapa 1: Confirme se você tem uma assinatura que inclui o Azure Rights Management
Há mais de um tipo de assinatura que inclui [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Consulte [Assinaturas da nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md) e verifique se sua assinatura inclui a funcionalidade que você deseja usar em sua organização fazendo referência à tabela em [Ofertas de comparação do Rights Management Services (RMS)](https://technet.microsoft.com/dn858608). Você precisará atribuir uma licença dessa assinatura para cada usuário em sua organização que vai proteger arquivos e emails usando o Azure RMS.

## Etapa 2: Prepare a sua conta de locatário para usar o Rights Management
Antes de começar a usar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], faça a seguinte preparação:

1.  Certifique-se de que seu locatário do Azure ou Office 365 contém as contas de usuário e grupos que serão usados pelo Azure RMS para autenticar usuários de sua organização. Se necessário, crie essas contas e grupos ou sincronize-as à partir do seu diretório local. Para obter mais informações, consulte [Preparação para o Azure Rights Management](prepare.md).

2.  Decida se deseja que a Microsoft gerencie sua chave de locatário (a padrão), ou se quer gerar e gerenciar sua chave de locatário por conta própria (conhecido como trazer a sua própria chave, ou BYOK). Observe que, no momento, você não pode usar o BYOK se usar o Exchange Online. Para mais informações, consulte o [Planejamento e implementação de sua chave de locatário do Azure Rights Management](plan-implement-tenant-key.md).

3.  Instale o módulo do Windows PowerShell do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] em pelo menos um computador que tenha acesso à Internet. Você pode executar esta etapa agora ou mais tarde. Para obter mais informações, consulte [Instalação do Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

4.  Se você estiver usando os serviços do Rights Management local: execute uma migração para mover as chaves, modelos e URLs para a nuvem. Para mais informações, consulte [Migrando do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).

5.  Ative o Rights Management de modo que você possa começar a usar o serviço. Se uma implantação em fases for necessária, configure controles de integração de usuário para restringir o uso a usuários específicos. Para obter mais informações, consulte [Ativando o Azure Rights Management](../deploy-use/activate-service.md).

Opcionalmente, considere a configuração a seguir:

-   Personalize modelos se os modelos de política de direitos padrão não forem suficientes para a sua organização. Você pode executar esta etapa agora ou mais tarde. Para obter mais informações, consulte [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Log de uso para que você possa monitorar como a sua organização está usando o Rights Management. Você pode executar esta etapa agora ou mais tarde. Para obter mais informações, consulte [Registrando em log e analisando o uso do Azure Rights Management](../deploy-use/log-analyze-usage.md).

## Etapa 3: Configure os seus aplicativos e serviços para o Rights Management
A configuração dos seus aplicativos e serviços pode incluir a instalação do aplicativo de compartilhamento Rights Management e habilitar o suporte para os recursos de IRM (Gerenciamento de Direitos de Informação) no Exchange Online ou no SharePoint Online. Para obter mais informações, consulte [Configurando aplicativos para o Azure Rights Management](../deploy-use/configure-applications.md).

Se você tiver serviços de TI existentes que precisam inspecionar os arquivos que o Azure RMS protegerá — como soluções de DLP (prevenção de vazamento de dados), os CEGs (gateways de criptografia de conteúdo) e produtos antimalware — configure as contas de serviço que serão superusuários para o Azure RMS. Para mais informações, veja [Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou a recuperação de dados](../deploy-use/configure-super-users.md).

Para proteger em massa ou desproteger em massa todos os tipos de arquivo, instale a ferramenta de proteção do RMS, que usa o módulo do PowerShell de proteção do RMS. Para obter maiores informações, consulte [Cmdlets de Proteção do RMS](https://msdn.microsoft.com/library/mt433195.aspx).

Se você tiver serviços no local que deseja usar com o Azure Rights Management, instale e configure o conector Rights Management. Para obter mais informações, consulte [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Etapa 4: publique e consuma conteúdo com direitos protegidos
Você agora está pronto para publicar e consumir conteúdo protegido e registrar como a sua empresa está usando o gerenciamento de direitos. Para obter mais informações, consulte [Ajudando os usuários a proteger arquivos usando o Azure Rights Management](../deploy-use/help-users.md) e [Registro em log e análise do uso do Azure Rights Management](../deploy-use/log-analyze-usage.md).

Se você estiver interessado em proteger arquivos automaticamente usando a FCI (Infraestrutura de Classificação de Arquivos) em um servidor de arquivos do Windows, consulte [Proteção do RMS com FCI (Infraestrutura de Classificação de Arquivos) do Windows Server](../rms-client/configure-fci.md).

## Etapa 5: Administre o Rights Management para sua conta de locatário, conforme necessário
Ao começar a usar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], talvez você ache que o módulo do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para Windows PowerShell seja útil para ajudar o script ou automatizar alterações administrativas. Para obter mais informações, consulte [Administrando o Azure Rights Management usando o Windows PowerShell](../deploy-use/administer-powershell.md).





<!--HONumber=Jun16_HO4-->


