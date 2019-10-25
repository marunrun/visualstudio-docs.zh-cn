---
title: “提取接口”重构
ms.date: 01/26/2018
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.extractinterface
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 15da8bdf1a3df60a7ad4816ce578ec5672c85ecf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654420"
---
# <a name="extract-an-interface-refactoring"></a>“提取接口”重构

此重构适用于：

- C#

- Visual Basic

**功能：** 使用来自类、结构或接口的现有成员创建接口。

**使用时机：** 类、结构或接口中的成员可以由其他类、结构或接口继承。

操作原因：  接口是面向对象设计的出色构造。 假设有各类动物（狗、猫、鸟），这些动物都具有吃、喝、睡等一些共同方法。 使用 IAnimal 这样的接口，狗、猫和鸟即可拥有适用于这些方法的共同“签名”。

## <a name="extract-an-interface-refactoring"></a>“提取接口”重构

1. 请将光标置于类名称。

   - C#：

       ![突出显示的代码 - C#](media/extractinterface-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 - Visual Basic](media/extractinterface-highlight-vb.png)

2. 下一步，执行以下某项操作：

   - **键盘**
      - 按“Ctrl+R”  ，然后按“Ctrl+I”  。 （键盘快捷方式可能因所选的配置文件而有所不同。）
      - 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“提取接口”  。
   - **鼠标**
      - 选择“编辑”>“重构”>“提取接口”  。
      - 右键单击类名称，选择“快速操作和重构”  菜单，然后从“预览”弹出窗口中选择“提取接口”  。

3. 在弹出的“提取接口”对话框中，输入需提供的信息  ：

   ![提取接口](media/extractinterface-dialog-same-file.png)

   | 字段 | 说明 |
   | - | - |
   | “新接口名称”  | 要创建的接口的名称。 名称将默认为“IClassName”，其中“ClassName”是上面所选类的名称   。 |
   | “新文件名”  | 包含接口的生成文件的名称。 与接口名称一样，此名称将默认为“IClassName”，其中“ClassName”是上面所选类的名称   。 还可以选择“添加到当前文件”的选项  。 |
   | “选择构成接口的公共成员”  | 要提取到接口的项。 你可以选择你想要的数量。 |

4. 选择 **“确定”** 。

   在指定名称的文件中创建接口。 此外，所选类还会实现此接口。

   - C#：

      ![生成的类 - C#](media/extractinterface-class-cs.png)

      ![生成的接口 - C#](media/extractinterface-interface-cs.png)

   - Visual Basic：

      ![生成的类 - Visual Basic](media/extractinterface-class-vb.png)

      ![生成的接口 - Visual Basic](media/extractinterface-interface-vb.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)
