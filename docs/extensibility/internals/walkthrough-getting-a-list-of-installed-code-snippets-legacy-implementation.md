---
title: 获取已安装代码段的列表 (旧) |Microsoft Docs
description: 了解如何获取特定语言 GUID 的所有代码片段。 这些代码段的快捷方式可以插入 IntelliSense 完成列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, retrieving list
- code snippets, retrieving list
- GetSnippets method
ms.assetid: 7d142f8b-35b1-44c4-a13e-f89f6460c906
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 390f8e7030d0e758eb27fce4e83a30e30fbf64af
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487889"
---
# <a name="walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation"></a>演练：获取包含已安装的代码片段的列表（旧版实现）
代码段是一段代码，可以使用菜单命令将其插入到源缓冲区中 (这允许在已安装的代码段列表中进行选择) 或从 IntelliSense 完成列表中选择代码段快捷方式。

 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.EnumerateExpansions%2A>方法获取特定语言 GUID 的所有代码段。 这些代码段的快捷方式可以插入 IntelliSense 完成列表。

 有关在托管包框架中实现代码片段的详细信息，请参阅 [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md) (MPF) Language service。

### <a name="to-retrieve-a-list-of-code-snippets"></a>检索代码段列表

1. 下面的代码演示如何获取给定语言的代码段列表。 结果存储在结构的数组中 <xref:Microsoft.VisualStudio.TextManager.Interop.VsExpansion> 。 此方法使用静态 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> 从服务获取接口 <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 。 但是，还可以使用提供给 VSPackage 的服务提供程序，并调用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 方法。

    ```csharp
    using System;
    using System.Collections;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Package;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.TextManager.Interop;

    [Guid("00000000-0000-0000-0000-000000000000")] //create a new GUID for the language service
    namespace TestLanguage
    {
        class TestLanguageService : LanguageService
        {
            private void GetSnippets(Guid languageGuid,
                                     ref ArrayList expansionsList)
            {
                IVsTextManager textManager = (IVsTextManager)Package.GetGlobalService(typeof(SVsTextManager));
                if (textManager != null)
                {
                    IVsTextManager2 textManager2 = (IVsTextManager2)textManager;
                    if (textManager2 != null)
                    {
                        IVsExpansionManager expansionManager = null;
                        textManager2.GetExpansionManager(out expansionManager);
                        if (expansionManager != null)
                        {
                            // Tell the environment to fetch all of our snippets.
                            IVsExpansionEnumeration expansionEnumerator = null;
                            expansionManager.EnumerateExpansions(languageGuid,
                            0,     // return all info
                            null,    // return all types
                            0,     // return all types
                            1,     // include snippets without types
                            0,     // do not include duplicates
                            out expansionEnumerator);
                            if (expansionEnumerator != null)
                            {
                                // Cache our expansions in a VsExpansion array
                                uint count   = 0;
                                uint fetched = 0;
                                VsExpansion expansionInfo = new VsExpansion();
                                IntPtr[] pExpansionInfo   = new IntPtr[1];

                                // Allocate enough memory for one VSExpansion structure. This memory is filled in by the Next method.
                                pExpansionInfo[0] = Marshal.AllocCoTaskMem(Marshal.SizeOf(expansionInfo));

                                expansionEnumerator.GetCount(out count);
                                for (uint i = 0; i < count; i++)
                                {
                                    expansionEnumerator.Next(1, pExpansionInfo, out fetched);
                                    if (fetched > 0)
                                    {
                                        // Convert the returned blob of data into a structure that can be read in managed code.
                                        expansionInfo = (VsExpansion)Marshal.PtrToStructure(pExpansionInfo[0], typeof(VsExpansion));

                                        if (!String.IsNullOrEmpty(expansionInfo.shortcut))
                                        {
                                            expansionsList.Add(expansionInfo);
                                        }
                                    }
                                }
                                Marshal.FreeCoTaskMem(pExpansionInfo[0]);
                            }
                        }
                    }
                }
            }
        }
    }
    ```

### <a name="to-call-the-getsnippets-method"></a>调用 GetSnippets 方法

1. 下面的方法演示如何 `GetSnippets` 在分析操作完成时调用方法。 此 <xref:Microsoft.VisualStudio.Package.LanguageService.OnParseComplete%2A> 方法在使用原因启动的分析操作后调用 <xref:Microsoft.VisualStudio.Package.ParseReason> 。

> [!NOTE]
> `expansionsList`出于性能原因，将缓存数组列表。 代码段的更改不会反映在列表中，直到语言服务停止并重新加载 (例如，通过停止并重新启动 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]) 。

```csharp
class TestLanguageService : LanguageService
{
    private ArrayList expansionsList;

    public override void OnParseComplete(ParseRequest req)
    {
        if (this.expansionsList == null)
        {
            this.expansionsList = new ArrayList();
            GetSnippets(this.GetLanguageServiceGuid(),
                ref this.expansionsList);
        }
    }
}
```

### <a name="to-use-the-snippet-information"></a>使用代码段信息

1. 下面的代码演示如何使用方法返回的代码段信息 `GetSnippets` 。 `AddSnippets`从分析器调用方法，以响应用于填充代码段列表的任何分析原因。 这应在第一次完成完全分析之后发生。

     `AddDeclaration`方法生成稍后显示在完成列表中的声明列表。

     `TestDeclaration`类包含可以在完成列表中显示的所有信息以及声明类型。

    ```csharp
    class TestAuthoringScope : AuthoringScope
    {
        public void AddDeclarations(TestDeclaration declaration)
        {
            if (m_declarations == null)
                m_declarations = new List<TestDeclaration>();
            m_declarations.Add(declaration);
         }
    }
    class TestDeclaration
    {
        private string m_name;
        private string m_description;
        private string m_type;

        public TestDeclaration(string name, string desc, string type)
        {
            m_name = name;
            m_description = desc;
            m_type = type;
        }

    class TestLanguageService : LanguageService
    {
        internal void AddSnippets(ref TestAuthoringScope scope)
        {
            if (this.expansionsList != null && this.expansionsList.Count > 0)
            {
                int count = this.expansionsList.Count;
                for (int i = 0; i < count; i++)
                {
                    VsExpansion expansionInfo = (VsExpansion)this.expansionsList[i];
                    scope.AddDeclaration(new TestDeclaration(expansionInfo.title,
                         expansionInfo.description,
                         "snippet"));
                }
            }
        }
    }

    ```

## <a name="see-also"></a>请参阅
- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)
