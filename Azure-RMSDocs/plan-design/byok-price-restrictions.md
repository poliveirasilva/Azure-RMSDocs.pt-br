---
# required metadata

title: Preços e restrições do BYOK | Azure RMS
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

# Preços e restrições do BYOK

*Aplica-se a: Azure Rights Management, Office 365*


A organização que tem uma assinatura gerenciada de TI Azure pode usar o BYOK e registrar o seu uso, sem custo extra. As organizações que usam o RMS para indivíduos não podem usar BYOK e log, porque elas não têm um administrador do locatário para configurar esses recursos.


> [!NOTE]
> Para obter mais informações sobre o RMS para pessoas físicas, consulte [RMS para pessoas físicas e Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK não dá suporte ao Exchange Online](../media/RMS_BYOK_noExchange.png)

O BYOK e o log funcionam perfeitamente com todos os aplicativos que se integram com o Azure RMS. Isso inclui serviços de nuvem, como o SharePoint Online, servidores locais que executam o Exchange e servidores do SharePoint que trabalham com Azure RMS pelo uso do conector RMS e de aplicativos cliente, como o Office 2013. Você vai ter registros de uso de chave, independentemente de qual aplicativo faça solicitações de Azure RMS.

Há uma exceção: Atualmente, o **Azure RMS BYOK não é compatível com o Exchange Online**.  Se deseja usar o Exchange Online, recomendamos deixar o Azure RMS configurado no modo de gerenciamento de chave padrão, onde a Microsoft gera e gerencia a sua chave. Você tem a opção de mover para BYOK mais tarde, por exemplo, quando o Exchange Online oferece não oferece suporte ao BYOK do Azure RMS. No entanto, se você não puder esperar, outra opção é implantar o Azure RMS com BYOK agora, com funcionalidade reduzida do RMS para o Exchange Online (emails e anexos desprotegidos permanecerão totalmente funcionais):

-   Emails protegidos ou anexos protegidos no Outlook Web Access não poderão ser exibidos.

-   Emails protegidos em dispositivos móveis que usam o Exchange ActiveSync IRM não poderão ser exibidos.

-   Descriptografia de transporte (por exemplo, para verificar se há malware) e a descriptografia de diário não é possível, por isso emails e anexos protegidos serão ignorados.

-   Regras de proteção de transporte e prevenção de perda de dados (DLP) que impõem políticas de IRM não são possíveis, por isso a proteção RMS não pode ser aplicada usando esses métodos.

-   Pesquisa baseada em servidor para emails protegidos, portanto emails protegidos serão ignorados.

Quando você usa o Azure RMS BYOK com funcionalidade reduzida do RMS para o Exchange Online, o RMS funcionará com clientes de email no Outlook, Windows e Mac e outros clientes de email que não usam o Exchange ActiveSync IRM.

Se você estiver migrando para o Azure RMS do AD RMS, você pode importar a sua chave como um domínio de publicação confiável (TPD) para Exchange Online (também chamado BYOK na terminologia do Exchange, que é separada da terminologia do Azure RMS BYOK). Nesse cenário, você deve remover o TPD do Exchange Online para evitar modelos e diretivas em conflito. Para obter mais informações, consulte [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) da biblioteca de cmdlets do Exchange Online.

Às vezes, a exceção do BYOK do Azure RMS para o Exchange Online não é um problema na prática. Por exemplo, as organizações que precisam do BYOK e do log executam seus aplicativos de dados (Exchange, SharePoint, Office) no local e usam o Azure RMS para funcionalidades que não estão facilmente disponíveis com o AD RMS no local (por exemplo, a colaboração com outras empresas e acesso de clientes de telefonia móvel). O BYOK e o log operam bem neste cenário e permitem que a organização tenha controle total sobre a sua assinatura do Azure RMS.

## Próximas etapas

Se você decidiu gerenciar sua própria chave, vá para [Implementando sua chave de locatário do Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key).

Se você decidiu permanecer com a configuração padrão em que a Microsoft gerencia sua chave de locatário, consulte a seção [Próximas etapas](plan-implement-tenant-key.md#next-steps) do artigo Planejamento e implementação de sua chave de locatário do Azure Rights Management.



<!--HONumber=Apr16_HO4-->


