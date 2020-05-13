---
title: 重命名文件名以匹配类型
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 5b7a42a174fecd078e804f2ab3c35fbe442364a6
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594391"
---
# <a name="sync-a-type-to-a-filename-or-a-filename-to-a-type-refactoring"></a>将类型同步到文件名或反向操作

此重构适用于：

- C#

- Visual Basic

 功能：重命名类型以匹配文件名，或重命名文件名以匹配其包含的类型。

 时机：已重命名文件或类型，且尚未更新相应文件或类型进行匹配时。

 原因：将类型置于具有其他名称的文件中，将很难查找要搜索的内容，反之亦然。 通过重命名类型或文件名，代码变得更具可读性且更易于导航。

> [!NOTE]
> 此重构尚不可用于 .NET Standard 和 .NET Core 项目。

## <a name="how-to"></a>操作说明

1. 突出显示要同步的类型名称，或将文本光标置于其中：

   - C#：

       ![突出显示的代码 - C#](media/synctype-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 - Visual Basic](media/synctype-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“重命名文件为 TypeName.cs”  ，其中“TypeName”  是已选定的类型名称。
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“重命名类型为 **Filename _”_** ，其中“Filename”  是当前文件名。
   - **鼠标**
      - 右键单击代码，选择“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“重命名文件为 TypeName.cs”  ，其中“TypeName”  是已选定的类型名称。
      - 右键单击代码，选择“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“重命名类型为 **Filename _”_** ，其中“Filename”  是当前文件名。

   随即重命名类型或文件。

   - C#:：在下例中，文件“MyClass.cs”重命名为“MyNewClass.cs”以匹配类型名称   。

       ![内联结果 C#](media/synctype-result-cs.png)

   - Visual Basic：在下例中，文件“Employee.vb”重命名为“Person.vb”以匹配类型名称   。

       ![内联结果 Visual Basic](media/synctype-result-vb.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
