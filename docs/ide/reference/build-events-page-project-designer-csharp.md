---
title: “项目设计器”->“生成事件”页 (C#)
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ba429c116d44a5d79d935fe3a1ad07b6d5f36f79
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461841"
---
# <a name="build-events-page-project-designer-c"></a>“项目设计器”->“生成事件”页 (C#)

使用“项目设计器”的“生成事件”页指定生成配置说明   。 还可以指定任何生成后事件运行的条件。 有关详细信息，请参阅[如何：指定生成事件 (C#)](../../ide/how-to-specify-build-events-csharp.md) 以及[如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)。

## <a name="uielement-list"></a>UIElement 列表

**配置**

此控件在本页不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

**平台**

此控件在本页面上不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

预生成事件命令行 

在生成开始之前，指定要执行的任何命令。 要键入长命令，单击“编辑预生成”，显示[预生成事件/生成后事件命令行对话框](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)  。

> [!NOTE]
> 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。

生成后事件命令行 

在生成结束之后，指定要执行的任何命令。 要键入长命令，单击“编辑生成后”，显示“预生成事件/生成后事件命令行对话框”   。

> [!NOTE]
> 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。

运行生成后事件 

指定以下生成后事件运行的条件，如下表所示。

|选项|结果|
|------------|------------|
|始终 |无论生成是否成功，均运行生成后事件。|
|成功生成时 |如果生成成功，则运行生成后事件。 因此，即使项目已为最新状态，但只要生成成功，就会运行该事件。|
|生成更新项目输出时 |生成后事件仅在编译器的输出文件 (.exe or .dll) 不同于之前的编译器输出文件时才运行。 因此，如果项目为最新状态，则不会运行生成后事件。|

## <a name="see-also"></a>请参阅

- [如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [如何：指定生成事件 (C#)](../../ide/how-to-specify-build-events-csharp.md)
- [项目属性引用](../../ide/reference/project-properties-reference.md)
- [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)