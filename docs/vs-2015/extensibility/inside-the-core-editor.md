---
title: 在核心编辑器内 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - core editor
ms.assetid: 8265f31c-c45b-4858-882c-6d9f1e3b9083
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cf9bc42aec3aac5acc996487f99c7e1f29ca252c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203955"
---
# <a name="inside-the-core-editor"></a>核心编辑器内
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器是可用于修改和查询文本信息的几个组件的集合。 如果已使用旧版 API 自定义核心编辑器，则可以继续使用这些自定义项，这些自定义项将通过编辑器适配器进行路由。 但建议您将自定义修改为新的编辑器 API。  
  
 以下区域是核心编辑器的一些重要方面：  
  
- 文本缓冲区  
  
- 文本视图  
  
- 代码窗口  
  
- 文本标记  
  
- 文本管理器  
  
- 与语言服务集成  
  
## <a name="in-this-section"></a>本节内容  
 [使用旧 API 实例化核心编辑器](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)  
 提供有关如何使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 创建核心编辑器实例的分步说明。  
  
 [使用旧版 API 访问文本缓冲区](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)  
 讨论核心编辑器中的文本缓冲区角色，说明用于访问缓冲区的关联系统，并提供由文本缓冲区对象实现的接口的列表 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 。  
  
 [旧版 API 中的文本缓冲区事件](../extensibility/text-buffer-events-in-the-legacy-api.md)  
 提供用于通知文本缓冲区事件的接口的列表。  
  
 [如何：使用旧 API 注册文本缓冲区事件](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)  
 介绍如何对文本缓冲区事件进行建议。  
  
 [使用文本管理器监视全局设置](../extensibility/using-the-text-manager-to-monitor-global-settings.md)  
 讨论如何使用文本管理器与核心编辑器组件共享全局首选项信息以及如何接收文本管理器事件的通知。  
  
 [使用旧版 API 访问文本视图](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)  
 描述 "核心编辑器" 中的文本视图角色，并列出对象实现的接口 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 。  
  
 [使用旧版 API 自定义代码窗口](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)  
 提供有关如何使用代码窗口来包围文本视图的信息，并讨论如何使用代码窗口管理器向代码窗口提供修饰，并提供新视图的通知。  
  
 [使用旧版 API 更改视图设置](../extensibility/changing-view-settings-by-using-the-legacy-api.md)  
 提供有关如何强制进行查看设置以及如何删除强制设置的分步说明。  
  
 [语言服务和核心编辑器](../extensibility/language-services-and-the-core-editor.md)  
 描述用于控制代码修饰的语言服务实例化。  
  
## <a name="related-sections"></a>相关章节  
 [演练：创建核心编辑器并注册编辑器文件类型](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)  
 提供有关如何从托管代码启动核心编辑器的分步说明。  
  
 [下拉栏](../extensibility/drop-down-bar.md)  
 讨论如何在代码窗口中使用下拉栏，并介绍实现下拉栏时所使用的接口。  
  
 [对旧版 API 使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)  
 说明文本标记的概念以及如何在核心编辑器中使用它们，并列出了用于访问和管理文本标记的接口。  
  
 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)  
 提供有关如何创建文本标记以及如何将自定义命令添加到快捷菜单的分步说明。  
  
 [如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)  
 提供有关如何创建自定义文本标记以及如何将标记类型提供为服务的分步说明。
