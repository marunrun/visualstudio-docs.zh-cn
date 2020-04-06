---
title: 清单：创建传统语言服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11785dab63cbb6a95ab2d34c5edbfb4525ebf34c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709792"
---
# <a name="checklist-create-a-legacy-language-service"></a>检查表：创建旧语言服务
以下检查表总结了为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]核心编辑器创建语言服务必须执行的基本步骤。 要将语言服务集成到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中，必须创建调试表达式赋值器。 有关详细信息，请参阅在[可视化工作室调试器扩展中](../../extensibility/debugger/visual-studio-debugger-extensibility.md)[编写 CLR 表达式赋值](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)器 。

## <a name="steps-to-create-a-language-service"></a>创建语言服务的步骤

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 接口。

    - 在 VSPackage 中，<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>实现接口以提供语言服务。

    - 使语言服务可用于<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>实现中的集成开发环境 （IDE）。

2. 在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>主语言服务类中实现接口。

     接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>是核心编辑器与语言服务之间交互的起点。

### <a name="optional-features"></a>可选功能
 以下功能是可选的，可以按任意顺序实现。 这些功能增加了语言服务的功能。

- 语法着色

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 接口。 此接口的实现应解析器信息返回相应的颜色信息。

  该方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>返回接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>。 为每个文本缓冲区创建单独的着色器实例，因此应单独实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>接口。 有关详细信息，请参阅[旧语言服务 中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。

- 代码窗口

  实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>接口，使语言服务能够接收创建新代码窗口的通知。

  该方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>返回接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>。 然后，语言服务可以将特殊 UI 添加到 中<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A>的代码窗口。 语言服务还可以执行任何特殊处理，例如在 中<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A>添加文本视图筛选器。

- 文本视图筛选器

  要在语言服务中提供 IntelliSense 语句完成，必须拦截文本视图将处理的某些命令。 要拦截这些命令，完成以下步骤：

  - 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>参与命令链和处理编辑器命令。

  - 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法并传递实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>。

  - 从视图<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A>分离时调用 方法，以便不再将这些命令传递给您。

  必须处理的命令取决于提供的服务。 有关详细信息，请参阅[语言服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。

  > [!NOTE]
  > 接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>必须在与<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口相同的对象上实现。

- 语句结束

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口。

  支持语句<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>完成命令 （即 ），并在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>接口中调用方法，传递<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>接口。 有关详细信息，请参阅[旧语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。

- 方法提示

  实现接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>以提供方法提示窗口的数据。

  安装文本视图筛选器以适当地处理命令，以便知道何时显示方法数据提示窗口。 有关详细信息，请参阅[旧语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。

- 错误标记

  实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 接口。

  创建实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>接口并调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A>方法的错误标记对象，传递错误标记对象的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>接口。

  通常，每个错误标记都会管理任务列表窗口中的项。

- 任务列表项

  实现提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem>接口的任务项类。

  实现提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider>接口和<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2>接口的任务提供程序类。

  实现提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems>接口的任务枚举器类。

  使用任务列表<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A>的方法注册任务提供程序。

  通过使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>服务 GUID<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>调用语言服务的服务提供商来获取接口。

  创建新任务或更新的任务时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A>创建任务项<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>对象并在接口中调用 方法。

- 注释任务项

  使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>接口和<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>接口获取注释任务令牌。

  从服务<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>接口。

  从<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens><xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A>方法获取接口。

  实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents>接口以侦听令牌列表中的更改。

- 大纲显示

  有几个选项可用于支持大纲。 例如，可以支持 **"折叠到定义"** 命令、提供编辑器控制的大纲区域或支持客户端控制的区域。 有关详细信息，请参阅[：在旧语言服务中提供扩展的大纲支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)。

- 语言服务注册

  有关如何注册语言服务的详细信息，请参阅[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service2.md)[和管理 VSPackages](../../extensibility/managing-vspackages.md)。

- 上下文相关帮助

  以下列方式之一向编辑器提供上下文：

  - 通过实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>接口为文本标记提供上下文。

  - 通过实现接口提供<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>所有用户上下文。

## <a name="see-also"></a>请参阅
- [开发传统语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
