---
# required metadata

title: Cenário - Proteger arquivos em um compartilhamento de servidor de arquivos | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cenário - Proteger arquivos em um compartilhamento de servidor de arquivos
Este cenário e a documentação de usuário de suporte usam o Azure Rights Management para proteger em massa todos os arquivos que você deseja proteger em um servidor de arquivos, a fim de garantir que somente os funcionários de sua organização possam acessá-los, mesmo que eles sejam copiados e salvos em armazenamentos que não estejam sob controle de seu departamento de TI ou sejam enviados por email para outras pessoas.

Essas instruções usam um dos modelos padrão, que restringe o acesso a todos os funcionários com todos os direitos de uso. Mas, se for necessário, você pode restringir ainda mais os direitos de acesso e uso configurando um modelo personalizado em vez de usar um modelo padrão.

As instruções são adequadas para o seguinte conjunto de circunstâncias:

-   Você precisa proteger todos os tipos de arquivo e não apenas os arquivos do Office. Os arquivos que não podem ser protegidos nativamente pelo Azure RMS serão protegidos genericamente.

-   Todos os arquivos no caminho especificado (incluindo subpastas) serão protegidos.

-   Todos os arquivos passam por uma reaplicação agendada da proteção, a fim de garantir que as alterações nos modelos de política de direitos sejam aplicadas aos arquivos protegidos.

## Instruções de implantação
![](../media/AzRMS_AdminBanner.png)

Verifique se os requisitos a seguir foram aplicados e siga as instruções para os procedimentos de suporte antes de ir para a documentação do usuário.

## Requisitos para este cenário
Para que as instruções desse cenário funcionem, deve ser feito o seguinte:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Você sincronizou suas contas de usuário do Active Directory local com o Active Directory do Azure ou o Office 365, incluindo seu endereço de email. Isso é necessário para todos os usuários que talvez precisem acessar arquivos depois que eles foram protegidos pelo FCI e pelo Azure Rights Management.|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Um das seguintes condições:<br /><br />Para usar um modelo padrão para todos os usuários: Você não arquivou o padrão, &lt;nome da organização&gt; -Confidencial<br /><br />Para usar um modelo personalizado para usuários específicos: Você criou e publicou este modelo personalizado|[Configurando modelos personalizados do Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|O aplicativo Rights Management sharing é implantado nos computadores dos usuários que executam o Windows|[Implantação automática para o aplicativo de compartilhamento Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|Você baixou a ferramenta de Proteção do RMS e configurou os pré-requisitos para o Azure RMS|Para obter instruções sobre como baixar a ferramenta e seus pré-requisitos: [Cmdlets da Proteção do RMS](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />Para configurar os pré-requisitos adicionais para o Azure RMS, como a conta de entidade do serviço: [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### Configuração de um servidor de arquivos para proteger todos os arquivos usando o Azure RMS e o Gerenciador de Recursos de Servidor de Arquivos com a Infraestrutura de Classificação de Arquivos

1.  Inicie uma sessão do Windows PowerShell. Não é necessário executar essa sessão como administrador.

2.  Autentique no Azure RMS:

    ```
    Set-RMSServerAuthentication
    ```
    Quando receber uma solicitação, forneça os valores para a conta de entidade do serviço que você criou como pré-requisito para os cmdlets da Proteção do RMS.

3.  Execute o seguinte para identificar a ID do modelo que será usada para proteger os arquivos:

    ```
    Get-RMSTemplate
    ```
    Para usar o modelo padrão que restringe o acesso a todos os funcionários com todos os direitos de uso, procure o nome do modelo de **&lt;nome da organização&gt; - Confidencial**. Por exemplo, **VanArsdel, Ltd - Confidencial**.

4.  Siga as instruções passo a passo em [Proteção RMS com a FCI (Infraestrutura de Classificação de Arquivos) do Windows Server ](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx).

    Essas instruções incluem um script do Windows PowerShell que você especifica para ser executado como um executável personalizado no Gerenciador de Recursos do Servidor de Arquivos. As instruções também incluem como verificar se os arquivos estão protegidos pelo Azure Rights Management.

## Instruções sobre a documentação do usuário
Se os arquivos que você está protegendo forem somente arquivos do Office, não será necessário fornecer as instruções sobre os arquivos protegidos aos usuários. Quando os usuários autorizados abrem esses documentos, normalmente abrem no Office, com a única diferença de que os usuários podem receber uma solicitação de autenticação, e provavelmente verão uma barra de informações na parte superior do documento informando que o documento está protegido.

Se os arquivos protegidos tiverem uma extensão de nome de arquivo **.ppdf** ou se forem um arquivo de texto ou de imagem protegido (por exemplo, se tiverem uma extensão de nome de arquivo **.ptxt** ou **.pjpg**), esses arquivos agora serão somente leitura e não poderão ser editados. Os usuários podem exibi-los usando o visualizador do aplicativo de compartilhamento do RMS, que carrega automaticamente para esses tipos de arquivo. Esses arquivos são protegidos de forma nativa pelo Azure RMS e aplicam todas as configurações de política do modelo que você aplicou, exceto os direitos de uso, pois o próprio arquivo é somente leitura. A menos que você saiba que protegerá esses tipos de arquivo, é improvável que precise de instruções de usuário para esse cenário, mas avise a assistência técnica que talvez eles precisem explicar aos usuários o motivo de esses arquivos não poderem ser editados.

Se os arquivos protegidos tiverem uma extensão de nome de arquivo **.pfile**, os usuários poderão visualizá-los, mas eles deverão ser salvos com o nome do arquivo original (remova a extensão de nome de arquivo .pfile) se os usuários quiserem editar e salvar suas alterações. Esses arquivos estão genericamente protegidos pelo Azure RMS e não podem impor os direitos de uso do modelo que você aplicou, ou seja, a proteção será perdida se o arquivo for salvo com um novo nome. Este cenário precisará de instruções para os usuários.

Usando o modelo a seguir, copie e cole as instruções para os usuários finais para que eles saibam como editar arquivos genericamente protegidos. Faça essas modificações para refletir seu ambiente:

-   Substitua *&lt;tipo de arquivo&gt;* e *&lt;arquivo de compartilhamento do servidor&gt;* pelo tipo de arquivo que será protegido genericamente e pelo nome do compartilhamento de servidor de arquivo.

-   Substitua *&lt;nome da organização&gt;* pelo nome de sua organização, como ele é exibido em seus modelos do Azure Rights Management.

-   Substitua *&lt;nome de organização&gt;* pelo nome de sua organização.

-   Substitua *&lt;instruções de como salvar o arquivo e remover a extensão de nome de arquivo .pfile&gt;* pelas instruções específicas do aplicativo para este tipo de arquivo.

-   Substitua detalhes de contato por instruções de como os usuários podem entrar em contato com o suporte técnico, como um link de site, endereço de email ou número de telefone.

-   Faça modificações adicionais que você queira para esse conjunto de instruções e, em seguida, envie-o para esses usuários.

A documentação de exemplo mostra como essas instruções pode parecer para os usuários, após as personalizações.

![](../media/AzRMS_UsersBanner.png)

### Como editar &lt;tipo de arquivo&gt; do &lt;compartilhamento do servidor de arquivos&gt;

1.  Clique duas vezes no arquivo para abri-lo. Suas credenciais serão solicitadas.

2.  Você verá uma caixa de diálogo **Arquivo protegido** do aplicativo de compartilhamento do Microsoft Rights Management, que informa você sobre a necessidade de cumprir com as permissões para **&lt;nome de organização&gt; - Confidencial**. Isso significa que você não deve compartilhar esse documento com outras pessoas, se elas não trabalharem para &lt;nome da organização&gt;.

3.  Clique em **Abrir**.

4.  Para editar o arquivo, salve primeiro o arquivo e remova a extensão de nome de arquivo .pfile:

    -   &lt;Instruções sobre como salvar o arquivo e remover a extensão de nome de arquivo .pfile&gt;

5.  Agora você pode editar e salvar o arquivo como de costume.

Periodicamente, o arquivo será protegido novamente, o que adiciona novamente a extensão de nome de arquivo .pfile, e será necessário repetir essas etapas.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Exibir e usar os arquivos que foram protegidos](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Entre em contato com o suporte técnico:

    -   *&lt;detalhes do contato&gt;*

### Documentação do usuário personalizada de exemplo
![](../media/AzRMS_ExampleBanner.png)

#### Como editar desenhos em CAD no compartilhamento de ProjectNextGen

1.  Clique duas vezes no arquivo para abri-lo. Suas credenciais serão solicitadas.

2.  Você verá uma caixa de diálogo **Arquivo protegido** do aplicativo de compartilhamento do Microsoft Rights Management, que informa você sobre a necessidade de cumprir com as permissões para **VanArsdel, Ltd - Confidencial**. Isso significa que você não deve compartilhar esse documento com outras pessoas, se elas não trabalharem para VanArsdel, Ltd.

3.  Clique em **Abrir**.

4.  Para editar o arquivo, salve primeiro o arquivo e remova a extensão de nome de arquivo .pfile:

    -   **Arquivo** &gt; **Salvar como**

    -   Exclua **.pfile** do final do nome do arquivo e clique em **OK**.

5.  Agora você pode editar e salvar o arquivo como de costume.

Periodicamente, o arquivo será protegido novamente, o que adiciona novamente a extensão de nome de arquivo .pfile, e será necessário repetir essas etapas.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Exibir e usar os arquivos que foram protegidos](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contate o suporte técnico: helpdesk@vanarsdelltd.com



<!--HONumber=Apr16_HO4-->


