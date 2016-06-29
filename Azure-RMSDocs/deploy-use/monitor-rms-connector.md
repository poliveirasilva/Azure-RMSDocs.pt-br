---
# required metadata

title: Monitorizar o conector Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Monitorizar o conector Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Após ter instalado e configurado o conector RMS, pode utilizar os métodos e as informações seguintes para ajudar a monitorizar o conector e a utilização da organização do Azure RMS.

## Registo de eventos da aplicação

O conector RMS utiliza o registo de eventos de Aplicações para registar as entradas para o **conector do Microsoft RMS**. 

Por exemplo, eventos de Informação, tais como o ID 1000 confirmam que o serviço de conectores foi iniciado, o ID de 1002 quando um servidor estabelece corretamente ligação com o conector do RMS e o ID 1004 sempre que a lista de contas autorizados (cada conta é listada) é transferida para o conector. 

Se não tiver configurado o conector para utilizar HTTPS, espere ver um Aviso de ID 2002, que informa que um cliente está a utilizar uma ligação (HTTP) não segura.

Se o conector não conseguir estabelece ligação ao Azure RMS, provavelmente verá erro 3001. Por exemplo, isto poderá dever-se a um problema DNS ou à falta de acesso à Internet para um ou mais servidores que executem o conector do RMS. 

> [!TIP] Quando os servidores do conector de RMS não consegue ligar ao Azure RMS, as configurações de proxy web são, muitas vezes, o motivo.

Tal como acontece com todas as entradas de registo de eventos, explore a mensagem para mais detalhes.

Para além de verificar o registo de eventos quando implementa o conector pela primeira vez, verifique a existência de avisos e de erros continuamente. Por exemplo, o conector pode funcionar como esperado inicialmente, mas outros administradores poderão alterar as configurações dependentes. Por exemplo, outro administrador altera a configuração de servidor de proxy web para que os servidores do conector RMS já não possam aceder à Internet (Erro 3001), ou remove uma conta de computador a partir de um grupo que especificou como autorizado para utilizar o conector (Aviso 2001).

## Contadores de desempenho

Ao instalar o conector RMS, este cria automaticamente um contadores de desempenho do **conector Microsoft Rights Management** que poderão ser úteis para ajudar a monitorizar o desempenho de utilização do Azure RMS através do conector. 

Por exemplo, se regularmente ocorrerem atrasos ao proteger documentos ou e-mails, ou ao abrir documentos ou e-mails protegidos, os contadores de desempenho podem ajudar a determinar se o atraso se deve ao tempo de processamento no conector, ao tempo de processamento a partir do Azure RMS ou a atrasos de rede. Para ajudar a identificar onde está a ocorrer o atraso, procure contadores que incluam contagens de média para o **Tempo de Processamento do Conector**, para o **Tempo de Resposta do Serviço**, e para o **Tempo de Resposta do Conector**. Por exemplo: **licenciamento com êxito do pedido em batch com tempo de resposta médio do conector**.

Se tiver adicionado recentemente novas contas de servidor para utilizar o conector, um com contador para verificar é o **Tempo desde a última atualização da política de autorização**, para confirmar que o conector transferiu a lista desde que a atualizou, ou se terá de aguardar um pouco mais (até 15 minutos).

## RMS Analyzer

Pode utilizar a ferramenta Rights Management Services Analyzer para ajudar a monitorizar o estado de funcionamento do conector e identificar problemas de configuração.

Se não tiver já transferido esta ferramenta, pode fazê-lo a partir do [Centro de Transferências](https://www.microsoft.com/en-us/download/details.aspx?id=46437) e, em seguida, instalá-la em qualquer computador que tenha acesso à Internet e que possa ligar ao conector RMS. Execute a ferramenta e, na página **Bem-vindo**, selecione a opção **conector Azure RMS**.

Para informação adicional e instruções, consulte os **Detalhes** e as **Instruções de Instalação** na página de transferência.

## Registo

O registo de utilização ajuda-o a identificar quando os e-mails e os documentos são protegidos e consumidos. Quando isto é feito utilizando o conector RMS, o campo de ID de utilizador nos registos contém o nome do principal serviço que é gerado automaticamente ao instalar o conector RMS.

Para obter mais informações, consulte [Registo e análise da utilização do Azure Rights Management](log-analyze-usage.md).

Se necessitar de registos mais detalhados para fins de diagnóstico, pode utilizar a [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) a partir do Windows Sysinternals e ativar o rastreio para o conector de RMS, modificando o ficheiro web.config para o site predefinido no IIS. Para efetuar este procedimento:

1. Localize o ficheiro web.config em **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Localize a seguinte linha:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Substitua essa linha com o seguinte:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Pare e inicie o IIS para ativar o rastreio. 

5.  Quando tiver capturado os rastreios que necessita, reverta a linha do passo 3, e pare e iniciar o IIS novamente.



<!--HONumber=Jun16_HO2-->


