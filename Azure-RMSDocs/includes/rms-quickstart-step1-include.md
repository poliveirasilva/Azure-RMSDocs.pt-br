![Etapa 1 do tutorial de início rápido](../media/AzRMS_QuickStartSteps1.PNG)

Ainda que você tenha uma assinatura que ofereça suporte ao Azure Rights Management, o serviço estará desabilitado por padrão. Para ativá-lo, você pode usar o Centro de administração do Office 365 ou o portal clássico do Azure:

-   Se você tiver uma assinatura do Office 365 que inclua o Azure Rights Management ou uma assinatura do Office 365 que não inclua o Azure Rights Management, mas que tenha uma assinatura do Azure RMS Premium: **use o centro de administração do Office 365**.

-   Se você não tiver uma assinatura do Office 365: **use o portal clássico do Azure**.

![Portal clássico do Azure](../media/AzRMS_Tutorial_1_Screenshots.png)

#### Para ativar o Rights Management do centro de administração do Office 365

1.  Acesse o [portal do Office 365](https://portal.office.com/) e entre com sua conta corporativa ou de estudante.

2.  Se o centro de administração do Office 365 não for exibido automaticamente, selecione o ícone inicializador de aplicativos na parte superior esquerda e escolha **Admin**. O bloco do **Admin** é exibido apenas aos administradores do Office 365.

    > [!TIP]
    > Para obter ajuda do centro de administração, consulte [sobre o Centro de administração do Office 365 - Ajuda para Administradores](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  No painel esquerdo, expanda **CONFIGURAÇÕES DE SERVIÇO**.

4.  Clique em **Rights Management**.

5.  Na página **RIGHTS MANAGEMENT** , clique em **Gerenciar**.

6.  Na página de **gerenciamento de direitos** clique em **ativar**.

7.  Quando solicitado a responder **Deseja ativar o Rights Management?**, clique em **ativar**.

Agora você deve ver **Rights management está ativado** e a opção para desativar (pode ser necessário atualizar a página manualmente).

Por hora, não clique em **recursos avançados**. Isso levaria você até o portal clássico do Azure, onde você pode configurar modelos que não são necessários para este tutorial. Ao invés disso, você pode fechar o centro de administração do Office 365.

#### Para ativar o Rights Management no portal do Azure

1.  Acesse o [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081) e entre.

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory** , clique em **RIGHTS MANAGEMENT**.

4.  Selecione o diretório a gerenciar para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **ATIVAR** e confirme sua ação.

O **STATUS do RIGHTS MANAGEMENT** agora deve exibir **Ativo** e a opção **ATIVAR** é substituída por **DESATIVAR**.

Embora você possa configurar outras opções de Rights Management no portal, isso não é necessário para este tutorial, então você pode fechar o portal clássico do Azure.

Isso é tudo o que você precisa fazer para a primeira etapa. Agora, o serviço está ativado, e todos os usuários em sua organização podem começar a proteger documentos importantes e confidenciais. Inicialmente, em um ambiente de produção, talvez seja melhor restringir quem possa fazer isso e optar por uma distribuição em fases. Mas isso não é necessário para este tutorial.

Embora não incluímos aqui, em uma implantação em produção provavelmente você decidirá por configurar modelos personalizados. Modelos facilitam que usuários apliquem rapidamente as configurações corretas quando precisam proteger arquivos. Quando você ativa o Rights Management, você obtém automaticamente 2 modelos padrão, e é provável que você decida complementá-los com seus próprios modelos personalizados em um ambiente de produção. Mas modelos não são necessários para este tutorial, então você está pronto para a próxima etapa.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Sobre a ativação do Rights Management e o controle de quem pode proteger arquivos e email quando o serviço for ativado   →|[Ativando o Azure Rights Management](../deploy-use/activate-azure-classic.md)|
|Sobre os modelos padrão e como criar modelos novos e personalizados   →|[Configurando modelos personalizados do Azure Rights Management](../deploy-use/create-template.md)|


<!--HONumber=Jun16_HO4-->


