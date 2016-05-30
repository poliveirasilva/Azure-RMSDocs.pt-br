---
# metadados necessários

título: Tutorial de início rápido do Azure RMS - Etapa 4 | Descrição do Azure RMS: a quarta etapa de um tutorial para testar rapidamente o Microsoft Azure Rights Management para sua organização em apenas 5 etapas que devem levar menos de 15 minutos.
palavras-chave: autor: cabailey manager: mbaldwin ms.date: ms.topic 28/04/2016: get-started-article ms.prod: azure ms.service: rights-management ms.technology: techgroup-identity ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c

# metadados opcionais

ROBÔS: público-alvo: ms.devlang: ms.reviewer: esaggese ms.suite: ems ms.tgt_pltfrm: ms.technology: ms.custom:

---


# Etapa 4 do início rápido do Azure RMS: Pedir que seus destinatários abram o documento enviado por email

*Aplica-se a: Azure Rights Management, Office 365*


Ir para: 
> [!div class="op_single_selector"]
- [Introdução](quick-start-tutorial.md)
- [Etapa 1: Ativar o Azure RMS](tutorial-step1.md)
- [Etapa 2: Instalar o aplicativo RMS sharing](tutorial-step2.md)
- [Etapa 3: Enviar o documento confidencial por email](tutorial-step3.md)
- [Etapa 4: O destinatário lê o documento](tutorial-step4.md)
- [Etapa 5: Rastrear o seu documento](tutorial-step5.md)


![Tutorial de início rápido do Azure RMS - Etapa 4](../media/AzRMS_QuickStartSteps4.PNG)

Os destinatários podem usar vários dispositivos para ler o documento protegido enviado como anexo de email. Os dispositivos incluem iPads, iPhones, telefones e tablets Android, computadores Mac, bem como computadores Windows.

Peça que eles leiam a mensagem de email que você enviou. Eles verão a mensagem de email e, antes disso, o seguinte texto:

**O remetente protegeu os anexos com o Microsoft RMS. Você deve** [entrar](http://aka.ms/rms)
      **para abri-los.**

Ao clicarem no link, eles acessarão as instruções para instalação do aplicativo RMS sharing e, caso necessário, inscrição de uma conta gratuita. A conta gratuita concederá uma assinatura do RMS para indivíduos, que garante que os usuários autorizados sempre possam ler um documento protegido, mesmo se a organização deles não tiver o Azure RMS. Assim, eles estarão prontos para ler o anexo protegido usando as instruções a seguir.

![Capturas de tela da etapa 4 do tutorial](../media/AzRMS_Tutorial_4_Screenshots.png)

### Para exibir o documento protegido do anexo

1.  Como o Azure Rights Management protegeu um documento do Word, existem dois anexos na mensagem de email. Eles são, na verdade, duas versões do mesmo arquivo, mas com diferentes extensões de nome de arquivo. Abra a versão que tem a extensão de nome de arquivo **.ppdf** (**Confidential.ppdf**).

    Se você tiver uma versão do [Office no seu dispositivo que dá suporte ao Rights Management](https://technet.microsoft.com/library/dn655136.aspx), você poderá abrir a outra versão do arquivo (**Confidential.docx**) para abri-lo no Word.

2.  Se for solicitado seu nome de usuário e senha, insira seu nome de usuário no mesmo formato do endereço de email usado para enviar o email e os anexos. Por exemplo, **janetm@contoso.com** ou **p.dover@fabrikam.com**. Para sua senha, digite a senha que você forneceu ao se inscrever para o RMS para indivíduos. Ou, se sua organização tiver o Azure RMS, digite sua senha de trabalho normal.

O documento será aberto, e você poderá ler o conteúdo. Por exemplo, pode ser que esteja escrito **Se você conseguiu ler este documento de seu anexo de email, o remetente compartilhou com êxito um arquivo que foi protegido com o Azure RMS.** Por ser somente leitura, o conteúdo não pode ser alterado.

Como uma etapa opcional, você pode pedir que seu destinatário encaminhe o email a outras pessoas que você não incluiu em seu email original. Mesmo que as outras pessoas trabalhem para uma organização que possui o Azure Rights Management ou inscrevam suas próprias assinaturas do RMS para indivíduos, não poderão abrir o anexo. Quando o nome de usuário for solicitado, será negado o acesso ao documento para elas.

Agora que o destinatário abriu o anexo e, opcionalmente, encaminhou o mesmo para outra pessoa, espere receber uma notificação por email relatando essa atividade. Como é muito fácil perder mensagens de email com o passar do tempo, uma maneira ainda melhor de controlar quem acessou o documento é usar o site de controle de documentos, abordado na etapa final.

|Se deseja obter mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Instruções completas para exibir os arquivos protegidos pelo Azure Rights Management|[Exiba e use os arquivos que foram protegidos pelo Rights Management](../rms-client/sharing-app-view-use-files.md)|
|Sobre a assinatura gratuita do RMS para indivíduos|[RMS para pessoas físicas e Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Sobre as duas versões do arquivo que você vê anexados à mensagem de email|[O que é o arquivo .ppdf, criado automaticamente?](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)|


>[!div class="step-by-step"] [« Etapa 3](tutorial-step3.md)
[Etapa 5 »](tutorial-step5.md)

<!--HONumber=May16_HO2-->


