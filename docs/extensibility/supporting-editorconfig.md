---
title: 扩展语言服务以支持编辑器配置
ms.date: 11/22/2017
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [extensibility]
- editorconfig, supporting in a language service
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddfe0e30904d000b4fd70c85371d29a2ee486932
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699587"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>为您的语言服务提供编辑器配置

[EditorConfig](https://editorconfig.org/)文件使您能够按项目描述常见的文本编辑器选项，如缩进大小。 要了解有关 Visual Studio 支持编辑器配置文件的详细信息，请参阅使用[Editor Config 创建便携式编辑器设置](../ide/create-portable-custom-editor-options.md)。

在大多数情况下，实现 Visual Studio 语言服务时，无需任何其他工作即可支持 EditorConfig 通用属性。 当用户打开文件时，核心编辑器将自动发现并读取 .editorconfig 文件，并设置相应的文本缓冲区和视图选项。 但是，对于选项卡和空格等编辑，某些语言服务选择使用适当的上下文文本视图选项，而不是使用全局设置。 在这些情况下，必须更新语言服务以支持 EditorConfig 文件。

以下是更新语言服务以支持 Editor Config 文件所需的更改，这些更改将特定于全局_的语言_选项替换为_上下文_选项：

## <a name="indent-style"></a>缩进样式

特定于语言的选项 | 上下文选项
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>缩进大小

特定于语言的选项 | 上下文选项
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>制表符大小

特定于语言的选项 | 上下文选项
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>请参阅

- [使用编辑器配置创建便携式编辑器设置](../ide/create-portable-custom-editor-options.md)
- [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)
