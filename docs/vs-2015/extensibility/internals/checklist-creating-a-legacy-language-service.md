---
title: 清单：创建旧版语言服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3b79afe64aafac473d4fe5d22464998d0c2f0537
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437617"
---
# <a name="checklist-creating-a-legacy-language-service"></a>清单：创建旧版语言服务
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

以下清单汇总了要创建的语言服务，必须执行的基本步骤[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]核心编辑器。 若要将集成到语言服务[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，必须创建调试表达式计算器。 有关详细信息，请参阅[编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)中[Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)。  
  
## <a name="steps-for-creating-a-language-service"></a>创建语言服务的步骤  
  
1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 接口。  
  
    - 在你的 VSPackage，实现<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>接口，以提供语言服务。  
  
    - 集成的开发环境 (IDE) 中提供语言服务你<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>实现。  
  
2. 实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>主要语言服务类中的接口。  
  
     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口是核心编辑器和语言服务之间的交互的起始点。  
  
### <a name="optional-features"></a>可选功能  
 以下功能是可选的可以按任意顺序实现。 这些功能增强语言服务的功能。  
  
- 语法着色  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 此接口的实现应返回适当的颜色信息的分析程序信息。  
  
   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>方法将返回<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口。 因此，应实现单独的着色器实例为每个文本缓冲区创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>单独接口。 有关详细信息，请参阅[语法突出显示旧版语言服务中](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。  
  
- “代码”窗口  
  
   实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>接口，以使语言服务以接收通知时将创建一个新的代码窗口。  
  
   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法将返回<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>接口。 语言服务然后到代码窗口中添加特殊 UI <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A>。 语言服务还可以执行任何特殊处理，例如，添加在文本视图筛选器<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A>。  
  
- 文本视图筛选器  
  
   若要提供语言服务中的 IntelliSense 语句完成功能，必须截获的一些命令用来处理文本视图。 若要截获这些命令，完成以下步骤：  
  
  - 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>参与命令链和句柄编辑器命令。  
  
  - 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法并传入你<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现。  
  
  - 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A>方法，以便不再将这些命令传递给您从视图分离时。  
  
    必须处理的命令取决于所提供服务。 有关详细信息，请参阅[语言服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。  
  
  > [!NOTE]
  > <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>必须为同一对象上实现接口<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。  
  
- 语句结束  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口。  
  
   支持的语句完成命令 (即<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>)，并调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>中的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口，传递<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>接口。 有关详细信息，请参阅[旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。  
  
- 方法提示  
  
   实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>接口方法提示窗口中提供数据。  
  
   安装要适当地处理命令的文本视图筛选器，以便您知道何时显示方法数据提示窗口。 有关详细信息，请参阅[旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。  
  
- 错误标记  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 接口。  
  
   创建实现的标记对象的错误<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>接口并调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A>方法，传递<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>错误标记对象的接口。  
  
   通常，每个错误标记管理任务列表窗口中的项。  
  
- 任务列表项  
  
   实现任务项类提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem>接口。  
  
   实现任务提供程序类提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider>接口和<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2>接口。  
  
   实现任务枚举器类提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems>接口。  
  
   将任务提供程序注册任务列表<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A>方法。  
  
   获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>通过调用与服务 GUID 的语言服务的服务提供程序接口<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>。  
  
   创建任务项对象，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A>中的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>接口时有新或更新的任务。  
  
- 注释任务项  
  
   使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>接口和<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>接口来获取令牌，任务的注释。  
  
   获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>接口从<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>服务。  
  
   获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>接口从<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A>方法。  
  
   实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents>接口来侦听标记列表中的更改。  
  
- 大纲显示  
  
   有几个选项用于支持大纲显示。 例如，可以支持**折叠到定义**命令，提供控制编辑器的大纲区域，或支持客户端控制区域。 有关详细信息，请参阅[如何：提供旧版语言服务中的展开大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)。  
  
- 语言服务注册  
  
   有关如何注册语言服务的详细信息，请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)并[管理 Vspackage](../../extensibility/managing-vspackages.md)。  
  
- 上下文相关帮助  
  
   提供上下文到编辑器中的以下方法之一：  
  
  - 通过实现文本标记为提供的上下文<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>接口。  
  
  通过实现来提供所有的用户上下文<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>接口。  
  
## <a name="see-also"></a>请参阅  
 [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
