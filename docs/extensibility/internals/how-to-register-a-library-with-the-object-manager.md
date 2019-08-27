---
title: 如何：使用对象管理器注册库 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- libraries, registering with object manager
- IVsLibrary2 interface, registering library with object manager
- IVsSimpleLibrary2 interface, registering library with object manager
- IVsObjectManager2 interface, registering library with object manager
- libraries, symbol-browsing tools
ms.assetid: f124dd05-cb0f-44ad-bb2a-7c0b34ef4038
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7481b9710237bcd1e624b07f8985b5708f271bef
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312055"
---
# <a name="how-to-register-a-library-with-the-object-manager"></a>如何：与对象管理器注册库
符号浏览工具，如**类视图**，**对象浏览器**，**调用浏览器**并**查找符号结果**，可以查看在项目中或在外部组件的符号。 符号包括命名空间、 类、 接口、 方法和其他语言元素。 库跟踪这些符号和公开到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对象管理器填充的数据的工具。

 对象管理器跟踪的所有可用的库。 每个库必须注册对象管理器，在符号浏览工具提供符号之前。

 通常情况下，当加载 VSPackage 时注册库。 但是，它可以在另一个时根据需要。 当 VSPackage 关闭时注销库。

 若要注册一个库，请使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterLibrary%2A>方法。 对于托管的代码库，使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。

 若要取消注册一个库，请使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A>方法。

 若要获取对对象管理器，引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>，传递<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>服务 ID 到`GetService`方法。

## <a name="register-and-unregister-a-library-with-the-object-manager"></a>注册和注销对象管理器库

### <a name="to-register-a-library-with-the-object-manager"></a>若要向对象管理器注册库

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

### <a name="to-unregister-a-library-with-the-object-manager"></a>若要注销的对象管理器库

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
- [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [如何：公开库提供对对象管理器的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)