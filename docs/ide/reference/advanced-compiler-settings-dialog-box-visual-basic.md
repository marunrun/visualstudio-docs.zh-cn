---
title: “高级编译器设置”对话框 (Visual Basic)
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedCompile
helpviewer_keywords:
- Advanced Compiler Settings dialog box
ms.assetid: 1f81133a-293f-4dba-bc1c-8baafb01d857
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0cb77021818fd77205a598f54a4a64a1929348f2
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919360"
---
# <a name="advanced-compiler-settings-dialog-box-visual-basic"></a>“高级编译器设置”对话框 (Visual Basic)

使用“项目设计器”的“高级编译器设置”对话框可指定项目的高级生成配置属性   。 此对话框仅适用于 Visual Basic 项目。

## <a name="to-access-this-dialog-box"></a>访问此对话框

1. 在“解决方案资源管理器”中，选择项目节点（而非“解决方案”节点）。  

2. 在“项目”菜单上，单击“属性”   。 当“项目设计器”出现时，单击“编译”选项卡   。

3. 在[“编译”->“项目设计器”(Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)上，依次选择“配置”和“平台”   。 在简化生成配置中，不会显示“配置”和“平台”列表   。 有关详细信息，请参阅[如何：设置调试和发布配置](../../debugger/how-to-set-debug-and-release-configurations.md)。

4. 单击“高级编译选项”  。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="optimizations"></a>优化

以下选项可以指定优化，在某些情况下缩小程序文件、加快程序运行速度或加速生成过程。

**不做整数溢出检查**

默认情况下，清除此复选框可启用整数溢出检查。 选中此复选框可不做整数溢出检查。 如果选中此复选框，整数计算可能会更快。 但是，如果删除溢出检查和数据类型功能溢出，可能会存储不正确结果并且引发错误。

如果溢出条件已选中并且整数操作溢出，将引发 <xref:System.OverflowException> 异常。 如果未选中溢出条件，整数操作溢出不会引发异常。

**启用优化**

默认情况下，清除此复选框可禁用编译器优化。 选择此复选框可启用编译器优化。 编译器优化会使输出文件更智能、更快并且更有效。 但优化会导致代码在输出文件中重新排列，因此编译器优化可能使调试变得困难。

 **DLL 基址**

此文本框以十六进制格式显示默认 DLL 基址。 在类库和控件库项目中，可以使用此文本框指定创建 DLL 时将要使用的基址。

 **生成调试信息**

从列表中选择“无”、“完整”或“仅 pdb”    。 “无”指定不生成调试信息  。 “完整”指定生成完整调试信息，“仅 pdb”指定仅生成 PDB 调试信息   。 该选项的默认值为“完整”  。

## <a name="compilation-constants"></a>编译常量

条件编译常量具有与在源文件中使用 [#Const](/dotnet/visual-basic/language-reference/directives/const-directive) 预处理器指令类似的效果，只是定义的常数为公共的且应用于项目中的所有文件。 可以将条件编译常量与 [#If...Then...#Else](/dotnet/visual-basic/language-reference/directives/if-then-else-directives) 指令一起使用，从而有条件地编译源文件。 请参阅[条件编译](/dotnet/visual-basic/programming-guide/program-structure/conditional-compilation)。

 “定义 DEBUG 常量” 

默认为选中此复选框，指定设置 DEBUG 常量。

 “定义 TRACE 常量” 

默认为选中此复选框，指定设置 TRACE 常量。

 **自定义常量**

在此文本框中输入应用程序的任何自定义常量。 条目应使用以下形式用逗号分隔：**Name1="Value1",Name2="Value2",Name3="Value3"** 。

## <a name="other-settings"></a>其他设置

**生成序列化程序集**

此设置指定编译器是否创建 XML 序列化程序集。 序列化程序集可以提高 <xref:System.Xml.Serialization.XmlSerializer> 的启动性能（如果已使用该类序列化代码中的类型）。 该选项的默认值为“自动”  。“自动”指定仅在已使用 <xref:System.Xml.Serialization.XmlSerializer> 将代码中的类型编码为 XML 的情况下，才会生成序列化程序集  。 若设置为“关闭”，则指定永远不会生成序列化程序集，无论代码是否使用 <xref:System.Xml.Serialization.XmlSerializer>  。 若设置为“打开”  ，则指定始终会生成序列化程序集。 序列化程序集命名为 `TypeName`.XmlSerializers.dll。

## <a name="see-also"></a>请参阅

- [“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)