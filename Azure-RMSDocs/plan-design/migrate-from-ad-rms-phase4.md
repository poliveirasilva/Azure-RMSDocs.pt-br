---
# required metadata

title: Migração do AD RMS para o Azure Rights Management - Fase 4 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Fase de migração 4 - tarefas pós-migração

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*


Use as informações a seguir para a Fase 4 da migração do AD RMS para o Azure RMS (Azure Rights Management). Esses procedimentos abrangem as etapas 8 a 9 em [Migrando do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Etapa 8. Descomissionamento do AD RMS

Opcional: remova o ponto de conexão de serviço (SCP) do Active Directory para impedir que os computadores descubram sua infraestrutura de Rigths Management local. Isso é opcional por causa do redirecionamento configurado no registro (por exemplo, executando o script de migração). Para remover o Ponto de Conexão de Serviço, use a ferramenta de registro AD SCP do [Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479).

Monitore os seus servidores AD RMS para atividade, por exemplo, verificando as [solicitações no relatório de Integridade do sistema](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), a [tabela ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) ou [a auditoria de acesso do usuário ao conteúdo protegido](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Depois de confirmar que os clientes RMS não estão se comunicando com esses servidores e os clientes estão usando o Azure RMS com sucesso, remova a função de servidor do AD RMS desse servidor. Se estiver usando servidores dedicados, talvez você prefira a etapa preventiva de desligar primeiro os servidores por um tempo para garantir que não haja nenhum problema que talvez exija a reinicialização desses servidores para garantir a continuidade do serviço enquanto você investiga por que os clientes não estão usando o Azure RMS.

Após o encerramento dos servidores de AD RMS, você pode querer aproveitar a oportunidade para examinar os modelos no Portal clássico do Azure e consolidá-los para que os usuários tenham menos modelos para escolha ou reconfigurá-los ou até mesmo adicionar novos modelos. Esse também é um bom momento para publicar os modelos padrão. Para obter mais informações, confira [Configurando modelos personalizados para o Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Etapa 9. Criar novamente a sua chave de locatário do Azure RMS
Esta etapa é necessária quando a migração é concluída, se sua implantação do AD RMS estava usando o Modo de Criptografia 1 do RMS, porque o rechaveamento cria uma nova chave de locatário que usa o Modo de Criptografia 2 do RMS. Usar o Azure RMS com modo de criptografia 1 é suportado apenas durante o processo de migração.

Esta etapa é opcional, mas recomendada quando a migração é concluída, mesmo se estivesse operando no Modo de Criptografia 2 do RMS, pois ajuda a proteger a sua chave de locatário do Azure RMS contra possíveis violações de segurança na sua chave de AD RMS. Quando você cria novamente sua chave de locatário do Azure RMS (também conhecida como “distribuir sua chave”), uma nova chave é criada e a chave original é arquivada. No entanto, como a mudança de uma chave para outra não acontece imediatamente, pois leva semanas, não espere até suspeitar de uma violação na chave original. Crie novamente sua chave de locatário RMS assim que a migração for concluída.

Para criar novamente sua chave de locatário do Azure RMS:

-   Se a chave de locatário do RMS for gerenciada pela Microsoft: Ligue para o Suporte ao Cliente da Microsoft (CSS) e prove que você é o administrador do locatário do RMS.

-   Se a chave de locatário do RMS for gerenciada por você (BYOK): Repita o procedimento BYOK para gerar e criar uma nova chave pela Internet ou pessoalmente.

Para obter mais informações sobre como gerenciar sua chave de locatário do RMS, consulte [Operações para sua chave de locatário do Azure Rights Management](../deploy-use/operations-tenant-key.md).

## Próximas etapas

Agora que você concluiu a migração, examine o [roteiro de implantação](deployment-roadmap.md) para identificar outras tarefas de implantação que você pode precisar fazer.



<!--HONumber=Apr16_HO4-->


