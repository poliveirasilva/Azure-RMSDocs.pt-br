---
# required metadata

title: Plano de implementação do Azure Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Plano de implementação do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Utilize os seguintes passos para preparar, implementar e gerir o Azure Rights Management (Azure RMS) na sua organização.

No entanto, se apenas pretender experimentar rapidamente o Azure RMS para si próprio, em vez de o implementar num ambiente de produção, consulte [Tutorial de início rápido do Azure Rights Management](../get-started/quick-start-tutorial.md).

Para ver uma lista de cenários específicos e passos de configuração associados e a documentação do utilizador final, consulte o [Guia de implementação rápida do Azure Rights Management](../get-started/rapid-deployment-guide.md)..

> [!IMPORTANT]
> Antes de efetuar os passos seguintes, certifique-se de que consultou [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

## Passo 1: confirmar se tem uma subscrição que inclui o Azure Rights Management
Existe mais do que um tipo de subscrição que inclui o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Consulte [Subscrições na nuvem que suportam o Azure RMS](../get-started/requirements-subscriptions.md) e verifique se a subscrição inclui as funcionalidades que pretende utilizar na sua organização ao consultar a tabela [Comparação das Ofertas do Rights Management Services (RMS)](https://technet.microsoft.com/dn858608). Terá de atribuir uma licença desta subscrição a cada utilizador na sua organização que venha a proteger ficheiros e mensagens de e-mail utilizando o Azure RMS.

## Passo 2: preparar a sua conta de inquilino para utilizar o Rights Management
Antes de começar a utilizar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], efetue a preparação seguinte:

1.  Certifique-se de que o seu inquilino do Azure ou do Office 365 contém as contas de utilizador e grupos que vão ser utilizados pelo Azure RMS para autenticar os utilizadores da sua organização. Se for necessário, crie estas contas e grupos ou sincronize-os partir do seu diretório local. Para obter mais informações, consulte [Preparar para o Azure Rights Management](prepare.md).

2.  Decida se pretende que a Microsoft efetue a gestão da sua chave de inquilino (predefinição) ou se pretende gerar e gerir a sua chave de inquilino sozinho (conhecido como traga a sua própria chave ou BYOK). Tenha em atenção que, atualmente, não é possível utilizar BYOK se utilizar o Exchange Online. Para mais informações, consulte [Planear e implementar a chave de inquilino do Azure Rights Management](plan-implement-tenant-key.md).

3.  Instale o módulo do Windows PowerShell para o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] em, pelo menos, um computador que tenha acesso à Internet. Pode efetuar este passo agora ou mais tarde. Para mais informações, consulte [Instalar o Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

4.  Se estiver a utilizar serviços de Gestão de Direitos no local: efetue uma migração para mover as chaves, os modelos e os URLs para a nuvem. Para mais informações, consulte [Migrar do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md)..

5.  Ative o Rights Management de modo a poder começar a utilizar o serviço. Se for necessária uma implementação faseada, configure os controlos de inclusão do utilizador para restringir a utilização a utilizadores específicos. Para mais informações, consulte [Ativar o Azure Rights Management](../deploy-use/activate-service.md).

Opcionalmente, considere configurar o seguinte:

-   Modelos personalizados se os modelos de política de direitos predefinidos não forem suficientes para a sua organização. Pode efetuar este passo agora ou mais tarde. Para obter mais informações, consulte [Configurar modelos personalizados para o Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registo de utilização para que possa monitorizar a forma como a sua organização utiliza o Rights Management. Pode efetuar este passo agora ou mais tarde. Para obter mais informações, consulte [Registo e análise da utilização do Azure Rights Management](../deploy-use/log-analyze-usage.md).

## Passo 3: configurar as suas aplicações e serviços para o Rights Management
Configurar as suas aplicações e serviços pode incluir a instalação da aplicação de partilha Rights Management e a ativação do suporte para funcionalidades de Gestão de Direitos de Informação (IRM) no SharePoint Online ou no Exchange Online. Para obter mais informações, consulte [Configurar aplicações para o Azure Rights Management](../deploy-use/configure-applications.md).

Se possuir serviços de TI existentes que necessitem de inspecionar ficheiros que o Azure RMS vai proteger, tais como soluções de prevenção de fuga de dados (DLP), gateways de encriptação de conteúdo (CEG) e produtos antimalware, configure as contas de serviço para que sejam superutilizadores do Azure RMS. Para mais informações, consulte [Configurar superutilizadores para o Azure Rights Management e serviços de deteção ou recuperação de dados](../deploy-use/configure-super-users.md).

Para poder proteger/desproteger em volume todos os tipos de ficheiros, instale a Ferramenta de Proteção RMS, que utiliza o módulo do PowerShell da Proteção do RMS. Para mais informações, consulte [Cmdlets da Proteção RMS](https://msdn.microsoft.com/library/mt433195.aspx)..

Se possuir serviços no local que pretende utilizar com o Azure Rights Management, instale e configure o conector Rights Management. Para mais informações, consulte [Implementar o conetor Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Passo 4: publicar e consumir conteúdo protegido por direitos
Agora está pronto para publicar e consumir conteúdo protegido, bem como para registar de que forma a sua empresa está a utilizar o Rights Management. Para obter mais informações, consulte [Ajudar os utilizadores a proteger ficheiros ao utilizar o Azure Rights Management](../deploy-use/help-users.md) e [Registo e análise da utilização do Azure Rights Management](../deploy-use/log-analyze-usage.md).

Se estiver interessado em proteger ficheiros automaticamente ao utilizar a Infraestrutura de Classificação de Ficheiros num servidor de ficheiros baseado no Windows, consulte [Proteção RMS com Infraestrutura de Classificação de Ficheiros (FCI) do Windows Server](../rms-client/configure-fci.md).

## Passo 5: administrar o Rights Management para a sua conta de inquilino, conforme necessário
À medida que começar a utilizar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], poderá considerar o módulo [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para o Windows PowerShell útil para ajudar a efetuar scripts ou a automatizar alterações administrativas. Para obter mais informações, consulte [Administrar o Azure Rights Management ao utilizar o Windows PowerShell](../deploy-use/administer-powershell.md).




<!--HONumber=May16_HO2-->


