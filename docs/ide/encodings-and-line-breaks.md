---
title: 编码和换行符字符
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.Encoding
helpviewer_keywords:
- line breaks
- encoding
- Visual Studio, encoding
- editors, line breaks
- line break characters
- Visual Studio, line break characters
ms.assetid: 8f9b3ffc-7b8d-44f4-87cb-dc29105be12d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 59ed38c28c6818fb618156450d47c05b4f35d63d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978156"
---
# <a name="encodings-and-line-endings"></a>编码和行尾

在 Visual Studio 中，以下字符将解释为换行符：

- CR LF:回车符 + 换行符，Unicode 字符 000D + 000A

- LF：换行符，Unicode 字符 000A

- NEL：下一行，Unicode 字符 0085

- LS：行分隔符，Unicode 字符 2028

- PS：段落分隔符，Unicode 字符 2029

从其他应用程序复制的文本将保留原始编码和换行符。 例如，当从记事本复制文本并将其粘贴到 Visual Studio 中的文本文件时，此文本的设置仍与在记事本中的设置相同。

当打开包含不同换行符的文件时，可能会看到一个对话框，询问是否应规范化不一致的换行符以及要选择哪一种换行类型。

## <a name="advanced-save-options"></a>高级保存选项

可以使用“文件” > “高级保存选项”对话框来确定所需的换行符类型。 还可使用相同的设置更改文件的编码。

![“高级保存选项”对话框](media/line_endings.png)

> [!NOTE]
> 如果在“文件”菜单上看不到“高级保存选项”，则可以添加它。 选择“工具”、“自定义”，然后选择“命令”选项卡。在“菜单栏”下拉列表中，选择“文件”，然后选择“添加命令”按钮。 在“添加命令”对话框中的“类别”，选择“文件”，然后在“命令”列表中，选择“高级保存选项”。 选择“确定”，然后选择“下移”按钮以将命令移动到菜单中的任何位置。 选择“关闭”以关闭“自定义”对话框。 有关详细信息，请参阅[自定义菜单和工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#customizing_menu)。
>
> 或者，可以通过选择“文件” > “将 \<文件\> 另存为”，来访问“高级保存选项”对话框。 在“将文件另存为”对话框中，选择“保存”按钮旁的下拉三角形，然后选择“保存时使用编码”。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)