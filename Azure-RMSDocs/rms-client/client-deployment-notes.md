---
# required metadata

title: Notas de implementação do cliente do RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Notas de implementação do cliente do RMS

*Aplica-se a: Serviços do Active Directory Rights Management, Azure Rights Management, Windows 7 com SP1, Windows 8, Windows 8.1, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Vista*

A versão 2 do cliente dos Serviços de Gestão de Direitos (cliente do RMS) é também conhecida como cliente MSIPC. É o software para computadores com o Windows que comunica com os serviços do Microsoft Rights Management no local ou na nuvem, para ajudar a proteger o acesso e a utilização de informações que fluem através de aplicações e dispositivos, dentro dos limites da sua organização ou fora desses limites geridos. Além de ser fornecido com a [aplicação de partilha Rights Management para Windows](sharing-app-windows.md), o cliente do RMS está disponível [como uma transferência opcional](http://www.microsoft.com/download/details.aspx?id=38396) que pode, com a confirmação e a aceitação do respetivo contrato de licença, ser livremente distribuída com software de terceiros para que os clientes possam proteger e consumir conteúdos protegidos por serviços Rights Management.


## Redistribuir o cliente do RMS
O cliente do RMS pode ser livremente redistribuído e incluído com outras aplicações e soluções de TI. Se for programador de aplicações ou fornecedor de soluções e quiser redistribuir o cliente do RMS, tem duas opções:

-   Recomendado: incorporar o instalador do cliente do RMS na instalação da aplicação e executá-lo no modo silencioso (o parâmetro **/quiet**, detalhado na secção seguinte).

-   Tornar o cliente do RMS um pré-requisito da sua aplicação. Com esta opção, poderá ser necessário fornecer aos utilizadores instruções adicionais para que obtenham, instalem e atualizem os seus computadores com o cliente, para poderem utilizar a aplicação.

## Instalar o cliente do RMS
O cliente do RMS está contido num ficheiro executável do instalador denominado **setup_msipc_***<arch>***.exe**, em que *<arch>* corresponde à versão **x86** (computadores cliente de 32 bits) ou **x64** (computadores cliente de 64 bits). O pacote do instalador de 64 bits (x64) instala um executável de 32 bits, para compatibilidade com aplicações de 32 bits executadas numa instalação de sistema operativo de 64 bits, e um executável de 64 bits, para suportar aplicações de 64 bits nativas. O instalador de 32 bits (x86) não irá funcionar numa instalação do Windows de 64 bits.

> [!NOTE] São necessários privilégios elevados para instalar o cliente do RMS, por exemplo enquanto membro do grupo Administradores no computador local.

Pode instalar o cliente do RMS através de um dos seguintes métodos de instalação:

-   **Modo silencioso.** Ao utilizar o parâmetro **/quiet** como parte das opções da linha de comandos, pode instalar silenciosamente o cliente do RMS nos computadores. O exemplo seguinte mostra uma instalação do cliente do RMS no modo silencioso, num computador cliente de 64 bits:

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **Modo interativo.** Em alternativa, pode instalar o cliente do RMS através do programa de configuração baseado na GUI, fornecido pelo Assistente de Instalação do Cliente do RMS. Para tal, faça duplo clique no pacote de instalador do cliente do RMS (**setup_msipc_***<arch>***.exe**) na pasta para a qual foi copiado ou transferido no computador local.

## Perguntas e respostas sobre o cliente do RMS
A secção seguinte contém as perguntas mais frequentes sobre o cliente do RMS e as respostas às mesmas.

### Que sistemas operativos suportam o cliente do RMS?
O cliente do RMS é suportado nos seguintes sistemas operativos:

|Sistema Operativo Windows Server|Sistema Operativo Windows Client|
|-----------------------------------|-----------------------------------|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 com, pelo menos, o SP1|
|Windows Server 2008 (apenas AD RMS)|Windows Vista com, pelo menos, o SP2 (apenas AD RMS)|

### Que processadores ou plataformas suportam o cliente do RMS?
O cliente do RMS é suportado nas plataformas de processamento x86 e x64.

### Onde está instalado o cliente do RMS?
Por predefinição, o cliente do RMS é instalado em %Programas%\Active Directory Rights Management Services Client 2.<minor version number>.

### Que ficheiros estão associados ao software do cliente do RMS?
Os seguintes ficheiros são instalados como parte do software do cliente do RMS:

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Além destes ficheiros, o cliente do RMS também instala ficheiros de suporte da interface de utilizador multilingues (MUI) em 44 idiomas. Para verificar os idiomas suportados, execute a instalação do cliente do RMS e, quando a instalação for concluída, consulte os conteúdos das pastas de suporte multilingue no caminho predefinido.

### O cliente do RMS está incluído por predefinição quando instalo um sistema operativo suportado?
Não. Esta versão do cliente do RMS é fornecida como uma transferência opcional que pode ser instalada separadamente em computadores com versões suportadas do sistema operativo Microsoft Windows.

### O cliente do RMS é automaticamente atualizado pelo Microsoft Update?
Se instalou o cliente do RMS através da opção de instalação silenciosa, o cliente do RMS herda as suas definições atuais do Microsoft Update. Se instalou o cliente do RMS com o programa de configuração baseado na GUI, o assistente de instalação do cliente do RMS pede para ativar o Microsoft Update.

## Definições do cliente do RMS
A secção seguinte contém informações sobre as definições do cliente do RMS. Estas informações poderão ser úteis se tiver problemas com aplicações ou serviços que utilizam o cliente do RMS.

> [!NOTE]
> Algumas definições só estão disponíveis se a aplicação otimizada para o RMS for executada como uma aplicação de modo de cliente (tal como o Microsoft Word e o Outlook ou a aplicação de partilha RMS) ou uma aplicação de modo de servidor (tal como o SharePoint e o Exchange).  Nas tabelas seguintes, estas definições são identificadas como **Modo de Cliente** e **Modo de Servidor**, respetivamente.

### Local onde o cliente do RMS armazena licenças nos computadores cliente
O cliente do RMS armazena licenças no disco local e também coloca em cache algumas informações no registo do Windows.

|Descrição|Caminhos do Modo de Cliente|Caminhos do Modo de Servidor|
|---------------|---------------------|---------------------|
|Localização do arquivo das licenças|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\*<SID>*\|
|Localização do arquivo dos modelos|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\Templates\*<SID>*\|
|Localização do Registo|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*<SID>*|
> [!NOTE]
> *<SID>* é o identificador de segurança (SID) da conta na qual a aplicação de servidor está a ser executada. Por exemplo, se a aplicação estiver a ser executada na conta de Serviço de Rede incorporada, substitua *<SID>* pelo valor do SID já conhecido dessa conta (S–1–5–20).

### Definições do registo do Windows para o cliente do RMS
Pode utilizar as chaves do registo do Windows para definir ou modificar algumas configurações do cliente do RMS. Por exemplo, enquanto administrador de aplicações otimizadas para o RMS que comunicam com servidores do AD RMS, poderá querer atualizar a localização de serviço da empresa (substituir o servidor do AD RMS atualmente selecionado para publicação), dependendo da localização atual do computador cliente na topologia do Active Directory. Em alternativa, poderá querer ativar o controlo de RMS no computador cliente, para ajudar a resolver um problema com uma aplicação otimizada para o RMS. Utilize a seguinte tabela para identificar as definições do registo que podem ser alteradas para o cliente do RMS.

|Tarefa|Definições|
|--------|------------|
|Apenas AD RMS: para atualizar a localização de serviço da empresa de um computador cliente|Atualize as seguintes chaves do registo:<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />REG_SZ: default<br /><br />**Valor:**<http or https>:// *Nome_do_Cluster_do_RMS*/_wmcs/Certification<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />REG_SZ: default<br /><br />**Valor:** <http or https>:// *Nome_do_Cluster_do_RMS*/_wmcs/Licensing|
|Para ativar e desativar o rastreio|Atualize a seguinte chave do registo:<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />REG_DWORD: Trace<br /><br />**Valor:** 1 para ativar o rastreio, 0 para desativar o rastreio (predefinição)|
|Para alterar a frequência de atualização dos modelos em dias|Os seguintes valores do registo especificam a frequência de atualização dos modelos no computador do utilizador, se o valor de TemplateUpdateFrequencyInSeconds não estiver definido.  Se nenhum destes valores estiver definido, o intervalo de atualização predefinido para que as aplicações com o cliente do RMS (versão 1.0.1784.0) transfiram modelos é de 1 dia. As versões anteriores a esta têm o valor predefinido de 7 dias.<br /><br />**Modo de Cliente:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valor:** um valor inteiro que especifica o número de dias (mínimo de 1) entre transferências.<br /><br />**Modo de Servidor:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\*\<SID\>\*<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valor:** um valor inteiro que especifica o número de dias (mínimo de 1) entre transferências.|
|Para alterar a frequência de atualização dos modelos em segundos<br /><br />Importante: se esta definição for especificada, o valor de atualização dos modelos em dias será ignorado. Especifique uma das definições, não ambas.|Os seguintes valores de registo especificam a frequência de atualização dos modelos no computador do utilizador. Se este valor ou o valor para alterar a frequência em dias (TemplateUpdateFrequency) não for definido, o intervalo de atualização predefinido para que as aplicações com o cliente do RMS (versão 1.0.1784.0) transfiram modelos é de 1 dia. As versões anteriores a esta têm o valor predefinido de 7 dias.<br /><br />**Modo de Cliente:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valor:** um valor inteiro que especifica o número de segundos (mínimo de 1) entre transferências.<br /><br />**Modo de Servidor:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\*\<SID\>\*<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valor:** um valor inteiro que especifica o número de segundos (mínimo de 1) entre transferências.|
|Apenas AD RMS: para transferir modelos imediatamente no próximo pedido de publicação|No decorrer de testes e avaliações, poderá querer que o cliente do RMS transfira modelos logo que seja possível. Para o fazer, remova a seguinte chave do registo para que o cliente do RMS transfira modelos imediatamente no próximo pedido de publicação, em vez de aguardar a hora especificada pela definição do registo TemplateUpdateFrequency:<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<Nome do Servidor>\Template<br /><br />**Nota**: <Server Name> é possível ter URLs externos (corprights.contoso.com) e internos (corprights) e, por conseguinte, duas entradas diferentes.|
|Apenas AD RMS: para ativar o suporte para a autenticação federada|Se o computador do cliente do RMS estiver ligado a um cluster do AD RMS, através de uma fidedignidade federada, é necessário configurar o realm inicial da federação.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_SZ: FederationHomeRealm<br /><br />**Valor:** o valor desta entrada do registo é o identificador de recurso uniforme (URI) do serviço de federação (por exemplo, "http://TreyADFS.trey.net/adfs/services/trust").<br /><br /> **Nota**: é importante que especifique http e não https para este valor. Além disso, se a aplicação baseada em MSIPC de 32 bits estiver a ser executada numa versão de 64 bits do Windows, a localização será HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Federation. Para uma configuração de exemplo, consulte [Implementar os Serviços de Gestão de Direitos do Active Directory com os Serviços de Federação do Active Directory](https://technet.microsoft.com/library/dn758110.aspx).|
|Apenas AD RMS: para suportar servidores de federação parceiros que exigem autenticação baseada em formulários, para a introdução de dados pelo utilizador|Por predefinição, o cliente do RMS funciona em modo silencioso e não é necessária a introdução de dados pelo utilizador. No entanto, os servidores de federação parceiros poderão ser configurados para exigir a introdução de dados pelo utilizador, através, por exemplo, da autenticação baseada em formulários. Neste caso, é necessário configurar o cliente do RMS para ignorar o modo silencioso, para que o formulário de autenticação federada seja apresentado numa janela do browser e seja pedida autenticação ao utilizador.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_DWORD: EnableBrowser<br /><br />**Nota**: se o servidor de federação estiver configurado para utilizar a autenticação baseada em formulários, esta chave é necessária. Se o servidor de federação estiver configurado para utilizar a autenticação integrada do Windows, esta chave não é necessária.|
|Apenas AD RMS: para bloquear o consumo do serviço ILS|Por predefinição, o cliente do RMS ativa o consumo de conteúdos protegidos pelo serviço ILS, mas é possível configurar o cliente para bloquear este serviço ao definir a seguinte chave do registo. Se esta chave do registo estiver definida para bloquear o serviço ILS, todas as tentativas para abrir e consumir conteúdos protegidos pelo serviço ILS irão devolver o seguinte erro:<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: **DisablePassportCertification**<br /><br />**Valor:** 1 para bloquear o consumo de ILS, 0 para permitir o consumo de ILS (predefinição)|

### Gerir a distribuição de modelos para o cliente do RMS
Os modelos fazem com que seja mais fácil para os utilizadores e administradores aplicarem rapidamente a proteção da Gestão de Direitos, para que o cliente do RMS transfira automaticamente modelos dos respetivos servidores ou serviço RMS. Se colocar os modelos na seguinte localização de pasta, o cliente do RMS não irá transferir nenhum modelo a partir da localização predefinida, mas sim transferir os modelos colocados nesta pasta. O cliente do RMS poderá continuar a transferir modelos a partir de outros servidores de RMS disponíveis.

**Modo de Cliente:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Modo de Servidor:** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\\*\<SID\>\*

Ao utilizar esta pasta, não é necessária qualquer convenção de nomenclatura especial, embora os modelos devam ser emitidos pelo servidor ou serviço RMS e tenham de ter a extensão de nome de ficheiro .xml. Por exemplo, Contoso–Confidencial.xml ou Contoso–ApenasLeitura.xml são nomes válidos.

## Apenas AD RMS: limitar o cliente do RMS para utilizar servidores do AD RMS fidedignos
É possível limitar o cliente do RMS apenas à utilização de servidores do AD RMS fidedignos específicos, ao fazer as seguintes alterações no registo do Windows, nos computadores locais.

**Para limitar o cliente do RMS para utilizar apenas servidores do AD RMS fidedignos**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **Valor:** se for especificado um valor diferente de zero, o cliente do RMS irá considerar como fidedignos apenas os servidores especificados que estejam configurados na lista TrustedServers e no serviço Azure Rights Management.

**Para adicionar membros à lista de servidores do AD RMS fidedignos**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ: *<URL_ou_NomeDoAnfitrião>*

    **Valor:** os valores de cadeias adicionados a esta localização da chave do registo podem ter um formato de nome de domínio DNS (por exemplo, **adrms.contoso.com**) ou URLs completos para servidores do AD RMS fidedignos (por exemplo, **https://adrms.contoso.com**). Se um URL especificado começar por **https://**, o cliente do RMS irá utilizar SSL ou TLS para contactar o servidor do AD RMS especificado.

## Deteção do serviço RMS
A deteção do serviço RMS permite que o cliente do RMS verifique com que servidor ou serviço RMS irá comunicar antes de proteger conteúdos. A deteção do serviço também poderá ocorrer se o cliente do RMS consumir conteúdos protegidos, embora seja pouco provável, uma vez que a política associada aos conteúdos inclui o servidor ou serviço RMS preferenciais e o cliente só executará a deteção do serviço se esse procedimento não for concluído com êxito.

A deteção do serviço procura primeiro uma versão no local do Rights Management (AD RMS). Se esse procedimento não for concluído com êxito, a deteção do serviço procura automaticamente a versão na nuvem do Rights Management (Azure RMS).

Para efetuar a deteção do serviço numa implementação no local, o cliente do RMS verifica o seguinte:

1.  O registo do Windows no computador local: se as definições de deteção do serviço estiverem configuradas no registo, estas definições são experimentadas em primeiro lugar.  Por predefinição, estas definições não estão configuradas no registo.

2.  Serviços de Domínio do Active Directory: um computador associado a um domínio consulta o Active Directory para procurar um ponto de ligação de serviço (SCP). Se estiver registado um SCP, é devolvido o URL do servidor de RMS para o cliente do RMS utilizar.

### Apenas AD RMS: ativar a deteção do serviço do lado do servidor através do Active Directory
Se a sua conta tiver privilégios suficientes (Administradores da Empresa e administrador local para o servidor do AD RMS), pode registar automaticamente um ponto de ligação de serviço (SCP) quando instalar o servidor de cluster de raiz do AD RMS. Se já existir um SCP na floresta, é necessário eliminar primeiro o SCP existente para poder registar um novo.

Pode registar e eliminar um SCP após a instalação do AD RMS, através do seguinte procedimento. Antes de começar, certifique-se de que a sua conta tem os privilégios necessários (Administradores da Empresa e administrador local para o servidor do AD RMS).

#### Para ativar a deteção do serviço AD RMS ao registar um SCP no Active Directory

1.  Abra a consola dos Serviços de Gestão do Active Directory no servidor do AD RMS:

    -   Se estiver a utilizar o Windows Server 2008 R2 ou o Windows Server 2008, clique em **Iniciar**, **Ferramentas Administrativas** e em **Serviços do Active Directory Rights Management**.

    -   Se estiver a utilizar o Windows Server 2012 R2 ou o Windows Server 2012, no Gestor de Servidor, clique em **Ferramentas** e em **Serviços do Active Directory Rights Management**.

2.  Na consola do AD RMS, clique com o botão direito do rato no cluster do AD RMS e, em seguida, clique em **Propriedades**.

3.  Clique no separador **SCP**.

4.  Selecione a caixa de verificação **Alterar SCP**.

5.  Selecione a opção **Definir SCP para o cluster de certificação atual** e clique em **OK**.

### Ativar a deteção do serviço do lado do cliente através do registo do Windows
Como alternativa à utilização de um SCP, ou caso não exista um SCP, pode configurar o registo do computador cliente para que o cliente do RMS possa localizar o respetivo servidor do AD RMS.

#### Para ativar a deteção do serviço AD RMS do lado do cliente através do registo do Windows

1.  Abra o editor de registo do Windows, Regedit.exe:

    -   No computador cliente, na janela Executar, escreva **regedit** e prima Enter para abrir o Editor de Registo.

2.  No Editor de Registo, navegue até **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!IMPORTANT] Se estiver a executar uma aplicação de 32 bits num computador de 64 bits, o caminho será o seguinte: **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  Para criar a subchave ServiceLocation, clique com o botão direito do rato em **MSIPC**, aponte para **Novo**, clique em **Chave** e escreva **ServiceLocation**.

4.  Para criar a subchave EnterpriseCertification, clique com o botão direito do rato em **ServiceLocation**, aponte para **Novo**, clique em **Chave** e escreva **EnterpriseCertification**.

5.  Para definir o URL de certificação da empresa, faça duplo clique no valor **(Default)** na subchave **EnterpriseCertification** e, quando a caixa de diálogo **Editar Cadeia** for apresentada, para **Dados do valor**, escreva <http or https>://*nome_do_cluster_do_AD RMS*/_wmcs/Certification e, em seguida, clique em **OK**.

6.  Para criar a subchave EnterprisePublishing, clique com o botão direito do rato em **ServiceLocation**, aponte para **Novo**, clique em **Chave** e escreva EnterprisePublishing.

7.  Para definir o URL de publicação da empresa, faça duplo clique em **(Default)** na subchave **EnterprisePublishing** e, quando a caixa de diálogo **Editar Cadeia** for apresentada, para **Dados do valor**, escreva o seguinte <http or https>://*nome_do_cluster_do_AD RMS*/_wmcs/Licensing e, em seguida, clique em **OK**.

8.  Feche o Editor de Registo.

Se o cliente do RMS não conseguir encontrar um SCP através da consulta do Active Directory e não estiver especificado um no registo, as chamadas de deteção do serviço para o AD RMS irão falhar.

### Redirecionar o tráfego do servidor de licenciamento
Em alguns casos, poderá ser necessário redirecionar o tráfego durante a deteção do serviço quando, por exemplo, duas organizações são fundidas e o servidor de licenciamento antigo numa organização é extinto, fazendo com que os clientes tenham de ser redirecionados para um novo servidor de licenciamento. Em alternativa, pode efetuar a migração do AD RMS para o Azure RMS. Para ativar o redirecionamento do licenciamento, utilize o seguinte procedimento.

#### Para ativar o redirecionamento do licenciamento do RMS através do registo do Windows

1.  Abra o editor de registo do Windows, Regedit.exe:

    -   No computador cliente, na janela Executar, escreva **regedit** e prima Enter para abrir o Editor de Registo.

2.  No Editor de Registo, navegue até um dos seguintes caminhos:

    -   Para a versão de 64 bits do Office numa plataforma x64: HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   Para a versão de 32 bits do Office numa plataforma x64: HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Para criar uma subchave LicensingRedirection, clique com o botão direito do rato em **Servicelocation**, aponte para **Novo**, clique em **Chave** e escreva **LicensingRedirection**.

4.  Para definir o redirecionamento do licenciamento, clique com o botão direito do rato na subchave **LicensingRedirection**, selecione **Novo** e selecione **Valor de cadeia**.  Para **Nome**, especifique o URL de licenciamento do servidor anterior e, para **Valor**, especifique o URL de licenciamento do servidor novo.

    Por exemplo, para redirecionar o licenciamento de um servidor em Contoso.com para outro em Fabrikam.com, poderá introduzir os seguintes valores:

    **Nome:** https://contoso.com/_wmcs/licensing

    **Valor:** https://fabrikam.com/_wmcs/licensing

    > [!NOTE] Se o servidor de licenciamento antigo tiver URLs da intranet e da extranet, especifique um novo nome e defina o mapeamento de valores para os dois URLs na chave LicensingRedirection.

5.  Repita o passo anterior para todos os servidores que precisem de ser redirecionados.

6.  Feche o Editor de Registo.



<!--HONumber=May16_HO3-->


