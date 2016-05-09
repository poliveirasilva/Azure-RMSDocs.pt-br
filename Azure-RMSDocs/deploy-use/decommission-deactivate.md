---
# required metadata

title: Descomissionamento e desativação do Azure Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Descomissionamento e desativação do Azure Rights Management
Você tem sempre a opção de decidir se sua organização protege o conteúdo usando o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) e, se você optar por não usar esta solução de proteção de informações, terá a garantia de que o conteúdo anteriormente protegido não será bloqueado. Se não precisar de acesso contínuo ao conteúdo anteriormente protegido, simplesmente desative o serviço e permita que sua assinatura do Azure Rights Management expire. Por exemplo, isto é apropriado para quando você tiver concluído o teste do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] antes de implantá-lo em um ambiente de produção.

No entanto, se você tiver implantado o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] em produção, certifique-se de que tenha uma cópia da chave de locatário do Azure Rights Management antes de desativar o serviço e faça isso antes que sua assinatura expire. Dessa forma, você poderá manter o acesso ao conteúdo protegido pelo Azure Rights Management após o serviço ser desativado. Se usou a solução "Traga sua própria chave" (BYOK) em que o usuário gera e gerencia sua própria chave em um HSM (Módulo de segurança de hardware), você já terá sua chave de locatário do Azure Rights Management. Porém, se isso tiver sido gerenciado pela Microsoft (o padrão), consulte as instruções para exportar sua chave de locatário no artigo [Operações para sua chave de locatário do Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Mesmo depois de sua assinatura expirar, seu locatário do Azure Rights Management permanece disponível para consumo de conteúdo por um período de tempo estendido. No entanto, você não poderá mais exportar sua chave de locatário.

Assim que tiver a chave de locatário do Azure Rights Management, você poderá implantar o Rights Management no local (AD RMS) e importar sua chave de locatário como um domínio de publicação confiável (TPD). Em seguida, você tem as seguintes opções para encerrar a sua implantação do Azure Rights Management:

|Se isto se aplica a você...|… faça isto:|
|----------------------------|--------------|
|Você deseja que todos os usuários possam continuar usando o Rights Management, mas uma solução local em vez do Azure RMS    →|Use o cmdlet [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) para direcionar os usuários existentes para sua implantação local quando acessarem conteúdo protegido após esta alteração. Os usuários usarão a instalação do AD RMS automaticamente para consumir o conteúdo protegido.<br /><br />Para que os usuários possam consumir o conteúdo que foi protegido antes desta alteração, redirecione seus clientes para a implantação local usando a chave do Registro **LicensingRedirection** para o Office 2016 ou Office 2013, conforme descrito na [seção de descoberta de serviços](../rms-client/client-deployment-notes.md) nas notas de implantação do cliente RMS, e a chave do Registro **LicenseServerRedirection** para o Office 2010, conforme descrito em [Configurações de Registro do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Você deseja interromper totalmente o uso de tecnologias do Rights Management    →|Conceda [direitos de superusuário](../deploy-use/configure-super-users.md) a um administrador designado e forneça a [Ferramenta de Proteção RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) a essa pessoa.<br /><br />Esse administrador poderá, então, usar a ferramenta para descriptografar arquivos em massa nas pastas protegidas pelo Azure Rights Management para que os arquivos sejam revertidos para desprotegidos e, portanto, possam ser lidos sem uma tecnologia do Rights Management, como o Azure RMS ou o AD RMS. Essa ferramenta pode ser usada com o Azure RMS e o AD RMS, pelo que você tem a opção de descriptografar arquivos antes ou depois de desativar o Azure RMS, ou uma combinação.|
|Não é possível identificar todos os arquivos que foram protegidos pelo Azure RMS ou você deseja que todos os usuários possam ler automaticamente todos os arquivos protegidos que foram perdidos    →|Implante uma configuração de registro em todos os computadores cliente usando a chave do Registro **LicensingRedirection** para o Office 2016 e Office 2013, conforme descrito na [seção de descoberta de serviços](../rms-client/client-deployment-notes.md) nas notas de implantação de cliente RMS, e a chave do Registro **LicenseServerRedirection** para o Office 2010, conforme descrito em [Configurações de Registro do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Além disso, implante outra configuração do Registro para impedir que usuários protejam novos arquivos, definindo **DisableCreation** para **1**, conforme descrito em [Configurações de Registro do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Você deseja um serviço de recuperação controlado e manual para todos os arquivos que foram perdidos    →|Conceda [direitos de superusuário](../deploy-use/configure-super-users.md) aos usuários designados em um grupo de recuperação de dados e forneça a [Ferramenta de Proteção RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) para que eles possam desproteger arquivos quando solicitado por usuários padrão.<br /><br />Em todos os computadores, implante a configuração de Registro para impedir que usuários protejam novos arquivos, definindo **DisableCreation** para **1**, conforme descrito em [Configurações de Registro do Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Para obter mais informações sobre os procedimentos nesta tabela, consulte os seguintes recursos:

-   Para obter informações sobre o AD RMS e referências de implantação, consulte [Visão geral sobre o Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

-   Para obter instruções para importar sua chave de locatário do Azure RMS como um arquivo TPD, consulte [Adicionar um domínio de publicação confiável](https://technet.microsoft.com/library/cc771460.aspx).

-   Se você precisa instalar o módulo do Windows PowerShell para o Azure RMS, para definir a URL de migração, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

Quando você estiver pronto para desativar o serviço do Azure RMS para sua organização, use as instruções a seguir.

## Desativando o Rights Management
Use um dos seguintes procedimentos para desativar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> Você também pode usar o cmdlet do Windows PowerShell, [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) para desativar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### Para desativar o Rights Management no centro de administração do Office 365

1.  [Entre no Office 365 com sua conta corporativa ou de estudante](https://portal.office.com/) que seja administrador, para a implantação do Office 365.

2.  Se o centro de administração do Office 365 não for exibido automaticamente, selecione o ícone inicializador de aplicativos na parte superior esquerda e escolha **Admin**. O bloco do **Admin** é exibido apenas aos administradores do Office 365.

    > [!TIP]
    > Para obter ajuda do centro de administração, consulte [sobre o Centro de administração do Office 365 - Ajuda para Administradores](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  No painel esquerdo, expanda **CONFIGURAÇÕES DE SERVIÇO**.

4.  Clique em **Rights Management**.

5.  Na página **RIGHTS MANAGEMENT** , clique em **Gerenciar**.

6.  Na página **rights management** , clique em **desativar**.

7.  Quando solicitado a responder **Deseja desativar o Rights Management?**, clique em **desativar**.

Você deverá ver agora **O Rights Management não está ativo** e a opção para ativar.

#### Para desativar o Rights Management no Portal clássico do Azure

1.  Entre no [Portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory** clique em **RIGHTS MANAGEMENT**.

4.  Selecione o diretório a gerenciar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **DEACTIVATE** e, em seguida, confirme sua ação.

O **STATUS do RIGHTS MANAGEMENT** agora deve exibir **Inativo** e a opção **DESATIVAR** é substituída por **ATIVAR**.





<!--HONumber=Apr16_HO3-->


