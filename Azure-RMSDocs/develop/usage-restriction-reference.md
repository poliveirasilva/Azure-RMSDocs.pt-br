---
# required metadata

title: Referência de restrição de uso | Azure RMS
description: As restrições de uso são definidas pelas constantes listadas neste tópico.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 16E36039-0FD6-4A0A-82C8-2C9DB19D27DD
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Referência de restrição de uso

As restrições de uso são definidas pelas constantes listadas neste tópico.



Cada direito de usuário, listado na coluna à direita do AD RMS, tem uma descrição, um ponto de imposição e métodos de imposição sugeridos.

| Direitos do AD RMS | Descrição | Pontos de imposição comuns | Como impor |
|--------------|-------------|---------------------------|----------------|
|IPC_GENERIC_ALL |Concede todos os direitos de usuário.| Nenhum |Esse direito é usado pelo sistema e, de maneira geral, não deve ser verificado diretamente. <br><br> [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) usa esse direito para determinar se deve conceder ao usuário outros direitos, como neste exemplo.<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`
|IPC_GENERIC_READ |O direito de ler o conteúdo do documento.|Carregamento de documentos|Não carregar ou apresentar o conteúdo do documento|
|IPC_GENERIC_WRITE|O direito de editar o conteúdo do documento|Modificação de documento|Faz com que todos os controles da interface do usuário que podem ser usados para modificar o conteúdo do documento não possam ser editados. <br><br> Desabilita os itens de menu que disparam alterações de documento. **Editar** > **Recortar**, **Editar** > **Colar** e **Inserir** são exemplos típicos. <br><br>Desabilita os itens de menu de atalho que disparam alterações de documento.|
|Nenhum direito de AD RMS|O chamador não tem os direitos de AD RMS|Salvar|Desabilite o menu **Arquivo** > **Salvar**. <br><br> **Observação** Este direito não controla **Arquivo** > **Salvar Como** porque ele não representa uma alteração no documento original.<br><br> Desabilita qualquer atalho de teclado que pode ser usado para disparar um salvamento (por exemplo, Ctrl+S).<br><br> **Dica** Uma prática recomendada será atualizar o seu código **Arquivo** > **Salvar** principal para falhar se o usuário não tiver esse direito. Isso funcionará como uma rede de segurança se você perder os mecanismos de experiência do usuário que podem ser usados para disparar um salvamento.
|IPC_GENERIC_EXTRACT|O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato não protegido.|Copiar para a área de transferência|Desabilite o menu **Editar** > **Copiar**. Desabilite o menu **Editar** > **Cortar**. <br><br>Desabilite **Copiar** e **Recortar** dos menus de atalho.<br><br>Desabilite atalhos de teclado que podem ser usados para disparar uma cópia (por exemplo, Ctrl+C ou Ctrl+X).<br><br>Atualize manipuladores de mensagens de janela para [**WM_CUT**](https://msdn.microsoft.com/library/windows/desktop/ms649023) a fim de rejeitar a cópia de dados se o usuário não tem esse direito. Se a janela está usando o manipulador de mensagem fornecido pelo Windows padrão, coloque essa janela como subclasse e forneça seus próprios manipuladores para **WM_COPY** e **WM_CUT**.
|Nenhum direito de AD RMS|O chamador não tem os direitos de AD RMS|Salvar como|Na sua caixa de diálogo **Salvar como**, desabilite os formatos de arquivo que resultariam no salvamento do arquivo sem proteção RMS.|
|Nenhum direito de AD RMS|O chamador não tem os direitos de AD RMS|Alt+PrtScn|Chame [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) nas janelas que processam o conteúdo do documento.|
|IPC_GENERIC_EXPORT|O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato protegido do AD RMS diferente.|Salvar como|Na sua caixa de diálogo **Salvar como**, desabilite a capacidade de salvar em outros formatos de arquivo.<br><br>**Dica**Uma prática recomendada será atualizar seu código principal **Arquivo** > **Salvar Como** para falhar se o usuário tentar salvar esse arquivo em um formato diferente e não tiver esse direito. Isso funcionará como uma rede de segurança se você perder os mecanismos de experiência do usuário que podem ser usados para disparar um salvar como.|
|IPC_GENERIC_PRINT|O direito de imprimir o conteúdo do documento.|Imprimir|Desabilite o menu **Arquivo** > **Imprimir**.<br><br>Desabilita qualquer atalho de teclado que pode ser usado para disparar uma impressão (por exemplo, Ctrl+P).<br><br>Desabilite itens de menu de atalho que poderiam ser usados para disparar uma impressão.<br><br>**Dica** Uma prática recomendada será atualizar o seu principal código **Arquivo** > **Imprimir** para falhar se o usuário não tiver esse direito. Isso funcionará como uma rede de segurança se você perder os mecanismos de experiência do usuário que podem ser usados para disparar uma impressão.|
|IPC_GENERIC_COMMENT|Alguns aplicativos dão suporte à capacidade de adicionar comentários e anotações ao documento sem atualizar o conteúdo do documento principal.<br><br>Este direito dá ao usuário acesso a esse recurso.|Revisão > Inserir comentário <br><br> Revisão > Excluir Comentário | Desabilite os itens de menu que podem ser usados para modificar comentários ou anotações do documento. **Examinar** > **Inserir comentário** e **Examinar** > **Excluir Comentário** são exemplos. <br><br>Desabilite os atalhos de teclado que poderiam disparar a modificação de comentários do documento.<br><br>**Observação** Uma implementação padrão requer tanto **IPC_GENERIC_COMMENT** quanto **IPC_GENERIC_WRITE** para persistir novos comentários em um arquivo. Os aplicativos podem escolher adicionar suporte quando o direito **IPC_GENERIC_COMMENT** é concedido e o direito **IPC_GENERIC_WRITE**, não. Nesse caso, a permissão de permitir Salvar é concedida, desde que as modificações ao documento fiquem restringidas somente aos comentários.|
|IPC_VIEW_RIGHTS||N/D|Imposta pelo sistema. O sistema não permitirá que o desenvolvedor consulte a [**lista de direitos de usuário**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_user_rights_list) de uma licença, a não ser que esse direito seja concedido.
|IPC_EDIT_RIGHTS|Alguns aplicativos permitem que os usuários modifiquem o conjunto de usuários e direitos para conteúdo protegido por AD RMS.<br><br>Este direito dá ao usuário acesso a esse recurso.|Controle de interface do usuário de edição de direitos do aplicativo|Desabilite o acesso de usuário a qualquer interface de usuário que pode ser usada para editar a política do RMS para um documento.|

 

 

 


<!--HONumber=May16_HO2-->


