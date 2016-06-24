---
# required metadata

title: Remover a proteção de um arquivo usando o aplicativo de compartilhamento Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Remover a proteção de um arquivo usando o aplicativo de compartilhamento Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Para remover a proteção de um arquivo (ou seja, desproteger um arquivo) que foi anteriormente protegido usando o aplicativo RMS sharing, use a opção **Remover Proteção** no Explorador de Arquivos.

> [!IMPORTANT]
> Você deve ser um proprietário do arquivo para remover a proteção.

## Para remover a proteção de um arquivo

1.  No Explorador de Arquivos, clique com o botão direito do mouse no arquivo (por exemplo, Exemplo.ptxt), selecione **Proteger com o RMS**, clique em **Proteção no local**, e, em seguida, clique em **Remover proteção**:

    ![Remover a opção de menu de proteção para o aplicativo de compartilhamento RMS](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    Suas credenciais não serão solicitadas.

Observação: caso você não veja essas opções, é provável que o aplicativo RMS sharing não esteja instalado no seu computador, a versão mais recente não esteja instalada ou o computador deve ser reiniciado para concluir a instalação. Para obter mais informações sobre como instalar o aplicativo de compartilhamento, consulte [Baixar e instalar o aplicativo de compartilhamento do Rights Management](install-sharing-app.md).

O arquivo original protegido é excluído (por exemplo, Sample.ptxt) e substituído por um arquivo que tem o mesmo nome, mas com a extensão de nome de arquivo desprotegido (por exemplo, Sample.txt).

## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


