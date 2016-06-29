---
# required metadata

title: Migrar do AD RMS para o Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Migrar do AD RMS para o Azure Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*

Utilize o seguinte conjunto de instruções para migrar a implementação dos Serviços de Gestão de Direitos do Active Directory (AD RMS) para o Azure Rights Management (Azure RMS). Após a migração, os utilizadores continuam a ter acesso a documentos e a mensagens de e-mail que a sua organização protegeu através da utilização do AD RMS, sendo que o conteúdo recentemente protegido utilizará o Azure RMS.

Não tem a certeza se esta migração do AD RMS é adequada para a sua organização?

-   Para ver uma introdução ao Azure RMS, os problemas empresariais que pode resolver, o aspeto que tem para administradores e utilizadores e como funciona, consulte [O que é o Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

-   Para ver uma comparação entre o Azure RMS e o AD RMS, consulte [Comparar o Azure Rights Management e o AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## Pré-requisitos para migrar o AD RMS para o Azure RMS
Antes de iniciar a migração para o Azure RMS, certifique-se de que os seguintes pré-requisitos estão assegurados e de que compreende quaisquer limitações.


- **Uma implementação suportada do RMS**

    Todas as versões do AD RMS, do Windows Server 2008 até ao Windows Server 2012 R2, suportam a migração para o Azure RMS:

    - Windows Server 2008 (x86 ou x64)

    - Windows Server 2008 R2 (x64)

    - Windows Server 2012 (x64)

    - Windows Server 2012 R2 (x64)

    Todas as topologias válidas do AD RMS são suportadas:

    - Floresta única, cluster RMS único

    - Floresta única, vários clusters RMS só de licenciamento

    - Várias florestas, vários clusters RMS

    **Nota**: por predefinição, vários clusters RMS migram para um único inquilino do Azure RMS. Se pretender inquilinos do RMS diferentes, tem de tratá-los como migrações diferentes. Uma chave de um cluster RMS não pode ser importada para mais do que um inquilino do Azure RMS.


- **Todos os requisitos para executar o Azure RMS, incluindo um inquilino do Azure RMS (não ativado)**

    Consulte [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

    Embora tenha de possuir um inquilino do Azure RMS para poder migrar do AD RMS, recomendamos que não ative o serviço Rights Management antes da migração. O processo de migração inclui este passo após a exportação de chaves e modelos do AD RMS e respetiva importação para o Azure RMS. No entanto, se o Azure RMS já estiver ativado, ainda pode migrar a partir do AD RMS.


- **Preparação para o Azure RMS:**

    - Sincronização de diretórios entre o diretório no local e o Azure Active Directory

    - Grupos com capacidade de correio no Azure Active Directory

    Consulte [Preparar para o Azure Rights Management](prepare.md).


- **Se tiver utilizado a funcionalidade de Gestão de Direitos de Informação (IRM) do Exchange Server** (por exemplo, regras de transporte e Outlook Web Access) ou do SharePoint Server com o AD RMS:

    - A IRM não estará disponível nestes servidores durante um curto período de tempo
 
    Pode continuar a utilizar a IRM nestes servidores com o Azure RMS após a migração. No entanto, um dos passos da migração é a desativação temporária do serviço de IRM, a instalação e configuração de um conetor, a reconfiguração dos servidores e reativação da IRM.

    Esta é a única interrupção no serviço durante o processo de migração.


Limitações:

-   Embora o processo de migração permita migrar a chave do certificado de licenciamento de servidor (SLC) para um módulo de segurança de hardware (HSM) para o Azure RMS, o Exchange Online não suporta atualmente esta configuração. Caso pretenda todas as funcionalidades da IRM com o Exchange Online após a migração para o Azure RMS, a chave de inquilino do Azure RMS tem de ser [gerida pela Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-). Em alternativa, pode executar a IRM com funcionalidade reduzida no Exchange Online quando o inquilino do Azure RMS é gerido por si (BYOK). Para obter mais informações acerca da utilização do Exchange Online com o Azure RMS, consulte o [Passo 6. Configurar a integração de IRM para o Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online) nestas instruções de migração.

-   Se tiver software e clientes que não são suportados com o Azure RMS, não conseguirão proteger ou consumir conteúdo que seja protegido pelo Azure RMS. Não se esqueça de verificar as secções de aplicações e clientes suportados no artigo [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Se importar a chave no local para o Azure RMS como arquivada (se não definir o TPD para ser o ativo durante o processo de importação) e migrar utilizadores em lotes para uma migração faseada, o conteúdo protegido recentemente pelos utilizadores migrados não estará acessível aos utilizadores que permanecerem no AD RMS. Neste cenário, sempre que possível, mantenha o tempo de migração curto e migre os utilizadores em lotes lógicos, de tal forma que se colaborarem mutuamente, sejam migrados em conjunto.

    Esta limitação não se aplica quando define o TPD para ativo durante o processo de importação, porque todos os utilizadores irão proteger o conteúdo através da mesma chave. Recomendamos esta configuração porque lhe permite migrar todos os utilizadores de forma independente e ao seu ritmo.

-   Se colaborar com parceiros externos (por exemplo, através da utilização de domínios ou federações de utilizadores fidedignos), estes também devem migrar para o Azure RMS em simultâneo com a sua migração ou logo que seja possível posteriormente. Para continuarem a aceder a conteúdo que a sua organização protegia anteriormente ao utilizar o AD RMS, têm de efetuar alterações na configuração de clientes semelhantes àquelas que o utilizador efetuou e que estão incluídas neste documento.

    Devido às possíveis variações de configuração que os seus parceiros possam ter, as instruções exatas para esta reconfiguração não estão incluídas neste documento. Para ajuda, [contacte o Suporte da Microsoft](../get-started/information-support#support-options-and-community-resources).

## Visão geral dos passos para migrar o AD RMS para o Azure RMS


Os 9 passos de migração podem ser divididos em 4 fases que podem ser efetuadas em alturas diferentes e por administradores diferentes.

[**FASE 1: CONFIGURAÇÃO DO LADO DO SERVIDOR PARA O AD RMS**](migrate-from-ad-rms-phase1.md)

- **Passo 1: Transferir a Ferramenta de Administração de Gestão do Azure RMS**

    O processo de migração requer a execução de um ou mais cmdlets do Windows PowerShell do módulo do Azure RMS que é instalado com a Ferramenta de Administração de Gestão do Azure RMS.

- **Passo 2. Exportar os dados de configuração do AD RMS e importá-los para o Azure RMS**

    Exporte os dados de configuração (chaves, modelos, URLs) do AD RMS para um ficheiro XML e, em seguida, carregue esse ficheiro para o Azure RMS utilizando o cmdlet Import-AadrmTpd do Windows PowerShell. É possível que sejam necessários mais passos, consoante a configuração da sua chave do AD RMS:

    - **Migração de chave protegida por software para chave protegida por software**:

        Chaves geridas centralmente com base em palavras-passe no AD RMS para a chave de inquilino do Azure RMS gerida pela Microsoft. Este é o caminho de migração mais simples e não são necessários passos adicionais.

    - **Migração de chave protegida por HSM para chave protegida por HSM**:

        Chaves que são armazenadas por um HSM do AD RMS para a chave de inquilino do Azure RMS gerida pelo cliente (o cenário “traga a sua própria chave” ou BYOK). Isto requer passos adicionais para transferir a chave do seu HSM da Thales no local para o HSM do Azure RMS. A sua chave existente protegida por HSM tem de ser protegida por módulo. As chaves protegidas por OCS não são suportadas pelo conjunto de ferramentas BYOK.

    - **Migração de chave protegida por software para chave protegida por HSM**:

        Chaves geridas centralmente e baseadas em palavras-passe no AD RMS para a chave de inquilino do Azure RMS gerida pelo cliente (o cenário “traga a sua própria chave” ou BYOK). Esta é a migração que requer mais configuração porque tem primeiro de extrair a chave de software e importá-la para um HSM no local e, em seguida, efetuar os passos adicionais para transferir a chave do seu HSM da Thales no local para o HSM do Azure RMS.

- **Passo 3. Ativar o inquilino do Azure RMS**

    Se possível, efetue este passo depois do processo de importação e não antes.

- **Passo 4. Configurar modelos importados**

    Quando importar os seus modelos de política de direitos, o estado dos mesmos é arquivado. Se pretender que os utilizadores os possam ver e utilizar, tem de alterar o estado do modelo para publicado no portal clássico do Azure.


[**FASE 2: CONFIGURAÇÃO DO LADO DO CLIENTE**](migrate-from-ad-rms-phase2.md)


- **Passo 5: reconfigurar clientes para utilizarem o Azure RMS**

    Os computadores existentes com Windows têm de ser reconfigurados para utilizarem o serviço do Azure RMS em vez do AD RMS. Este passo aplica-se aos computadores na sua organização e aos computadores nas organizações parceiras, caso tenha colaborado com as mesmas enquanto executou o AD RMS.

    Além disso, se tiver implementado a [extensão de dispositivo móvel](http://technet.microsoft.com/library/dn673574.aspx) para suportar dispositivos móveis, tais como iPads e telemóveis com iOS, tablets e telemóveis Android, telemóvel Windows e computadores Mac, tem de remover os registos SRV no DNS que redirecionou estes clientes para utilizarem o AD RMS


[**PASSO 3: CONFIGURAÇÃO DE SERVIÇOS DE SUPORTE**](migrate-from-ad-rms-phase3.md)


- **Passo 6: configurar a integração de IRM com o Exchange Online**

    Este passo é obrigatório se pretender utilizar o Exchange Online com o Azure RMS.


- **Passo 7: implementar o conetor RMS**

    Este passo é obrigatório se pretender utilizar qualquer um dos seguintes serviços no local com o Azure RMS:

    - Exchange Server (por exemplo, regras de transporte e Outlook Web Access)

    - SharePoint Server

    - Windows Server que executa a Infraestrutura de Classificação de Ficheiros (FCI)


[**FASE 4: TAREFAS PÓS-MIGRAÇÃO**](migrate-from-ad-rms-phase4.md )

- **Passo 8: desativar o AD RMS**

    Quando tiver confirmado que todos os clientes estão a utilizar o Azure RMS e já não acedem aos servidores AD RMS, pode desativar a implementação do AD RMS.


- **Passo 9: efetuar o rechaveamento da chave de inquilino do Azure RMS**

    Este passo é obrigatório se não estava a executar no Modo Criptográfico 2 antes da migração, sendo opcional, mas recomendado, para todas as migrações para ajudar a salvaguardar a segurança da sua chave de inquilino do Azure RMS.


## Passos seguintes
Para iniciar a migração, aceda a [Fase 1 – configuração do lado do servidor](migrate-from-ad-rms-phase1.md).



<!--HONumber=Jun16_HO2-->


