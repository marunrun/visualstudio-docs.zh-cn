---
title: 如何：保存和打开带有编码的文件
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Unicode, bidirectional language support
- files, encoding
- bidirectional language support, encoded files
- file encoding, bidirectional languages
ms.assetid: cb52b732-b395-4ba1-a3ef-104b3942a12a
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b02734af3efb24e1e3791246b0cea405b12d7b15
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645799"
---
# <a name="how-to-save-and-open-files-with-encoding"></a>如何：保存和打开带有编码的文件

可以使用特定字符编码保存文件，以支持双向语言。 还可以在打开文件时指定编码，以便 Visual Studio 正确显示文件。

## <a name="to-save-a-file-with-encoding"></a>使用编码保存文件

1. 从“文件”  菜单中选择“将文件另存为”  ，然后单击“保存”  按钮旁边的下拉按钮。

     随即出现“高级保存选项”对话框  。

2. 在“编码”  下，选择要用于文件的编码。

3. 或者，在“行尾”  下，选择行尾字符的格式。

     如果要与使用不同操作系统的用户交换文件，此选项很有用。

     如果要使用已知通过特定方式编码的文件，则可以让 Visual Studio 在打开该文件时使用相应编码。 所使用的方法取决于文件是否是项目的一部分。

## <a name="to-open-an-encoded-file-that-is-part-of-a-project"></a>打开属于项目一部分的编码文件

1. 在 **“解决方案资源管理器”** 中右键单击文件，然后选择 **“打开方式”**

2. 在“打开方式”  对话框中，选择用于打开文件的编辑器。

     许多 Visual Studio 编辑器（例如窗体编辑器）将自动检测编码并使用相应编码打开文件。 如果所选择的编码器允许选择编码，将显示“编码”  对话框。

3. 在“编码”  对话框中，选择编辑器应使用的编码。

## <a name="to-open-an-encoded-file-that-is-not-part-of-a-project"></a>打开不属于项目一部分的编码文件

1. 在“文件”  菜单上，指向“打开”  、选择“文件”  或“来自 Web 的文件”  ，然后选择要打开的文件。

2. 单击“打开”  按钮旁边的下拉按钮，然后选择“打开方式”  。

3. 按照上述步骤中的步骤 2 和步骤 3 操作。

## <a name="see-also"></a>请参阅

- [编码和换行符](encodings-and-line-breaks.md)
- [编码和 Windows 窗体全球化](/dotnet/framework/winforms/advanced/encoding-and-windows-forms-globalization)
- [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)