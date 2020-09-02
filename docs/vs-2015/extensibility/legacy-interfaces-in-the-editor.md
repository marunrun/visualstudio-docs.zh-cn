---
title: 编辑器中的旧接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy
ms.assetid: 741d45f5-0ea3-4614-972a-8728fe054e07
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8483068ae03c9a57fc67b528393e5d6830c3ec33
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180282"
---
# <a name="legacy-interfaces-in-the-editor"></a>编辑器中的旧接口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以从旧界面访问 Visual Studio 编辑器。 Visual Studio SDK 包括称为 *填充*程序的适配器，这使得这些接口可与新编辑器交互。 尽管如此，我们建议您更新旧版代码以使用新的编辑器 API。 你的代码可以更好地执行，你可以使用诸如 Windows Presentation Foundation (WPF) 和 Managed Extensibility Framework (MEF) 的新技术。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|说明|  
|-----------|-----------------|  
|[根据编辑器调整旧代码](../extensibility/adapting-legacy-code-to-the-editor.md)|说明如何将代码调整为新编辑器。|  
|[编辑器适配器的新增或更改行为](../extensibility/new-or-changed-behavior-with-editor-adapters.md)|说明编辑器适配器的行为与早期版本的编辑器的行为的不同之处。|  
|[核心编辑器内](../extensibility/inside-the-core-editor.md)|描述编辑器的早期版本的不同组件。|  
|[使用旧 API 实例化核心编辑器](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)|介绍如何使用旧版 API 来实例化核心编辑器。|  
|[编辑器工厂](../extensibility/editor-factories.md)|说明如何在旧版 API 中使用编辑器工厂。|  
|[如何：注册编辑器文件类型](../extensibility/how-to-register-editor-file-types.md)|说明如何将文件扩展名链接到编辑器。|  
|[演练：创建核心编辑器并注册编辑器文件类型](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)|说明如何创建核心编辑器并将文件扩展名链接到该编辑器。|  
|[如何：为编辑器提供上下文](../extensibility/how-to-provide-context-for-editors.md)|说明如何为编辑器提供上下文。|  
|[语言服务和核心编辑器](../extensibility/language-services-and-the-core-editor.md)|说明语言服务和编辑器之间的交互。|  
|[使用旧版 API 访问文本缓冲区](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)|说明如何使用旧 API 访问文本缓冲区。|  
|[使用旧版 API 访问文本视图](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)|说明如何使用旧 API 访问文本视图。|  
|[使用旧版 API 自定义代码窗口](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)|介绍如何使用旧版 API 自定义代码窗口。|  
|[使用旧版 API 访问文本层](../extensibility/accessing-text-layers-by-using-the-legacy-api.md)|介绍如何使用旧 API 访问不同文本层。|  
|[对旧版 API 使用文本标记](../extensibility/using-text-markers-with-the-legacy-api.md)|介绍如何使用旧版 API 添加文本标记。|  
|[使用旧版 API 自定义编辑器控件和菜单](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md)|介绍如何使用旧版 API 自定义编辑器控件。|  
|[使用旧版 API 管理撤消和恢复](../extensibility/managing-undo-and-redo-by-using-the-legacy-api.md)|介绍如何使用旧版 API 管理撤消和重做。|  
|[如何：实现查找和替换机制](../extensibility/how-to-implement-the-find-and-replace-mechanism.md)|介绍如何使用旧版 API 管理查找和替换。|  
|[如何：禁止显示文件更改通知](../extensibility/how-to-suppress-file-change-notifications.md)|说明如何使用旧 API 禁止显示文件更改通知。|  
|[创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)|说明如何创建自定义编辑器和设计器。|  
|[开发旧版语言服务](../extensibility/internals/developing-a-legacy-language-service.md)|提供一些链接，这些链接指向一些功能，这些功能 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 通过添加对语言服务的支持为核心编辑器提供自定义功能。|  
|[使用字体和颜色](../extensibility/using-fonts-and-colors.md)|说明如何将字体和颜色与旧版接口一起使用。|
