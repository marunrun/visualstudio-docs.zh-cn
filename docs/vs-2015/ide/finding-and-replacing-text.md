---
title: 查找和替换文本 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.find
- vs.findreplacecontrol
- vs.findreplace.findsymbol
- vs.findreplace.symbol
- findresultswindow
- vs.findreplace.quickreplace
- vs.findsymbol
- vs.findinfiles
- vs.findresults1
- vs,findsymbolwindow
- vs.findreplace.quickfind
- vs.lookin
- vs.replace
helpviewer_keywords:
- text searches
- Replace in Files dialog box
- find, text
- Find in Files dialog box
- find
- text searches, finding and replacing text
- Replace dialog box
- text, finding and replacing
- find, symbol
- find and replace
- replace
- find text
- replacing text
ms.assetid: a62545c3-1570-4d12-99fb-a82607eb35a1
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 025ba2eb95514efc740d1f8f7b3bf674d6bf237a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645633"
---
# <a name="finding-and-replacing-text"></a>Finding and Replacing Text
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 代码编辑器以及“查找结果”窗口等基于文本的输出窗口中，可以使用“查找和替换”控件或“在文件中查找/替换”查找和替换文本。 还可以在某些设计器窗口中搜索和替换，例如 XAML 设计器、Windows 窗体设计器和工具窗口

 可以将搜索范围限制到当前文档、当前解决方案或一组自定义文件夹中。 还可以指定一组文件扩展名，用于多文件搜索。 可以使用 .NET 正则表达式自定义搜索语法。

 若要查找和替换正则表达式，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

> [!TIP]
> “查找/命令”框仍可用作工具栏控件，但不再默认可见。 通过在“标准”工具栏上选择“添加或删除按钮”，然后选择“查找”，即可显示“查找/命令”框。 有关详细信息，请参阅[“查找/命令”框](../ide/find-command-box.md)。

## <a name="find-and-replace-control"></a>“查找和替换”控件
 “查找和替换”控件显示在代码编辑器窗口的右上角。 “查找和替换”控件会立即突出显示给定搜索字符串在当前文档中的每个匹配项。 通过在搜索控件上选择“查找下一个”按钮或“查找上一个”按钮，可以从一个匹配项导航到另一个匹配项。

 通过选择“查找”文本框旁边的按钮，可以访问替换选项。 若要一次替换一个，请选择“替换”文本框旁边的“替换下一个”按钮。 若要替换所有匹配项，请选择“全部替换”按钮。

 若要更改匹配项的突出显示颜色，请依次选择“工具”菜单、“选项”、“环境”、“字体和颜色”。 在“显示设置对象”列表中，选择“文本编辑器”，然后在“显示项”列表中，选择“查找突出显示项(扩展名)”。

### <a name="searching-tool-windows"></a>搜索工具窗口
 通过在“编辑”菜单上选择“查找和替换”或按 Ctrl+F，可以在代码或文本窗口（如“输出”窗口和“查找结果”窗口）中使用“查找”控件。

 某些工具窗口也提供某版本的查找控件。 例如，通过在搜索框中输入文本可以在“工具箱”窗口中筛选控件列表。 还可以在其中搜索内容的其他工具窗口包括“解决方案资源管理器”、“属性”窗口和“团队资源管理器”等等。

## <a name="findreplace-in-files"></a>在文件中查找/替换
 “在文件中查找/替换”与“查找和替换”控件类似，区别在于可以定义搜索范围。 不仅可以搜索当前在编辑器中打开的文件，还可以搜索所有打开的文档、整个解决方案、当前项目，及所选文件夹集。 还可以按文件扩展名搜索。 若要访问“在文件中查找/替换”对话框，请在“编辑”菜单上选择“查找和替换”（或按 Ctrl+Shift+F）。

 选择“查找全部”后，“查找结果”窗口随即打开，并列出搜索的匹配项。 在列表中选择一个结果会显示相关联的文件，并突出显示匹配项。 如果文件尚未打开进行编辑，则可以在选项卡右侧的预览选项卡中打开。 可以使用“查找”控件在“查找结果”列表中搜索。

### <a name="creating-custom-search-folder-sets"></a>创建自定义搜索文件夹集
 通过选择“查找范围”框旁边的“选择搜索文件夹”按钮（类似于 …），可以定义搜索范围。 在“选择搜索文件夹”对话框中，可以指定在其中进行搜索的一组文件夹，并且可以保存规范，供以后重复使用。 只有将远程计算机的驱动器映射到本地计算机后，才可以指定远程计算机上的文件夹。

### <a name="creating-custom-component-sets"></a>创建自定义组件集
 通过选择“查找范围”框旁边的“编辑自定义组件集”按钮，可以将组件集定义为搜索范围。 可以指定已安装的 .NET 或 COM 组件，以及包含在解决方案或任何程序集或类型库（.dll、.tlb、.olb、.exe 或 .ocx）中的 Visual Studio 项目。 若要搜索引用，请选择“查找引用”框。

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)
