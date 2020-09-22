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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840731"
---
# <a name="checklist-creating-a-legacy-language-service"></a>清单：创建旧版语言服务
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

以下清单汇总了为核心编辑器创建语言服务时必须执行的基本步骤 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 若要将语言服务集成到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中，必须创建一个调试表达式计算器。 有关详细信息，请参阅在[Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)中[编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)。  
  
## <a name="steps-for-creating-a-language-service"></a>创建语言服务的步骤  
  
1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 接口。  
  
    - 在 VSPackage 中，实现 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 接口以提供语言服务。  
  
    - 使你的语言服务可用于实现中 (IDE) 的集成开发环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 。  
  
2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>在主语言服务类中实现接口。  
  
     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>接口是核心编辑器和语言服务之间的起点交互点。  
  
### <a name="optional-features"></a>可选功能  
 以下功能是可选的，可以按任意顺序实现。 这些功能会提高语言服务的功能。  
  
- 语法着色  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 此接口的实现应分析器信息返回相应的颜色信息。  
  
   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>方法返回 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 为每个文本缓冲区创建一个单独的 colorizer 实例，因此应单独实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 有关详细信息，请参阅 [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。  
  
- 代码窗口  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 接口，以使语言服务能够在创建新代码窗口时接收的通知。  
  
   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>方法返回 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 接口。 然后，语言服务可以将特殊 UI 添加到中的代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> 。 语言服务还可以执行任何特殊处理，如在中添加文本视图筛选器 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A> 。  
  
- 文本视图筛选器  
  
   若要在语言服务中提供 IntelliSense 语句完成功能，必须截获文本视图将处理的某些命令。 若要截获这些命令，请完成以下步骤：  
  
  - 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 以参与命令链并处理编辑器命令。  
  
  - 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 方法并传入您的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 实现。  
  
  - <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A>从视图中分离时调用方法，以便不再将这些命令传递给你。  
  
    必须处理的命令取决于提供的服务。 有关详细信息，请参阅 [语言服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。  
  
  > [!NOTE]
  > <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>接口必须在与接口相同的对象上实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。  
  
- 语句结束  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口。  
  
   支持语句完成命令 (即 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>) 并调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 接口中的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ，并传递 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口。 有关详细信息，请参阅 [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。  
  
- 方法提示  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 接口，为方法提示窗口提供数据。  
  
   安装文本视图筛选器以适当地处理命令，以便您知道何时显示 "方法数据提示" 窗口。 有关详细信息，请参阅 [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。  
  
- 错误标记  
  
   实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 接口。  
  
   创建用于实现接口的错误标记对象， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 并调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> 方法，传递 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 错误标记对象的接口。  
  
   通常，每个错误标记管理 "任务列表" 窗口中的项。  
  
- 任务列表项  
  
   实现提供接口的任务项类 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem> 。  
  
   实现提供接口和接口的任务提供程序类 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> 。  
  
   实现提供接口的任务枚举器类 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems> 。  
  
   向任务列表的方法注册任务提供程序 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A> 。  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>通过使用服务 GUID 调用语言服务的服务提供程序来获取接口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> 。  
  
   创建任务项对象，并在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> 有新的或更新的任务时调用接口中的方法。  
  
- 注释任务项  
  
   使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> 接口和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> 接口可获取注释任务标记。  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>从服务获取接口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> 。  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>从方法获取接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A> 。  
  
   实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents> 接口以侦听标记列表中的更改。  
  
- 大纲显示  
  
   有多个用于支持大纲显示的选项。 例如，您可以支持 " **折叠到定义** " 命令、提供编辑器控制的大纲区域或支持客户端控制的区域。 有关详细信息，请参阅 [如何：提供旧版语言服务中的扩展大纲支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)。  
  
- 语言服务注册  
  
   有关如何注册语言服务的详细信息，请参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md) 和 [管理 vspackage](../../extensibility/managing-vspackages.md)。  
  
- 区分上下文的帮助  
  
   通过以下方式之一向编辑器提供上下文：  
  
  - 通过实现接口为文本标记提供上下文 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> 。  
  
  通过实现接口提供所有用户上下文 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> 。  
  
## <a name="see-also"></a>另请参阅  
 [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
