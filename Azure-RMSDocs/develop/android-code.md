---
title: "Exemplos de código do Android | Azure RMS"
description: "Este tópico apresenta-lhe elementos de código importantes para a versão Android do SDK RMS."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 5d8c7ab53f76005d7efbfd2d795da08e41f83941


---

# Exemplos de código do Android

Este tópico apresenta-lhe elementos de código importantes para a versão Android do SDK RMS.

**Nota** No código de exemplo e nas descrições que se seguem, utilizamos o termo MSIPC (Microsoft Information Protection and Control) para referir o processo de cliente.


## Utilizar o SDK Microsoft Rights Management 4.2 – cenários principais

Seguem-se exemplos de código de uma aplicação de exemplo maior que representam cenários de desenvolvimento importantes para se orientar neste SDK. Estes demonstram a utilização do formato de Ficheiro Protegido da Microsoft referido como ficheiro protegido, a utilização de formatos de ficheiros protegidos personalizados e a utilização de controlos de IU personalizados.



A aplicação de exemplo, *MSIPCSampleApp*, está disponível para utilização com este SDK para o sistema operativo Android. Consulte [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android) no GitHub para ter acesso a esta aplicação de exemplo.

### Cenário: consumir um ficheiro de RMS protegido

-   **Passo 1**: criar um [**ProtectedFileInputStream**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedfileinputstream_class_java)

    **Origem**: *MsipcAuthenticationCallback.java*

    **Descrição**: instanciar um objeto [**ProtectedFileInputStream**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedfileinputstream_class_java) através do respetivo método de criação que implementa o serviço de autenticação através do [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) para obter um token transferindo uma instância de **AuthenticationRequestCallback** como o parâmetro *mRmsAuthCallback* para a API de MSIPC. Consulte a chamada para [**ProtectedFileInputStream.create**](/rights-management/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_method) perto do fim da seguinte secção de código de exemplo.

        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }  
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }


-   **Passo 2**: configurar a autenticação com a Active Directory Authentication Library (ADAL).

    **Origem**: *MsipcAuthenticationCallback.java*.

    **Descrição**: neste passo, verá a ADAL utilizada para implementar um [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) com parâmetros de autenticação de exemplo. Para obter mais informações sobre a utilização da ADAL, consulte [Biblioteca de Autenticação do Azure AD (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx).


        class MsipcAuthenticationCallback implements AuthenticationRequestCallback
        {

        …

        @Override
        public void getToken(Map<String, String> authenticationParametersMap,
                             final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
        {
            String authority = authenticationParametersMap.get("oauth2.authority");
            String resource = authenticationParametersMap.get("oauth2.resource");
            String userId = authenticationParametersMap.get("userId");
            final String userHint = (userId == null)? "" : userId;
            AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
            if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
            {
                try
                {
                    authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                    App.getInstance().setAuthenticationContext(authenticationContext);
                }
                catch (NoSuchAlgorithmException e)
                {
                    …
                    authenticationCompletionCallbackToMsipc.onFailure();
                }
                catch (NoSuchPaddingException e)
                {
                    …
                    authenticationCompletionCallbackToMsipc.onFailure();
                }
           }
            App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                           "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                            {
                                @Override
                                public void onError(Exception exc)
                                {
                                    …
                                    if (exc instanceof AuthenticationCancelError)
                                    {
                                         …
                                        authenticationCompletionCallbackToMsipc.onCancel();
                                    }
                                    else
                                    {
                                         …
                                        authenticationCompletionCallbackToMsipc.onFailure();
                                    }
                                }

                                @Override
                                public void onSuccess(AuthenticationResult result)
                                {
                                    …
                                    if (result == null || result.getAccessToken() == null
                                            || result.getAccessToken().isEmpty())
                                    {
                                         …
                                    }
                                    else
                                    {
                                        // request is successful
                                        …
                                        authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                    }
                                }
                            }

                            );
                      }


-   **Passo 3**: verificar se o direito **Editar** existe para o utilizador com este conteúdo através do método [**accessCheck**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_accesscheck_method_java) de [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy).

    **Origem**: *TextEditorFragment.java*


         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }


### Cenário: criar um novo ficheiro protegido através de um modelo

Este cenário começa com a obtenção de uma lista de modelo ao selecionar o primeiro para criar uma política e, em seguida, ao cria e escreve no novo ficheiro protegido.

-   **Passo 1**: obter lista de modelos através de um objeto [**TemplateDescriptor**](/rights-management/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_class_java).

    **Origem**: *MsipcTaskFragment.java*



    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      }; try { …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) { …
      }


-    **Passo 2**: criar um [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) utilizando o primeiro modelo na lista.

    **Origem**: *MsipcTaskFragment.java*



      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      }; try { …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback); …
      } catch (InvalidParameterException e) { …
      }


-    **Passo 3**: criar um [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java) e escrever o conteúdo no mesmo.

    **Origem**: *MsipcTaskFragment.java*


    private void createPTxt(final byte[] contentToProtect) { …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>() { @Override public Context getContext() { …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }



### Cenário: abrir um ficheiro protegido personalizado

-   **Passo 1**: criar um [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) a partir de um *serializedContentPolicy*.

    **Origem**: *MsipcTaskFragment.java*


    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>() { @Override public void onSuccess(UserPolicy userPolicy) { …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };


    try {   ...

      // Read the serializedContentPolicyLength from the inputStream.
      long serializedContentPolicyLength = readUnsignedInt(inputStream);

      // Read the PL bytes from the input stream using the PL size.
      byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength]; inputStream.read(serializedContentPolicy);

      ...

      UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,           userPolicyCreationCallbackFromSerializedContentPolicy); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {   ... } catch (IOException e) {   ... }



-    **Passo 2**: criar um [**CustomProtectedInputStream**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_class_java) utilizando o [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) do **Passo 1**.

    **Origem**: *MsipcTaskFragment.java*



      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>() { @Override public Context getContext() { …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try {  ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,                                 encryptedContentLength,                                 customProtectedInputStreamCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {  ... } catch (IOException e) {  ... }


-    **Passo 3**: ler conteúdo do [**CustomProtectedInputStream**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_class_java) para *mDecryptedContent* e fechar.

    **Origem**: *MsipcTaskFragment.java*


    @Override public void onSuccess(CustomProtectedInputStream customProtectedInputStream) {  mUserPolicy = customProtectedInputStream.getUserPolicy();  ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try  {    while ((nRead = customProtectedInputStream.read(dataChunk, 0,                                                        dataChunk.length)) != -1)    {       buffer.write(dataChunk, 0, nRead);    }

        buffer.flush();    mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();    customProtectedInputStream.close();  }  catch (IOException e)  {    ...  } }


### Cenário: criar um ficheiro protegido personalizado utilizando uma política personalizada (ad hoc)

-   **Passo 1**: com um endereço de e-mail fornecido pelo utilizador, criar um descritor de política.

    **Origem**: *MsipcTaskFragment.java*

    **Descrição**: na prática, seria possível criar os seguintes objetos utilizando entradas do utilizador a partir da interface do dispositivo; [**UserRights**](/rights-management/sdk/4.2/api/android/userrights#msipcthin2_userrights_class_java) e [**PolicyDescriptor**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java).



      // create userRights list   UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),     Arrays.asList( CommonRights.View, EditableDocumentRights.Print));   ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();   usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list   PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(                                                          usersRigthsList);   policyDescriptor.setOfflineCacheLifetimeInDays(10);   policyDescriptor.setContentValidUntil(new Date());



-    **Passo 2**: criar um [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) personalizado do descritor de política *selectedDescriptor*.

    **Origem**: *MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,                                          mEmailId, mRmsAuthCallback,                                          UserPolicyCreationFlags.NONE,                                          userPolicyCreationCallback);



-   **Passo 3**: criar e escrever conteúdo para o [**CustomProtectedOutputStream**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_class_java) e fechar.

    **Origem**: *MsipcTaskFragment.java*


    File file = new File(filePath); final OutputStream outputStream = new FileOutputStream(file); CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>() { @Override public Context getContext() { …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }


 

 



<!--HONumber=Jul16_HO2-->


