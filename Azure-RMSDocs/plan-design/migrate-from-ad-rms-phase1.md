---
# required metadata

title: Migração do AD RMS para o Azure Rights Management - Fase 1 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Fase de migração 1: configuração do lado do servidor para o AD RMS

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*

Use as informações a seguir para a Fase 1 da migração do AD RMS para o Azure RMS (Azure Rights Management). Esses procedimentos abrangem as etapas 1 a 4 de [Migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Etapa 1: baixar a ferramenta de Administração do Azure Rights Management
Vá para a Central de Download da Microsoft e baixe a [Ferramenta de Administração do Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721), que contém o módulo de administração do Azure RMS para o Windows PowerShell.

Instale o aplicativo. Para obter instruções de instalação, confira [Instalação do Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

## Etapa 2. Exportar os dados de configuração do AD RMS e importá-los para o Azure RMS
Esta etapa é um processo de duas partes:

1.  Exporte os dados de configuração do AD RMS, exportando os domínios de publicação confiável (TPDs) para um arquivo .xml. Esse processo é o mesmo para todas as migrações.

2.  Importe os dados de configuração para o Azure RMS. Existem processos diferentes para essa etapa, dependendo da sua configuração atual de implantação do AD RMS e da sua topologia preferencial para a chave de locatário do Azure RMS.

### Exportar os dados de configuração do AD RMS
Faça o seguinte em todos os clusters do AD RMS, para todos os domínios de publicação confiáveis que já protegeram o conteúdo da sua organização. Você não precisa executar isso em clusters somente de licenciamento.

> [!NOTE] Se você estiver usando o Windows Server 2003 Rights Management, em vez dessas instruções, siga o procedimento [Exportar chave privada de SLC, TUD, TPD e RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) do artigo [Migrando do Windows RMS para AD RMS em uma infraestrutura diferente](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx).

#### Para exportar os dados de configuração (informações de domínio de publicação confiável)

1.  Faça logon no cluster do AD RMS como um usuário com permissões administrativas do AD RMS.

2.  No console de gerenciamento do AD RMS (**Active Directory Rights Management Services**), expanda o nome do cluster AD RMS, expanda **Diretivas de confiança**e clique em **Domínios de Publicação Confiável**.

3.  No painel de resultados, selecione o domínio de publicação confiável e, no painel de ações, clique em **Exportar Domínio de Publicação Confiável**.

4.  Na caixa de diálogo **Exportar Domínio de Publicação Confiável** :

    -   Clique em **Salvar Como** e salve o caminho e o nome de arquivo de sua escolha. Verifique se você especificou **.xml** como a extensão do nome do arquivo (ela não é acrescentada automaticamente).

    -   Especifique e confirme uma senha forte. Guarde essa senha, pois você precisará dela mais tarde, quando importar os dados de configuração para o Azure RMS.

    -   Não marque a caixa de seleção para salvar o arquivo de domínio confiável na versão 1.0 do RMS.

Quando tiver exportado todos os domínios de publicação confiáveis, você estará pronto para iniciar o procedimento de importação desses dados para o Azure RMS. HSM (Módulo de segurança de hardware) de Thales. Para saber mais, 

### Importar os dados de configuração para o Azure RMS
Os procedimentos exatos para essa etapa dependem da sua configuração atual de implantação do AD RMS e da sua topologia preferencial para a chave de locatário do Azure RMS.

Sua implantação atual do AD RMS usará uma das seguintes configurações para sua chave do certificado de licenciante para servidor (SLC):

-   Proteção por senha no banco de dados do AD RMS. Essa é a configuração padrão.

-   Proteção de HSM usando um módulo de segurança de hardware (HSM) Thales.

-   Proteção de HSM usando um módulo de segurança de hardware (HSM) de um fornecedor que não seja a Thales.

-   Senha protegida usando um provedor criptográfico externo.

> [!NOTE] Para saber mais sobre como usar módulos de segurança de hardware com o AD RMS, consulte [Usando o AD RMS com módulos de segurança de hardware](http://technet.microsoft.com/library/jj651024.aspx).

As duas opções de topologia de chave de locatário do Azure RMS são: a Microsoft gerencia sua chave de locatário (**gerenciada pela Microsoft**) ou você pode gerenciar a sua chave de locatário (**gerenciada pelo cliente**). Quando você gerencia a sua própria chave de locatário do Azure RMS, nós chamamos isso de “traga sua própria chave” (BYOK) e requer um módulo de segurança de hardware (HSM) da Thales. Para saber mais, confira o artigo [Planejamento e implementação de sua chave de locatário do Azure Rights Management](plan-implement-tenant-key.md).

> [!IMPORTANT]
> Atualmente o Exchange Online não é compatível com Azure RMS BYOK.  Se você quiser usar o BYOK após a migração e planeja usar o Exchange Online, certifique-se de que você compreende como essa configuração reduz a funcionalidade do IRM para o Exchange Online. Veja as informações em [Preços e restrições de BYOK](byok-price-restrictions.md) para obter ajuda com a escolha da melhor topologia de chave de locatário do Azure RMS para a migração.

Use a tabela a seguir para identificar o procedimento a ser usado para a migração. Não há suporte para combinações que não estão listadas.

|Implantação atual do AD RMS|Topologia de chave de locatário escolhida do Azure RMS|Instruções de migração|
|-----------------------------|----------------------------------------|--------------------------|
|Proteção por senha no banco de dados do AD RMS|Gerenciado pela Microsoft|Veja o procedimento de migração de **Chave protegida por software para chave protegida por software** depois desta tabela.<br /><br />Esse é o caminho de migração mais simples e requer apenas que você transfira os dados de configuração para o Azure RMS.|
|Proteção de HSM usando um módulo de segurança de hardware (HSM) Thales nShield|Gerenciada pelo cliente (BYOK)|Consulte o procedimento de migração **Chave protegida por HSM para chave protegida por HSM** depois desta tabela.<br /><br />Isso exige que o conjunto de ferramentas BYOK e dois conjuntos de etapas transfiram a chave do seu HSM local para o Azure RMS HSM e depois transfiram os dados de configuração para o Azure RMS.|
|Proteção por senha no banco de dados do AD RMS|Gerenciada pelo cliente (BYOK)|Consulte o procedimento **Migração de chave protegida por software para chave protegida por HSM** depois desta tabela.<br /><br />Isso exige que o conjunto de ferramentas BYOK e três conjuntos de etapas extraiam primeiro sua chave de software e importem-na para um HSM local, transfiram a chave de seu HSM local para os Azure RMS HSMs e, finalmente, transfiram os dados de configuração para o Azure RMS.|
|Proteção de HSM usando um módulo de segurança de hardware (HSM) de um fornecedor que não seja a Thales|Gerenciada pelo cliente (BYOK)|Contate o fornecedor do seu HSM para saber como transferir a sua chave desse HSM para um Módulo de Segurança de Hardware (HSM) Thales nShield. Em seguida, siga as instruções para o procedimento **Migração de chave protegida por HSM para chave protegida por HSM** depois desta tabela.|
|Senha protegida usando um provedor criptográfico externo|Gerenciada pelo cliente (BYOK)|Contate o fornecedor para o provedor criptográfico para saber como transferir sua chave para um Módulo de Segurança de Hardware (HSM) Thales nShield. Em seguida, siga as instruções para o procedimento **Migração de chave protegida por HSM para chave protegida por HSM** depois desta tabela.|
Antes de começar estes procedimentos, verifique se você pode acessar os arquivos .xml que você criou antes quando exportou os domínios de publicação confiáveis. Por exemplo, eles podem ter sido salvos em um pen drive USB que você tirou do servidor AD RMS na estação de trabalho conectada à Internet.

> [!NOTE] Embora você armazene esses arquivos, use as práticas recomendadas de segurança para protegê-los porque esses dados incluem sua chave privada.


Para concluir a Etapa 2, escolha e selecione as instruções para seu caminho de migração: 


- [Chave de software para chave de software](migrate-softwarekey-to-softwarekey.md)
- [Chave HSM para chave HSM](migrate-hsmkey-to-hsmkey.md)
- [Chave de software para chave HSM](migrate-softwarekey-to-hsmkey.md)


## Etapa 3. Ativar o seu locatário do RMS
As instruções para esta etapa foram completamente abordadas no artigo [Ativação do Azure Rights Management](../deploy-use/activate-service.md).


> [!TIP]
> Se tiver uma assinatura do Office 365, será possível ativar o Azure RMS no Centro de administração do Office 365 ou no Portal clássico do Azure. Recomendamos usar o Portal clássico do Azure, porque você usará esse portal de gerenciamento para concluir a próxima etapa.

**E se o seu locatário do Azure RMS já estiver ativado?** Se o serviço do Azure RMS já estiver ativado para a sua organização, talvez os usuários já tenham usado o Azure RMS para proteger o conteúdo com uma chave de locatário gerada automaticamente (e os modelos padrão) em vez de suas chaves (e modelos) existentes do AD RMS. Isso é improvável de acontecer em computadores que estão bem gerenciados em sua intranet, pois eles serão configurados automaticamente para sua infraestrutura do AD RMS. Mas isso pode acontecer em computadores do grupo de trabalho ou computadores que raramente se conectam à sua intranet. Infelizmente, também é difícil identificar esses computadores, por isso, recomendamos que você não ative o serviço antes de importar os dados de configuração do AD RMS.

Se seu locatário do Azure RMS já estiver ativado e você puder identificar esses computadores, execute o script CleanUpRMS_RUN_Elevated.cmd nesses computadores conforme descrito na Etapa 5. A execução deste script força a reinicializar o ambiente do usuário, para que eles baixem a chave de locatário atualizada e os modelos importados.

## Etapa 4. Configurar modelos importados
Como os modelos importados têm um estado padrão de **Arquivado**, você deve alterar esse estado para ser **Publicado** se desejar que os usuários possam utilizá-los com o Azure RMS.

Além disso, se seus modelos no AD RMS tiverem usado o grupo **QUALQUER PESSOA**, esse grupo será removido automaticamente quando você importar os modelos para o Azure RMS; é necessário adicionar manualmente o grupo ou os usuários equivalentes e os mesmos direitos aos modelos importados. O grupo equivalente para o Azure RMS é chamado de **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<nome_do_locatário>.onmicrosoft.com**. Por exemplo, esse grupo pode parecer com o seguinte para a Contoso: **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Se você não tiver certeza se os seus modelos do AD RMS incluem o grupo QUALQUER PESSOA, use o exemplo de script do Windows PowerShell para identificar esses modelos. Para saber mais sobre como usar o Windows PowerShell com o AD RMS, confira [Como usar o Windows PowerShell para administrar o AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

Você poderá ver o grupo de sua organização criado automaticamente se copiar um dos modelos de política de direitos padrão no Portal Clássico do Azure e identificar o **NOME DE USUÁRIO** na página **DIREITOS**. No entanto, você não poderá usar o Portal clássico do Azure para adicionar esse grupo a um modelo criado manualmente ou importado. Em vez disso, deverá usar uma das opções do Azure RMS PowerShell:

-   Use o cmdlet do PowerShell [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para definir o grupo "AllStaff" e os direitos como um objeto de definição de direitos, e execute este comando novamente para cada um dos outros grupos ou usuários com direitos já concedidos no modelo original além do grupo QUALQUER PESSOA. Em seguida, adicione esses objetos de definição de direitos aos modelos usando o cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx).

-   Use o cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar o modelo para um arquivo .XML que você possa editar a fim de adicionar o grupo e os direitos de "AllStaff" aos grupos e direitos existentes e use o cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para importar essa mudança de volta para o Azure RMS.

> [!NOTE] Esse grupo equivalente ao "AllStaff" não é exatamente o mesmo que o grupo QUALQUER PESSOA no AD RMS: o grupo "AllStaff" inclui todos os usuários em seu locatário do Azure, considerando que o grupo QUALQUER PESSOA inclui todos os usuários autenticados, que poderiam estar fora da sua organização.
> 
> Devido a esta diferença entre os dois grupos, talvez seja necessário também adicionar usuários externos, além do grupo "AllStaff". Atualmente, não há suporte para endereços de email externos para grupos.

Os modelos que você importar do AD RMS terão a aparência e o comportamento iguais aos modelos personalizados que você pode criar no Portal clássico do Azure. Para alterar os modelos importados de modo que sejam publicados para que os usuários possam vê-los e selecioná-los nos aplicativos, ou para fazer outras mudanças nos modelos, confira [Configurando modelos personalizados do Azure Rights Management](../deploy-use/configure-custom-templates.md).

> [!TIP]
> Para dar aos usuários uma experiência mais consistente durante o processo de migração, não faça alterações aos modelos importados além destas duas alterações; e não publique os dois modelos padrão fornecidos com o Azure RMS nem crie novos modelos no momento. Em vez disso, aguarde a conclusão do processo de migração e encerre os servidores AD RMS.

### Exemplo de script do Windows PowerShell para identificar modelos do AD RMS que incluem o grupo ANYONE
Esta seção contém o script de exemplo para ajudar a identificar modelos do AD RMS que têm o grupo ANYONE definido, conforme descrito na seção anterior.

**Aviso de isenção de responsabilidade:** não há suporte para esse exemplo de script em nenhum serviço ou programa de suporte padrão da Microsoft. Esse exemplo de script é fornecido COMO ESTÁ sem garantias de qualquer tipo.*

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```


## Próximas etapas
Acesse a [fase 2 - configuração do lado do cliente](migrate-from-ad-rms-phase2.md).



<!--HONumber=May16_HO3-->


