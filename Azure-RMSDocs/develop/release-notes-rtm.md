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

Este tópico contém informações importantes sobre esta versão e sobre versões anteriores do SDK 2.1 do RMS.

## Novidade para fevereiro de 2016 - Atualização de documentação do SDK

>[!Note]  As atualizações de documentação de recurso nesta seção aplicam-se ao download do SDK datado de 11/12/2015.

- **Fluxo de autenticação melhorado** - usando a autenticação baseada em token OAuth2 por meio do [ADAL (Azure Active Directory Authentication Library)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/). Para obter mais informações sobre esse processo e as extensões de API para ele, consulte [Autenticação ADAL para aplicativo habilitado para RMS](https://msdn.microsoft.com/en-us/library/windows/desktop/mt661865(v=vs.85).aspx).
- **Atualizar para o ADAL** - Ao atualizar seu aplicativo para usar a autenticação ADAL em vez do Assistente de Conexão do Microsoft Online, você e seus clientes poderão:

 - Usar a autenticação multifator
 - Instalar o cliente do RMS 2.1 sem exigir privilégios administrativos no computador
 - Certificar o aplicativo para o Windows 10

- **O suporte para o SIA (Assistente de Conexão) do Microsoft Online com RMS SDK está sendo removido.** Continuaremos a dar suporte ao uso do SIA por 6 meses, após o qual suporte vai parar.


## Atualização de dezembro de 2015

-   Implementação de aprimoramentos no desempenho em várias áreas, incluindo:

    Publicação do servidor primário de licenciamento ao usar servidores somente para licenciamento.

    O SDK 2.1 do RMS falha com mais rapidez quando não há conexão de rede.

-   Muitas atualizações para melhorar a experiência com mensagens de erro e com a solução de problemas.
-   Observe também que a listagem de [plataformas com suporte](supported-platforms.md) foi atualizada.

## Atualização de maio de 2015

-   **Aplicativos de serviço e RMS baseado em nuvem** - [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) precisam de três informações; chave simétrica **AppPrincipalId** e **TenantBposId**. O tópico sobre isso foi atualizado para fornecer orientações sobre como processar a aquisição dessas informações. Para essa atualização, consulte a versão atualizada de [Permitir que o aplicativo de serviço funcione com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Atualização de abril de 2015

-   Agora, o **rastreamento de documentos** é possível por meio de um conjunto de novas APIs. Para saber mais, confira [Acompanhando conteúdo](tracking-content.md)..
-   **Tipo de criptografia** - Agora, oferecemos suporte ao controle de nível de API para seleção do pacote de criptografia. Para saber mais, confira [Trabalhando com criptografia](working-with-encryption.md)..

    **Observação** Não exporemos mais o sinalizador **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** em nossa API. Isso significa que aplicativos futuros não serão mais compilados se fizerem referência a esse sinalizador, mas os aplicativos já compilados continuarão a funcionar, já que respeitaremos o sinalizador de forma privada no código da API. Ainda é possível obter o benefício do sinalizador de algoritmos de criptografia antigo preterido simplesmente alterando um sinalizador. Para saber mais, confira [Trabalhando com criptografia](working-with-encryption.md)..

     

-   **Aplicativos de modo de servidor**, aqueles que usarem um [**valor de modo de API**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER) de **IPC\_API\_MODE\_SERVER**, não exigirão um manifesto de aplicativo. Você pode testar o aplicativo em um servidor de produção RMS e não precisa obter uma licença de produção ao alternar para o ambiente de produção. Para saber mais sobre aplicativos no modo de servidor, confira [Tipos de Aplicativo](application-types.md)..
-   Agora, o **registro em log** é implementado por meio do arquivo e por métodos de Rastreamento de Eventos para Windows.
-   Se você estiver executando em uma **máquina com Windows 7 SP1 ou Windows Server 2008 R2**, confira a observação logo após "Observações importantes para o desenvolvedor".

## Atualização de janeiro de 2015

-   **Aumento do tamanho de arquivo protegido (pfile) com suporte** - Agora, há suporte para pfiles maiores do que um gigabyte (1 GB). Para saber mais sobre pfiles, confira [Formatos de arquivo de suporte](supported-file-formats.md).
-   **Registro em log aprimorado para diagnósticos mais precisos** - Os níveis de registro em log mostrarão **ERRO** ou **AVISO** para mensagens que devem ser revisadas. Todas as outras mensagens, incluindo exceções que ainda são exibidas, serão registradas em log como **INFORMAÇÕES**.

    Escolhemos essa abordagem para que você não perca quaisquer detalhes. Agora, apenas as mensagens importantes são mostradas com o nível AVISO.

-   **Aquisição de modelos de empresa** – Correções consideráveis no código de aquisição de modelo, com base nos comentários e relatórios do cliente.
-   Consistência de localização aprimorada

## Atualização de outubro de 2014

-   Os comportamentos padrão para o componente de API do arquivo do SDK foram atualizados. Para saber mais, confira [Configuração de API do arquivo](file-api-configuration.md)..
-   A notificação por email, um novo recurso, está descrita no tópico Notas do desenvolvedor, [Habilitando notificação por email](how-to-enable-email-notification.md).

## Atualização de julho de 2014

Os componentes da API do arquivo do SDK foram ampliados e oferecem os seguintes recursos:

-   Identificação de qual protetor usar.
-   Proteção RMS no nível de granularidade de um arquivo.

    Funções adicionadas nesta versão:

    **Observação** O suporte a outras estruturas e tipos de dados, não listados aqui, foi adicionado para as extensões da API do arquivo. Todos os tópicos atualizados para esta versão estão marcados como **preliminares e sujeitos a alterações**.

     

    -   [**IpcfOpenFileOnHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonhandle)
    -   [**IpcfOpenFileOnILockBytes**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonilockbytes)
    -   [**IpcfGetFileProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetfileproperty)
    -   [**IpcfLogicalFileRangeToRawFileRange**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcflogicalfilerangetorawfilerange)
    -   [**IpcfReadFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfreadfile)
    -   [**IpcfSetEndOfFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfsetendoffile)
    -   [**IpcfWriteFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfwritefile)

## Atualização de abril de 2014

-   **O uso de memória da API do arquivo**, especialmente para PFiles grandes, foi consideravelmente aprimorado.
-   **A ID de conteúdo** agora pode gravável por meio da propriedade **IPC\_LI\_CONTENT\_ID**. Para saber mais, consulte [**Tipos de propriedade da licença**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA).
-   **Requisito de manifesto de produção** - Quando seu aplicativo/serviço habilitados para RMS estiver sendo executado no modo de servidor, não exigiremos mais um manifesto. Para saber mais, confira [Tipos de aplicativo](application-types.md)..
-   **Atualizações da documentação**

    Uso de **instruções** - [reorganizado](how-to-use-msipc.md) para esclarecer a ordem das etapas para a configuração do ambiente e teste do aplicativo.

    **Prática recomendada para testes** - Adição de orientação sobre o uso do servidor local antes de testar com o Azure RMS. Para obter mais informações, consulte [Habilitar seu aplicativo de serviço para funcionar com o RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

## Notas importantes para o desenvolvedor

-   **Suporte nativo para todos os tipos de arquivo**

    O suporte nativo pode ser adicionado para qualquer tipo de arquivo (extensão) com esta versão do Rights Management Services SDK 2.1. Por exemplo, para qualquer extensão &lt;ext&gt; (não office e pdf), \*.p&lt;ext&gt; \*.p&lt;ext&gt; será usado se a configuração de administração para essa extensão for "NATIVA".

    Para saber mais sobre os tipos de arquivo com suporte, consulte [Configuração da API do arquivo](file-api-configuration.md).

-   **Computadores com Windows 7 SP1 e Windows Server 2008 R2 SP1** sem a atualização, [KB2533623](https://support.microsoft.com/en-us/kb/2533623), podem apresentar o seguinte erro ao proteger qualquer arquivo do Office: "O parâmetro está incorreto. Código do erro 0x80070057". Se você vir isso, instale a atualização e tente novamente. Se você ainda tiver problemas, entre em contato com o alias de Feedback Beta do RMS SDK <rmcstbeta@microsoft.com>..

    **Observação** Desde a versão de abril de 2015, foi adicionada uma verificação ao processo de instalação deste KB.

     

-   **Integração da API do arquivo**

    A API do arquivo do Active Directory Rights Management Services, com a adição da API do arquivo, fornece os seguintes benefícios e recursos.

    Você pode proteger os dados confidenciais de uma maneira automatizada sem precisar saber os detalhes da implementação do IRM (Gerenciamento de Direitos de Informação) usado por vários formatos de arquivo.

    Os arquivos do Microsoft Office, os arquivos PDF (Portable Document Format) e outros tipos de arquivo selecionados podem ser protegidos usando a proteção nativa. Para obter uma lista completa dos tipos de arquivo que podem ser protegidos com proteção nativa, confira [Configuração da API do arquivo](file-api-configuration.md).

    Todos os arquivos, exceto arquivos do sistema e arquivos do Office, podem ser protegidos usando o formato PFile (Arquivo Protegido por RMS).

-   **Problema**: durante a criação de uma licença do zero, os direitos de propriedade devem ser concedidos explicitamente.

    **Solução**: seu aplicativo deve adicionar de forma explícita direitos de **Proprietário** ao proprietário da licença durante a criação de uma licença do zero usando [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch). Para saber mais, confira [Adicionar direitos de proprietário explícitos](add-explicit-owner-rights.md).

-   **Problema**: se um aplicativo chamar [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) ou [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow) duas vezes para a mesma janela usando seu identificador, o RMS SDK 2.1 retornará uma falha no **HRESULT**..

    **Solução**: para obter orientações específicas sobre isso, consulte a seção Comentários no [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) e no [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow).

-   **Problema**: ao compilar para várias arquiteturas, use este guia.

    **Solução**: se você quiser usar o Ipcsecproc\*isv.dll para uma arquitetura diferente (por exemplo, se você tiver instalado o SDK de 64 bits em um computador de 64 bits, mas agora deseja implantar em um computador de 32 bits que exige o Ipcsecproc\*isv.dll), será necessário instalar o SDK de 32 bits em um computador diferente e copiar os arquivos de Ipcsecproc\*isv.dll nesse local a partir da pasta "%PROGRAMFILES%\\Microsoft Information Protection And Control" (o local padrão ou onde quer que você escolha instalar o SDK).

## Perguntas frequentes

**P**: Como funciona o comportamento da linguagem padrão com funções que usam um parâmetro LCID?

**R**: Use 0 para a localidade padrão. Nesse caso, o AD RMS Client 2.1 procura nomes e descrições na sequência a seguir e recupera o primeira disponível:

1 - LCID de preferência do usuário.
2 - LCID de localidade do sistema.
3 - O primeiro idioma disponível especificado no modelo do RMS (Rights Management Server).
Se não for possível recuperar nenhum nome e descrição, um erro retornará. Pode haver apenas um nome e uma descrição para um LCID específico.

## Tópicos relacionados

* [Visão geral](ad-rms-overview.md)
* [Adicionar direitos de proprietário explícitos](add-explicit-owner-rights.md)
* [Configuração da API do arquivo](file-api-configuration.md)
* [**IpcfGetSerializedLicenseFromFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile)
* [**IpcfEncryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfIsFileEncrypted**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow)
* [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow)
 

 


<!--HONumber=May16_HO1-->


