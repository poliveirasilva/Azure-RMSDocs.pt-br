---
# required metadata

title: Instalar e configurar o conector Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalar e configurar o conector Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Utilize as seguintes informações para o ajudar a instalar e configurar o conector Azure Rights Management (RMS). Estes procedimentos estão descritos nos passos 1 a 4 do artigo [Deploying the Azure Rights Management connector (Implementar o conector Azure Rights Management – em inglês)](deploy-rms-connector.md).

Antes de começar, certifique-se de que consultou e verificou os [pré-requisitos](deploy-rms-connector.md#prerequisites-for-the-rms-connector) para esta implementação.


## Instalar o conector RMS

1.  Identifique os computadores (no mínimo dois) que irão executar o conector RMS. Os computadores têm de cumprir as especificações mínimas descritas nos pré-requisitos.

    > [!NOTE]
    > Deve instalar um único conector RMS (composto por múltiplos servidores para elevada disponibilidade) por inquilino (inquilino do Office 365 ou do Azure AD). Ao contrário do Active Directory RMS, não precisa de instalar um conector RMS em cada floresta.

2.  Transfira os ficheiros de origem do conector RMS a partir do [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

    Para instalar o conector RMS, transfira o ficheiro RMSConnectorSetup.exe.

    Além disso:

    -   Se posteriormente quiser configurar o conector de um computador de 32 bits, transfira também o ficheiro RMSConnectorAdminToolSetup_x86.exe.

    -   Se quiser utilizar a ferramenta de configuração do servidor para o conector RMS, para automatizar a configuração das definições de registo nos seus servidores no local, transfira também o ficheiro GenConnectorConfig.ps1.

3.  No computador em que pretende instalar o conector RMS, execute o ficheiro **RMSConnectorSetup.exe** com privilégios de Administrador.

4.  Na página de boas-vindas da página Configuração do Conector Microsoft Rights Management, selecione **Instalar o conector Microsoft Rights Management no computador** e, em seguida, clique em **Seguinte**.

5.  Leia e concorde com os termos de licenciamento do conector RMS e, em seguida, clique em **Seguinte**.

Para continuar, introduza uma conta e palavra-passe para configurar o conector RMS.

## Introduzir credenciais
Antes de configurar o conector RMS, tem de introduzir as credenciais da conta que tem privilégios suficientes para configurar o conector RMS. Por exemplo, pode escrever **admin@contoso.com** e, em seguida, especificar a palavra-passe desta conta.

Existem algumas restrições de carateres para esta palavra-passe. Não pode utilizar uma palavra-passe que tenha os seguintes carateres: "E" comercial ( **&** ); parêntese reto esquerdo ( **[** ); parêntese reto direito ( **]** ); aspas direitas ( **"** ) e apóstrofo ( **'** ). Se a sua palavra-passe tiver algum destes carateres, a autenticação do conector RMS irá falhar e receberá a mensagem de erro "Essa combinação de nome de utilizador e palavra-passe não está correta", mesmo que já tenha conseguido iniciar sessão com esta conta e palavra-passe noutros cenários. Se este caso se aplicar à sua palavra-passe, utilize uma conta com uma palavra-passe que não tenha nenhum destes carateres especiais ou reponha a palavra-passe para remover os carateres especiais.

Além disso, se tiver implementado [controlos de integração](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), certifique-se de que a conta especificada tem a capacidade de proteger conteúdos. Por exemplo, se tiver restringido a capacidade de proteger conteúdos ao grupo "Departamento de TI", a conta que especificar tem de ser membro desse grupo. Caso contrário, receberá a mensagem de erro: **Ocorreu uma falha ao tentar descobrir a localização da organização e do serviço de administração. Certifique-se de que o serviço Microsoft Rights Management está ativado para a sua organização.**

Pode utilizar uma conta que tenha um dos seguintes privilégios:

-   **Administrador do inquilino do Office 365**: uma conta que seja um administrador global do seu inquilino do Office 365.

-   **Administrador global do Azure Rights Management**: uma conta com privilégios de administrador do inquilino do Azure RMS.

-   **Administrador do conector Microsoft RMS**: uma conta no Azure Active Directory com direitos para instalar e administrar o conector RMS na sua organização.

    > [!NOTE]
    > Se quiser utilizar a conta de Administrador do conector Microsoft RMS, tem primeiro de atribuir a função de administrador do conector RMS, da seguinte forma:
    >
    > 1.  No mesmo computador, transfira e instale o Windows PowerShell para o Rights Management. Para mais informações, consulte [Installing Windows PowerShell for Azure Rights Management (Instalar o Windows PowerShell para o Azure Rights Management – em inglês)](install-powershell.md).
    >
    >     Inicie o Windows PowerShell com o comando **Executar como administrador** e estabeleça ligação ao serviço Azure RMS através do comando [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx):
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  Em seguida, execute o comando [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) com apenas um dos seguintes parâmetros:
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
    >     Por exemplo, escreva: **Add-AadrmRoleBasedAdministrator -EmailAddress mariana@contoso.com -Role " ConnectorAdministrator "**
    >
    >     Embora estes comandos utilizem a função ConnectorAdministrator, também pode utilizar a função GlobalAdministrator aqui.

Durante o processo de instalação do conector RMS, todos os softwares de pré-requisito são validados e instalados, os Serviços de Informação Internet (IIS) são instalados se ainda não estiverem presentes e o software do conector é instalado e configurado. Além disso, o Azure RMS é preparado para configuração ao criar o seguinte:

-   Uma tabela vazia dos servidores que têm autorização para utilizar o conector para comunicar com o Azure RMS. Adicionará os servidores a esta tabela mais tarde.

-   Um conjunto de tokens de segurança do conector, que autoriza operações no Azure RMS. Estes tokens são transferidos a partir do Azure RMS e instalados no computador local no registo. São protegidos através da interface de programação da aplicação de proteção de dados (DPAPI) e das credenciais de conta do Sistema Local.

Na página final do assistente, efetue o seguinte procedimento e, em seguida, clique em **Concluir**:

-   Se este for o primeiro conector que instala, não selecione ainda a opção **Iniciar a consola do administrador do conector para autorizar servidores**. Selecione esta opção depois de instalar o seu segundo (ou último) conector RMS. Em alternativa, execute novamente o assistente em pelo menos mais um computador. Tem de instalar um mínimo de dois conectores.

-   Se já tiver instalado o seu segundo (ou último) conector, selecione a opção **Iniciar a consola do administrador do conector para autorizar servidores**.

> [!TIP]
> Nesta fase, existe um teste de verificação que pode realizar para testar se os serviços Web do conector RMS estão operacionais:
>
> -   Num browser, estabeleça ligação a **http://&lt;endereçodoconector&gt;/_wmcs/certification/servercertification.asmx** e substitua *&lt;endereçodoconector&gt;* pelo nome ou endereço do servidor que tem o conector RMS instalado. Uma ligação com êxito apresenta a página **ServerCertificationWebService**.

Se precisar de desinstalar o conector RMS, execute novamente o assistente e selecione a opção Desinstalar.

## Autorizar os servidores a utilizar o conector RMS
Quando tiver instalado o conector RMS em pelo menos dois computadores, está pronto para autorizar os servidores e os serviços com os quais quer utilizar o conector RMS. Por exemplo, os servidores com o Exchange Server 2013 ou o SharePoint Server 2013.

Para definir estes servidores, execute a ferramenta de administração do conector RMS e adicione entradas à lista de servidores permitidos. Pode executar esta ferramenta quando selecionar a opção **Iniciar a consola do administrador do conector para autorizar servidores** no final do Assistente de configuração do conector Microsoft Rights Management ou pode executá-la separadamente do assistente.

Quando autorizar estes servidores, tenha em consideração o seguinte:

-   Os servidores que adicionar terão privilégios especiais. Todas as contas que especificar para a função do Exchange Server na configuração do conector terão a [função de superutilizador](configure-super-users.md) no Azure RMS, que lhes concede acesso a todos os conteúdos deste inquilino RMS. Se necessário, a funcionalidade de superutilizador é ativada automaticamente nesta fase. Para evitar o risco de segurança da elevação de privilégios, tenha o cuidado de especificar apenas as contas que são utilizadas pelos servidores Exchange da sua organização. Todos os servidores configurados como servidores do SharePoint ou servidores de ficheiros que utilizem a FCI (Infraestrutura de Classificação de Ficheiros) terão privilégios de utilizador normais.

-   Pode adicionar múltiplos servidores como uma única entrada, ao especificar um grupo de distribuição ou de segurança do Active Directory ou uma conta de serviço que seja utilizada por mais do que um servidor. Se utilizar esta configuração, o grupo de servidores partilhará os mesmos certificados RMS e todos serão considerados proprietários dos conteúdos que cada um deles protege. Para minimizar as tarefas administrativas adicionais, recomendamos que utilize esta configuração de um único grupo, em vez de servidores individuais, para autorizar os servidores Exchange da sua organização ou um farm de servidores do SharePoint.

Na página **Servidores com permissão para utilizar o conector**, clique em **Adicionar**.

> [!NOTE]
> A autorização de servidores é a configuração do Azure RMS equivalente à configuração do AD RMS, que consiste em aplicar manualmente direitos NTFS ao ServerCertification.asmx para a conta de serviço ou do computador servidor e, também, em conceder manualmente direitos de superutilizador às contas do Exchange. Não é necessário aplicar direitos NTFS ao ServerCertification.asmx no conector.


### Adicionar um servidor à lista de servidores permitidos
Na página **Permitir que um servidor utilize o conector**, introduza o nome do objeto ou procure para identificar o objeto a autorizar.

É importante que autorize o objeto correto. Para um servidor utilizar o conector, a conta que executa o serviço no local (por exemplo, o Exchange ou o SharePoint) tem de estar selecionada para autorização. Por exemplo, se o serviço estiver a ser executado como conta de serviço configurada, adicione o nome dessa conta de serviço à lista. Se o serviço estiver a ser executado como Sistema Local, adicione o nome do objeto do computador (por exemplo, NOMEDOSERVIDOR$) Como melhor prática, crie um grupo composto por estas contas e especifique o grupo em vez de nomes de servidores individuais.

Mais informações sobre as diferentes funções de servidor:

-   Para os servidores que executam o Exchange: tem de especificar um grupo de segurança e pode utilizar o grupo predefinido (**Servidores Exchange**) que o Exchange cria e guarda automaticamente com todos os servidores Exchange na floresta.

-   Para os servidores que executam o SharePoint:

    -   Se um servidor do SharePoint 2010 estiver configurado para executar como Sistema Local (não está a utilizar uma conta de serviço), crie manualmente um grupo de segurança nos Serviços de Domínio do Active Directory e adicione o nome de objeto de computador do servidor nesta configuração ao grupo.

    -   Se um servidor do SharePoint estiver configurado para utilizar uma conta de serviço (a prática recomendada para o SharePoint 2010 e a única opção para o SharePoint 2016 e o SharePoint 2013), faça o seguinte:

        1.  Adicione a conta de serviço que executa o serviço da Administração Central do SharePoint para permitir que o SharePoint seja configurado a partir da respetiva consola do administrador.

        2.  Adicione a conta que está configurada para o Conjunto Aplicacional do SharePoint.

        > [!TIP]
        > Se estas duas contas forem diferentes, pondere criar um único grupo que contenha ambas as contas para minimizar as tarefas administrativas adicionais.

-   Para os servidores de ficheiros que utilizam a Infraestrutura de Classificação de Ficheiros, os serviços associados são executados como a conta do Sistema Local, por isso, tem de autorizar a conta do computador para os servidores de ficheiros (por exemplo, NOMEDOSERVIDOR$) ou um grupo que contenha essas contas de computador.

Quando terminar de adicionar os servidores à lista, clique em **Fechar**.

Se ainda não o tiver feito, tem de configurar agora o balanceamento de carga dos servidores que têm o conector RMS instalado e decidir se quer utilizar HTTPS nas ligações entre estes servidores e os servidores que acabou de autorizar.

## Configurar o balanceamento de carga e a elevada disponibilidade
Depois de instalar a segunda ou última instância do conector RMS, defina um nome de servidor do URL do conector e configure um sistema de balanceamento de carga.

O nome de servidor do URL do conector pode ser qualquer nome dentro do espaço de nomes controlado por si. Por exemplo, pode criar uma entrada no seu sistema DNS para **rmsconnector.contoso.com** e configurar esta entrada para utilizar um endereço IP no seu sistema de balanceamento de carga. Não existem requisitos especiais para este nome e não precisa de ser configurado nos próprios servidores do conector. A menos que os seus servidores Exchange e do SharePoint comuniquem com o conector através da Internet, este nome não precisa de resolver na Internet.

> [!IMPORTANT]
> Recomendamos que não altere este nome após ter configurado os servidores Exchange e do SharePoint para utilizar o conector, uma vez que teria de limpar as configurações de IRM destes servidores e, depois, reconfigurá-las.

Depois de criar o nome no DNS e de o configurar para um endereço IP, configure o balanceamento de carga desse endereço, que redireciona o tráfego para os servidores do conector. Pode utilizar qualquer balanceador de carga baseado em IP para este fim, que inclua a funcionalidade Balanceamento de Carga na Rede (NLB) no Windows Server. Para mais informações, consulte o [Load Balancing Deployment Guide (Guia de Implementação do Balanceamento de Carga – em inglês)](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Utilize as seguintes definições para configurar o cluster com balanceamento de carga em rede (NLB):

-   Portas: 80 (para HTTP) ou 443 (para HTTPS)

    Para mais informações sobre quando utilizar HTTP ou HTTPS, consulte a secção seguinte.

-   Afinidade: nenhuma

-   Método de distribuição: igual

O nome que define para o sistema com balanceamento de carga (para os servidores a executar o serviço do conector RMS) é o nome do conector RMS da sua organização que irá utilizar mais tarde, quando configurar os servidores no local para utilizar o Azure RMS.

## Configurar o conector RMS para utilizar HTTPS
> [!NOTE]
> Este passo da configuração é opcional, mas é recomendado para uma segurança adicional.

Embora o uso de TLS ou SSL seja opcional para o conector RMS, recomendamos que seja utilizado para todos os serviços de segurança importantes baseados em HTTP. Esta configuração autentica os servidores que estão a executar o conector nos seus servidores Exchange e do SharePoint que utilizam o conector. Além disso, todos os dados enviados a partir destes servidores para o conector são encriptados.

Para ativar o conector RMS para utilizar TLS, em cada servidor que executa o conector RMS, instale um certificado de autenticação de servidor que contenha o nome que irá utilizar para o conector. Por exemplo, se o nome do seu conector RMS que definiu no DNS for **rmsconnector.contoso.com**, implemente um certificado de autenticação de servidor que contenha **rmsconnector.contoso.com** como nome comum no requerente do certificado. Em alternativa, especifique **rmsconnector.contoso.com** como valor DNS no nome alternativo do certificado. O certificado não precisa de incluir o nome do servidor. Em seguida, nos IIS, vincule este certificado ao Web Site Predefinido.

Se utilizar a opção HTTPS, certifique-se de que todos os servidores que executam o conector têm um certificado de autenticação de servidor válido que encadeia numa AC de raiz considerada fidedigna pelos servidores Exchange e do SharePoint. Além disso, se a autoridade de certificação (AC) que emitiu o certificado para os servidores do conector publicar uma lista de revogação de certificados (CRL), os servidores Exchange e do SharePoint têm de conseguir transferir esta CRL.

> [!TIP]
> Pode utilizar os seguintes recursos e informações para o ajudar a pedir e instalar um certificado de autenticação de servidor e para vincular este certificado ao Web Site Predefinido no IIS:
>
> -   Se utilizar os Serviços de Certificados do Active Directory (AD CS) e uma autoridade de certificação empresarial (AC) para implementar estes certificados de autenticação de servidor, pode duplicar e utilizar o modelo de certificado do Web Server. Este modelo de certificado utiliza a opção **Fornecido no pedido** para o nome do requerente do certificado, o que significa que pode fornecer o FQDN do nome do conector RMS para o nome do requerente do certificado ou um nome de requerente alternativo quando pedir o certificado.
> -   Se utilizar uma AC autónoma ou adquirir este certificado a partir de outra empresa, consulte [Configuring Internet Server Certificates (IIS 7) (Configurar Certificados do Servidor de Internet (IIS 7) – em inglês)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) na biblioteca de documentos referente ao [Web Server (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) no TechNet.
> -   Para configurar o IIS para utilizar o certificado, consulte [Add a Binding to a Site (IIS 7) (Adicionar um Enlace a um Site (IIS 7) – em inglês)](http://technet.microsoft.com/library/cc731692.aspx) na biblioteca de documentos referente ao [Web Server (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) no TechNet.

## Configurar o conector RMS para um servidor proxy Web
Se os servidores do seu conector estiverem instalados numa rede que não tem conectividade Internet direta e que necessita de configuração manual de um servidor proxy Web para o acesso à Internet de saída, tem de configurar o registo nestes servidores para o conector RMS.

#### Para configurar o conector RMS para utilizar um servidor proxy Web

1.  Abra o editor de registo, por exemplo o Regedit, em cada servidor que executa o conector RMS.

2.  Navegue para **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  Adicione o valor de cadeia de **ProxyAddress** e, em seguida, defina os Dados deste valor como **http://&lt;OMeuDomínioDeProxyOuEndereçoIP&gt;:&lt;AMinhaPortaDeProxy&gt;**

    Por exemplo: **http://proxyserver.contoso.com:8080**

4.  Feche o editor de registo e, em seguida, reinicie o servidor ou execute o comando IISReset para reiniciar o IIS.

## Instalar a ferramenta de administração do conector RMS em computadores administrativos
Pode executar a ferramenta de administração do conector RMS a partir de um computador que não tenha o conector RMS instalado, se esse computador cumprir os seguintes requisitos:

-   Um computador físico ou virtual com o Windows Server 2012 ou Windows Server 2012 R2 (todas as edições), o Windows Server 2008 R2 ou Windows Server 2008 R2 Service Pack 1 (todas as edições), o Windows 8.1, o Windows 8 ou o Windows 7.

-   Um mínimo de 1 GB de RAM.

-   Um mínimo de 64 GB de espaço em disco.

-   Pelo menos uma interface de rede.

-   Acesso à Internet através da firewall (ou proxy Web).

Para instalar a ferramenta de administração do conector RMS, execute os seguintes ficheiros:

-   Para um computador de 32 bits: RMSConnectorAdminToolSetup_x86.exe

-   Para um computador de 64 bits: RMSConnectorSetup.exe

Se ainda não tiver transferido estes ficheiros, pode fazê-lo no [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).


## Passos seguintes
Agora que o conector RMS está instalado e configurado, está pronto para configurar os seus servidores no local para utilizá-lo. Aceda a [Configuring servers for the Azure Rights Management connector (Configurar servidores para o conector Azure Rights Management – em inglês)](configure-servers-rms-connector.md).

<!--HONumber=Apr16_HO4-->


