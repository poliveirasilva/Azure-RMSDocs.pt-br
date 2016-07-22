---
title: Monitorizar o conector Azure Rights Management | Azure RMS
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

# Monitorizar o conector Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Após ter instalado e configurado o conector RMS, pode utilizar os métodos e as informações seguintes para ajudar a monitorizar o conector e a utilização da organização do Azure RMS.

## Registo de eventos da aplicação

O conector RMS utiliza o registo de eventos de Aplicações para registar as entradas para o **conector do Microsoft RMS**. 

Por exemplo, eventos de Informação, tais como o ID 1000 confirmam que o serviço de conectores foi iniciado, o ID de 1002 quando um servidor estabelece corretamente ligação com o conector do RMS e o ID 1004 sempre que a lista de contas autorizados (cada conta é listada) é transferida para o conector. 

Se não tiver configurado o conector para utilizar HTTPS, espere ver um Aviso de ID 2002, que informa que um cliente está a utilizar uma ligação (HTTP) não segura.

Se o conector não conseguir estabelece ligação ao Azure RMS, provavelmente verá erro 3001. Por exemplo, isto poderá dever-se a um problema DNS ou à falta de acesso à Internet para um ou mais servidores que executem o conector do RMS. 

> [!TIP]
> Quando os servidores do conector do RMS não consegue ligar ao Azure RMS, as configurações de proxy Web são, muitas vezes, o motivo.

Tal como acontece com todas as entradas de registo de eventos, explore a mensagem para mais detalhes.

Para além de verificar o registo de eventos quando implementa o conector pela primeira vez, verifique a existência de avisos e de erros continuamente. Por exemplo, o conector pode funcionar como esperado inicialmente, mas outros administradores poderão alterar as configurações dependentes. Por exemplo, outro administrador altera a configuração de servidor de proxy web para que os servidores do conector RMS já não possam aceder à Internet (Erro 3001), ou remove uma conta de computador a partir de um grupo que especificou como autorizado para utilizar o conector (Aviso 2001).

### IDs e descrições do registo de eventos

Utilize as secções seguintes para identificar os IDs de eventos possíveis, as descrições e qualquer informação adicional.

-----

Informações **1000**

**O serviço Web do conector do Microsoft RMS foi iniciado.**

Este evento é registado quando o conector do RMS tenta primeiro iniciar.

----

Informações **1001**

**O serviço Web do conector do Microsoft RMS foi parado.**

Este evento é registado quando o conector do RMS para como resultado do funcionamento normal. Por exemplo, o IIS é reiniciado ou o computador é encerrado. 

----

Informações **1002**

**O acesso ao conector do Microsoft RMS foi permitido para um servidor autorizado.**

Este evento é registado quando uma conta de um servidor no local se liga ao conector do RMS pela primeira vez, depois de a conta ser autorizada pelo administrador do Azure RMS na ferramenta de administrador do conector do RMS. O SID, o nome de conta e o nome do computador que faz a ligação são incluídos na mensagem do evento.

----

Informações **1003**

**A ligação do cliente listado abaixo mudou de uma ligação de não segura (HTTP) para uma ligação segura (HTTPS).**

Este evento é registado quando um servidor no local muda a ligação do conector do RMS de HTTP (menos seguro) para HTTPS (mais seguro). O SID, o nome de conta e o nome do computador que faz a ligação são incluídos na mensagem do evento.

----

Informações **1004**

**A lista de contas autorizadas foi atualizada.**

Este evento é registado quando o conector do RMS transferiu a lista mais recente de contas (contas existentes e quaisquer alterações) que estão autorizadas a utilizar o conector do RMS. Esta lista é transferida a cada quinze minutos, desde que o conector do RMS consiga comunicar com o Azure RMS.

----

Aviso **2000**

**O principal de utilizador no contexto HTTP está em falta ou é inválido; verifique se o site do conector do Microsoft RMS tem a Autenticação Anónima desativada no IIS e apenas a Autenticação do Windows está ativada.**

Este evento é registado quando o conector do RMS não consegue identificar exclusivamente a conta que está a tentar ligar ao conector do RMS. Isto poderá ocorrer devido a uma configuração incorreta da autenticação para o IIS ou quando a conta está numa floresta não fidedigna.

----

Aviso **2001**

**Tentativa de acesso não autorizado ao conector do Microsoft RMS.**

Este evento é registado quando uma conta tenta ligar ao conector do RMS, mas falha. Normalmente, tal ocorre porque a conta que faz a ligação não está na lista transferida de contas autorizadas que o conector do RMS transfere a partir do Azure RMS.  Por exemplo, a lista mais recente ainda não foi transferida (tal ocorre a cada 15 minutos) ou a conta está em falta na lista. 

Outra razão pode indicar que o conector do RMS foi instalado no mesmo servidor configurado para utilizar o conector. Por exemplo, instala o conector do RMS num servidor que executa o Exchange Server e está a autorizar a uma conta do Exchange para utilizar o conector. Esta configuração não é suportada porque o conector do RMS não consegue identificar corretamente a conta quando tenta ligar.

A mensagem de evento contém informações sobre a conta e o computador que está a tentar ligar ao conector do RMS:

- Se a conta que está a tentar ligar ao conector do RMS for uma conta válida, utilize a ferramenta de administrador do conector do RMS para adicionar a conta à lista de contas autorizadas. Para obter mais informações sobre as contas que devem estar autorizadas, consulte [Adicionar um servidor à lista de servidores permitidos](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers). 

- Se a conta que está a tentar ligar ao conector do RMS pertencer ao mesmo computador que o servidor do conector do RMS, instale o conector num servidor separado. Para obter mais informações sobre os pré-requisitos para o conector, consulte [Pré-requisitos para o conector do RMS]( deploy-rms-connector.md#prerequisites-for-the-rms-connector).

----

Aviso **2002**

**A ligação do cliente listada abaixo está a utilizar uma ligação (HTTP) não segura.**

Este evento é registado quando um servidor no local liga com êxito ao conector do RMS, mas a ligação utiliza HTTP (menos seguro) em vez de HTTPS (mais seguro). É registado um evento por conta, em vez de por ligação. Este evento é acionado novamente se a conta mudar com êxito para utilização de HTTPS, mas reverte para HTTP.

A mensagem de evento contém a conta de SID, o nome de conta e o nome do computador liga ao conector do RMS.

Para obter informações sobre como configurar o conector do RMS para ligações HTTPS, consulte o [Configurar o conector do RMS para utilizar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https).

----

Aviso **2003**

**A lista de autorizações está vazia. O serviço só poderá ser utilizado depois de a lista de utilizadores e grupos autorizados do conector ser povoada.**

Este evento é registado quando o conector do RMS não tem uma lista de contas autorizadas, pelo que os servidores no local não podem ligar à mesma. O conector do RMS transfere a lista a cada 15 minutos a partir do Azure RMS. 

Para especificar as contas, utilize a ferramenta de administrador de conector do RMS. Para obter mais informações, consulte [Autorizar os servidores a utilizar o conector do RMS]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

----

Erro **3000**

**Ocorreu uma exceção não processada no conector do Microsoft RMS.**

Este evento é registado sempre que o conector do RMS encontra um erro inesperado com os detalhes do erro na mensagem de evento.

----

Erro **3001**

**Ocorreu uma exceção ao transferir as informações de autorização.**

Este evento é registado se o conector do RMS não conseguir a lista mais recente de contas que estão autorizadas a utilizar o conector do RMS, com os detalhes do erro na mensagem de evento.

----

## Contadores de desempenho

Ao instalar o conector RMS, este cria automaticamente um contadores de desempenho do **conector Microsoft Rights Management** que poderão ser úteis para ajudar a monitorizar o desempenho de utilização do Azure RMS através do conector. 

Por exemplo, se regularmente ocorrerem atrasos ao proteger documentos ou e-mails, ou ao abrir documentos ou e-mails protegidos, os contadores de desempenho podem ajudar a determinar se o atraso se deve ao tempo de processamento no conector, ao tempo de processamento a partir do Azure RMS ou a atrasos de rede. Para ajudar a identificar onde está a ocorrer o atraso, procure contadores que incluam contagens de média para o **Tempo de Processamento do Conector**, para o **Tempo de Resposta do Serviço**, e para o **Tempo de Resposta do Conector**. Por exemplo: **licenciamento com êxito do pedido em batch com tempo de resposta médio do conector**.

Se tiver adicionado recentemente novas contas de servidor para utilizar o conector, um com contador para verificar é o **Tempo desde a última atualização da política de autorização**, para confirmar que o conector transferiu a lista desde que a atualizou, ou se terá de aguardar um pouco mais (até 15 minutos).

## RMS Analyzer

Pode utilizar a ferramenta Rights Management Services Analyzer para ajudar a monitorizar o estado de funcionamento do conector e identificar problemas de configuração.

Se não tiver já transferido esta ferramenta, pode fazê-lo a partir do [Centro de Transferências](https://www.microsoft.com/en-us/download/details.aspx?id=46437) e, em seguida, instalá-la em qualquer computador que tenha acesso à Internet e que possa ligar ao conector RMS. Execute a ferramenta e, na página **Bem-vindo**, selecione a opção **conector Azure RMS**.

Para informação adicional e instruções, consulte os **Detalhes** e as **Instruções de Instalação** na página de transferência.

## Registo

O registo de utilização ajuda-o a identificar quando os e-mails e os documentos são protegidos e consumidos. Quando isto é feito com o conector do RMS, o campo de ID de utilizador nos registos contém o nome do principal do serviço de **Aadrm_S-1-7-0** que é criado automaticamente para o conector do RMS.

Para obter mais informações sobre o registo de utilização, consulte [Registo e análise da utilização do Azure Rights Management](log-analyze-usage.md).

Se necessitar de registos mais detalhados para fins de diagnóstico, pode utilizar a [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) a partir do Windows Sysinternals e ativar o rastreio para o conector de RMS, modificando o ficheiro web.config para o site predefinido no IIS. Para efetuar este procedimento:

1. Localize o ficheiro web.config em **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Localize a seguinte linha:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Substitua essa linha com o seguinte:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Pare e inicie o IIS para ativar o rastreio. 

5.  Quando tiver capturado os rastreios que necessita, reverta a linha do passo 3, e pare e iniciar o IIS novamente.




<!--HONumber=Jun16_HO4-->


