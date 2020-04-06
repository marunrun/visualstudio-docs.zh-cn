---
title: 如何：向对象管理器注册库 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- libraries, registering with object manager
- IVsLibrary2 interface, registering library with object manager
- IVsSimpleLibrary2 interface, registering library with object manager
- IVsObjectManager2 interface, registering library with object manager
- libraries, symbol-browsing tools
ms.assetid: f124dd05-cb0f-44ad-bb2a-7c0b34ef4038
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4bd1032d2ba67a0c0f3338560a80038ed3215531
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707945"
---
# <a name="how-to-register-a-library-with-the-object-manager"></a>如何：向对象管理器注册库
符号浏览工具（如**类视图**、**对象浏览器**、**调用浏览器**和**查找符号结果**）使您能够查看项目或外部组件中的符号。 这些符号包括命名空间、类、接口、方法和其他语言元素。 库跟踪这些符号，并将其公开给使用数据填充工具[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的对象管理器。

 对象管理器跟踪所有可用的库。 在提供符号浏览工具的符号之前，每个库都必须向对象管理器注册。

 通常，在 VSPackage 加载时注册库。 但是，可以根据需要在另一时间完成。 当 VSPackage 关闭时，您将取消注册库。

 要注册库，请使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterLibrary%2A>。 对于托管代码库，请使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>。

 要取消注册库，请使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A>。

 要获取对对象管理器的引用，<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>将<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>服务 ID 传递给`GetService`方法。

## <a name="register-and-unregister-a-library-with-the-object-manager"></a>向对象管理器注册和取消注册库

### <a name="to-register-a-library-with-the-object-manager"></a>向对象管理器注册库

1. 创建库。

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

2. 获取对<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>类型对象的引用，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>方法。

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

### <a name="to-unregister-a-library-with-the-object-manager"></a>向对象管理器取消注册库

1. 获取对<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>类型对象的引用，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A>方法。

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
- [传统语言服务可扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
