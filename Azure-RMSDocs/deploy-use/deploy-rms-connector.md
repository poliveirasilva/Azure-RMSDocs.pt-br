---
title: Implementar o conector Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e31656e417a0861d33deb2436d2e4b596a7512a7
ms.openlocfilehash: 6b9b3b039ba2de0de174a134768afd763d26b5dd


---

# Implementar o conector Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Utilize estas informações para saber mais acerca do conector Azure Rights Management (RMS) e como pode utilizá-lo para proporcionar proteção de informações com as implementações no local existentes que utilizam o Microsoft Exchange Server, o Microsoft SharePoint Server ou servidores de ficheiros que executam o Windows Server e utilizam a capacidade de Infraestrutura de Classificação de Ficheiros (FCI) do Gestor de Recursos do Servidor de Ficheiros.

> [!TIP]
> Para um cenário geral de exemplo com capturas de ecrã, consulte a secção [Proteger automaticamente ficheiros em servidores de ficheiros a executar o Windows Server e a Infraestrutura de Classificação de Ficheiros](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure) no artigo [O Azure RMS em ação](../understand-explore/what-admins-users-see.md).

## Descrição geral do conector Microsoft Rights Management
O conector Microsoft Rights Management (RMS) permite-lhe ativar rapidamente servidores no local existentes para utilizar a respetiva funcionalidade de Gestão de Direitos de Informação (IRM) com o serviço Microsoft Rights Management (Azure RMS) baseado na nuvem. Com esta funcionalidade, o departamento de TI e os utilizadores podem proteger facilmente documentos e imagens dentro e fora da organização, sem terem de instalar outras infraestruturas ou estabelecer relações de fidedignidade com outras organizações. Pode utilizar este conector, mesmo que alguns dos seus utilizadores estabeleçam ligação a serviços online, num cenário híbrido. Por exemplo, as caixas de correio de alguns utilizadores utilizam o Exchange Online e as caixas de correio de alguns utilizadores utilizam o Exchange Server. Depois de instalar o conector RMS, todos os utilizadores podem proteger e consumir mensagens de e-mail e anexos ao utilizar o Azure RMS, sendo que a proteção de informações funciona na perfeição entre as duas configurações de implementação.

O conector RMS é um serviço com poucos requisitos de espaço que se instala no local, em servidores que executem o Windows Server 2012 R2, o Windows Server 2012 ou o Windows Server 2008 R2. Além de executar o conector em computadores físicos, também pode executá-lo em máquinas virtuais, incluindo VMs IaaS do Azure. Depois de instalar e configurar o conector, este funciona como uma interface de comunicações (um reencaminhamento) entre os servidores no local e o serviço em nuvem.

Se gerir a sua própria chave de inquilino para o Azure RMS (o cenário traga a sua própria chave ou BYOK), o conector RMS e os servidores no local que a utilizam não acedem ao módulo de hardware de segurança (HSM) que contém a chave de inquilino. Isto acontece porque todas as operações de criptografia que utilizam a chave de inquilino são executadas no Azure RMS e não no local.

![Descrição geral da arquitetura do conector RMS](../media/RMS_connector.png)

O conector RMS suporta os seguintes servidores no local: Exchange Server, SharePoint Server e servidores de ficheiros que executam o Windows Server e utilizam a Infraestrutura de Classificação de Ficheiros para classificar e aplicar políticas a documentos do Office numa pasta. Se pretender proteger todos os tipos de ficheiros ao utilizar a Classificação de Ficheiros, não utilize o conector RMS, mas sim os [cmdlets Proteção RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> Para ficar a conhecer as versões suportadas destes serviços no local, consulte [Servidores no local que suportam o Azure RMS](..\get-started\requirements-servers.md).

Utilize as seguintes informações para o ajudar a planear, instalar e configurar o conector RMS. Em seguida, é necessário efetuar algumas tarefas de configuração pós-instalação para que os servidores possam utilizar o conector.

-   [Pré-requisitos do conector RMS](deploy-rms-connector.md#prerequisites-for-the-rms-connector)

-   **Passo 1:**  [instalar o conector RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Passo 2:**  [introduzir credenciais](install-configure-rms-connector.md#entering-credentials)

-   **Passo 3:**  [autorizar os servidores a utilizar o conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Passo 4:**  [configurar o balanceamento de carga e a elevada disponibilidade](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   Opcional: [configurar o conector RMS para utilizar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   Opcional: [configurar o conector RMS para um servidor proxy Web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   Opcional: [instalar a ferramenta de administração do conector RMS em computadores administrativos](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Passo 5:**  [configurar servidores para utilizar o conector RMS](configure-servers-rms-connector.md)

    -   [Configurar um servidor Exchange para utilizar o conector](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configurar um servidor SharePoint para utilizar o conector](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configurar um servidor de ficheiros da Infraestrutura de Classificação de Ficheiros para utilizar o conector](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## Pré-requisitos do conector RMS
Antes de instalar o conector RMS, certifique-se de que os seguintes requisitos são cumpridos.

|Requisito|Mais informações|
|---------------|--------------------|
|O serviço Rights Management (RMS) está ativado|[Ativar o Azure Rights Management](activate-service.md)|
|Sincronização de diretórios entre as suas florestas do Active Directory no local e o Azure Active Directory|Depois de o RMS estar ativado, tem de configurar o Azure Active Directory para funcionar com os utilizadores e os grupos na sua base de dados do Active Directory.<br /><br />**Importante**: é necessário efetuar este passo de sincronização de diretórios para que o conector RMS funcione, inclusivamente para uma rede de teste. Apesar de poder utilizar o Office 365 e o Azure Active Directory através de contas que cria manualmente no Azure Active Directory, este conector requer que as contas no Azure Active Directory estejam sincronizadas com os Serviços de Domínio do Active Directory. A sincronização manual de palavra-passe não é suficiente.<br /><br />Para mais informações, consulte os seguintes recursos:<br /><br />[Integrar as suas identidades no local com o Azure Active Directory](/active-directory/active-directory-aadconnect)<br /><br />[Comparação de ferramentas de integração de diretórios de Identidade Híbrida](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|Opcional mas recomendado:<br /><br />Ativar a federação entre o Active Directory no local e o Azure Active Directory|Pode ativar a federação de identidade entre o diretório no local e o Azure Active Directory. Esta configuração permite uma experiência de utilizador mais estável através da utilização do início de sessão único no serviço RMS. Sem o início de sessão único, é pedido aos utilizadores para indicarem as respetivas credenciais antes de poderem utilizar conteúdo protegido por direitos.<br /><br />Para obter instruções para configurar a federação ao utilizar Serviços de Federação do Active Directory (AD FS) entre os Serviços de Domínio do Active Directory e o Azure Active Directory, consulte a [Lista de Verificação: utilizar o AD FS para implementar e gerir o início de sessão único](http://technet.microsoft.com/library/jj205462.aspx) na biblioteca do Windows Server.|
|Um mínimo de dois computadores membros em que pretende instalar o conector RMS:<br /><br />- Um computador físico ou virtual de 64 bits com um dos seguintes sistemas operativos: Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.<br /><br />- Um mínimo de 1 GB de RAM.<br /><br />- Um mínimo de 64 GB de espaço em disco.<br /><br />- Pelo menos uma interface de rede.<br /><br />- Acesso à Internet através de uma firewall (ou proxy Web) que não exija autenticação.<br /><br />- Tem de estar numa floresta ou domínio que confie noutras florestas na organização que contêm instalações de servidores do Exchange ou do SharePoint que pretenda utilizar com o conector RMS.|Para conseguir tolerância a falhas e elevada disponibilidade, tem de instalar o conector RMS, no mínimo, em dois computadores.<br /><br />**Sugestão**: se estiver a utilizar o Outlook Web Access ou dispositivos móveis que utilizem o Exchange ActiveSync IRM e se for fundamental manter o acesso a e-mails e anexos que estão protegidos pelo Azure RMS, recomendamos que implemente um grupo com balanceamento de carga de servidores de conector para assegurar a elevada disponibilidade.<br /><br />Não necessita de servidores dedicados para executar o conector, mas tem de instalá-lo num computador separado dos servidores que irão utilizar o conector.<br /><br />**Importante**: não instale o conector num computador que executa o Exchange Server, o SharePoint Server ou um servidor de ficheiros que esteja configurado para a infraestrutura de classificação de ficheiros se pretender utilizar a funcionalidade a partir destes serviços com o Azure RMS. Além disso, não instale este conector num controlador de domínio.|

## Passos seguintes

Aceda a [Instalar e configurar o conector Azure Rights Management](install-configure-rms-connector.md).


<!--HONumber=Jun16_HO4-->


