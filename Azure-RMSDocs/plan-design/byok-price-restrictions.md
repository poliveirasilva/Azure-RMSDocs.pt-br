---
# required metadata

title: Preços e restrições de BYOK | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Preços e restrições de BYOK

*Aplica-se a: Azure Rights Management, Office 365*


As organizações com uma subscrição do Azure gerida pelo departamento de TI podem utilizar o BYOK e registar a sua utilização sem qualquer custo adicional. As organizações que utilizam o RMS para utilizadores autónomos não podem utilizar o BYOK e o registo, porque não têm um administrador de inquilinos para configurar estas funcionalidades.


> [!NOTE]
> Para mais informações sobre o RMS para utilizadores autónomos, consulte [RMS para indivíduos e Azure Rights Management](../understand-explore/rms-for-individuals.md).

![O BYOK não suporta o Exchange Online](../media/RMS_BYOK_noExchange.png)

O BYOK e o registo funcionam perfeitamente com todas as aplicações integradas no Azure RMS. Isto inclui serviços em nuvem como o SharePoint Online, servidores no local que executam o Exchange e SharePoint e que funcionam com o Azure RMS ao utilizar o conector RMS e aplicações de cliente como o Office 2013. Irá obter registos de utilização da chave, independentemente da aplicação que efetua os pedidos do Azure RMS.

Existe uma exceção: atualmente, o **BYOK do Azure RMS não é compatível com o Exchange Online**.  Se desejar utilizar o Exchange Online, recomendamos que implemente agora o Azure RMS no modo de gestão de chaves predefinido, em que a Microsoft gera e faz a gestão da sua chave. Pode mudar para o BYOK posteriormente, por exemplo, quando o Exchange Online suportar o BYOK do Azure RMS. No entanto, se não puder aguardar, pode implementar o Azure RMS com o BYOK agora, com a funcionalidade do RMS reduzida no Exchange Online (os e-mails e anexos desprotegidos permanecem totalmente funcionais):

-   Os e-mails e anexos protegidos no Outlook Web Access não podem ser apresentados.

-   Os e-mails protegidos em dispositivos móveis que utilizem a IRM do Exchange ActiveSync não podem ser apresentados.

-   Não é possível realizar a desencriptação de transporte (por exemplo, para procurar software maligno) e a desencriptação do diário, por isso, os e-mails e anexos protegidos serão ignorados.

-   As regras de proteção de transporte e a prevenção de perda de dados (DLP) que impõem as políticas IRM não podem ser executadas, pelo que não é possível aplicar a proteção RMS com estes métodos.

-   A pesquisa baseada no servidor não abrange e-mails protegidos, por isso, estes serão ignorados.

Quando utilizar o BYOK do Azure RMS com funcionalidade reduzida do RMS no Exchange Online, o RMS irá funcionar com os clientes de e-mail no Outlook, Windows e Mac e noutros clientes de e-mail que não utilizem a IRM do Exchange ActiveSync.

Caso esteja a migrar para o Azure RMS a partir do AD RMS, pode ter importado a chave como um domínio de publicação fidedigno (TPD) para o Exchange Online (também denominado BYOK na terminologia de Exchange, que é diferente do BYOK do Azure RMS). Neste cenário, tem de remover o TPD do Exchange Online para evitar que os modelos e políticas entrem em conflito. Para obter mais informações, consulte [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) na biblioteca de cmdlets do Exchange Online.

Por vezes, a exceção do BYOK do Azure RMS para o Exchange Online não é um problema a níveis práticos. Por exemplo, as organizações que precisam do BYOK e do registo executam as suas aplicações de dados (Exchange, SharePoint, Office) no local e utilizam o Azure RMS para obter funcionalidades que não estão facilmente disponíveis no AD RMS no local (por exemplo, a colaboração com outras empresas e o acesso a partir de clientes móveis). O BYOK e o registo funcionam bem neste cenário e permitem que a organização tenha um controlo total sobre a sua subscrição do Azure RMS.

## Passos seguintes

Se tiver tomado a decisão de gerir a sua própria chave, aceda a [Implementar a sua chave de inquilino do Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key).

Se tiver decidido manter a configuração predefinida, em que a Microsoft gere a sua chave de inquilino, consulte a secção [Passos seguintes](plan-implement-tenant-key.md#next-steps) do artigo Planear e implementar a sua chave de inquilino do Azure Rights Management.



<!--HONumber=Apr16_HO4-->


