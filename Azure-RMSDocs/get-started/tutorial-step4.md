---
# required metadata

title: "Tutorial de início rápido do Azure RMS – Passo 4 | AZURE RMS"
description: "o quarto passo de um tutorial para experimentar rapidamente o Microsoft Azure Rights Management na sua organização com apenas 5 passos que devem demorar menos de 15 minutos."
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c

# optional metadata

ROBOTS:
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---


# Passo 4 do início rápido do Azure RMS: pedir aos destinatários para abrir o documento enviado por e-mail

*Aplica-se a: Azure Rights Management, Office 365*


Passar para: 
> [!div class="op_single_selector"]
- [Introdução](quick-start-tutorial.md)
- [Passo 1: ativar o Azure RMS](tutorial-step1.md)
- [Passo 2: instalar aplicação de partilha RMS](tutorial-step2.md)
- [Passo 3: enviar e-mail do documento confidencial](tutorial-step3.md)
- [Passo 4: o destinatário lê o documento](tutorial-step4.md)
- [Passo 5: controlar o documento](tutorial-step5.md)


![Passo 4 do tutorial de início rápido do Azure RMS](../media/AzRMS_QuickStartSteps4.PNG)

Os destinatários podem utilizar vários dispositivos para ler o documento protegido que enviou como anexo de e-mail. Os dispositivos incluem iPads, iPhones, tablets e telemóveis Android, computadores Mac, bem como computadores com o Windows.

Peça-lhes para lerem a mensagem de e-mail que enviou. Eles verão a mensagem de e-mail e, antes disso, o seguinte texto:

**O remetente protegeu os anexos com Microsoft RMS. Tem de** [iniciar sessão](http://aka.ms/rms)
      **para os abrir.**

Quando clicam na ligação, são encaminhados para as instruções de instalação da aplicação de partilha RMS e, se necessário, para se inscreverem numa conta gratuita. A conta gratuita concede-lhes uma subscrição do RMS para indivíduos, que garante que os utilizadores autorizados podem sempre ler um documento protegido, mesmo que a organização não tenha o Azure RMS. Em seguida, podem ler o anexo protegido ao utilizar as instruções seguintes.

![Capturas de ecrã do passo 4 do tutorial](../media/AzRMS_Tutorial_4_Screenshots.png)

### Para ver o anexo do documento protegido

1.  Uma vez que o Azure Rights Management protegeu um documento do Word, existem dois anexos na mensagem de e-mail. Estes anexos são, na verdade, duas versões do mesmo ficheiro, mas com extensões de nome de ficheiro diferentes. Abra a versão que tem a extensão de nome de ficheiro **.ppdf** (**Confidencial.ppdf**).

    Se tiver uma versão do [Office no dispositivo que suporte o Rights Management](https://technet.microsoft.com/library/dn655136.aspx), pode abrir a outra versão do ficheiro (**Confidencial.docx**), de modo a ser aberto no Word.

2.  Se lhe for pedido o nome de utilizador e a palavra-passe, introduza o nome de utilizador no mesmo formato que o endereço de e-mail que foi utilizado para lhe enviar a mensagem de e-mail e o anexo. Por exemplo, **juliam@contoso.com** ou **p.barbosa@fabrikam.com**. Para a palavra-passe, escreva a que especificou quando se inscreveu no RMS para indivíduos. Ou, se a sua organização tiver o Azure RMS, introduza a palavra-passe habitual do trabalho.

O documento é aberto e já pode ler o conteúdo. Por exemplo, pode dizer **Se conseguir ler isto no anexo de e-mail, significa que o remetente partilhou com êxito um ficheiro que foi protegido com o Azure RMS.** Uma vez que é só de leitura, não é possível alterar o conteúdo.

Como passo opcional, pode pedir ao destinatário para reencaminhar o e-mail para outras pessoas que não tenha incluído no e-mail original. Mesmo que essas pessoas trabalhem numa organização que tenha o Azure Rights Management ou que se candidatem à própria subscrição do RMS para indivíduos, não vão poder abrir o anexo. Quando lhes for solicitado o respetivo nome de utilizador, o acesso ao documento será negado.

Agora que o destinatário abriu o anexo e, opcionalmente, o reencaminhou para outra pessoa, aguarde a receção de uma notificação de e-mail a comunicar esta atividade. No entanto, é fácil perder mensagens de e-mail ao longo do tempo. Por isso, para melhor controlar quem acede ao documento, utilize o site de controlo de documentos (descrito no último passo).

|Se pretender mais informações|Informações adicionais|
|--------------------------------|--------------------------|
|Instruções completas para visualizar ficheiros que estão protegidos pelo Azure Rights Management|[Ver e utilizar ficheiros que foram protegidos pelo Rights Management](../rms-client/sharing-app-view-use-files.md)|
|Acerca da subscrição gratuita, RMS para indivíduos|[RMS para Indivíduos e Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Acerca das duas versões do ficheiro que vê anexado à mensagem de e-mail|[O que é o ficheiro .ppdf criado automaticamente?](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)|


>[!div class="step-by-step"] [« Passo 3](tutorial-step3.md)
[Passo 5 »](tutorial-step5.md)

<!--HONumber=May16_HO2-->


