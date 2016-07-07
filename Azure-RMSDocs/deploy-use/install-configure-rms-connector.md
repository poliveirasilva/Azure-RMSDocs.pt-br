---
title: "Instalação e configuração do conector do Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/27/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ea4b7539ab311d782c3987a8fd74940aad72e65b
ms.openlocfilehash: 165292482349e4a233ab4030f49a297f57b041ac


---

# Instalação e configuração do conector do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use as informações a seguir para ajudá-lo a instalar e configurar o conector do Azure RMS (Rights Management). Esses procedimentos abrangem as etapas de 1 a 4 da [Implantação do conector do Azure Rights Management](deploy-rms-connector.md).

Antes de começar, certifique-se de ter revisado e verificado os [pré-requisitos](deploy-rms-connector.md#prerequisites-for-the-rms-connector) para essa implantação.


## Instalando o conector RMS

1.  Identifique os computadores (mínimo de dois) que executarão o conector do RMS. Eles devem atender as especificações mínimas listadas nos pré-requisitos.

    > [!NOTE]
    > Você terá que instalar um único conector do RMS (consistindo de vários servidores para alta disponibilidade) por locatário (locatário do Office 365 ou locatário do AD do Azure). Ao contrário do RMS do Active Directory, não é necessário instalar um conector RMS em cada floresta.

2.  Baixe os arquivos de origem para o conector do RMS do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

    Para instalar o conector RMS, baixe o RMSConnectorSetup.exe.

    Além disso:

    -   Se mais tarde quiser configurar o conector de um computador de 32 bits, baixe também o RMSConnectorAdminToolSetup_x86.exe.

    -   Se quiser usar a ferramenta de configuração do servidor para o conector RMS, para automatizar a configuração de configurações de registro nos servidores locais, baixe também o GenConnectorConfig.ps1.

3.  No computador no qual deseja instalar o conector RMS, execute o **RMSConnectorSetup.exe** com privilégios de administrador.

4.  Na página de boas-vindas da página de Configuração do Conector do Microsoft Rights Management, selecione **Instalar o conector do Microsoft Rights Management no computador**e clique em **Avançar**.

5.  Leia e aceite os termos de licença do conector do RMS e clique em **Avançar**.

Para continuar, digite uma conta e senha para configurar o conector RMS.

## Digitando credenciais
Antes de configurar o conector RMS, é necessário digitar as credenciais de uma conta que tenha privilégios suficientes para configurar o conector RMS. Por exemplo, você pode digitar **admin@contoso.com** e, em seguida, especificar a senha para essa conta.

Existem algumas restrições de caractere para essa senha. Não é possível usar uma senha que tenha qualquer um dos seguintes caracteres: E comercial ( **&** ); colchete angular esquerdo ( **[** ); colchete angular direito ( **]** ); aspas retas ( **»** ); e apóstrofo ( **“** ). Se sua senha tiver qualquer um desses caracteres, a autenticação falhará para o conector do RMS e você verá a mensagem de erro informando que essa combinação de senha e nome de usuário não é correta, mesmo que você entre com êxito usando essa conta e senha para outros cenários. Se isso se aplica à sua senha, use uma conta diferente com uma senha que não tenha nenhum desses caracteres especiais, ou então redefina sua senha de modo que ela não tenha nenhum desses caracteres especiais.

Além disso, se você tiver implementado os [controles de integração](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), certifique-se de que a conta especificada é capaz de proteger o conteúdo. Por exemplo, se você restringiu a capacidade de proteção de conteúdo para o grupo "Departamento de TI", a conta que você especificar aqui deverá ser um membro desse grupo. Caso contrário, você verá a mensagem de erro: **Falha na tentativa de descobrir o local do serviço de administração e organização. Verifique se o serviço Microsoft Rights Management está habilitado para sua organização.**

Você pode usar uma conta que tenha um dos seguintes privilégios:

-   **Administrador global para seu locatário**: uma conta que seja um administrador global para seu locatário do Office 365 ou locatário do Azure AD.

-   **Administrador global do Azure Rights Management**: uma conta no Azure Active Directory que recebeu a função de administrador global do Azure RMS.

-   **Administrador do conector do Azure Rights Management**: uma conta no Azure Active Directory com direitos para instalar e administrar o conector RMS para sua organização.

    > [!NOTE]
    > A função de administrador global do Azure Rights Management e a função de administrador do conector do Azure Rights Management são atribuídas às contas usando o cmdlet [Add- AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) do Azure RMS.
    > 
    > Para executar o conector RMS com menos privilégios, crie uma conta dedicada para essa finalidade que você atribui a função de administrador do conector RMS do Azure fazendo o seguinte:
    >
    > 1.  Se ainda não o tiver feito, baixe e instale o Windows PowerShell para o Rights Management. Para obter mais informações, consulte [Instalação do Windows PowerShell para o Azure Rights Management](install-powershell.md).
    >
    >     Inicie o Windows PowerShell com o comando **Executar como administrador** e conecte-se ao serviço do Azure RMS usando o comando [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx):
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  Em seguida, execute o comando [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx), usando apenas um dos seguintes parâmetros:
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     Por exemplo, digite: **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role «ConnectorAdministrator»**
    >
    >     Embora esses comandos atribuam a função de administrador do conector, você também pode usar a função GlobalAdministrator aqui.

Durante o processo de instalação do conector RMS, todo o software de pré-requisitos é validado e instalado, os Serviços de Informações da Internet (IIS) são instalados, se ainda não estiverem presentes, e o software do conector é instalado e configurado. Além disso, o Azure RMS está preparado para a configuração criando o seguinte:

-   Uma tabela vazia de servidores que estão autorizados a usar o conector para se comunicarem com o Azure RMS. Você adicionará servidores a essa tabela mais tarde.

-   Um conjunto de tokens de segurança para o conector que autoriza operações com o Azure RMS. Esses tokens são baixados do Azure RMS e instalados no computador local no registro. Eles são protegidos usando a interface de programação do aplicativo de proteção de dados (DPAPI) e as credenciais da conta do Sistema Local.

Na página final do assistente, faça o seguinte e clique em **Concluir**:

-   Se este for o primeiro conector que você instalou, não selecione **Iniciar console do administrador do conector para autorizar servidores** neste momento. Você selecionará essa opção após instalar o seu segundo conector RMS (ou último). Em vez disso, execute o assistente novamente em pelo menos um computador diferente. É necessário instalar no mínimo dois conectores.

-   Se você tiver instalado o seu segundo (ou último) conector, selecione **Iniciar console do administrador do conector para autorizar servidores**.

> [!TIP]
> Neste ponto, há um teste de verificação que você pode executar para testar se os serviços da Web para o conector RMS estão funcionando:
>
> -   Em um navegador da Web, conecte-se a **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx**, substituindo *&lt;connectoraddress&gt;* pelo endereço do servidor ou o nome que tem o conector RMS instalado. Uma conexão bem-sucedida exibe uma página **ServerCertificationWebService** .

Se precisar desinstalar o conector RMS, execute o assistente novamente e selecione a opção de desinstalação.

## Autorizando servidores para usar o conector RMS
Após instalar o conector RMS em pelo menos dois computadores, você estará pronto para autorizar os servidores que deseja que usam o conector RMS. Por exemplo, os servidores que executam o Exchange Server 2013 ou o SharePoint Server 2013.

Para definir esses servidores, execute a ferramenta de administração do conector RMS e adicione entradas à lista de servidores permitidos. Você pode executar essa ferramenta ao selecionar **Iniciar console do administrador do conector para autorizar servidores** no final do assistente de Configuração do conector do Microsoft Rights Management ou você pode executá-lo separadamente do assistente.

Ao autorizar esses servidores, lembre-se das seguintes considerações:

-   Os servidores adicionados terão privilégios especiais concedidos. Todas as contas que você especificar para a função do Exchange Server na configuração do conector serão concedidas à [função de superusuário](configure-super-users.md) no Azure RMS, o que oferece acesso a todo o conteúdo para esse locatário do RMS. O recurso de superusuário é habilitado automaticamente neste ponto, se necessário. Para evitar o risco de elevação de privilégios de segurança, tenha cuidado para especificar apenas as contas que são usadas pelos servidores do Exchange da sua organização. Todos os servidores configurados como servidores SharePoint ou servidores de arquivos que usam FCI terão privilégios de usuários regulares concedidos.

-   É possível adicionar vários servidores como uma única entrada, especificando uma segurança do Active Directory ou um grupo de distribuição ou uma conta de serviço que seja usada por mais de um servidor. Ao usar essa configuração, o grupo de servidores compartilhará os mesmos certificados RMS e todos serão considerados proprietários do conteúdo que qualquer um deles tiver protegido. Para minimizar custos administrativos, recomendamos o uso desta configuração de um único grupo, em vez de servidores individuais para autorizar servidores Exchange da sua empresa ou um farm de servidores do SharePoint.

Na página **Servidores que têm permissão para utilizar o conector** , clique em **Adicionar**.

> [!NOTE]
> A autorização de servidores é a configuração equivalente no Azure RMS à configuração do AD RMS para aplicar manualmente os direitos de NTFS ao ServerCertification.asmx para as contas de computador do servidor ou serviço, e concede manualmente direitos de superusuário para as contas do Exchange. Não é necessário aplicar direitos NTFS ao ServerCertification no conector.


### Adicionar um servidor à lista de servidores permitidos
Na página **Permitir que um servidor utilize o conector** , digite o nome do objeto ou procure identificar o objeto a autorizar.

É importante que você autorize o objeto correto. Para um servidor usar o conector, a conta que executa o serviço no local (por exemplo, Exchange ou SharePoint) deve ser selecionada para autorização. Por exemplo, se o serviço estiver sendo executado como uma conta de serviço configurado, adicione o nome dessa conta de serviço à lista. Se o serviço estiver sendo executado como Sistema Local, adicione o nome do objeto do computador (por exemplo, SERVERNAME$). Como uma prática recomendada, crie um grupo que contenha essas contas e especifique o grupo, em vez de nomes de servidores individuais.

Para obter mais informações sobre as diferentes funções de servidor:

-   Para servidores que executam o Exchange: Você deve especificar um grupo de segurança e pode usar o grupo padrão (**Servidores Exchange**) que o Exchange cria e mantém automaticamente de todos os servidores Exchange da floresta.

-   Para servidores que executam o SharePoint:

    -   Se um servidor do SharePoint 2010 for configurado para ser executado como Sistema Local (não estiver usando uma conta de serviço), crie manualmente um grupo de segurança nos Serviços de Domínio do Active Directory e adicione o objeto de nome do computador do servidor nesta configuração a esse grupo.

    -   Se um servidor do SharePoint for configurado para usar uma conta de serviço (a prática recomendada para o SharePoint 2010 e a única opção para o SharePoint 2016 e SharePoint 2013), faça o seguinte:

        1.  Adicione a conta de serviço que executa o serviço da Administração Central do SharePoint para permitir que o SharePoint seja configurado em seu console do administrador.

        2.  Adicione a conta que está configurada para o pool do aplicativo SharePoint.

        > [!TIP]
        > Se estas duas contas forem diferentes, considere criar um único grupo que contenha as duas contas para minimizar as despesas administrativas gerais.

-   Para servidores de arquivos que usam Infraestrutura de Classificação de Arquivos, os serviços associados são executados como a conta do Sistema Local, por isso é necessário autorizar a conta de computador para os servidores de arquivos (por exemplo, SERVERNAME$) ou um grupo que contém as contas de computador.

Quando terminar de adicionar servidores à lista, clique em **Fechar**.

Se você ainda não tiver feito isso, agora será preciso configurar o balanceamento de carga para os servidores que possuem o conector RMS instalado, e considerar a possibilidade de usar HTTPS para as conexões entre esses servidores e os servidores autorizados recentemente.

## Configurar o balanceamento de carga e alta disponibilidade
Após instalar a segunda ou a última instância do conector RMS, defina um nome de servidor da URL do conector e configure um sistema de balanceamento de carga.

O nome do servidor da URL do conector pode ser qualquer nome em um namespace que você controle. Por exemplo, você pode criar uma entrada no seu sistema de DNS para **rmsconnector.contoso.com** e configurar essa entrada para utilizar um endereço IP em seu sistema de balanceamento de carga. Não existem requisitos especiais para este nome e ele não precisa ser configurado nos servidores do conector em si. A menos que os servidores Exchange e SharePoint estejam se comunicando com o conector pela Internet, esse nome não precisa ser resolvido na Internet.

> [!IMPORTANT]
> Recomendamos que você não altere esse nome após configurar os servidores Exchange ou SharePoint para usar o conector, porque, depois, será preciso limpar esses servidores de todas as configurações de IRM e reconfigurá-los.

Depois de criar o nome no DNS e configurá-lo para um endereço IP, configure o balanceamento de carga para esse endereço, que direciona o tráfego para os servidores de conector. Você pode usar qualquer balanceador de carga com base em IP para essa finalidade, o que inclui o recurso NLB (Balanceamento de Carga de Rede) no Windows Server. Para obter mais informações, consulte [Guia de Implantação de Balanceamento de Carga](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Use as seguintes configurações para configurar o cluster NLB:

-   Portas: 80 (para HTTP) ou 443 (para HTTPS)

    Para obter mais informações sobre o uso de HTTP ou HTTPS, consulte a próxima seção.

-   Afinidade: Nenhum

-   Método de distribuição: Igual

Esse nome que você define para o sistema de balanceamento de carga (para os servidores que executam o serviço do conector RMS) é o nome do conector RMS da sua organização que você usará mais tarde, quando você configura os servidores no local para usar o Azure RMS.

## Configurando o conector RMS para usar HTTPS
> [!NOTE]
> Essa etapa de configuração é opcional, mas é recomendada para proporcionar mais segurança.

Embora o uso de TLS ou SSL seja opcional para o conector RMS, recomendamos para qualquer serviço sensível à segurança com base em HTTP. Esta configuração autentica os servidores que executam o conector para seus servidores Exchange e SharePoint que usam o conector. Além disso, todos os dados que são enviados a partir destes servidores para o conector são criptografados.

Para ativar o conector RMS para usar o TLS, em cada servidor que executa o conector RMS, instale um certificado de autenticação do servidor que contenha o nome que você usará para o conector. Por exemplo, se o nome do conector do RMS que você definiu no DNS for **rmsconnector.contoso.com**, implante um certificado de autenticação de servidor que contenha **rmsconnector.contoso.com** no assunto do certificado como o nome comum. Ou especifique **rmsconnector.contoso.com** no nome alternativo do certificado como o valor de DNS. O certificado não precisa incluir o nome do servidor. Em seguida, no IIS, vincule esse certificado ao site padrão.

Se você usar a opção HTTPS, certifique-se de que todos os servidores que executam o conector tenham um certificado de autenticação de servidor válido que se conecte a um CA raiz usado pelos servidores Exchange e SharePoint. Além disso, se a CA (Autoridade de Certificação) que emitiu os certificados para os servidores de conector publicar uma CRL (Lista de Certificados Revogados), os servidores Exchange e SharePoint poderão baixar essa CRL.

> [!TIP]
> Você pode usar as seguintes informações e recursos para lhe ajudar a solicitar e instalar um certificado de autenticação do servidor, e para vincular esse certificado ao site padrão no IIS:
>
> -   Se você usar os Serviços de Certificados do Active Directory (AD CS) e uma autoridade de certificação corporativa (CA) para implantar esses certificados de autenticação do servidor, você pode duplicar e, em seguida, usar o modelo de certificado de servidor web. Este modelo de certificado usa **Fornecido na solicitação** para o nome do assunto do certificado, o que significa que você pode fornecer o FQDN do nome do conector RMS para o nome do assunto do certificado ou nome alternativo do assunto quando solicitar o certificado.
> -   Se você usa uma CA autônoma ou adquiriu esse certificado de outra empresa, consulte [Configuração de Certificados de Servidor da Internet (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) no [Servidor Web (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) da biblioteca de documentação no TechNet.
> -   Para configurar o IIS para usar o certificado, consulte [Adicionar uma associação a um site (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx) no [Servidor Web (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) da biblioteca de documentação no TechNet.

## Configurando o conector RMS para um servidor proxy da Web
Se os seus servidores de conector estiverem instalados em uma rede que não tem conectividade direta com a Internet e exigirem a configuração manual de um servidor proxy da Web para acesso à Internet de saída, será preciso configurar o registro nos servidores para o conector do RMS.

#### Para configurar o conector RMS para usar um servidor proxy da Web

1.  Em cada servidor que executa o conector do RMS, abra um editor de registro, como o Regedit.

2.  Navegue até **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  Adicione o valor de cadeia de caracteres de **ProxyAddress** e, em seguida, defina os dados para que esse valor seja **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    Por exemplo: **http://proxyserver.contoso.com:8080**

4.  Feche o editor do Registro e reinicie o servidor ou execute um comando IISReset para reiniciar o IIS.

## Instalando a ferramenta de administração do conector RMS em computadores administrativos
É possível executar a ferramenta de administração de conector do RMS a partir de um computador que não tenha o conector do RMS se cumprir com os seguintes requisitos:

-   Um computador físico ou virtual com o Windows Server 2012 ou Windows Server 2012 R2 (todas as edições), Windows Server 2008 R2 ou Windows Server 2008 R2 Service Pack 1 (todas as edições), Windows 8.1, Windows 8 ou Windows 7.

-   Pelo menos 1 GB de RAM.

-   Um mínimo de 64 GB de espaço em disco.

-   Pelo menos uma interface de rede.

-   Acesso à Internet através de um firewall (ou proxy da Web).

Para instalar a ferramenta de administração do conector RMS, execute os seguintes arquivos:

-   Para um computador de 32 bits: RMSConnectorAdminToolSetup_x86.exe

-   Para um computador de 64 bits: RMSConnectorSetup.exe

Se você ainda não tiver baixado esses arquivos, você pode fazer isso da [Central de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).


## Próximas etapas
Agora que o conector do RMS está instalado e configurado, você está pronto para configurar seus servidores locais para usá-lo. Vá para [Configuração de servidores para o conector do Azure Rights Management](configure-servers-rms-connector.md).


<!--HONumber=Jun16_HO4-->


