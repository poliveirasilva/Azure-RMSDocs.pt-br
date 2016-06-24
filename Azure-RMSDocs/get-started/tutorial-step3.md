---
# required metadata

title: Tutorial de início rápido do Azure RMS - Etapa 3 | Azure RMS
description: A terceira etapa de um tutorial para testar rapidamente o Microsoft Azure Rights Management para sua organização em apenas 5 etapas que devem levar menos de 15 minutos.
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c604e749-8918-40e8-8148-6bd000cb2be2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Etapa 3 do início rápido do Azure RMS: Enviar por email o documento que você deseja proteger

*Aplica-se a: Azure Rights Management, Office 365*


Ir para: 
> [!div class="op_single_selector"]
- [Introdução](quick-start-tutorial.md)
- [Etapa 1: Ativar o Azure RMS](tutorial-step1.md)
- [Etapa 2: Instalar o aplicativo RMS sharing](tutorial-step2.md)
- [Etapa 3: Enviar o documento confidencial por email](tutorial-step3.md)
- [Etapa 4: O destinatário lê o documento](tutorial-step4.md)
- [Etapa 5: Rastrear o seu documento](tutorial-step5.md)


Para essa etapa, primeiro crie e salve um documento usando o Word, que representará o documento que você deseja proteger, e nomeie-o **Confidential.docx**. Para este tutorial, não importa qual o texto nele, mas algum texto deve ser escrito para que você possa confirmar se o destinatário autorizado conseguiu lê-lo. Por exemplo, você pode digitar: **Se você conseguiu ler este documento de seu anexo de email, o remetente compartilhou com êxito um arquivo que foi protegido com o Azure RMS.**

Assim, você estará pronto para compartilhar com segurança este documento por email.

![Tutorial de início rápido do Azure RMS - Etapa 3](../media/AzRMS_Tutorial_3_Screenshots.png)

### Para compartilhar com segurança o seu documento por email

1.  Usando o Outlook, crie uma nova mensagem e anexe o arquivo que você acabou de criar.

2.  Na caixa **Para** , digite um ou mais endereços de email comerciais. Verifique se você especificou um endereço de email comercial como **janetm@contoso.com** ou **p.dover@fabrikam.com**, porque atualmente o Azure Rights Management não dá suporte a endereços de email pessoais que você possa usar em casa, do seu provedor de Internet. Não se preocupe se a pessoa para a qual você está enviando também tem o Azure Rights Management.

3.  Digite um assunto, como  **Documento confidencial** e depois digite uma mensagem curta para o email, como **Leia este documento confidencial e não compartilhe com ninguém.**

4.  Depois, na guia **Mensagem** no grupo **RMS** , clique em **Compartilhamento protegido** , e então clique em **Compartilhamento protegido** novamente:

5.  Na caixa de diálogo **compartilhamento protegido** :

    1.  Selecione **Visualizador - Somente exibição**.

        Com isso, os destinatários poderão exibir o documento, mas não editá-lo ou imprimi-lo.

    2.  Selecione **Enviar um email para mim quando alguém tentar abrir esses documentos**.

        Você receberá uma notificação por email sempre que os destinatários tentarem abrir o anexo, e também se outra pessoa tentar abri-lo; por exemplo, se o destinatário encaminhar o email para um colega de trabalho. Nesta última hipótese, você verá que o acesso foi negado e, a partir dos detalhes do usuário, pode optar por enviar uma cópia do documento que essa pessoa possa abrir.

    3.  Selecione **Permitir que eu revogue instantaneamente o acesso a esses documentos**.

        Esta opção requer que os destinatários tenham uma conexão de Internet sempre que abrirem o anexo, mas possui o benefício de, se você revogar posteriormente o documento, não conseguirem abri-lo na próxima tentativa que fizerem. Se você não selecionar essa opção os destinatários poderão abri-lo mesmo sem uma conexão à Internet, mas a desvantagem é que, se você revogar posteriormente o documento, pode haver um atraso para a revogação entrar em vigor.

    4.  Clique em **Enviar agora**.

        O email com anexo é enviado para os endereços de email que você especificou. Além de sua mensagem de email, eles verão instruções de como ler o documento anexado protegido pelo Azure Rights Management.

Agora que você enviou o documento protegido está pronto para solicitar que os destinatários aguardem a chegada dele, e abram-no. Mas não feche o Outlook, pois usaremos ele novamente na etapa final, para controlar o anexo.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Instruções completas e métodos alternativos para proteger arquivos compartilhados por email|[Proteja arquivos que você compartilha por email usando o aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-protect-by-email.md)|
|Sobre as opções da caixa de diálogo **compartilhamento protegido**|[Opções da caixa de diálogo do aplicativo de compartilhamento do Rights Management](../rms-client/sharing-app-dialog-box.md)|


>[!div class="step-by-step"] [« Etapa 2](tutorial-step2.md)
[Etapa 4 »](tutorial-step4.md)

<!--HONumber=May16_HO2-->


