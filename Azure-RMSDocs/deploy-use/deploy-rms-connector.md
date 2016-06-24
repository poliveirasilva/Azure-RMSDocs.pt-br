---
# required metadata

title: Implantando o conector do Azure Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Implantando o conector do Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Use essas informações para saber mais sobre o conector RMS (Microsoft Rights Management) e como você pode usá-lo para fornecer proteção de informações com atuais implantações locais que usam o Microsoft Exchange Server, o Microsoft SharePoint Server ou servidores de arquivos que executam o Windows Server, além de usar a capacidade FCI (Infraestrutura de Classificação de Arquivos) do Gerenciador de Recursos de Servidor de Arquivos.

> [!TIP] Para obter um exemplo de alto nível com capturas de tela, consulte a seção [Protegendo automaticamente arquivos em servidores de arquivos executando o Windows Server e a infraestrutura de classificação de arquivos](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure) no artigo [Azure RMS em ação](../understand-explore/what-admins-users-see.md).

## Visão geral do conector do Microsoft Rights Management
O conector Microsoft Rights Management (RMS) permite que você ative rapidamente servidores locais existentes para usar a funcionalidade Information Rights Management (IRM) com o Microsoft Rights Management Service (Azure RMS) baseado em nuvem. Com essa funcionalidade, o departamento de TI e os usuários podem facilmente proteger documentos e imagens, tanto dentro quanto fora da organização, sem ter que instalar infraestrutura adicional ou estabelecer relações de confiança com outras organizações. Você pode usar este conector em um cenário híbrido, mesmo se alguns dos seus usuários estiverem se conectando a serviços online. Por exemplo, caixas de correio de alguns usuários usam o Exchange Online e caixas de correio de outros usuários usam o Exchange Server. Depois de instalar o conector RMS, todos os usuários podem proteger e consumir emails e anexos usando o Azure RMS e a proteção de informações funciona perfeitamente entre as duas configurações de implantação.

O conector RMS é um serviço de superfície pequena que você instala localmente, em servidores que executam o Windows Server 2012 R2, o Windows Server 2012 ou o Windows Server 2008 R2. Além de executar o conector em computadores físicos, você também pode executá-lo em máquinas virtuais, incluindo as VMs de IaaS do Azure. Depois de instalar e configurar o conector, ele atua como uma interface de comunicação (um relê) entre os servidores locais e o serviço de nuvem.

Se você gerenciar sua própria chave de locatário para o Azure RMS (traga sua própria chave ou cenário BYOK), o conector RMS e os servidores locais que o utilizam não acessarão o HSM (módulo de segurança de hardware) que contém sua chave de locatário. Isso ocorre porque todas as operações criptográficas que usam a chave de locatário são executadas no Azure RMS e não localmente.

![Visão geral de arquitetura do conector RMS](../media/RMS_connector.png)

O conector RMS dá suporte aos seguintes servidores locais: Exchange Server, SharePoint Server e os servidores de arquivos que executam o Windows Server e usam a Infraestrutura de Classificação de Arquivos para classificar e aplicar políticas de documentos do Office em uma pasta. Se você deseja proteger todos os tipos de arquivos usando a classificação de arquivos, não use o conector RMS, mas, em vez disso, use os [cmdlets do RMS Protection](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE] Para obter as versões com suporte desses servidores locais, consulte [Servidores locais que dão suporte ao Azure RMS](..\get-started\requirements-servers.md).

Use as informações a seguir para lhe ajudar a planejar, instalar e configurar o conector RMS. Depois, será necessário fazer algumas configurações pós-instalação para que os servidores possam usar o conector.

-   [Pré-requisitos para o conector RMS](deploy-rms-connector.md#prerequisites-for-the-rms-connector)

-   **Etapa 1:** [Instalando o conector RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Etapa 2:** [Digitando credenciais](install-configure-rms-connector.md#entering-credentials)

-   **Etapa 3:** [Autorizando servidores para usar o conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Etapa 4:** [Configurando o balanceamento de carga e alta disponibilidade](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   Opcional: [Configurando o conector RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   Opcional: [Configurando o conector RMS para um servidor proxy da Web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   Opcional: [Instalando a ferramenta de administração do conector RMS em computadores administrativos](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Etapa 5:** [Configurando servidores para usar o conector RMS](configure-servers-rms-connector.md)

    -   [Configurando um servidor Exchange para usar o conector](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configurando um servidor SharePoint para usar o conector](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configurando um servidor de arquivos para a Infraestrutura de Classificação de Arquivos usar o conector](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## Pré-requisitos para o conector RMS
Antes de instalar o conector do RMS, verifique se os requisitos a seguir estão sendo seguidos.

|Requisito|Mais informações|
|---------------|--------------------|
|O serviço do Rights Management (RMS) está ativado|[Ativando o Azure Rights Management](activate-service.md)|
|A sincronização de diretórios entre as florestas do Active Directory locais e o Azure Active Directory|Após ativar o RMS, o Azure Active Directory deverá ser configurado para funcionar com os usuários e grupos no seu banco de dados do Active Directory.<br /><br />**Importante**: é necessário executar esta etapa de sincronização de diretório para que o conector RMS funcione, mesmo para uma rede de teste. Embora você possa usar o Office 365 e o Azure Active Directory usando as contas criadas manualmente no Active Directory do Azure, este conector requer que as contas no Active Directory do Azure sejam sincronizadas com os Serviços de Domínio do Active Directory.<br /><br />Para obter mais informações, consulte os seguintes recursos:<br /><br />[Integrando suas identidades locais com o Azure Active Directory](/active-directory/active-directory-aadconnect)<br /><br />[Comparação das ferramentas de integração de diretório de identidade híbrida](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|Opcional, mas recomendado:<br /><br />Ativar federação entre o Active Directory e o Azure Active Directory no local|É possível habilitar a federação de identidade entre o diretório local e o Azure Active Directory. Essa configuração proporciona ao usuário uma melhor experiência usando o logon único para o serviço RMS. Sem o logon único, os usuários serão solicitados a fornecer suas credenciais antes que possam usar o conteúdo protegido por direitos.<br /><br />Para obter instruções para configurar a federação usando os Serviços de federação do Active Directory (AD FS) entre os Serviços de domínio do Active Directory e o Active Directory do Azure, consulte a [Lista de verificação: Use os AD FS para implementar e gerenciar o logon único](http://technet.microsoft.com/library/jj205462.aspx) na biblioteca do Windows Server.|
|Um mínimo de dois computadores membros nos quais instalar o conector RMS:<br /><br />- Um computador físico ou virtual de 64 bits que execute um dos seguintes sistemas operacionais: Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.<br /><br />- Pelo menos 1 GB de RAM.<br /><br />- Um mínimo de 64 GB de espaço em disco.<br /><br />- Pelo menos uma interface de rede.<br /><br />- Acesso à Internet através de um firewall (ou proxy Web) que não requer autenticação.<br /><br />- Deve estar em uma floresta ou um domínio que tenha relação de confiança com outras florestas da organização que contenham instalações dos servidores Exchange ou SharePoint que você quer usar com o conector RMS.|Para a tolerância a falhas e alta disponibilidade, você deve instalar o conector RMS em um mínimo de dois computadores.<br /><br />**Dica**: caso você esteja usando o Outlook Web Access ou dispositivos móveis que utilizam o Exchange ActiveSync IRM e for muito importante que você mantenha o acesso a emails e anexos que são protegidos pelo Azure RMS, recomendamos que você implante um grupo de balanceamento de carga dos servidores de conector para garantir a alta disponibilidade.<br /><br />Você não precisa de servidores dedicados para executar o conector, mas é necessário instalá-lo em um computador separado dos servidores que utilizarão o conector.<br /><br />**Importante**: não instale o conector em um computador que execute o Exchange Server, o SharePoint Server ou um servidor de arquivos configurado para infraestrutura de classificação de arquivos se quiser usar a funcionalidade desses serviços com o Azure RMS. Além disso, não instale esse conector em um controlador de domínio.|

## Próximas etapas

Acesse [Instalação e configuração do conector do Azure Rights Management](install-configure-rms-connector.md).

<!--HONumber=May16_HO3-->


