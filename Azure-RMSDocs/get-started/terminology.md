---
title: Terminologia do Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 75f868c4428e7b434e6a115a3e70508c3ff7f93d
ms.openlocfilehash: 1a45457548d8cba6424e92bc18ef085d095742f3


---

# Terminologia do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Confuso com uma palavra, frase ou acrônimo relacionado ao Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS)? Encontre aqui a definição de termos e abreviações que são específicos do Azure RMS ou que têm um significado específico quando usados no contexto de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

|Termo|Definição|
|--------|--------------|
|AADRM|O nome do módulo do Windows PowerShell para Azure Rights Management, que deriva da abreviação não oficial de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] quando ele era denominado (Windows) Azure Active Directory Rights Management.|
|ativar|Para habilitar o serviço do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] de forma que uma organização possa adicionar proteção de informações aos seus documentos e emails. Esta ação também habilita os recursos do Rights Management no Exchange Online e no SharePoint Online.|
|Active Directory Rights Management Services|Abreviado frequentemente para *AD RMS*.<br /><br />Uma função do Windows Server que fornece proteção de informações usando criptografia e política para ajudar a proteger documentos, arquivos e emails.|
|AD RMS|Consulte *Active Directory Rights Management Services*.|
|Azure Information Protection|Atualmente em visualização, um serviço que usa a classificação, a rotulação e a proteção para ajudar a proteger documentos e emails. O Azure Rights Management fornece a proteção usando políticas de criptografia, identidade e autorização.|
|Azure Rights Management|Abreviado frequentemente para *Azure RMS*.<br /><br />Um serviço do Azure que fornece proteção de informações usando criptografia e política para ajudar a proteger documentos, arquivos e email.  Também conhecido como *Azure Rights Management Service*. Nomes anteriores incluíram:<br /><br />- *Microsoft Azure Active Directory Rights Management*: abreviado frequentemente para Microsot Azure AD Rights Management Service.<br /><br />- *RMS Online*: o nome original proposto que às vezes você pode ver em mensagens de erro e entradas de arquivos de log.|
|Azure RMS|Consulte *Azure Rights Management*.|
|BYOK|Consulte *Traga a sua própria chave*.|
|Traga a sua própria chave|Abreviado frequentemente para *BYOK*.<br /><br />Uma opção de configuração e topologia escolhida por uma organização que deseja gerar e gerenciar sua própria chave de locatário do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].|
|chave de conteúdo|Uma chave exclusiva que é criada por aplicativos habilitados para RMS para cada documento ou email que está protegido usando o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] e que ajuda a limitar o risco de divulgação de informações.|
|consumo|Para desbloquear um arquivo para lê-lo ou usá-lo quando esse arquivo tiver sido protegido pelo [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|
|desativar|Para desabilitar o serviço do Rights Management de forma que a organização não possa mais usar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].|
|modelo departamental|Um modelo de política de direitos que você cria (um modelo personalizado) e é configurado para ficar visível para os usuários selecionados, e não para todos os usuários da sua organização.|
|aplicativos habilitados|Aplicativos que oferecem suporte nativo ao Rights Management, que inclui aplicativos do Office, como o Word e o Excel. ISVs (Independent Software Vendors - Fornecedores de Software Independentes) e desenvolvedores também podem gravar aplicativos que oferecem suporte nativo ao [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|
|gerenciamento de direitos empresariais|Um padrão da indústria, termo genérico que é muitas vezes usado para descrever os produtos e soluções que ajudam as organizações a proteger informações confidenciais ou valiosas usando uma combinação de criptografia e ferramentas de autorização de política. O Microsoft Rights Management é um exemplo de uma solução de ERM (Enterprise Rights Management - Gerenciamento de Direitos Empresariais).|
|ERM|Consulte *gerenciamento de direitos empresariais*.|
|proteção genérica|Um nível de proteção que criptografa qualquer tipo de arquivo e impede que pessoas não autorizadas abram o arquivo. Depois que o arquivo é aberto, ele está então descriptografado e é utilizável em um aplicativo que não ofereça suporte nativo ao [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|
|HYOK|Veja *mantenha sua própria chave*.|
|mantenha sua própria chave|Abreviado frequentemente para *HYOK*.<br /><br />Uma opção de configuração e topologia para uma organização que deseja gerar e armazenar sua próprias chaves localmente, em geral, por motivos regulatórios ou de conformidade.|
|proteção de informações|Abreviado algumas vezes para *IP*.<br /><br />Um padrão da indústria, termo genérico que se refere à proteção de dados e arquivos de acesso não autorizado, mesmo depois que os arquivos e dados deixam as fronteiras organizacionais usando um email ou o compartilhamento de documentos. O Microsoft Rights Management é um exemplo de uma solução de IP (Information Protection - Proteção de Informações).|
|Gerenciamento de Direitos de Informação|Abreviado frequentemente para *IRM*.<br /><br />Um termo usado em conjunto com os serviços do Office, como o Exchange Server, Word e SharePoint Online, para descrever a capacidade de oferecer suporte ao Rights Management.|
|IRM|Consulte *Gerenciamento de Direitos de Informação*.|
|MSDRM|Às vezes, visto como referência para o cliente RMS 1.0, que é substituído pelo cliente RMS mais recente, o MSIPC. Este cliente mais antigo oferece suporte a aplicativos que são desenvolvidos com o RMS SDK 1.0 e oferece suporte ao Office 2010 e Office 2007, ao Exchange 2010 e Exchange 2013 e ao SharePoint 2010 e SharePoint 2007.|
|MSIPC|Às vezes, visto como referência para o cliente RMS 2.0, que substituiu o cliente RMS mais antigo, o MSDRM. Este último cliente oferece suporte a aplicativos que são desenvolvidos com o RMS SDK 2.0 e oferece suporte ao Office 2016 e Office 2013, SharePoint 2013 e ao aplicativo de compartilhamento do RMS.|
|proteção nativa|Um nível de proteção disponível em todos os aplicativos habilitados que impede que pessoas não autorizadas abram um arquivo, e que também pode impor políticas mais rigorosas, como somente leitura e não imprimir. Além disso, essa proteção fica com o arquivo, mesmo quando o arquivo é encaminhado para outras pessoas ou salvo em um local público que outras pessoas possam acessar.|
|.pfile|A extensão de nome de arquivo que é anexada a todos os arquivos que o Rights Management protege genericamente.|
|.ppdf|Extensão de nome de arquivo criado pelo Rights Management quando cria automaticamente uma cópia em PDF de um arquivo (Word, Excel, PowerPoint ou PDF) que você compartilha por email, de forma que seja possível ler (mas não editar) o arquivo em todos os dispositivos.|
|nível de permissões|Um agrupamento lógico de direitos de uso que facilitam para usuários finais e administradores escolherem as opções de configuração baseadas em funções. Por exemplo, Revisor e Coautor.|
|proteger|Aplique controles do Rights Management em arquivos ou mensagens de email usando as políticas de criptografia, identidade e controle de acesso para ajudar a proteger seus dados.|
|publish|Para proteger um arquivo a fim de salvaguardá-lo de acesso e uso não autorizados.|
|Conector do Rights Management|Um relé do proxy de saída que você pode implantar para serviços locais, como o Exchange Server e o SharePoint, para proteger os dados usando o Azure Rights Management.|
|Serviços do Rights Management|O termo genérico que se aplica tanto à versão na nuvem do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]) quanto à versão local do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] (AD RMS).|
|Aplicativo de compartilhamento do Rights Management|Um aplicativo para download opcional de dispositivos móveis mais populares e do Windows, que oferece suporte ao compartilhamento de arquivos com segurança no local e por email.|
|RMS|Consulte *Rights Management services*.|
|Conector RMS|Consulte *Conector do Rights Management*.|
|RMS para pessoas físicas|Uma assinatura gratuita para um usuário utilizar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] quando a sua organização não tiver uma assinatura do Office 365 ou do Azure Active Directory.|
|Aplicativo RMS sharing|Consulte *Aplicativo de compartilhamento Rights Management*.|
|superusuário|Um grupo de administradores altamente confiáveis ​​que podem descriptografar e acessar arquivos que a organização protegeu usando o Rights Management. Normalmente, este nível de acesso é exigido para descoberta eletrônica jurídica e pelas equipes de auditoria.|
|chave de locatário|Também conhecida como chave SLC (Server Licensor Certificate - Certificado de Licenciante para Servidor).<br /><br />A chave que é exclusiva de uma organização e, basicamente, protege todas as funções criptográficas do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] que se encadeiam com esta chave de locatário.|
|desproteger|Remova os controles do Rights Management de arquivos ou mensagens de email que usaram políticas de criptografia, identidade e controle de acesso para ajudar a proteger seus dados.|
|licença de uso|Um certificado de cada documento que é concedido a um usuário que abre uma mensagem de email ou arquivo que foi protegido pelo [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Esse certificado contém os direitos desse usuário para o arquivo ou a mensagem de email e a chave de criptografia que foi usada para criptografar o conteúdo, bem como as restrições de acesso adicional definidas na política do documento.|






<!--HONumber=Aug16_HO2-->


