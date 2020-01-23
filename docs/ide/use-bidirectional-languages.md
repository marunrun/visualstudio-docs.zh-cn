---
title: 支持阿拉伯语和希伯来语
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Hebrew character display [Visual Studio]
- bidirectional language support
- Arabic, creating applications
ms.assetid: b56f9795-ed8d-4452-9d49-8ca0b0145d86
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 57bccfccb77c5a80fd2630680564f88f08d7ca5b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591991"
---
# <a name="support-for-bidirectional-languages-in-visual-studio"></a>对 Visual Studio 中双向语言的支持

Visual Studio 可以正确显示阿拉伯语和希伯来语文本，让你可以输入对象名称和值的双向语言文本。

> [!NOTE]
> 要输入和显示双向语言，必须使用已配置相应语言的 Windows 版本。 可以是安装了适当语言包的英文版 Windows，或者是已相应本地化的 Windows 版本。

## <a name="fully-supported-features"></a>完全受支持的功能

在 Visual Studio 中进行设计时，可以在输入文本、命名对象以及保存和打开文件的同时使用双向语言。

### <a name="text-entry"></a>文本输入

Visual Studio 支持 Unicode，因此，如果系统设置了适当的区域设置和输入语言，则可以用阿拉伯语或希伯来语输入文本。 （阿拉伯语支持包括 Kashida 和音调符号。）

### <a name="arabic-or-hebrew-object-names"></a>阿拉伯语或希伯来语对象名

可使用双向语言向解决方案、项目、文件、文件夹等分配名称。 在代码中，可针对变量名、类名、对象名、特性名、元数据名和其他元素名使用双向语言。 使用阿拉伯语时，可使用包括 Kashida 和音调符号在内的任何阿拉伯语字符。

以下元素可使用阿拉伯语或希伯来语命名，Visual Studio 会正确处理此类元素：

- 解决方案名、项目名和文件名，包括项目路径中所含的任何文件夹。

   解决方案资源管理器会正确显示解决方案名和元素名  。

- 文件内容。

   可使用 Unicode 编码或选定的代码页来打开或保存文件。

- 数据元素。

   “服务器资源管理器”将正确显示这些元素，并允许对其进行编辑  。

- 复制到 Windows 剪贴板上的元素。

- 特性和元数据。

- 属性值。

   可在“属性”窗口中使用阿拉伯语或希伯来语文本  。 可在此窗口使用标准的 Windows 击键（“Ctrl+右 Shift”组合键用于从右到左读取，“Ctrl+左 Shift”组合键用于从左到右读取）选择从右到左或从左到右读取顺序     。

- 代码和文本。

   在代码编辑器中，可使用阿拉伯语或希伯来语命名类、函数、变量、属性、字符串文本、特性等。 但是，编辑器不支持从右向左的读取顺序；文本总是从左边开始。

   > [!TIP]
   > 应将字符串文本放在资源文件中，而不是将其硬编码到程序中。 有关详细信息，请参阅[桌面应用中的资源 (.NET Framework)](/dotnet/framework/resources/index)。

   > [!NOTE]
   > 用阿拉伯语或希伯来语命名的对象的引用方式必须保持一致。 例如，如果使用 Kashida 命名阿拉伯语变量，则引用该变量时必须总是使用 Kashida，否则会产生错误。

- 代码注释。 可使用阿拉伯语或希伯来语创建注释。 还可在注释生成器工具中使用这些语言。

### <a name="file-encoding"></a>文件编码

可使用特定语言的编码或 Unicode 编码保存和打开文件。 有关详细信息，请参阅[如何：保存和打开带有编码的文件](../ide/how-to-save-and-open-files-with-encoding.md)。

## <a name="right-to-left-reading-order"></a>从右到左的读取顺序

Visual Studio 对从右到左的读取顺序提供有限支持。 默认情况下，Visual Studio 中使用的文本输入控件使用的是从右到左的读取顺序。 大多数情况可以使用标准 Window 手势来切换读取顺序。 例如，可以按“Ctrl+右 Shift”组合键，将“属性”窗口切换为支持按从右到左的顺序读取属性值    。

在 Visual Studio 中，以下情况不支持从右到左的读取顺序：

- Visual Studio 对话框中的复选框、下拉列表和其他控件始终使用从左向右的读取顺序。

- 代码编辑器（和文本编辑器）不支持从右到左的读取顺序。 可以用双向语言输入文本，但读取顺序总是从左到右。

## <a name="see-also"></a>请参阅

- [开发全球化和本地化应用](globalizing-and-localizing-applications.md)
