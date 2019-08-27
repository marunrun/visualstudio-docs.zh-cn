---
title: 如何：使用对象管理器注册库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- libraries, registering with object manager
- IVsLibrary2 interface, registering library with object manager
- IVsSimpleLibrary2 interface, registering library with object manager
- IVsObjectManager2 interface, registering library with object manager
- libraries, symbol-browsing tools
ms.assetid: f124dd05-cb0f-44ad-bb2a-7c0b34ef4038
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c40c695a912e97269263ba14747b72382847324d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162038"
---
# <a name="how-to-register-a-library-with-the-object-manager"></a>如何：使用对象管理器注册库
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

符号浏览工具，如**类视图**，**对象浏览器**，**调用浏览器**并**查找符号结果**，可以查看在项目中或在外部组件的符号。 符号包括命名空间、 类、 接口、 方法和其他语言元素。 库跟踪这些符号和公开到[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]对象管理器填充的数据的工具。  
  
 对象管理器跟踪的所有可用的库。 每个库必须注册对象管理器，在符号浏览工具提供符号之前。  
  
 通常情况下，当加载 VSPackage 时注册库。 但是，它可以在另一个时根据需要。 当 VSPackage 关闭时注销库。  
  
 若要注册一个库，请使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterLibrary%2A>方法。 在托管的代码库的情况下使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。  
  
 若要取消注册一个库，请使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A>方法。  
  
 若要获取对对象管理器，引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>，传递<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>服务 ID 到`GetService`方法。  
  
## <a name="registering-and-unregistering-a-library-with-the-object-manager"></a>注册和注销库与对象管理器  
  
#### <a name="to-register-a-library-with-the-object-manager"></a>若要向对象管理器注册库  
  
1. 创建一个库。  
  
    ```vb  
    Private m_CallBrowserLibrary As CallBrowser.Library = Nothing  
    Private m_nLibraryCookie As UInteger = 0  
    ' Create Library.  
    m_CallBrowserLibrary = New CallBrowser.Library()  
    ```  
  
    ```csharp  
    private CallBrowser.Library m_CallBrowserLibrary = null;  
    private uint m_nLibraryCookie = 0;  
    // Create Library.  
    m_CallBrowserLibrary = new CallBrowser.Library();  
  
    ```  
  
2. 获取对的对象的引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>类型并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。  
  
    ```vb  
    Private Sub RegisterLibrary()  
        If m_nLibraryCookie <> 0 Then  
            Throw New Exception("Library already registered with Object Manager")  
        End If  
  
        ' Obtain a reference to IVsObjectManager2 type object.  
        Dim objManager As IVsObjectManager2 = TryCast(GetService(GetType(SVsObjectManager)), IVsObjectManager2)  
        If objManager Is Nothing Then  
            Throw New NullReferenceException("GetService failed for SVsObjectManager")  
        End If  
  
        Try  
            Dim hr As Integer = objManager.RegisterSimpleLibrary(m_CallBrowserLibrary, m_nLibraryCookie)  
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr)  
        Catch e As Exception  
            ' Code to handle any CLS-compliant exception.  
            Trace.WriteLine(e.Message)  
            Throw  
        End Try  
    End Sub  
    ```  
  
    ```csharp  
    private void RegisterLibrary()  
    {  
        if (m_nLibraryCookie != 0)  
            throw new Exception("Library already registered with Object Manager");  
  
        // Obtain a reference to IVsObjectManager2 type object.  
        IVsObjectManager2 objManager =   
                          GetService(typeof(SVsObjectManager)) as IVsObjectManager2;  
        if (objManager == null)  
            throw new NullReferenceException("GetService failed for SVsObjectManager");  
  
        try  
        {  
            int hr =   
                objManager.RegisterSimpleLibrary(m_CallBrowserLibrary,   
                                                 out m_nLibraryCookie);  
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);  
        }  
        catch (Exception e)  
        {  
            // Code to handle any CLS-compliant exception.  
            Trace.WriteLine(e.Message);  
            throw;  
        }  
    }  
  
    ```  
  
#### <a name="to-unregister-a-library-with-the-object-manager"></a>若要注销的对象管理器库  
  
1. 获取对的对象的引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>类型并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A>方法。  
  
    ```vb  
    Private Sub UnregisterLibrary()  
        If m_nLibraryCookie <> 0 Then  
            ' Obtain a reference to IVsObjectManager2 type object.  
            Dim objManager As IVsObjectManager2 = TryCast(GetService(GetType(SVsObjectManager)), IVsObjectManager2)  
            If objManager Is Nothing Then  
                Throw New NullReferenceException("GetService failed for SVsObjectManager")  
            End If  
  
            Try  
                objManager.UnregisterLibrary(m_nLibraryCookie)  
            Catch e As Exception  
                ' Code to handle any CLS-compliant exception.  
                Trace.WriteLine(e.Message)  
                Throw  
            Finally  
                m_nLibraryCookie = 0  
            End Try  
        End If  
    End Sub  
    ```  
  
    ```csharp  
    private void UnregisterLibrary()  
    {  
        if (m_nLibraryCookie != 0)  
        {  
            // Obtain a reference to IVsObjectManager2 type object.  
            IVsObjectManager2 objManager = GetService(typeof(SVsObjectManager)) as IVsObjectManager2;  
            if (objManager == null)  
                throw new NullReferenceException("GetService failed for SVsObjectManager");  
  
            try  
            {  
                objManager.UnregisterLibrary(m_nLibraryCookie);  
            }  
            catch (Exception e)  
            {  
                // Code to handle any CLS-compliant exception.  
                Trace.WriteLine(e.Message);  
                throw;  
            }  
            finally  
            {  
                m_nLibraryCookie = 0;  
            }  
        }  
    }  
  
    ```  
  
## <a name="see-also"></a>请参阅  
 [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)   
 [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)   
 [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
