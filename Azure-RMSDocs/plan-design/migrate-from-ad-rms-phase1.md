---
# required metadata

title: Migrar do AD RMS para o Azure Rights Management – Fase 1 | Azure RMS
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

# Fase de migração 1 – configuração do lado do servidor para o AD RMS

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*

Utilize as seguintes informações para a Fase 1 da migração do AD RMS para o Azure Rights Management (Azure RMS). Estes procedimentos abrangem os passos 1 a 4 de [Migrar do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passo 1: transferir a Ferramenta de Administração do Azure Rights Management
Aceda ao Centro de Transferências da Microsoft e transfira a [Ferramenta de Administração do Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721), que contém o módulo de administração do Azure RMS para o Windows PowerShell.

Instale a ferramenta. Para obter instruções, consulte [Instalar o Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

## Passo 2. exportar os dados de configuração do AD RMS e importá-los para o Azure RMS
Este passo divide-se em duas partes:

1.  Exportar os dados de configuração do AD RMS através da exportação dos domínios de publicação fidedignos (TPD) para um ficheiro. xml. Este processo é igual para todas as migrações.

2.  Importar os dados de configuração para o Azure RMS Existem diferentes processos para este passo consoante a configuração da implementação atual do AD RMS e a topologia preferida para a sua chave de inquilino do Azure RMS.

### Exportar os dados de configuração do AD RMS
Efetue o seguinte procedimento em todos os clusters do AD RMS de todos os domínios de publicação fidedignos que possuem conteúdos protegidos da sua organização. Não tem de o executar em clusters só de licenciamento.

> [!NOTE] Se estiver a utilizar a Gestão de Direitos do Windows Server 2003, em vez de seguir estas instruções, siga o procedimento [Exportar a chave privada do SLC, do TUD, do TPD e do RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) do artigo [Migrar do Windows RMS para o AD RMS numa Infraestrutura Diferente](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx).

#### Para exportar os dados de configuração (informações de domínio de publicação fidedigno)

1.  Inicie sessão no cluster do AD RMS como utilizador com permissões de administração do AD RMS.

2.  Na consola de gestão do AD RMS (**Serviços de Gestão de Direitos do Active Directory**), expanda o nome do cluster do AD RMS, expanda as **Políticas de Fidedignidade** e, em seguida, clique em **Domínios de Publicação Fidedignos**.

3.  No painel de resultados, selecione o domínio de publicação fidedigno e, em seguida, no painel Ações, clique em **Exportar Domínio de Publicação Fidedigno**.

4.  Na caixa de diálogo **Exportar Domínio de Publicação Fidedigno**:

    -   Clique em **Guardar Como** e guarde no caminho e com um nome de ficheiro à sua escolha. Certifique-se de que especifica **. xml** a extensão de nome de ficheiro (esta não é acrescentada automaticamente).

    -   Especifique e confirme uma palavra-passe segura. Lembre-se desta palavra-passe, dado que precisará dela mais tarde quando importar os dados de configuração para o Azure RMS.

    -   Não selecione a caixa de verificação para guardar o ficheiro de domínio fidedigno na versão 1.0 do RMS.

Após exportar todos os domínios de publicação fidedignos, estará pronto para iniciar a importação destes dados para o módulo de hardware de segurança do Azure RMS (HSM) da Thales. Para mais informações, 

### Importar os dados de configuração para o Azure RMS
Os processos exatos para este passo dependem da configuração da sua implementação atual do AD RMS e da topologia preferida para a sua chave de inquilino do Azure RMS.

A sua implementação atual do AD RMS utilizará uma das seguintes configurações para a sua chave do certificado de licenciante para servidor (SLC):

-   Proteção por palavra-passe na base de dados do AD RMS. Esta é a configuração predefinida.

-   Proteção HSM através da utilização de um módulo de hardware de segurança (HSM) da Thales.

-   Proteção HSM através da utilização de um módulo de hardware de segurança (HSM) de um fornecedor diferente da Thales.

-   Proteção por palavra-passe através de um fornecedor de serviços de criptografia externo.

> [!NOTE] Para mais informações sobre a utilização de módulos de hardware de segurança com o AD RMS, consulte [Utilizar o AD RMS com Módulos de Hardware de Segurança](http://technet.microsoft.com/library/jj651024.aspx).

As duas opções de topologia de chaves de inquilino do Azure RMS estão relacionadas com o facto de a sua chave de inquilino poder ser gerida pela Microsoft (**gerida pela Microsoft**) ou por si (**gerida pelo cliente**). Quando faz a gestão da sua própria chave de inquilino do AD RMS, essa gestão é por vezes referida como "bring your own key" (BYOK – Traga a Sua Própria Chave) e requer um módulo de hardware de segurança (HSM) da Thales. Para mais informações, consulte [Planear e implementar a sua chave de inquilino do Azure Rights Management](plan-implement-tenant-key.md).

> [!IMPORTANT]
> O Exchange Online não é atualmente compatível com o Azure RMS BYOK.  Se quer utilizar o BYOK após a migração e tenciona utilizar o Exchange Online, certifique-se de que compreende como esta configuração reduz a funcionalidade IRM no Exchange Online. Reveja as informações em [BYOK pricing and restrictions (Preços e restrições do BYOK – em inglês)](byok-price-restrictions.md) para o ajudar a escolher a melhor topologia de chaves de inquilino do Azure RMS para a sua migração.

Utilize a seguinte tabela para identificar o procedimento a utilizar para a sua migração. As combinações que não estão listadas não são suportadas.

|Implementação atual do AD RMS|Topologia de chaves de inquilino do Azure RMS selecionada|Instruções de migração|
|-----------------------------|----------------------------------------|--------------------------|
|Proteção por palavra-passe na base de dados do AD RMS|Gerida pela Microsoft|Consulte o procedimento de migração **Chave protegida por software para chave protegida por software** que se encontra após esta tabela.<br /><br />Este é o caminho de migração mais simples e requer apenas que transfira os seus dados de configuração para o Azure RMS.|
|Proteção HSM através da utilização de um módulo de hardware de segurança (HSM) nShield da Thales.|Gerida pelo cliente (BYOK)|Consulte o procedimento de migração **Chave protegida por HMS para chave protegida por HMS ** que se encontra após esta tabela.<br /><br />Para este procedimento, é necessário o conjunto de ferramentas BYOK e seguir dois conjuntos de passos para transferir a chave do seu HSM no local para os HSMs do RMS do Azure e, em seguida, transferir os seus dados de configuração para o Azure RMS.|
|Proteção por palavra-passe na base de dados do AD RMS|Gerida pelo cliente (BYOK)|Consulte o procedimento de migração **Chave protegida por software para chave protegida por HMS ** que se encontra após esta tabela.<br /><br />Para este procedimento, é necessário o conjunto de ferramentas BYOK e seguir três conjuntos de passos para, em primeiro lugar, extrair a sua chave de software e importá-la para um HSM no local; em seguida, transferir a chave do seu HSM no local para os HSMs do Azure RMS e, por último, transferir os seus dados de configuração para o Azure RMS.|
|Proteção HSM através da utilização de um módulo de hardware de segurança (HSM) a partir de um fornecedor que não seja a Thales|Gerida pelo cliente (BYOK)|Contacte o seu fornecedor do HSM para obter instruções sobre como transferir a chave deste HSM para um Módulo de Hardware de Segurança (HSM) nShield da Thales. Em seguida, siga as instruções do procedimento de migração **Chave protegida por HMS para chave protegida por HMS** que se encontram após esta tabela.|
|Proteção por palavra-passe através de um fornecedor de serviços de criptografia externo|Gerida pelo cliente (BYOK)|Contacte o seu fornecedor de serviços de criptografia para obter instruções sobre como transferir a sua chave para um Módulo de Hardware de Segurança (HSM) nShield da Thales. Em seguida, siga as instruções do procedimento de migração **Chave protegida por HMS para chave protegida por HMS** que se encontram após esta tabela.|
Antes de iniciar estes procedimentos, certifique-se de que consegue aceder aos ficheiros. xml que criou anteriormente, quando exportou os domínios de publicação fidedignos. Estes poderão estar guardados, por exemplo, numa pen USB que pode ser movida do servidor do AD RMS para uma estação de trabalho com ligação à Internet.

> [!NOTE] Independentemente da forma como guarda estes ficheiros, siga os procedimentos de segurança recomendados para os proteger, uma vez que estes dados incluem a sua chave privada.


Para concluir o passo 2, escolha e selecione as instruções para o seu caminho de migração: 


- [Software key to software key (Chave de software para chave de software – em inglês)](migrate-softwarekey-to-softwarekey.md)
- [HSM key to HSM key (Chave HSM para chave HSM – em inglês)](migrate-hsmkey-to-hsmkey.md)
- [Software key to HSM key (Chave de software para chave HSM – em inglês)](migrate-softwarekey-to-hsmkey.md)


## Passo 3: ativar o seu inquilino do RMS
As instruções para este passo encontram-se descritas na íntegra no artigo [Activating Azure Rights Management (Ativar o Azure Rights Management – em inglês)](../deploy-use/activate-service.md).


> [!TIP]
> Se tiver uma subscrição do Office 365, pode ativar o Azure RMS a partir do centro de administração do Office 365 ou do portal clássico do Azure. Recomendamos que utilize o portal clássico do Azure, dado que irá utilizar este portal de gestão para concluir o passo seguinte.

**E se o inquilino do Azure RMS já estiver ativado?** Se o serviço Azure RMS já estiver ativado na sua organização, os utilizadores poderão já ter utilizado o Azure RMS para proteger conteúdos com uma chave de inquilino gerada automaticamente (e com os modelos predefinidos) em vez das chaves (e modelos) existentes do AD RMS. É pouco provável que tal ocorra em computadores que são bem geridos na sua intranet, dado que estes serão automaticamente configurados para a sua infraestrutura do AD RMS. No entanto, esta situação pode ocorrer em computadores de grupo de trabalho ou em computadores que raramente estabelecem ligação à sua intranet. Infelizmente, também é difícil identificar estes computadores, razão pela qual recomendamos que não ative o serviço antes de importar os dados de configuração do AD RMS.

Se o seu inquilino do Azure RMS já estiver ativado e conseguir identificar estes computadores, certifique-se de que executa o script CleanUpRMS_RUN_Elevated.cmd nestes computadores, conforme descrito no passo 5. A execução deste script força-os a reinicializar o ambiente do utilizador para que seja possível transferir a chave de inquilino atualizada e os modelos importados.

## Passo 4. configurar modelos importados
Como os modelos que importou estão predefinidos para o estado **Arquivado**, tem de alterar este estado para **Publicado** se quiser que os utilizadores possam utilizar estes modelos com o Azure RMS.

Além disso, se os seus modelos no AD RMS utilizaram o grupo **ANYONE**, este grupo será removido automaticamente quando importar os modelos para o Azure RMS, pelo que tem de adicionar manualmente o grupo ou os utilizadores equivalentes, bem como adicionar os mesmos direitos aos modelos importados. O grupo equivalente do Azure RMS é designado por **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<tenant_name>.onmicrosoft.com**. Por exemplo, para a Contoso, este grupo poderá ser algo semelhante a **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**

Se não tiver a certeza se os seus modelos do AD RMS incluem o grupo ANYONE, pode utilizar o script de exemplo do Windows PowerShell para identificar estes modelos. Para obter mais informações sobre como utilizar o Windows PowerShell com o AD RMS, consulte [Utilizar o Windows PowerShell para Administrar o AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

Pode ver o grupo automaticamente criado da sua organização se copiar um dos modelos da política de direitos predefinidos no portal clássico do Azure e, em seguida, identificar o **NOME DE UTILIZADOR** na página **DIREITOS**. No entanto, não pode utilizar o portal clássico para adicionar este grupo a um modelo criado ou importado manualmente. Em vez disso, tem de utilizar uma das seguintes opções do PowerShell do Azure RMS:

-   Utilize o cmdlet PowerShell [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para definir os direitos e o grupo "AllStaff" como um objeto de definição de direitos e execute novamente este comando para cada um dos outros grupos ou utilizadores aos quais já foram concedidos direitos no modelo original juntamente com o grupo ANYONE. Em seguida, adicione os objetos de definição de direitos aos modelos através do cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx).

-   Utilize o cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar o modelo para um ficheiro .XML que consiga editar para adicionar os direitos e o grupo “AllStaff” aos grupos e direitos existentes e, em seguida, utilize o cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para voltar a importar esta alteração para o Azure RMS.

> [!NOTE] Este grupo equivalente "AllStaff" não é exatamente igual ao grupo ANYONE no AD RMS. O grupo "AllStaff" inclui todos os utilizadores no seu inquilino do Azure, ao passo que o grupo ANYONE inclui todos os utilizadores autenticados, que podem estar fora da sua organização.
> 
> Devido a esta diferença entre os dois grupos, é possível que também tenha de adicionar utilizadores externos, além do grupo "AllStaff". Atualmente, não são suportados endereços de e-mails externos para grupos.

Os modelos que importa do AD RMS assemelham-se e comportam-se tal como os modelos personalizados que pode criar no portal clássico do Azure. Para alterar modelos importados a publicar para que os utilizadores os possam ver e selecionar a partir de aplicações ou para fazer outras alterações aos modelos, consulte [Configurar modelos personalizados para o Azure Rights Management](../deploy-use/configure-custom-templates.md).

> [!TIP]
> Para que os utilizadores tenham uma experiência mais consistente durante o processo de migração, não altere os modelos importados, com exceção destas duas alterações e não publique os dois modelos predefinidos que vêm com o Azure RMS nem crie novos modelos nessa altura. Em vez disso, aguarde até que o processo de migração seja concluído e até ter encerrado os servidores do AD RMS.

### Script de exemplo do Windows PowerShell para identificar modelos do AD RMS que incluem o grupo ANYONE
Esta secção contém o script de exemplo para o ajudar a identificar modelos do AD RMS que têm o grupo ANYONE definido, conforme descrito na secção anterior.

**Exclusão de responsabilidade:** este script de exemplo não é suportado por nenhum serviço ou programa de suporte padrão da Microsoft. Este script de exemplo é fornecido TAL COMO ESTÁ, sem qualquer tipo de garantias.*

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


## Passos seguintes
Vá para a [fase 2 - configuração do lado do cliente](migrate-from-ad-rms-phase2.md).



<!--HONumber=May16_HO3-->


