---
title: “生成事件”对话框 (Visual Basic)
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- build events, specifying
- pre-build events
- Build Events dialog box
- post-build events
ms.assetid: 3a81a7c7-39f9-47a8-ba5a-b351227f380e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb4cd0a46e5ab4cc9c3a9e00773818d536b84891
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "68461438"
---
# <a name="build-events-dialog-box-visual-basic"></a>“生成事件”对话框 (Visual Basic)

使用“生成事件”对话框可以指定生成配置说明  。 还可以指定运行任何预生成或生成后事件所依据的条件。 有关详细信息，请参阅[如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)。

预生成事件命令行 

在生成开始之前，指定要执行的任何命令。 要键入长命令，单击“编辑预生成”，显示[预生成事件/生成后事件命令行对话框](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)  。

> [!NOTE]
> 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。

生成后事件命令行 

在生成结束之后，指定要执行的任何命令。 要键入长命令，单击“编辑生成后”，显示“预生成事件/生成后事件命令行”对话框   。

> [!NOTE]
> 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。

运行生成后事件 

指定生成后事件运行的条件，如下表所示。

|选项|结果|
|------------|------------|
|始终 |无论生成是否成功，均运行生成后事件。|
|成功生成时 |如果生成成功，则运行生成后事件。 即使项目已为最新状态，但只要生成成功，就会运行该事件。 此为默认设置。|
|生成更新项目输出时 |生成后事件仅在编译器的输出文件 (.exe or .dll) 不同于之前的编译器输出文件时才运行。 如果项目为最新状态，则不会运行生成后事件。|

## <a name="see-also"></a>请参阅

- [“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)
- [如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [预生成事件/生成后事件命令行对话框](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)