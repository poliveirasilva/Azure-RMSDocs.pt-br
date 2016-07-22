---
title: Encerrar e desativar o Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 8c114336551417fdbf1503ffc8350e3fc28e9c95


---

# Encerrar e desativar o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Pode sempre controlar se a organização protege conteúdo utilizando o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) e, se decidir que já não pretende utilizar esta solução de proteção de informações, tem a garantia de que não ficará impedido de aceder ao conteúdo que foi protegido anteriormente. Se não necessitar de acesso contínuo ao conteúdo anteriormente protegido, basta desativar o serviço e pode deixar que a sua subscrição do Azure Rights Management expire. Por exemplo, isto poderá ser adequado para quando terminar de testar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] antes de o implementar num ambiente de produção.

No entanto, se tiver implementado o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] na produção, certifique-se de que tem uma cópia da sua chave de inquilino do Azure Rights Management antes de desativar o serviço e efetue este procedimento antes de a sua subscrição expirar, uma vez que isto irá garantir que pode manter o acesso ao conteúdo que foi protegido pelo Azure Rights Management após o serviço ser desativado. Se utilizou a solução traga a sua própria chave (BYOK), onde gera e faz a gestão da sua própria chave num HSM, já terá a chave de inquilino do Azure Rights Management. Mas se foi gerida pela Microsoft (predefinição), consulte as instruções para exportar a chave de inquilino no artigo [Operações para a chave de inquilino do Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Mesmo após a sua subscrição expirar, o seu inquilino do Azure Rights Management permanece disponível para consumir conteúdo durante um período prolongado. No entanto, vai deixar de poder exportar a sua chave de inquilino.

Quando tiver a sua chave de inquilino do Azure Rights Management, pode implementar o Rights Management no local (AD RMS) e importar a chave de inquilino como um domínio de publicação fidedigno (TPD). Em seguida, tem as seguintes opções para desativar a implementação do Azure Rights Management:

|Se isto se aplica a si...|… efetue o seguinte:|
|----------------------------|--------------|
|Pretende que todos os utilizadores continuem a utilizar o Rights Management, mas utiliza uma solução no local em vez de utilizar o Azure RMS    →|Utilize o cmdlet [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) para direcionar os utilizadores existentes para a sua implementação no local quando consumirem conteúdo protegido após esta alteração. Os utilizadores utilizarão automaticamente a instalação do AD RMS para consumir conteúdo protegido.<br /><br />Para que os utilizadores consumam conteúdo que foi protegido antes desta alteração, redirecione os seus clientes para a implementação no local utilizando a chave de registo **LicensingRedirection** para o Office 2016 ou o Office 2013, tal como descrito na [secção de deteção do serviço](../rms-client/client-deployment-notes.md) nas notas de implementação do cliente do RMS, bem como a chave de registo **LicenseServerRedirection** para o Office 2010, conforme descrito nas [Definições de Registo do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Pretende deixar de utilizar as tecnologias de Rights Management completamente    →|Conceda a um administrador designado [direitos de superutilizador](../deploy-use/configure-super-users.md) e forneça-lhe a [Ferramenta de Proteção RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />Este administrador pode então utilizar a ferramenta para desencriptar ficheiros em volume em pastas que estavam protegidas pelo Azure Rights Management, para que os ficheiros voltem a estar desprotegidos e, por conseguinte, possam ser lidos sem uma tecnologia de Rights Management, como o Azure RMS ou o AD RMS. Esta ferramenta pode ser utilizada com o Azure RMS e o AD RMS, pelo que terá a opção de desencriptar ficheiros antes ou depois de desativar o Azure RMS, ou uma combinação.|
|Não consegue identificar todos os ficheiros que estavam protegidos pelo Azure RMS ou pretende que todos os utilizadores possam ler automaticamente quaisquer ficheiros protegidos em falta    →|Implemente uma definição de registo em todos os computadores cliente utilizando a chave de registo **LicensingRedirection** para o Office 2016 ou o Office 2013, tal como descrito na [secção de deteção do serviço](../rms-client/client-deployment-notes.md) nas notas de implementação do cliente do RMS, bem como a chave de registo **LicenseServerRedirection** para o Office 2010, conforme descrito nas [Definições de Registo do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Implemente também outra definição de registo para impedir que os utilizadores protejam novos ficheiros ao definir **DisableCreation** como **1**, conforme descrito nas [Definições de Registo do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Pretende um serviço de recuperação manual controlado para ficheiros em falta    →|Conceda a utilizadores designados num grupo de recuperação de dados [direitos de superutilizador](../deploy-use/configure-super-users.md) e forneça-lhes a [Ferramenta de Proteção RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) para que possam desproteger ficheiros quando solicitado por utilizadores padrão.<br /><br />Implemente em todos os computadores a definição de registo para impedir que os utilizadores protejam novos ficheiros ao definir **DisableCreation** como **1**, conforme descrito nas [Definições de Registo do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Para obter mais informações sobre os procedimentos nesta tabela, consulte os recursos seguintes:

-   Para obter informações acerca do AD RMS e ter acesso às referências de implementação, consulte [Descrição Geral dos Serviços de Gestão de Direitos do Active Directory](https://technet.microsoft.com/library/hh831364.aspx).

-   Para obter instruções para importar a sua chave de inquilino do Azure RMS como um ficheiro TPD, consulte [Adicionar um Domínio de Publicação Fidedigno](https://technet.microsoft.com/library/cc771460.aspx).

-   Para instalar o módulo do Windows PowerShell para o Azure RMS, para definir o URL de migração, consulte [Instalar o Windows PowerShell para o Azure Rights Management](install-powershell.md).

Quando estiver pronto para desativar o serviço Azure RMS na sua organização, utilize as instruções que se seguem.

## Desativar o Rights Management
Utilize um dos seguintes procedimentos para desativar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Também pode utilizar o cmdlet do Windows PowerShell, [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx), para desativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### Para desativar o Rights Management a partir do centro de administração do Office 365

1.  [Inicie sessão no Office 365 com a sua conta escolar ou profissional](https://portal.office.com/) que seja de um administrador da implementação do Office 365.

2.  Se o centro de administração do Office 365 não for apresentado automaticamente, selecione o ícone do iniciador de aplicações no canto superior esquerdo e escolha **Administrador**. O mosaico **Administrador** só é apresentado para os administradores do Office 365.

    > [!TIP]
    > Para obter ajuda acerca do centro de administração, consulte [Acerca do centro de administração do Office 365 – Ajuda de Administração](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  No painel esquerdo, expanda **DEFINIÇÕES DE SERVIÇO**.

4.  Clique em **Rights Management**.

5.  Na página **RIGHTS MANAGEMENT**, clique em **Gerir**.

6.  Na página **gestão de direitos**, clique em **desativar**.

7.  Quando lhe for perguntado **Pretende desativar o Rights Management?**, clique em **desativar**.

Já deverá estar visível **O Rights Management não está ativado** e a opção para ativar.

#### Para desativar o Rights Management a partir do portal clássico do Azure

1.  Inicie sessão no [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory**, clique em **GESTÃO DE DIREITOS**.

4.  Selecione o diretório a gerir do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **DESATIVAR** e confirme a ação.

O **ESTADO DO RIGHTS MANAGEMENT** deverá agora apresentar **Inativo** e a opção **DESATIVAR** é substituída por **ATIVAR**.






<!--HONumber=Jun16_HO4-->


