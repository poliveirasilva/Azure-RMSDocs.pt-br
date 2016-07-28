---
title: Migrando do AD RMS para o Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: 8ef46d68594a6e559e050f846a844f566ff8770d


---

# Migrando do AD RMS para o Azure Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*

Use o seguinte conjunto de instruções para migrar sua implantação do Active Directory Rights Management Services (AD RMS) para o Azure Rights Management (Azure RMS). Após a migração, os usuários ainda terão acesso aos documentos e às mensagens de email que sua organização protegia usando o AD RMS, e o novo conteúdo protegido usará o Azure RMS.

Não sabe se essa migração do AD RMS é adequada para sua organização?

-   Para obter uma introdução ao Azure RMS, conhecer os problemas de negócios que ele pode solucionar, ver sua aparência para administradores e usuários e saber como funciona, consulte [O que é o Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

-   Para obter uma comparação entre Azure RMS e o AD RMS, consulte [Comparando o Azure Rights Management e o AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## Pré-requisitos para migrar do AD RMS para o Azure RMS
Antes de iniciar a migração para o Azure RMS, lembre-se de seguir estes pré-requisitos e entender as limitações.


- **Uma implantação do RMS com suporte**

    Todas as versões do AD RMS do Windows Server 2008 por meio do Windows Server 2012 R2 suportam uma migração para o Azure RMS:

    - Windows Server 2008 (x86 ou x64)

    - Windows Server 2008 R2 (x64)

    - Windows Server 2012 (x64)

    - Windows Server 2012 R2 (x64)

    Todas as topologias do AD RMS válidas têm suporte:

    - Floresta única, cluster de RMS único

    - Floresta única, vários clusters de RMS somente de licenciamento

    - Várias florestas, vários clusters de RMS

    **Observação**: por padrão, vários clusters de RMS migram para um único locatário do Azure RMS. Se desejar locatários diferentes do RMS, trate-os como migrações diferentes. Uma chave de um cluster do RMS não pode ser importada para mais de um locatário do Azure RMS.


- **Todos os requisitos para executar o Azure RMS, incluindo um locatário do Azure RMS (não ativado)**

    Consulte [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

    Embora você deva ter um locatário do Azure RMS antes de migrar do AD RMS, recomendamos que não ative o serviço de Rights Management antes da migração. O processo de migração inclui essa etapa depois de exportar chaves e modelos do AD RMS e importá-los para o Azure RMS. No entanto, se o Azure RMS já está ativado, você ainda pode migrar do AD RMS.


- **Preparação para o Azure RMS:**

    - Sincronização de diretórios entre seu diretório local e o Active Directory do Azure

    - Grupos habilitados para email no Active Directory do Azure

    Consulte [Preparação para o Azure Rights Management](prepare.md).


- **Se você usou a funcionalidade de IRM (Information Rights Management) do Exchange Server** (por exemplo, regras de transporte e o Outlook Web Access) ou o SharePoint Server com o AD RMS:

    - Planeje por um curto período de tempo em que o IRM não estará disponível nesses servidores
 
    Você pode continuar usando o IRM nesses servidores com o Azure RMS após a migração. Porém, uma das etapas de migração é desabilitar temporariamente o serviço IRM, instalar e configurar um conector, reconfigurar os servidores e reabilitar o IRM.

    Essa é a única interrupção no serviço durante o processo de migração.


Limitações:

-   Embora o processo de migração dê suporte para a migração da chave do SLC (Certificado de Licenciamento do Servidor) de um HSM (Módulo de Segurança de Hardware) para o Azure RMS, o Exchange Online não dá suporte a essa configuração no momento. Se desejar usar todas as funcionalidades do IRM com o Exchange Online após migrar do Azure RMS, sua chave de locatário do Azure RMS deverá ser [gerenciada pela Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). Como alternativa, você pode executar o IRM com funcionalidade reduzida no Exchange Online quando seu locatário do Azure RMS é gerenciado por você (BYOK). Para obter mais informações sobre como usar o Exchange Online com o Azure RMS, consulte [Etapa 6. Configure a integração do IRM para o Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online) destas instruções de migração.

-   Se tiver clientes e software sem suporte com o Azure RMS, eles não poderão proteger ou consumir conteúdo protegido pelo Azure RMS. Verifique as seções de clientes e aplicativos com suporte do artigo [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Se você importar sua chave local para o Azure RMS como arquivada (você não define o TPD para ativo durante o processo de importação) e migrar usuários em lotes para uma migração em fases, o conteúdo protegido recentemente pelos usuários migrados não estará acessível aos usuários que permanecem no AD RMS. Nesse cenário, sempre que possível, mantenha o tempo da migração curto e migre usuários em lotes lógicos de modo que se eles colaboram entre si, eles são migrados juntos.

    Essa limitação não se aplica quando você define o TPD para ativo durante o processo de importação, porque todos os usuários protegerão o conteúdo usando a mesma chave. Recomendamos essa configuração porque permite migrar todos os usuários independentemente e em seu próprio ritmo.

-   Se você colabora com parceiros externos (por exemplo, usando domínios de usuário confiáveis ou federação), eles também devem migrar para o Azure RMS, seja ao mesmo tempo que a migração ou assim que possível posteriormente. Para continuar acessando o conteúdo que a sua organização protegia anteriormente usando o AD RMS, deve-se fazer alterações na configuração do cliente que sejam semelhantes às feitas por você e incluídas neste documento.

    Devido as possíveis variações de configuração que seus parceiros possam ter, as instruções exatas para essa reconfiguração está fora do escopo deste documento. Para obter ajuda, [contate o Suporte da Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## Visão geral das etapas para migrar do AD RMS para o Azure RMS


As 9 etapas de migração podem ser divididas em 4 fases que podem ser feitas em momentos e administradores diferentes.

[**FASE 1: CONFIGURAÇÃO DO LADO DO SERVIDOR PARA O AD RMS**](migrate-from-ad-rms-phase1.md)

- **Etapa 1: baixar a ferramenta de administração de gerenciamento do Azure RMS Management**

    O processo de migração requer a execução de um ou mais dos cmdlets do Windows PowerShell do módulo do Azure RMS instalado com a ferramenta de administração de gerenciamento do Azure RMS.

- **Etapa 2. Exportar os dados de configuração do AD RMS e importá-los para o Azure RMS**

    Exporte os dados de configuração (chaves, modelos, URLs) do AD RMS para um arquivo XML e, em seguida, carregue esse arquivo para o Azure RMS usando o cmdlet Import-AadrmTpd do PowerShell do Windows. Dependendo da sua configuração de chave no AD RMS, poderão ser necessárias etapas adicionais:

    - **Migração de chave protegida por software para chave protegida por software**:

        Chaves com base em senha centralmente gerenciadas no AD RMS para chave de locatário gerenciada pelo Microsoft do Azure RMS. Este é o caminho de migração mais simples e não é preciso fazer mais nada.

    - **Migração de chave protegida por HSM para chave protegida por HSM**:

        Chaves que são armazenadas por HSM para AD RMS para chave de locatário do Azure RMS gerenciada pelo cliente (o cenário “traga a sua própria chave” ou BYOK). Isso exige etapas adicionais para transferir a chave do seu Thales HSM local para o Azure RMS HSM. Sua chave protegida por HSM existente deve ser protegida por módulo; não há suporte no conjunto de ferramentas BYOK para chaves protegidas por OCS.

    - **Migração de chave protegida por software para chave protegida por HSM**:

        Chaves com base em senha gerenciadas centralmente no AD RMS para chave de locatário do Azure RMS gerenciada pelo cliente (o cenário “traga a sua própria chave” ou BYOK). Isso exige a mais alta configuração, porque você deve primeiro extrair a sua chave de software e importá-la para um HSM local e, em seguida, seguir outros procedimentos para transferir a chave do seu Thales HSM local para o Azure RMS HSM.

- **Etapa 3. Ativar seu locatário do Azure RMS**

    Se possível, siga esta etapa após o processo de importação e não antes.

- **Etapa 4. Configurar modelos importados**

    Quando você importa seus modelos de política de direitos, o seu status é arquivado. Se desejar que os usuários possam vê-los e usá-los, altere o status do modelo para publicado no Portal clássico do Azure.


[**FASE 2: CONFIGURAÇÃO DO LADO DO CLIENTE**](migrate-from-ad-rms-phase2.md)


- **Etapa 5: reconfigurar os clientes para usar o Azure RMS**

    Os computadores existentes com Windows devem ser reconfigurados para usar o serviço do Azure RMS, em vez do AD RMS. Essa etapa se aplica a computadores da sua organização e a computadores de organizações parceiras se você tiver colaborado com elas enquanto estava executando o AD RMS.

    Além disso, se você tiver implantado a [extensão de dispositivos móveis](http://technet.microsoft.com/library/dn673574.aspx) para dar suporte aos dispositivos móveis como telefones iOS e iPads, telefones e tablets Android, Windows Phone e computadores Mac, deverá remover os registros SRV no DNS que redirecionaram esses clientes para usar o AD RMS


[**FASE 3: CONFIGURAÇÃO DE SERVIÇOS DE SUPORTE**](migrate-from-ad-rms-phase3.md)


- **Etapa 6: configurar a integração do IRM com o Exchange Online**

    Essa etapa será necessária se você quiser usar o Exchange Online com o Azure RMS.


- **Etapa 7: implantar o conector do RMS**

    Esta etapa é necessária se desejar usar qualquer um dos seguintes serviços locais com o Azure RMS:

    - Exchange Server (por exemplo, regras de transporte e Outlook Web Access)

    - SharePoint Server

    - Windows Server que executa a FCI (Infraestrutura de Classificação de Arquivos)


[**FASE 4: PUBLICAR TAREFAS DE MIGRAÇÃO**](migrate-from-ad-rms-phase4.md )

- **Etapa 8: Desativar o AD RMS**

    Depois de confirmar que todos os clientes estão usando o Azure RMS e não estão mais acessando os servidores do AD RMS, você pode encerrar sua implantação do AD RMS.


- **Etapa 9: criar novamente sua chave de locatário do Azure RMS**

    Essa etapa é necessária se não estiver executando no Modo Criptográfico 2 antes da migração e é opcional mas recomendado para todas as migrações, para ajudar a proteger a segurança da chave de locatário do Azure RMS.


## Próximas etapas
Para iniciar a migração, vá para [Fase 1 - configuração do lado do servidor](migrate-from-ad-rms-phase1.md).




<!--HONumber=Jul16_HO3-->


