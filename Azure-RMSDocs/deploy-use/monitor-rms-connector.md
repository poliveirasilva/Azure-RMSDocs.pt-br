---
title: Monitorar o conector do Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 04fbac4389671ed32f64c0840d81723f8314869c
ms.openlocfilehash: 4509126c61c4e37d9655d9bd080be3e097cd103f


---

# Monitorar o conector do Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Depois de instalar e configurar o conector RMS, você pode usar os métodos e as informações a seguir para ajudá-lo a monitorar o conector e o uso do Azure RMS pela sua organização.

## Entradas de log de eventos do aplicativo

O conector RMS usa o log de eventos do aplicativo para registrar entradas para o **conector Microsoft RMS**. 

Por exemplo, eventos de Informações, como ID 1000, confirmam que o serviço do conector foi iniciado, ID 1002 quando um servidor conecta-se com êxito ao conector RMS e ID 1004 sempre que a lista de contas autorizadas (cada conta é listada) é baixada para o conector. 

Se você não tiver configurado o conector para usar HTTPS, espere ver um Aviso ID 2002 dizendo que um cliente está usando uma conexão (HTTP) não segura.

Se a conexão do conector ao Azure RMS falhar, você provavelmente verá o Erro 3001. Por exemplo, isso pode ser o resultado de um problema de DNS ou da falta de acesso à Internet para um ou mais servidores que estão executando o conector RMS. 

> [!TIP]
> Quando servidores de conector RMS não conseguem se conectar ao Azure RMS, o motivo costuma ser as configurações de proxy Web.

Como acontece com todas as entradas de log de eventos, analise a mensagem para obter mais detalhes.

Além de verificar o log de eventos ao implantar o conector pela primeira vez, verifique se há avisos e erros de maneira contínua. Por exemplo, o conector pode estar funcionando conforme o esperado inicialmente, mas outros administradores podem alterar configurações dependentes. Por exemplo, outro administrador altera a configuração do servidor proxy Web de modo que os servidores do conector RMS não conseguem mais acessar a Internet (Erro 3001) ou remove uma conta de computador de um grupo que você especificou como autorizado a usar o conector (Aviso 2001).

### IDs e descrições do log do evento

Use as seções a seguir para identificar as possíveis IDs, descrições e informações adicionais do evento.

-----

Informação **1000**

**O serviço Web do conector Microsoft RMS foi iniciado.**

Esse evento é registrado quando o conector RMS tenta iniciar pela primeira vez.

----

Informação **1001**

**O serviço Web do conector Microsoft RMS foi interrompido.**

Esse evento é registrado quando o conector RMS é interrompido em decorrência de uma operação normal. Por exemplo, o IIS foi reiniciado ou o computador foi desligado. 

----

Informação **1002**

**O acesso ao conector Microsoft RMS foi permitido por um servidor autorizado.**

Esse evento é registrado quando uma conta de um servidor local se conecta pela primeira vez ao conector RMS, depois que a conta tiver sido autorizada pelo administrador do Azure RMS na ferramenta do administrador do conector RMS. O SID, nome da conta e o nome do computador que compõe a conexão está contido na mensagem do evento.

----

Informação **1003**

**A conexão do cliente listado abaixo foi alternada de uma conexão não segura (HTTP) para uma conexão segura (HTTPS).**

Esse evento é registrado quando um servidor local tem sua conexão com o conector RMS alterada de HTTP (menos seguro) para HTTPS (mais seguro). O SID, nome da conta e o nome do computador que compõe a conexão está contido na mensagem do evento.

----

Informação **1004**

**A lista de contas autorizadas foi atualizada.**

Esse evento é registrado quando o conector RMS tiver baixado a lista mais recente de contas (contas existentes e quaisquer alterações) que estão autorizadas a usar o conector RMS. Essa lista é baixada a cada quinze minutos, contanto que o conector RMS consiga se comunicar com o Azure RMS.

----

Aviso **2000**

**A entidade de usuário no contexto HTTP está ausente ou é inválida. Verifique se o site do conector Microsoft RMS está com a autenticação anônima desabilitada no IIS e está somente com a autenticação do Windows habilitada.**

Esse evento é registrado quando o conector RMS não pode identificar exclusivamente a conta que está tentando se conectar ao conector RMS. Isso pode ser resultado de autenticação anônima configurada incorretamente para o IIS ou a conta é de uma floresta não confiável.

----

Aviso **2001**

**Tentativa de acesso não autorizado ao conector do Microsoft RMS.**

Esse evento é registrado quando uma conta tenta se conectar ao conector RMS, mas falha. O motivo mais comum para isso é porque a conta que faz a conexão não está na lista baixada de contas autorizadas que o conector RMS baixa do Azure RMS.  Por exemplo, a lista mais recente ainda não foi baixada (isso ocorre a cada 15 minutos) ou a conta está ausente na lista. 

Outra razão pode ser se você instalou o conector RMS no mesmo servidor configurado para usar o conector. Por exemplo, você instala o conector RMS em um servidor que executa o Exchange Server e autoriza uma conta do Exchange a usar o conector. Essa configuração não tem suporte, porque o conector RMS não pode identificar corretamente a conta quando ele tenta se conectar.

A mensagem do evento contém informações sobre a conta e o computador que está tentando se conectar ao conector RMS:

- Se a conta que está tentando se conectar ao conector RMS for uma conta válida, use a ferramenta do administrador do conector RMS para adicionar a conta à lista de contas autorizadas. Para obter mais informações sobre quais contas devem ser autorizadas, consulte [Adicionar um servidor à lista de servidores permitidos](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers). 

- Se a conta que está tentando se conectar ao conector RMS for do mesmo computador que o servidor do conector RMS, instale o conector em um servidor separado. Para obter mais informações sobre os pré-requisitos para o conector, consulte [Pré-requisitos para o conector RMS]( deploy-rms-connector.md#prerequisites-for-the-rms-connector).

----

Aviso **2002**

**A conexão do cliente listada abaixo está usando uma conexão não segura (HTTP).**

Esse evento é registrado quando um servidor local faz uma conexão bem-sucedida com o conector RMS, mas a conexão usa HTTP (menos seguro) em vez de HTTPS (mais seguro). Um evento é registrado por conta, e não por conexão. Esse evento é acionado novamente se a conta foi alternada com êxito para usar HTTPS, mas reverte para HTTP.

A mensagem de evento contém o SID da conta, nome da conta e o nome do computador que faz a conexão com o conector RMS.

Para obter informações sobre como configurar o conector RMS para conexões HTTPS, consulte [Configurando o conector RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https).

----

Aviso **2003**

**A lista de autorizações está vazia. O serviço não será utilizável até que a lista de usuários e grupos autorizados para o conector seja preenchida.**

Esse evento é registrado quando o conector RMS não tem uma lista de contas autorizadas, portanto, nenhum servidor local pode se conectar a ele. O conector RMS baixa a lista a cada 15 minutos do Azure RMS. 

Para especificar as contas, use a ferramenta de administrador do conector RMS. Para obter mais informações, consulte [Autorizando servidores para usar o conector RMS]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

----

Erro **3000**

**Ocorreu uma exceção sem tratamento no conector do Microsoft RMS.**

Esse evento é registrado cada vez que o conector RMS encontrar um erro inesperado, com os detalhes do erro na mensagem do evento.

----

Erro **3001**

**Ocorreu uma exceção durante o download de informações de autorização.**

Esse evento será registrado se o conector RMS não puder baixar a mais recente lista de contas com autorização para usar o conector RMS com os detalhes do erro na mensagem do evento.

----

## Contadores de desempenho

Quando você instala o conector RMS, ele cria automaticamente contadores de desempenho do **conector do Microsoft Rights Management** que podem ser úteis para ajudá-lo a monitorar o desempenho do uso do Azure RMS por meio do conector. 

Por exemplo, se você enfrentar atrasos regularmente ao proteger documentos ou emails ou ao abrir documentos ou emails protegidos, os contadores de desempenho poderão ajudar a determinar se o atraso é devido ao tempo de processamento do conector, ao tempo de processamento do Azure RMS ou a atrasos na rede. Para ajudá-lo a identificar a origem do atraso, procure os contadores que incluem as contagens médias de **Tempo de Processamento do Conector**, **Tempo de Resposta do Serviço** e **Tempo de Resposta do Conector**. Por exemplo: **Tempo Médio de Resposta do Conector para Solicitação em Lote Bem-sucedida de Licenciamento**.

Se você tiver adicionado recentemente novas contas de servidor para usar o conector, um bom contador a verificar será o **Tempo desde a última atualização de política de autorização** para confirmar se o conector baixou a lista desde que você a atualizou, ou se você precisa esperar um pouco mais (até 15 minutos).

## Analisador do RMS

Você pode usar a ferramenta Analisador do Rights Management Services para ajudá-lo a monitorar a integridade do conector e identificar problemas de configuração.

Se você ainda não tiver baixado essa ferramenta, poderá fazer isso no [Centro de Download](https://www.microsoft.com/en-us/download/details.aspx?id=46437) e instalá-la em qualquer computador com acesso à Internet e que possa conectar-se ao conector RMS. Execute a ferramenta e, na página **Bem-vindo**, selecione a opção **Conector Azure RMS**.

Para obter informações e instruções adicionais, consulte o **Detalhes** e **Instruções de Instalação** na página de download.

## Logging

O log de uso ajuda a identificar quando os emails e documentos estão protegidos e consumidos. Quando isso é feito usando o conector RMS, o campo de ID de usuário nos logs contém o nome da entidade de serviço de **Aadrm_S-1-7-0** criado automaticamente para o conector RMS.

Para obter mais informações sobre registro em log de uso, consulte [Registrando em log e analisando o uso do Azure Rights Management](log-analyze-usage.md).

Se você precisar de logs mais detalhados para fins de diagnóstico, poderá usar [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) do Windows Sysinternals e habilitar o rastreamento para o conector RMS modificando o arquivo web.config para o site Padrão no IIS. Para fazer isto:

1. Localize o arquivo web.config em **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Altere a seguinte linha:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Substitua essa linha pela seguinte:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Pare e inicie o IIS para ativar o rastreamento. 

5.  Depois de capturar todos os rastreamentos necessários, reverta a linha na etapa 3 e pare e inicie o IIS novamente.




<!--HONumber=Jun16_HO4-->


