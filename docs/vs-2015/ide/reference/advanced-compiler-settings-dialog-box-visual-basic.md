---
title: “高级编译器设置”对话框 (Visual Basic) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedCompile
helpviewer_keywords:
- Advanced Compiler Settings dialog box
ms.assetid: 1f81133a-293f-4dba-bc1c-8baafb01d857
caps.latest.revision: 52
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba666b0ff5544b185f82a66c78d6259e9f1268fd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651769"
---
# <a name="advanced-compiler-settings-dialog-box-visual-basic"></a>“高级编译器设置”对话框 (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“项目设计器”的“高级编译器设置”对话框可指定项目的高级生成配置属性   。 此对话框仅适用于 Visual Basic 项目。

### <a name="to-access-this-dialog-box"></a>访问此对话框

1. 在“解决方案资源管理器”中，选择项目节点（而非“解决方案”节点）。  

2. 在“项目”菜单上，单击“属性”   。 当“项目设计器”出现时，单击“编译”选项卡   。

3. 在[“编译”->“项目设计器”(Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)上，依次选择“配置”和“平台”   。 在简化生成配置中，不会显示“配置”和“平台”列表   。 有关详细信息，请参阅[调试和发布项目配置](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)。

4. 单击“高级编译选项”  。

   [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

## <a name="optimizations"></a>优化
 以下选项可以指定优化，在某些情况下缩小程序文件、加快程序运行速度或加速生成过程。

 **删除整数溢出检查**默认情况下，清除此复选框以启用整数溢出检查。 选中此复选框可不做整数溢出检查。 如果选中此复选框，整数计算可能会更快。 但是，如果删除溢出检查和数据类型功能溢出，可能会存储不正确结果并且引发错误。

 如果溢出条件已选中并且整数操作溢出，将引发 <xref:System.OverflowException> 异常。 如果未选中溢出条件，整数操作溢出不会引发异常。

 **启用优化**默认情况下，清除此复选框以禁用编译器优化。 选择此复选框可启用编译器优化。 编译器优化会使输出文件更智能、更快并且更有效。 但优化会导致代码在输出文件中重新排列，因此编译器优化可能使调试变得困难。

 **DLL 基址**此文本框以十六进制格式显示默认的 DLL 基址。 在类库和控件库项目中，可以使用此文本框指定创建 DLL 时将要使用的基址。

 **生成调试信息**从列表中选择 "**无**"、"**完全**" 或 "**仅 pdb** "。 “无”指定不生成调试信息  。 “完整”指定生成完整调试信息，“仅 pdb”指定仅生成 PDB 调试信息   。 默认情况下，此选项设置为“完整”  。

## <a name="compilation-constants"></a>编译常量
 条件编译常量具有与在源文件中使用 [#Const](https://msdn.microsoft.com/library/707669e5-23f9-4f17-8622-a0d534429386) 预处理器指令类似的效果，只是定义的常数为公共的且应用于项目中的所有文件。 可以将条件编译常量与 [#If...Then...#Else](https://msdn.microsoft.com/library/10bba104-e3fd-451b-b672-faa472530502) 指令一起使用，从而有条件地编译源文件。 请参阅[条件编译](https://msdn.microsoft.com/library/9c35e55e-7eee-44fb-a586-dad1f1884848)。

 **定义 DEBUG 常量**默认情况下，此复选框处于选中状态，指定已设置调试常量。

 **定义 TRACE 常量**默认情况下，选中此复选框，指定设置 TRACE 常量。

 **自定义常量**在此文本框中输入应用程序的任何自定义常量。 条目应用逗号分隔开，格式为：Name1="Value1",Name2="Value2",Name3="Value3"  。

## <a name="other-settings"></a>其他设置
 **生成序列化程序集**此设置指定编译器是否将创建 XML 序列化程序集。 序列化程序集可以提高 <xref:System.Xml.Serialization.XmlSerializer> 的启动性能（如果已使用该类序列化代码中的类型）。 默认情况下，此选项设置为“自动”，用于指定仅在已使用 <xref:System.Xml.Serialization.XmlSerializer> 将代码中的类型编码为 XML 的情况下，才会生成序列化程序集  。 若设置为“关闭”，则指定永远不会生成序列化程序集，无论代码是否使用 <xref:System.Xml.Serialization.XmlSerializer>  。 若设置为“打开”  ，则指定始终会生成序列化程序集。 序列化程序集命名为 `TypeName`.XmlSerializers.dll。

## <a name="see-also"></a>另请参阅
 [“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)
