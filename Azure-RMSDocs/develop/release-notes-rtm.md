---
# required metadata

title: Notas de versão | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 05/03/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Notas de versão

Este tópico contém informações importantes sobre isto e sobre versões anteriores do SDK RMS 2.1.

## Novo na atualização da documentação do SDK de fevereiro de 2016

>[!Note]  As atualizações da documentação da funcionalidade nesta secção aplicam-se à transferência do SDK com a data de 11/12/2015.

- **Fluxo de autenticação melhorado** – utilizar a autenticação com base no token OAuth2 através da [Azure Active Directory Authentication Library (ADAL)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/). Para mais informações sobre este processo e as extensões da API para o mesmo, consulte [Autenticação ADAL para a aplicação com permissão para RMS](how-to-use-adal-authentication.md).

- **Atualizar para a ADAL** – ao atualizar a sua aplicação para utilizar a autenticação ADAL em vez do Assistente de Início de Sessão Online da Microsoft, o utilizador e os seus clientes poderão:

 - Utilizar a autenticação multifator
 - Instalar o cliente RMS 2.1 sem necessidade de privilégios administrativos no computador
 - Certificar a aplicação para o Windows 10

- **O suporte para o Assistente de Início de Sessão Online da Microsoft (SIA) com o SDK RMS está a ser removido.** Vamos continuar a suportar a utilização do SIA durante 6 meses, terminando o suporte após esse período.


## Atualização de dezembro de 2015

- As melhorias de desempenho têm sido implementadas em várias áreas, incluindo:
    - A publicação a partir do servidor de licenciamento principal quando utilizar servidores só de licenciamento.
    - O SDK RMS 2.1 falha mais rapidamente quando não existe qualquer ligação de rede.

- Muitas atualizações para melhorar a experiência de resolução de problemas e de mensagens de erro.
- Note também que a lista das [Plataformas suportadas](supported-platforms.md) também está atualizada.
- A necessidade para o ambiente de pré-produção e a utilização de manifestos de aplicação foi removida a partir do SDK RMS 2.1. Estas secções deste conjunto de documentação para programadores foram removidas e a documentação geral simplificada e reorganizada.

## Atualização de maio de 2015

-   **Aplicações do serviço e RMS baseado na nuvem** - [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) precisa de três tipos de informações: a chave simétrica, **AppPrincipalId** e **TenantBposId**. O tópico relativo a isto foi atualizado para fornecer orientações sobre o processamento destas informações de aquisição. Para esta atualização, consulte a versão atualizada de [Permitir que a aplicação do serviço funcione com o RMS baseado na nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Atualização de abril de 2015

-   O **controlo de documentos** é agora possível através de um conjunto de APIs novas. Para mais informações, consulte [Controlar Conteúdo](tracking-content.md).
-   **Tipo de encriptação** – agora suportamos o controlo de nível da API para a seleção do pacote de encriptação. Para mais informações, consulte [Trabalhar com a encriptação](working-with-encryption.md).

    **Nota** Já não expomos o sinalizador **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** na nossa API. Isto significa que as aplicações futuras vão deixar de compilar se fizerem referência a este sinalizador, mas as aplicações já criadas vão continuar a funcionar, uma vez que respeitamos o sinalizador em privado no código da API. Para aproveitar ainda as vantagens do sinalizador de algoritmos de encriptação preterido antigo, basta alterar um sinalizador. Para mais informações, consulte [Trabalhar com a encriptação](working-with-encryption.md).

-   **Aplicações de Modo de Servidor**, quem utilizar um [**Valor de modo de API**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER) de **IPC\_API\_MODE\_SERVER**, já não necessita de um manifesto da aplicação. Pode testar a aplicação relativamente a um servidor RMS de produção e não é necessário obter uma licença de produção quando mudar para um ambiente de produção. Para obter mais informações sobre as aplicações do modo de servidor, consulte [Tipos de aplicação](application-types.md).
-   O **registo** é agora implementado através dos métodos Rastreio de Eventos e ficheiros do Windows.
-   Se estiver a utilizar um **computador Windows 7 SP1 ou Windows Server 2008 R2**, consulte a nota em “Notas importantes do programador” a seguir.

## Atualização de janeiro de 2015

-   **Aumento do tamanho do ficheiro protegido (pfile)** – agora suporta tamanhos de pfile maiores do que um gigabyte (1 GB). Para mais informações sobre pfiles, consulte [Formatos de Ficheiro Suportados](supported-file-formats.md).
-   **Registo melhorado para um melhor diagnóstico** –os níveis de registo apresentarão um **ERRO** ou **AVISO** nas mensagens que devem ser revistas. Todas as outras mensagens, incluindo as exceções que ainda são apresentadas, serão registadas como **INFORMAÇÕES**.

    Escolhemos esta abordagem para nenhum detalhe seja perdido. Agora, apenas as mensagens importantes são apresentadas com o nível de AVISO.

-   **Adquirir modelos da Empresa** – correções substanciais no código de aquisição de modelos, com base em relatórios de cliente e comentários.
-   Consistência de localização melhorada

## Atualização de outubro de 2014

-   Foram atualizados os comportamentos predefinidos do componente da API de Ficheiros do SDK. Para mais informações, consulte [Configuração da API de Ficheiros](file-api-configuration.md).
-   A nova funcionalidade de notificação por e-mail é descrita no tópico Notas do programador, [Permitir notificação por e-mail](how-to-enable-email-notification.md).

## Atualização de julho de 2014

Os componentes da API de Ficheiros do SDK foram expandidos e oferecem as seguintes funcionalidades:

-   Identifica o protetor a utilizar.
-   Fornece a proteção do RMS ao nível de granularidade de um ficheiro.

    Funções adicionadas a esta versão:

    **Nota** Foram adicionadas estruturas e tipos de dados de suporte, não listados aqui, às extensões da API de Ficheiros. Todos os tópicos atualizados nesta versão estão marcados como **preliminares e estão sujeitos a alterações**.

    -   [**IpcfOpenFileOnHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonhandle)
    -   [**IpcfOpenFileOnILockBytes**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonilockbytes)
    -   [**IpcfGetFileProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetfileproperty)
    -   [**IpcfLogicalFileRangeToRawFileRange**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcflogicalfilerangetorawfilerange)
    -   [**IpcfReadFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfreadfile)
    -   [**IpcfSetEndOfFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfsetendoffile)
    -   [**IpcfWriteFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfwritefile)

## Atualização de abril de 2014

-   A **utilização da memória da API de Ficheiros**, especialmente para PFiles grandes, foi significativamente melhorada.
-   O **ID de conteúdo** agora é gravável através da propriedade **IPC\_LI\_CONTENT\_ID**. Para mais informações, consulte [**Tipos de propriedade de licença**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA).
-   **Requisito de manifesto de produção** – quando o serviço/aplicação com suporte RMS está a ser executado no modo de servidor, deixará de ser necessário um manifesto. Para mais informações, consulte [Tipos de aplicações](application-types.md).
-   **Atualizações da documentação**

    **Testar a melhor prática** – orientações adicionadas para a utilização do servidor no local antes de testar com o Azure RMS. Para mais informações, consulte [Permitir que a aplicação do serviço funcione com o RMS baseado na nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Notas importantes do programador

-   **Suporte nativo para todos os tipos de ficheiro**

    É possível adicionar suporte nativo para qualquer tipo de ficheiro (extensão) com esta versão do SDK Rights Management Services 2.1. Por exemplo, para qualquer extensão &lt;ext&gt; (não Office e pdf), \*.p&lt;ext&gt; será utilizado se a configuração de administração para essa extensão for “NATIVO”.

    Para mais informações sobre tipos de ficheiro suportados, consulte [Configuração da API de Ficheiros](file-api-configuration.md).

-   Os **computadores Windows 7 SP1 e Windows Server 2008 R2 SP1** sem a atualização [KB2533623](https://support.microsoft.com/en-us/kb/2533623) poderão apresentar o seguinte erro ao proteger um ficheiro do Office: “O parâmetro está incorreto. Código de erro 0x80070057”. Se vir isto, instale a atualização e tente novamente. Se os problemas persistirem, contacte o alias de Comentários Beta do SDK RMS <rmcstbeta@microsoft.com>.

    **Nota** Na versão de abril de 2015, foi adicionada uma verificação ao processo de instalação deste KB.

     

-   **Integração da API de Ficheiros**

    A API de Ficheiros dos Serviços de Gestão de Direitos do Active Directory, com a adição da API de Ficheiros, fornece as seguintes vantagens e capacidades.

      - Pode proteger dados confidenciais de uma forma automática sem necessitar de saber os detalhes sobre a implementação da Gestão de Direitos de Informação (IRM) utilizada por vários formatos de ficheiro.

      - É possível proteger ficheiros do Microsoft Office, Portable Document Format (PDF) e outros tipos de ficheiros selecionados através da proteção nativa. Para obter uma lista completa dos tipos de ficheiro que podem ser protegidos com a proteção nativa, consulte [Configuração da API de Ficheiros](file-api-configuration.md).

      - Todos os ficheiros, exceto ficheiros do sistema e ficheiros do Office, podem ser protegidos através do formato de Ficheiro Protegido (PFile) do RMS.

    A API de ficheiro é implementada através das seguintes quatro novas funções: [IpcfDecryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile), [IpcfEncryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile), [IpcfGetSerializedLicenseFromFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile) e [IpcfIsFileEncrypted](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted).

    A API de Ficheiro necessita que o Rights Management Service Client 2.1 seja instalado no computador cliente e que o computador tenha conectividade com um servidor RMS. Para obter mais informações sobre o servidor RMS, o cliente RMS e a respetiva funcionalidade, consulte o conteúdo do TechNet relativo à [Documentação do RMS para Profissionais de TI](https://technet.microsoft.com/en-us/library/cc771234(v=ws.10).aspx).

-   **Problema**: ao criar uma licença do zero, os direitos de propriedade têm de ser concedidos explicitamente.

    **Solução**: a aplicação tem de adicionar explicitamente direitos de **Proprietário** ao proprietário da licença ao criar uma licença do zero através de [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch). Para mais informações, consulte [Adicionar direitos de proprietário explícitos](add-explicit-owner-rights.md).

-   **Problema**: se uma aplicação chamar [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) ou [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow) duas vezes para a mesma janela utilizando o respetivo identificador, o SDK RMS 2.1 devolve uma falha no **HRESULT**.

    **Solução**: para obter instruções específicas sobre isto, consulte a secção Observações em [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) e [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow).

-   **Problema**: ao criar para várias arquiteturas, tem de utilizar esta orientação.

    **Solução**: se pretender utilizar o Ipcsecproc\*isv.dll para uma arquitetura diferente (por exemplo, tem instalado o SDK de 64 bits num computador de 64 bits, mas agora pretende implementar num computador de 32 bits que requer o Ipcsecproc\*isv.dll), tem de instalar o SDK de 32 bits num computador diferente e copiar os ficheiros Ipcsecproc\*isv.dll para lá da pasta “%PROGRAMFILES%\\Microsoft Information Protection And Control” (a localização predefinida ou onde quer que opte por instalar o SDK).

## Perguntas mais frequentes

**P**: como é que o comportamento de idioma predefinido funciona com funções que assumem um parâmetro LCID?

**R**: utilize 0 para a região predefinida. Neste caso, o Cliente de AD RMS 2.1 procura nomes e descrições na seguinte sequência e obtém o primeiro disponível:

    1 - User preferred LCID.
    2 - System locale LCID.
    3 - The first available language specified in the Rights Management Server (RMS) template.

Se não for possível obter um nome e uma descrição, é devolvido um erro. Apenas pode existir um nome e descrição para um LCID específico.

## Tópicos relacionados

* [Descrição Geral](ad-rms-overview.md)
* [Adicionar direitos de proprietário explícitos](add-explicit-owner-rights.md)
* [Configuração da API de Ficheiros](file-api-configuration.md)
* [**IpcfGetSerializedLicenseFromFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile)
* [**IpcfEncryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfIsFileEncrypted**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow)
* [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow)
 

 


<!--HONumber=Jun16_HO2-->


