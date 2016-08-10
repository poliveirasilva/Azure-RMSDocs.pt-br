---
title: Instalando o cliente Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: c8a7c7d7182df7b525b3425ab378126feb389d9f


---

# Instalando o cliente Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Para classificar os documentos e as mensagens de email usando o Azure Information Protection, primeiro você deve instalar o cliente Azure Information Protection. A instalação adiciona uma barra do Information Protection nos aplicativos do Office (Word, Excel, PowerPoint, Outlook) que exibe os rótulos de classificação da organização, além de um novo grupo **Proteção** na guia **Início** (Word, Excel, PowerPoint), com um botão chamado **Proteger**:

A figura a seguir mostra essa barra do Information Protection e os rótulos da [política padrão](configure-policy-default.md):

![Barra do Azure Information Protection com a política padrão](../media/info-protect-bar-default.png)

Baixe o cliente Azure Information Protection no [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Antes de instalar o cliente, verifique se você tem as versões de sistema operacional e os aplicativos necessários: [Requisitos do Azure Information Protection](requirements-azure-infoprotect.md).


## Para instalar o cliente Azure Information Protection manualmente

1. Depois de ter [baixado o cliente](https://www.microsoft.com/en-us/download/details.aspx?id=53018), execute **AZInfoProtection.exe** e siga os prompts para instalar o cliente. Esta instalação requer permissões administrativas locais.

    Selecione a opção para instalar uma política de demonstração se você não puder se conectar ao Office 365 ou ao Azure Active Directory, mas desejar ver e experimentar o lado do cliente do Azure Information Protection, usando uma política local para fins de demonstração. Quando o cliente se conecta a um serviço do Azure Information Protection, essa política de demonstração é substituída pela política do Azure Information Protection da organização. 

2. Para começar a usar o cliente Azure Information Protection: se o computador estiver executando o Office 2010, reinicie o computador. Para outras versões do Office, reinicie os aplicativos do Office.

## Para instalar o cliente Azure Information Protection para usuários

- Você pode criar scripts e automatizar a instalação do cliente Azure Information Protection empacotando AZInfoProtection.exe e usando as [Windows Installer (msiexec) command line options](https://technet.microsoft.com/library/cc759262(v=ws.10).aspx) [Opções de linha de comando do Windows Installer (msiexec)] padrão.

    Por exemplo, se você criar uma versão empacotada chamada InfoProtect.msi e desejar instalar o cliente silenciosamente: `msiexec /qn InfoProtection.msi`


## Para desinstalar o cliente Azure Information Protection

- Use o Painel de Controle para desinstalar um programa: clique em **Microsoft Azure Information Protection** > **Desinstalar**

## Para verificar a instalação, o status da conexão ou relatar um problema

1. Abra um aplicativo do Office e na guia **Início**, no grupo **Proteção** clique em **Proteger** e, em seguida, clique em **Ajuda e Comentários**.

2. Na caixa de diálogo **Microsoft Azure Information Protection**, observe o seguinte:

    - O valor **Última Conexão** que identifica quando o cliente se conectou pela última vez ao serviço do Azure Information Protection da organização. Quando o cliente se conecta ao serviço e encontra alterações com relação à sua política atual, ele baixa automaticamente a política mais recente. Se você tiver feito alterações na política após a hora exibida, feche e reabra o aplicativo do Office.

    - Seu nome de usuário exibido que identifica a conta usada para a sua autenticação no Azure Information Protection. Esse nome de usuário deve corresponder a uma conta usada para o Office 365 ou o Azure Active Directory.

    - A versão do cliente Azure Information Protection.

    - O link **Enviar comentários**, que você pode usar para anexar automaticamente os logs do cliente a uma mensagem de email que pode ser enviada à equipe do Information Protection para investigação.

    - O link **Executar diagnóstico**: essa funcionalidade não está implementada no momento.

## Locais de arquivo

Arquivos do cliente:   

- Para sistemas operacionais de 64 bits: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- Para sistemas operacionais de 32 bits: **\Program Files\Microsoft Azure Information Protection**

Arquivos de logs do cliente e o arquivo de política instalado atualmente:

- Para sistemas operacionais de 32 e 64 bits: **%localappdata%\Microsoft\MSIP**


## Próximas etapas

Para alterar os rótulos na barra do Information Protection, você deve configurar a política do Azure Information Protection. Para obter mais informações, consulte [Configuring Azure Information Protection policy](configure-policy.md) (Configurando a política do Azure Information Protection).

Para obter um exemplo de como personalizar a política padrão e ver o comportamento resultante em um aplicativo do Office, experimente o [Tutorial de início rápido do Azure Information Protection](infoprotect-quick-start-tutorial.md). 



<!--HONumber=Jul16_HO5-->


