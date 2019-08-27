---
title: 演练：获取一系列安装代码片段 （旧版实现） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- snippets, retrieving list
- code snippets, retrieving list
- GetSnippets method
ms.assetid: 7d142f8b-35b1-44c4-a13e-f89f6460c906
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 256430c0e41bfc0452282c89407335d997cc715c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440757"
---
# <a name="walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation"></a>演练：获取包含已安装的代码片段的列表（旧版实现）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

代码段是一段代码可以插入到源缓冲区 （它允许选择安装的代码片段的列表） 的菜单命令或通过从 IntelliSense 完成列表中选择代码片段快捷方式。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.EnumerateExpansions%2A>方法可获取特定语言 GUID 的所有代码片段。 这些代码段的快捷方式可以插入到 IntelliSense 完成列表。  
  
 请参阅[旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)有关托管的包框架 (MPF) 语言服务中实现代码片段的详细信息。  
  
### <a name="to-retrieve-a-list-of-code-snippets"></a>若要检索的代码段的列表  
  
1. 下面的代码演示如何获取给定语言的代码段的列表。 结果存储在一个数组中<xref:Microsoft.VisualStudio.TextManager.Interop.VsExpansion>结构。 此方法使用静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法以获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager>接口从<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>服务。 但是，还可以使用服务提供商提供给你的 VSPackage 和调用<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>方法。  
  
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
  
### <a name="to-call-the-getsnippets-method"></a>若要调用 GetSnippets 方法  
  
1. 下面的方法演示如何调用`GetSnippets`方法在分析操作完成。 <xref:Microsoft.VisualStudio.Package.LanguageService.OnParseComplete%2A>之后的分析操作中，原因是启动调用方法<xref:Microsoft.VisualStudio.Package.ParseReason>。  
  
> [!NOTE]
> `expansionsList`数组 listis 出于性能原因缓存。 停止并重新加载语言服务之前，在列表中不反映对这些代码片段更改 (例如，通过停止并重新启动[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)])。  
  
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
  
### <a name="to-use-the-snippet-information"></a>若要使用的代码段信息  
  
1. 下面的代码演示如何使用返回的代码段信息`GetSnippets`方法。 `AddSnippets`从用于填充的代码片段列表的任何分析原因响应中的分析器调用方法。 这应发生后第一次完成了完整的分析。  
  
     `AddDeclaration`方法可生成更高版本显示完成列表中声明的列表。  
  
     `TestDeclaration`类包含所有可完成列表，以及声明的类型中显示的信息。  
  
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
 [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)
