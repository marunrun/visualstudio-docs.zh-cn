---
title: 扩展语言服务以支持 EditorConfig
ms.date: 11/22/2017
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [extensibility]
- editorconfig, supporting in a language service
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 663a87ba15121896edcb4c049e7adc6b5c38492a
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983104"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>支持语言服务的 EditorConfig

使用[EditorConfig](https://editorconfig.org/)文件，您可以基于每个项目描述常见文本编辑器选项，如缩进大小。 若要了解有关 Visual Studio 对 EditorConfig 文件的支持的详细信息，请参阅[使用 EditorConfig 创建可移植的编辑器设置](../ide/create-portable-custom-editor-options.md)。

在大多数情况下，实现 Visual Studio 语言服务时，无需任何其他工作即可支持 EditorConfig 通用属性。 当用户打开文件时，核心编辑器将自动发现并读取 .editorconfig 文件，并设置相应的文本缓冲区和视图选项。 但是，对于选项卡和空格之类的编辑，某些语言服务选择使用合适的上下文文本视图选项，而不是使用全局设置。 在这些情况下，必须更新语言服务以支持 EditorConfig 文件。

以下是将_特定于全局语言_的选项替换为_上下文_选项，更新语言服务以支持 EditorConfig 文件所需的更改：

## <a name="indent-style"></a>缩进样式

语言特定的选项 | 上下文选项
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>缩进大小

语言特定的选项 | 上下文选项
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>制表符大小

语言特定的选项 | 上下文选项
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>请参阅

- [使用 EditorConfig 创建可移植编辑器设置](../ide/create-portable-custom-editor-options.md)
- [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)