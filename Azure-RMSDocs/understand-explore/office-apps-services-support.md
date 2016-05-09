---
# required metadata

title: Aplicativos e serviços do Office | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Aplicativos e serviços do Office
Os aplicativos de usuário final do Office (como o Word, Excel, PowerPoint e Outlook) e serviços do Office (como o Exchange e SharePoint) podem usar o Microsoft Azure Rights Management para ajudar a proteger os dados da sua organização.

## Aplicativos do Office: Word, Excel, PowerPoint, Outlook
Esses aplicativos dão suporte nativamente ao Gerenciamento de Direitos usando Gerenciamento de Direitos de Informação (IRM) e permitem que os usuários apliquem proteção a um documento salvo ou a uma mensagem de email a ser enviada. Os usuários podem aplicar modelos ou escolher configurações bem personalizadas de acesso, direitos e restrições de uso. 

Por exemplo, os usuários podem configurar um arquivo para que ele possa ser acessado somente por pessoas de sua organização, ou controlar se o arquivo pode ser editado ou restrito a somente leitura, ou impedir que ele seja impresso. Para arquivos que têm data para vencer, pode ser configurada uma data de validade (diretamente por usuários ou aplicando um modelo) para quando o arquivo não puder mais ser acessado. Para o Outlook, os usuários também podem escolher a opção **Não Encaminhar** para ajudar a impedir o vazamento de dados.

## Exchange Online e Exchange Server
Ao usar o Exchange Online ou o Exchange Server, você pode usar a integração de gerenciamento de direitos de informação (IRM), que fornece soluções de proteção de informações adicionais:

-   **IRM do Exchange ActiveSync** para que os dispositivos móveis possam proteger e consumir mensagens de email protegidas.

-   O suporte RMS para o **Outlook Web App**, implementado de forma semelhante ao cliente Outlook, de modo que os usuários possam proteger as mensagens de email por modelos ou especificando as opções individuais, e os usuários possam ler e usar emails protegidos enviados a eles.

-   **Regras de proteção** para clientes Outlook configuradas por um administrador para aplicar automaticamente modelos de RMS às mensagens de email para destinatários especificados. Por exemplo, quando emails internos forem enviados ao seu departamento jurídico, eles só poderão ser lidos por membros do departamento jurídico e não poderão ser encaminhados. Os usuários veem a proteção aplicada à mensagem de email antes de enviá-la e, por padrão, eles podem removê-la se decidirem que não é necessária. Os emails são criptografados antes de serem enviados. Para obter mais informações, consulte [Regras de Proteção do Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) e [Criar uma regra de proteção do Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) na biblioteca do Exchange.

-   As**Regras de transporte** que um administrador configura para aplicar automaticamente os modelos de RMS às mensagens de email com base em propriedades como: remetente, destinatário, assunto da mensagem e conteúdo. Elas são semelhantes ao conceito de regras de proteção, mas não permitem que os usuários removam a proteção, podem ser aplicadas ao Outlook Web Access e emails enviados por dispositivos móveis e não criptografa mensagens de email antes que sejam enviados do cliente. Para obter mais informações, consulte [Criar uma regra de proteção de transporte](https://technet.microsoft.com/library/dd302432.aspx) na biblioteca do Exchange.

-   **Políticas de prevenção de perda de dados (DLP)** que contêm conjuntos de condições para filtrar mensagens de email e tomar medidas para ajudar a evitar a perda de dados para conteúdos confidenciais (por exemplo, informações pessoais ou informações de cartão de crédito). As dicas de política podem ser usadas quando forem detectados dados confidenciais, para alertar os usuários que eles talvez precisem aplicar a proteção de informações, com base nas informações na mensagem de email. Para obter mais informações, consulte [Prevenção contra perda de dados](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) na biblioteca do Exchange.

-   A**Criptografia de mensagem do Office 365** que usa regras de transporte para enviar emails criptografados para pessoas de fora da empresa e o email é lido em um navegador com uma interface semelhante ao Outlook Web App. Você pode personalizar o texto de aviso e o texto do cabeçalho em emails criptografados de sua empresa, e até mesmo adicionar o logotipo da empresa. Para obter mais informações, consulte [Criptografia de Mensagens do Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) no site do Office.

Se usar o Exchange Server, você poderá usar os recursos de proteção de informações com o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] implantando o conector de RMS, que atua como um retransmissor entre os servidores no local e o serviço de nuvem do RMS. Para obter mais informações, consulte [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## SharePoint Online e SharePoint Server
Ao usar o SharePoint Online ou o SharePoint Server, você pode usar a integração de gerenciamento de direitos de informação (IRM), que permite que os administradores protejam listas ou bibliotecas, para que um arquivo fique protegido quando um usuário fechá-lo e apenas pessoas autorizadas possam visualizar e usar o arquivo de acordo com as políticas de proteção de informações especificadas. Por exemplo, o arquivo pode ser somente leitura, pode desativar a cópia de texto, pode impedir que uma cópia local seja salva e pode evitar a impressão do arquivo.

Para listas e bibliotecas, a proteção de informações é sempre aplicada por um administrador, nunca um usuário final. E isso é aplicado no nível de lista ou biblioteca para todos os documentos desse contêiner, e não em arquivos individuais.  Se você usar o SharePoint Online, os usuários também podem aplicar IRM para a sua biblioteca de Negócios OneDrive.

O serviço IRM deve primeiro ser habilitado para o SharePoint. Em seguida, especifique o Gerenciamento de Direitos de Informação para uma biblioteca. No caso do SharePoint Online e OneDrive para Negócios, os usuários podem especificar também Gerenciamento de Direitos de Informação do seu OneDrive para a biblioteca de Negócios. O SharePoint não usa modelos de política de direitos, embora haja definições de configuração do SharePoint para selecionar que se aproximam daquelas que você pode especificar em modelos.

Se usar o SharePoint Server, você poderá usar os recursos de proteção de informações com o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] implantando o conector de RMS, que atua como um retransmissor entre os servidores no local e o serviço de nuvem do RMS. Para obter mais informações, consulte [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Atualmente, existem algumas limitações quando você usa o IRM com o SharePoint:
> 
> -   Você não pode usar os modelos padrão ou personalizados que você gerencia no portal clássico do Azure.
> -   Arquivos que tenham uma extensão .PPDF para arquivos PDF protegidos, não são suportados. Arquivos que possuem extensão .PDF e que foram protegidos nativamente pelo RMS têm suporte quando você usa um leitor PDF que oferece suporte nativo ao RMS.
> -   Como ainda não há suporte para RMS no Office em dispositivos móveis, esses dispositivos devem usar um navegador para exibir arquivos que foram protegidos por RMS e os arquivos que são somente para leitura.

O Azure RMS aplica restrições de uso e criptografia de dados quando os documentos são baixados pelo SharePoint e não quando o documento é criado pela primeira vez no SharePoint ou carregado na biblioteca. Para obter informações sobre como os documentos são protegidos antes de serem baixados, veja [Criptografia de Dados no OneDrive for Business e SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) na documentação do SharePoint.

Para obter mais informações sobre como usar o Azure RMS com o SharePoint, consulte a publicação do blog do Office a seguir: [Novidades no Gerenciamento de Direitos de Informação do SharePoint e do SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## Próximas etapas

Para ver como outros aplicativos e serviços dão suporte ao Azure Rights Management, consulte [Como os aplicativos dão suporte ao Azure Rights Management](applications-support.md).

<!--HONumber=Apr16_HO3-->


