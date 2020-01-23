---
title: “查找-命令”框
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.findcommandbox
helpviewer_keywords:
- Find/Command box
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99b50c0503d313d4482d8370071220dbf1403d9a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591523"
---
# <a name="findcommand-box"></a>“查找/命令”框

可以从“查找/命令”框搜索文本并运行 Visual Studio 命令  。 “查找/命令”框仍可用作工具栏控件，但不再默认可见  。 通过在“标准”工具栏上选择“添加或删除按钮”，然后选择“查找”，即可显示“查找/命令”框     。

要运行 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 命令，请在该命令前面加一个大于 (>) 符号  。

“查找/命令”框保留最后输入的 20 个项，并将它们显示在下拉列表中  。 选择箭头键可以浏览该列表  。

![“查找&#47;命令”框](../ide/media/findcommandbox.png)

## <a name="searching-for-text"></a>搜索文本

默认情况下，如果在“查找/命令”框中指定了文本，然后选择了 Enter 键，Visual Studio 会使用“在文件中查找”对话框中指定的选项搜索当前文档或工具窗口    。 有关详细信息，请参阅[查找和替换文本](../ide/finding-and-replacing-text.md)。

## <a name="entering-commands"></a>输入命令

若要使用“查找/命令”框发布单个 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 命令或别名，而不是搜索文本，请在该命令前面加一个大于 (>) 符号   。 例如：

```
>File.NewFile c:\temp\MyFile /t:"General\Text File"
```

或者，还可以使用“命令”窗口输入和执行单个或多个命令  。 某些命令或别名可以自行输入并执行，其他则要求在他们的语法中具有参数。 有关一系列带参数的命令的信息，请参阅 [Visual Studio 命令](../ide/reference/visual-studio-commands.md)。

## <a name="escape-characters"></a>转义字符

命令中的插入符号 (^) 字符表示紧随其后的字符将按字面意思而不是作为控制字符进行解释  。 这可以用于嵌入参数或开关值中的直引号 (")、空格、前导斜杠，插入符号或其他任何字符，开关名称除外  。 例如：

```
>Edit.Find ^^t /regex
```

插入符号在引号内或引号外的作用相同。 如果插入符号是行的最后一个字符，则忽略不计。

## <a name="see-also"></a>请参阅

- [“命令”窗口](../ide/reference/command-window.md)
- [查找和替换文本](../ide/finding-and-replacing-text.md)
