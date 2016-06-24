---
# required metadata

title: Tutorial de início rápido do Azure RMS - Etapa 1 | Azure RMS
description: A primeira etapa de um tutorial para testar rapidamente o Microsoft Azure Rights Management para sua organização em apenas 5 etapas que devem levar menos de 15 minutos.
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# Etapa 1 do início rápido do Azure RMS: Ativar o serviço Rights Management

*Aplica-se a: Azure Rights Management, Office 365*


Ir para: 
> [!div class="op_single_selector"]
- [Introdução](quick-start-tutorial.md)
- [Etapa 1: Ativar o Azure RMS](tutorial-step1.md)
- [Etapa 2: Instalar o aplicativo RMS sharing](tutorial-step2.md)
- [Etapa 3: Enviar o documento confidencial por email](tutorial-step3.md)
- [Etapa 4: O destinatário lê o documento](tutorial-step4.md)
- [Etapa 5: Rastrear o seu documento](tutorial-step5.md)


![Tutorial de início rápido do Azure RMS - Etapa 1](../media/AzRMS_QuickStartSteps1.PNG)

Ainda que você tenha uma assinatura que ofereça suporte ao Azure Rights Management, o serviço estará desabilitado por padrão. Para ativá-lo, você pode usar o Centro de administração do Office 365 ou o portal clássico do Azure:

-   Se você tiver uma assinatura do Office 365 que inclua o Azure Rights Management ou uma assinatura do Office 365 que não inclua o Azure Rights Management, mas que tenha uma assinatura do Azure RMS Premium: **use o Centro de administração do Office 365**.

-   Se você não tiver uma assinatura do Office 365: **use o portal clássico do Azure**.

![Capturas de tela da etapa 1 do tutorial](../media/AzRMS_Tutorial_1_Screenshots.png)

### Para ativar o Azure Rights Management usando o centro de administração clássico do Office 365

1.  Acesse o [portal do Office 365](https://portal.office.com/) e entre com sua conta corporativa ou de estudante.

2.  Se o centro de administração do Office 365 não for exibido automaticamente, selecione o ícone inicializador de aplicativos na parte superior esquerda e escolha **Admin**. O bloco do **Admin** é exibido apenas aos administradores do Office 365.

    > [!TIP]
    > Para obter ajuda do centro de administração, consulte [Sobre o centro de administração do Office 365 - Ajuda para administradores](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  No painel esquerdo, expanda **CONFIGURAÇÕES DE SERVIÇO**.

4.  Clique em **Rights Management**.

5.  Na página **RIGHTS MANAGEMENT**, clique em **Gerenciar**.

6.  Na página do **rights management** clique em **ativar**.

7.  Quando solicitado a responder **Deseja ativar o Rights Management?**, clique em **ativar**.

Agora você deve ver **Rights management está ativado** e a opção para desativar (pode ser necessário atualizar a página manualmente).

Por hora, não clique em **recursos avançados**. Isso levaria você até o portal clássico do Azure, onde você pode configurar modelos que não são necessários para este tutorial. Ao invés disso, você pode fechar o centro de administração do Office 365.

### Para ativar o Rights Management no Portal clássico do Azure

1.  Acesse o [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081) e entre.

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory**, clique em **RIGHTS MANAGEMENT**.

4.  Selecione o diretório a gerenciar para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **ATIVAR** e confirme sua ação.

O **STATUS DO RIGHTS MANAGEMENT** agora deve exibir **Ativo** e a opção **ATIVAR** é substituída por **DESATIVAR**.

Embora você possa configurar outras opções de Rights Management no portal, isso não é necessário para este tutorial, então você pode fechar o portal clássico do Azure.

Isso é tudo o que você precisa fazer para a primeira etapa. Agora, o serviço está ativado, e todos os usuários em sua organização podem começar a proteger documentos importantes e confidenciais. Inicialmente, em um ambiente de produção, talvez seja melhor restringir quem possa fazer isso e optar por uma distribuição em fases. Mas isso não é necessário para este tutorial.

Embora não incluímos aqui, em uma implantação em produção provavelmente você decidirá por configurar modelos personalizados. Modelos facilitam que usuários apliquem rapidamente as configurações corretas quando precisam proteger arquivos. Quando você ativa o Rights Management, você obtém automaticamente 2 modelos padrão, e é provável que você decida complementá-los com seus próprios modelos personalizados em um ambiente de produção. Mas modelos não são necessários para este tutorial, então você está pronto para a próxima etapa.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Sobre a ativação do Rights Management e o controle de quem pode proteger arquivos e email quando o serviço for ativado|[Ativando o Azure Rights Management](../deploy-use/activate-service.md)|
|Sobre os modelos padrão e como criar modelos novos e personalizados|[Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[« Introdução](quick-start-tutorial.md)
[Etapa 2 »](tutorial-step2.md)

<!--HONumber=Apr16_HO4-->


