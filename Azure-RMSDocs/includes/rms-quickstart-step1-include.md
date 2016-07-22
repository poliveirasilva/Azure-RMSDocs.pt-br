![Passo 1 do tutorial de início rápido](../media/AzRMS_QuickStartSteps1.PNG)

Apesar de poder ter uma subscrição que suporta o Azure Rights Management, o serviço está desativado por predefinição. Para o ativar, pode utilizar o centro de administração do Office 365 ou o portal clássico do Azure:

-   Se tiver uma subscrição do Office 365 que inclua o Azure Rights Management ou uma subscrição do Office 365 que exclua o Azure Rights Management, mas tiver uma subscrição do Azure RMS Premium: **utilize o centro de administração do Office 365**.

-   Se não tiver uma subscrição do Office 365: **utilize o portal clássico do Azure**.

![Portal clássico do Azure](../media/AzRMS_Tutorial_1_Screenshots.png)

#### Para ativar o Rights Management a partir do centro de administração do Office 365

1.  Aceda ao [portal do Office 365](https://portal.office.com/) e inicie sessão com a sua conta escolar ou profissional.

2.  Se o centro de administração do Office 365 não for apresentado automaticamente, selecione o ícone do iniciador de aplicações no canto superior esquerdo e escolha **Administrador**. O mosaico **Administrador** só é apresentado para os administradores do Office 365.

    > [!TIP]
    > Para obter ajuda acerca do centro de administração, consulte [Acerca do centro de administração do Office 365 – Ajuda de Administração](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  No painel esquerdo, expanda **DEFINIÇÕES DE SERVIÇO**.

4.  Clique em **Rights Management**.

5.  Na página **RIGHTS MANAGEMENT**, clique em **Gerir**.

6.  Na página **rights management**, clique em **ativar**.

7.  Quando lhe for perguntado **Pretende ativar o Rights Management?**, clique em **ativar**.

Já deverá estar visível **O Rights Management encontra-se ativado** e a opção para desativar (poderá ter de atualizar manualmente a página)

Neste momento, não clique em **funcionalidades avançadas**. Isto leva-o para o portal clássico do Azure onde poderá configurar modelos, que não são necessários para este tutorial. Em vez disso, pode fechar o centro de administração do Office 365.

#### Para ativar o Rights Management a partir do portal do Azure

1.  Aceda ao [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081) e inicie sessão.

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory**, clique em **RIGHTS MANAGEMENT**.

4.  Selecione o diretório a gerir para o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **ATIVAR** e confirme a ação.

O **ESTADO DO RIGHTS MANAGEMENT** deverá agora apresentar **Ativo** e a opção **ATIVAR** é substituída por **DESATIVAR**.

Embora seja possível configurar outras opções do Rights Management no portal, estas não são necessárias para este tutorial, pelo que pode fechar o portal clássico do Azure.

É tudo o que precisa de fazer neste primeiro passo. O serviço está ativado para que todos os utilizadores na sua organização possam agora começar a proteger documentos importantes e confidenciais. Num ambiente de produção, pondere restringir quem pode fazer isto inicialmente, para uma implementação faseada. Mas não é necessário para este tutorial.

Embora não estejam incluídos aqui, para uma implementação de produção, provavelmente também pretenderá configurar modelos personalizados. Os modelos fazem com que seja mais fácil para os utilizadores aplicarem rapidamente as definições corretas quando necessitam de proteger ficheiros. Quando ativar o Rights Management, obtém automaticamente 2 modelos predefinidos e é provável que deseje complementá-los com os seus modelos personalizados num ambiente de produção. No entanto, os modelos não são necessários para este tutorial, pelo que pode ir para o passo seguinte.

|Se pretender mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Acerca da ativação do Rights Management e do controlo de quem pode proteger ficheiros e e-mails quando o serviço está ativado   →|[Ativar o Azure Rights Management](../deploy-use/activate-azure-classic.md)|
|Acerca dos modelos predefinidos e de como criar modelos novos e personalizados   →|[Configurar Modelos Personalizados para o Azure Rights Management](../deploy-use/create-template.md)|


<!--HONumber=Jun16_HO4-->


