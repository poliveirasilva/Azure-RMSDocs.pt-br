---
title: "Etapa 1 do tutorial de início rápido do Azure Information Protection | Azure Rights Management"
description: "Etapa 1 de um tutorial de introdução para testar rapidamente o Microsoft Azure Information Protection para sua organização com apenas 4 etapas que devem levar aproximadamente 10 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/11/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 78f0f07271414fb646f996e7273343f2abf8852b
ms.openlocfilehash: 633b24d0c23cbbee88a2647aaa9defe376ccb40e


---

# Etapa 1: Ative o serviço Rights Management
 
*Aplica-se a: visualização do Azure Information Protection*

> [!NOTE]
>Se você deseja apenas classificar seus dados e não protegê-los com o Azure Rights Management ou se já ativou o Azure Rights Management para seu locatário, vá direto para a [próxima etapa](infoprotect-tutorial-step2.md). 

Quando o Azure Rights Management está ativado, você pode proteger seus documentos e arquivos mais confidenciais depois que eles foram classificados. Para ativar o Azure Rights Management, é possível usar o Centro de administração do Office 365 ou o Portal Clássico do Azure:

-   Se você tiver uma assinatura do Office 365 que inclua o Azure Rights Management ou uma assinatura do Office 365 que não inclua o Azure Rights Management, mas que tenha uma assinatura do Azure RMS Premium: **use o centro de administração do Office 365**.

-   Se você não tiver uma assinatura do Office 365: **use o portal clássico do Azure**.

### Para ativar o Azure Rights Management usando o centro de administração clássico do Office 365

> [!NOTE]
> Se você estiver usando a **visualização do centro de administração do Office 365** em vez do centro de administração clássico do Office 365, você poderá usar as instruções de [Como ativar o Azure Rights Management da visualização do centro de administração do Office 365](../deploy-use/activate-office365-preview.md) ou mudar para a versão clássica para usar essas instruções. Para mudar, clique em **Ir para o centro de administração antigo** na página **Inicial** depois de ter entrado.

1.  Acesse o [portal do Office 365](https://portal.office.com/) e entre com sua conta de administrador global do Office 365.

2.  Se o centro de administração do Office 365 não for exibido automaticamente, selecione o ícone inicializador de aplicativos na parte superior esquerda e escolha **Admin**. O bloco do **Admin** é exibido apenas aos administradores do Office 365.

  > [!TIP]
  > Para obter ajuda do centro de administração, consulte [sobre o Centro de administração do Office 365 - Ajuda para Administradores](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  No painel esquerdo, expanda **CONFIGURAÇÕES DE SERVIÇO**.

4.  Clique em **Rights Management**.

5.  Na página **RIGHTS MANAGEMENT** , clique em **Gerenciar**.

6.  Na página de **gerenciamento de direitos** clique em **ativar**.

7.  Quando solicitado a responder **Deseja ativar o Rights Management?**, clique em **ativar**.

Agora você deve ver **Rights management está ativado** e a opção para desativar (pode ser necessário atualizar a página manualmente).

Por hora, não clique em **recursos avançados**. Isso levaria você até o Portal Clássico do Azure, no qual você pode configurar modelos personalizados que não são necessários para este tutorial. Ao invés disso, você pode fechar o centro de administração do Office 365.

### Para ativar o Rights Management no Portal clássico do Azure

1.  Acesse o [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081) e entre com sua conta de administrador global do Azure Active Directory.

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory** , clique em **RIGHTS MANAGEMENT**.

4.  Selecione o diretório a gerenciar para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **ATIVAR** e confirme sua ação.

O **STATUS do RIGHTS MANAGEMENT** agora deve exibir **Ativo** e a opção **ATIVAR** é substituída por **DESATIVAR**.

Embora você possa configurar outras opções de Rights Management no portal, isso não é necessário para este tutorial, então você pode fechar o portal clássico do Azure.

Isso é tudo o que você precisa fazer para a primeira etapa. O Azure Rights Management Service está ativado para que mais tarde no tutorial, você possa selecionar um dos modelos padrão do Azure Rights Management para proteger documentos e emails que são classificados como confidenciais.

Para uma implantação de produção, você provavelmente desejará configurar modelos personalizados além ou em vez dos dois modelos padrão do Azure Rights Management. Mas os modelos personalizados não são necessários para este tutorial, então você está pronto para a etapa 2.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Sobre a ativação do Rights Management|[Ativando o Azure Rights Management](../deploy-use/activate-service.md)|
|Sobre os modelos padrão e como criar modelos novos e personalizados|[Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; Introdução](infoprotect-quick-start-tutorial.md)
[Etapa 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Jul16_HO3-->


