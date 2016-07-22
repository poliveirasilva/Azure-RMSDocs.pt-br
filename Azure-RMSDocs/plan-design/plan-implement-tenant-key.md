---
title: Planear e implementar a sua chave de inquilino do Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f01d57759ab80b4946c07a627269550c80114131
ms.openlocfilehash: aa482dace1086222f63e9165e3089051b5de3e8c


---

# Planear e implementar a sua chave de inquilino do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Utilize as informações deste artigo para o ajudar a planear e gerir a sua chave de inquilino do RMS (Rights Management) do Azure RMS. Por exemplo, em vez de a sua chave de inquilino ser gerida pela Microsoft (predefinição), poderá querer gerir a sua própria chave de inquilino para cumprir os regulamentos específicos que se aplicam à sua organização.  A gestão da sua própria chave de inquilino também é referida como Bring Your Own Key (Traga a Sua Própria Chave) ou BYOK.

> [!NOTE]
> A chave de inquilino do RMS também é conhecida como a chave do Certificado de Licenciante para Servidor (SLC). O Azure RMS mantém uma ou mais chaves para cada organização que subscreve o Azure RMS. Sempre que uma chave é utilizada para o RMS numa organização (por exemplo, chaves de utilizador, chaves de computador, chaves de encriptação de documentos), esta associa-se criptograficamente à sua chave de inquilino do RMS.

**Resumindo:** utilize a seguinte tabela como um guia rápido para a sua topologia de chaves de inquilino recomendada. Em seguida, utilize a documentação adicional para obter mais informações.

Se implementar o Azure RMS com uma chave de inquilino gerida pela Microsoft, pode mudar para o BYOK mais tarde. No entanto, atualmente não pode alterar a gestão da sua chave de inquilino do Azure RMS do BYOK para gerida pela Microsoft.

|Necessidade comercial|Topologia de chaves de inquilino recomendada|
|------------------------|-----------------------------------|
|Implementar o Azure RMS rapidamente e sem necessitar de hardware especial|Gerida pela Microsoft|
|Necessita da funcionalidade IRM completa no Exchange Online com o Azure RMS|Gerida pela Microsoft|
|As suas chaves são criadas por si e protegidas num módulo de hardware de segurança (HSM)|BYOK<br /><br />Atualmente, esta configuração resultará na redução da funcionalidade IRM no Exchange Online. Para mais informações, consulte [Preços e restrições do BYOK](byok-price-restrictions.md).|

## Selecione a sua topologia de chaves de inquilino: gerida pela Microsoft (predefinição) ou gerida por si (BYOK)
Decida que topologia de chaves de inquilino é melhor para a sua organização. Por predefinição, o Azure RMS gera a sua chave de inquilino e gere a maioria dos aspetos do ciclo de vida da chave de inquilino. Esta é a opção mais simples e com menos tarefas administrativas adicionais. Na maioria dos casos, nem precisa de saber que tem uma chave de inquilino. Basta inscrever-se no Azure RMS e o processo de gestão de chaves restante é processado pela Microsoft.

Em alternativa, pode querer ter controlo total sobre a sua chave de inquilino, o que envolve criar a sua chave de inquilino e guardar a cópia principal no local. Este cenário é frequentemente referido como BYOK (Bring Your Own Key – Traga a Sua Própria Chave). Quando esta opção é selecionada, ocorre o seguinte:

1.  Você gera a sua chave de inquilino no local, de acordo com as suas políticas de TI.

2.  Transfere com segurança a chave de inquilino de um Módulo de Hardware de Segurança (HSM) do qual é proprietário para HSMs que são propriedade da Microsoft e geridos pela mesma. Durante este processo, a sua chave de inquilino nunca ultrapassa o limite de proteção de hardware.

3.  Quando transfere a chave de inquilino para a Microsoft, esta permanece protegida pelos HSMs da Thales. A Microsoft trabalhou com a Thales para se certificar de que não é possível extrair a sua chave de inquilino dos HSMs da Microsoft.

Embora seja opcional, provavelmente também irá querer utilizar os registos de utilização quase em tempo real do Azure RMS, para saber exatamente como e quando a sua chave de inquilino está a ser utilizada.

> [!NOTE]
> Como medida de proteção adicional, o Azure RMS utiliza universos de segurança separados nos seus centros de dados na América do Norte, EMEA (Europa, Médio Oriente e África) e Ásia. Quando faz a gestão da sua própria chave de inquilino, esta é associada ao universo de segurança da região na qual o seu inquilino do RMS está registado. Por exemplo, não é possível utilizar uma chave de inquilino de um cliente europeu nos centros de dados da América do Norte ou da Ásia.

## O ciclo de vida das chaves de inquilino
Se decidir que a Microsoft deve gerir a sua chave de inquilino, a maioria das operações de ciclo de vida da chave será processada pela Microsoft. No entanto, se optar por gerir a sua chave de inquilino, fica responsável por muitas das operações de ciclo de vida da chave e por alguns procedimentos adicionais.

Os diagramas seguintes apresentam e comparam estas duas opções. O primeiro diagrama mostra que há poucas tarefas administrativas adicionais para si na configuração predefinida quando a Microsoft gere a chave de inquilino.

![Ciclo de vida da chave de inquilino do Azure RMS – gerida pela Microsoft (a predefinição)](../media/RMS_BYOK_cloud.png)

O segundo diagrama mostra os passos adicionais necessários quando gere a sua própria chave de inquilino.

![Ciclo de vida da chave de inquilino do Azure RMS – gerida por si (BYOK)](../media/RMS_BYOK_onprem.png)

Se decidir deixar que a sua chave de inquilino seja gerida pela Microsoft, não precisa de tomar medidas adicionais para a gerar e pode ir diretamente para [Passos seguintes](plan-implement-tenant-key.md#next-steps).

Se optar por gerir a sua chave de inquilino, leia as secções seguintes para obter mais informações.

## Implementar a sua chave de inquilino do Azure Rights Management

Utilize as informações e os procedimentos desta secção, se tiver decidido gerar e gerir a sua chave de inquilino – o cenário BYOK (Bring Your Own Key – Traga a Sua Própria Chave):


> [!IMPORTANT]
> Se já começou a utilizar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (o serviço está ativado) e tem utilizadores que utilizam o Office 2010, [contacte o Suporte da Microsoft](../get-started/information-support.md#to-contact-microsoft-support) antes de executar estes procedimentos. Dependendo do cenário e dos requisitos, continua a poder utilizar o BYOK, mas com algumas restrições ou passos adicionais.
> 
> Também pode [contactar o Suporte da Microsoft](../get-started/information-support.md#to-contact-microsoft-support) caso a sua organização disponha de políticas para processar chaves específicas.

### Pré-requisitos para o BYOK
Consulte a seguinte tabela para obter uma lista de pré-requisitos para o BYOK (Bring Your Own Key – Traga a Sua Própria Chave).

|Requisito|Mais informações|
|---------------|--------------------|
|Uma subscrição que suporta Azure RMS.|Para mais informações sobre as subscrições disponíveis, consulte [Subscrições na nuvem que suportam o Azure RMS](../get-started/requirements-subscriptions.md).|
|Não utilizar o RMS para utilizadores autónomos ou para o Exchange Online. Em alternativa, se utilizar o Exchange Online, compreender e aceitar as limitações da utilização do BYOK com esta configuração.|Para mais informações sobre as restrições e limitações atuais do BYOK, consulte [Preços e restrições do BYOK](byok-price-restrictions.md).<br /><br />**Importante**: o BYOK não é atualmente compatível com o Exchange Online.|
|HMS da Thales, smart cards e software de suporte.<br /><br />**Nota**: se estiver a migrar do AD RMS para o Azure RMS através da utilização de chave de software para chave de hardware, tem de ter uma versão de controladores da Thales igual ou posterior à 11.62.|Tem de ter acesso a um Módulo de Hardware de Segurança da Thales e conhecimentos operacionais básicos dos HMSs da Thales. Consulte [Thales Hardware Security Module (Módulo de Hardware de Segurança da Thales – em inglês)](http://www.thales-esecurity.com/msrms/buy) para conhecer a lista de modelos compatíveis ou para comprar um HSM caso não tenha um.|
|Se quiser transferir a sua chave de inquilino através da Internet em vez de a transferir pessoalmente em Redmond, EUA, existem 3 requisitos:<br /><br />1: uma estação de trabalho offline x64, com o sistema operativo Windows 7 ou posterior e a versão 11.62 ou posterior do software nShield da Thales.<br /><br />Se esta estação de trabalho executar o Windows 7, tem de [instalar o Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br /><br />2: uma estação de trabalho que está ligada à Internet e com o sistema operativo Windows 7 ou posterior.<br /><br />3: uma unidade USB ou outro dispositivo de armazenamento portátil que tenha pelo menos 16 MB de espaço livre.|Estes pré-requisitos não são necessários se viajar até Redmond e transferir a sua chave de inquilino pessoalmente.<br /><br />Por motivos de segurança, recomendamos que a primeira estação de trabalho não esteja ligada a uma rede. Contudo, isto não é imposto a nível de programação.<br /><br />Nota: nas instruções que se seguem, esta primeira estação de trabalho é referida como a **estação de trabalho desligada**.<br /><br />Além disso, se a chave de inquilino se destinar a uma rede de produção, recomendamos que utilize uma segunda estação de trabalho separada para transferir o conjunto de ferramentas e carregar a chave de inquilino. Contudo, para fins de teste, pode utilizar a mesma estação de trabalho.<br /><br />Nota: nas instruções que se seguem, esta segunda estação de trabalho é referida como a **estação de trabalho ligada à Internet**.|

Os procedimentos para gerar e utilizar a sua própria chave de inquilino são diferentes consoante queira fazê-lo através da Internet ou pessoalmente:

-   **Através da Internet:** são necessários alguns passos de configuração adicionais, tais como transferir e utilizar um conjunto de ferramentas e cmdlets do Windows PowerShell. Contudo, não tem de estar fisicamente numa instalação da Microsoft para transferir a sua chave de inquilino. A segurança é mantida através dos seguintes métodos:

    -   A chave de inquilino é gerada a partir de uma estação de trabalho offline, o que reduz a superfície de ataque.

    -   A chave de inquilino é encriptada com uma Chave de Troca de Chaves (KEK), que permanece encriptada até ser transferida para os HSMs do Azure RMS. A versão encriptada da sua chave de inquilino é a única que deixa a estação de trabalho original.

    -   Uma ferramenta define as propriedades da sua chave de inquilino, vinculando-a a um universo de segurança do Azure RMS. Assim, depois de os HSMs do Azure RMS receberem e desencriptarem a chave de inquilino, esta só poderá ser utilizada por estes HSMs. Não é possível exportar a sua chave de inquilino. Este vínculo é imposto pelos HSMs da Thales.

    -   A Chave de Troca de Chaves (KEK) que é utilizada para encriptar a sua chave de inquilino é gerada nos HSMs do Azure RMS e não é exportável. Os HSMs impõem que não pode existir uma versão não encriptada da KEK fora dos mesmos. Além disso, o conjunto de ferramentas inclui um atestado da Thales que indica que a KEK não é exportável e que foi gerada num HSM genuíno fabricado pela Thales.

    -   O conjunto de ferramentas inclui um atestado da Thales que indica que o universo de segurança do Azure RMS também foi gerado num HSM genuíno fabricado pela Thales. Isto prova que a Microsoft está a utilizar hardware genuíno.

    -   A Microsoft utiliza KEKs separadas, bem como Universos de Segurança separados em cada região geográfica, garantindo que a sua chave de inquilino só pode ser utilizada nos centros de dados da região na qual a encriptou. Por exemplo, não é possível utilizar uma chave de inquilino de um cliente europeu nos centros de dados da América do Norte ou da Ásia.

    > [!NOTE]
    > A sua chave de inquilino pode ser movida com segurança através de computadores e redes não fidedignos, dado que está encriptada e protegida com permissões de controlo de acesso, o que faz com que só possa ser utilizada nos seus HSMs e nos HSMs da Microsoft para o Azure RMS. Pode utilizar os scripts que são fornecidos no conjunto de ferramentas para verificar as medidas de segurança e ler mais informações sobre como isto funciona a partir da Thales em [Hardware Key management in the RMS Cloud (Gestão de Chaves de Hardware na Nuvem do RMS – em inglês)](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **Pessoalmente:** terá de [contactar o Suporte da Microsoft](../get-started/information-support.md#to-contact-microsoft-support) para agendar uma sessão de transferência da chave para o Azure RMS. Tem de se deslocar até aos escritórios da Microsoft em Redmond, Washington, Estados Unidos da América, para transferir a sua chave de inquilino para o universo de segurança do Azure RMS.

Para obter instruções relativas aos procedimentos, selecione se irá gerar e transferir a sua chave de inquilino através da Internet ou pessoalmente: 

- [Através da Internet](generate-tenant-key-internet.md)
- [Pessoalmente](generate-tenant-key-in-person.md)


## Passos seguintes

Agora que já planeou e, se necessário, gerou a chave do inquilino, faça o seguinte:

1.  Comece a utilizar a sua chave de inquilino:

    -   Se ainda não o fez, tem agora de ativar o Rights Management para que a sua organização possa começar a utilizar o RMS. Os utilizadores começam a utilizar de imediato a sua chave de inquilino (gerida pela Microsoft ou por si).

        Para mais informações sobre a ativação, consulte [Ativar o Azure Rights Management](../deploy-use/activate-service.md).

    -   Se já tinha ativado o Rights Management e depois decidiu gerir a sua própria chave de inquilino, a transição dos utilizadores da chave de inquilino antiga para a nova chave de inquilino será efetuada gradualmente. A conclusão desta transição escalonada poderá demorar algumas semanas. Os documentos e ficheiros que foram protegidos com a chave de inquilino antiga permanecem acessíveis aos utilizadores autorizados.

2.  Pondere utilizar registos de utilização, que lhe permitem registar todas as transações efetuadas pelo RMS.

    Se decidiu gerir a sua própria chave de inquilino, o registo incluirá informações sobre como utilizar a sua chave de inquilino. Consulte o seguinte fragmento de um ficheiro de registo apresentado no Excel onde os tipos de pedido **KMSPDecrypt** e **KMSPSignDigest** mostram que a chave de inquilino está a ser utilizada.

    ![ficheiro de registo no Excel onde a chave de inquilino está a ser utilizada](../media/RMS_Logging.png)

    Para mais informações sobre o registo de utilização, consulte [Registo e análise da utilização do Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Guarde a sua chave de inquilino.

    Para mais informações, consulte [Operações para a sua chave de inquilino do Azure Rights Management](../deploy-use/operations-tenant-key.md).




<!--HONumber=Jun16_HO5-->


