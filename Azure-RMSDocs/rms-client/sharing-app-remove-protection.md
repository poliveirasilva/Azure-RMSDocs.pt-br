---
# required metadata

title: Remover a proteção de um ficheiro ao utilizar a aplicação de partilha Rights Management | Azure RMS
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

# Remover a proteção de um ficheiro ao utilizar a aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Para remover a proteção de um ficheiro (ou seja, desproteger um ficheiro) protegido anteriormente ao utilizar a aplicação de partilha RMS, utilize a opção **Remover Proteção** do Explorador de Ficheiros.

> [!IMPORTANT]
> Tem de ser um proprietário do ficheiro para remover a proteção.

## Para remover a proteção de um ficheiro

1.  No Explorador de Ficheiros, clique com o botão direito do rato no ficheiro (por exemplo, Amostra.ptxt), selecione **Proteger com RMS**, clique em **Proteger no local** e, em seguida, clique em **Remover Proteção**:

    ![Opção de menu Remover proteção da aplicação de partilha RMS](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    Poderão ser-lhe pedidas as credenciais.

Nota: se não vir estas opções de proteção, é provável que a aplicação de partilha RMS não esteja instalada no seu computador, que a versão mais recente não esteja instalada ou que seja necessário reiniciar o computador para concluir a instalação. Para obter mais informações sobre como instalar a aplicação de partilha, consulte [Transferir e instalar a aplicação de partilha Rights Management](install-sharing-app.md).

O ficheiro protegido original é eliminado (por exemplo, Amostra.ptxt) e substituído por um ficheiro que tem o mesmo nome, mas com a extensão de nome de ficheiro não protegido (por exemplo, Amostra.txt).

## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, consulte as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


