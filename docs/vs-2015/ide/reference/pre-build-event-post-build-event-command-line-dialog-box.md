---
title: 预生成事件/生成后事件命令行对话框 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEventsBuilder
- vb.ProjectPropertiesBuildEventsBuilder
helpviewer_keywords:
- $(SolutionExt)
- $(ProjectDir)
- $(TargetPath)
- $(ProjectExt)
- $(TargetFileName)
- $(PlatformName)
- $(SolutionName)
- macros, build events
- $(SolutionPath)
- $(ProjectPath)
- $(ProjectFileName)
- $(DevEnvDir)
- $(TargetName)
- $(TargetDir)
- $(SolutionDir)
- $(TargetExt)
- $(OutDir)
- $(ConfigurationName)
- $(SolutionFileName)
- $(ProjectName)
- build events, macros
ms.assetid: d49b2c57-24bf-4fb2-8351-5c4b6cca938f
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 213535d983f95f304b8e0fba3241fa502577f0f4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438057"
---
# <a name="pre-build-eventpost-build-event-command-line-dialog-box"></a>预生成事件/生成后事件命令行对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可以直接在编辑框中键入[“项目设计器”>“生成事件页”(C#)](../../ide/reference/build-events-page-project-designer-csharp.md)的预生成或生成后事件，或者可以从可用宏的列表中选择预生成和生成后宏。  
  
> [!NOTE]
> 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 命令行编辑框  
 包含为预生成或生成后运行的事件。  
  
> [!NOTE]
> 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。  
  
 **宏**  
 展开编辑框，显示要插入到命令行编辑框的宏列表。  
  
 宏表格  
 列出可用宏及其值。 有关每个宏的说明，请参见下面的“宏”。 一次只能选择一个插入命令行编辑框的宏。  
  
 插入  
 将在宏表格中选择的宏插入命令行编辑框。  
  
### <a name="macros"></a>宏  
 可以使用任何宏来指定文件位置，或在存在多种选择的情况下获取输入文件的实际名称。 这些宏不区分大小写。  
  
|宏|描述|  
|-----------|-----------------|  
|`$(ConfigurationName)`|当前项目配置的名称，例如，“调试”。|  
|`$(OutDir)`|相对于项目目录的输出文件目录的路径。 这解析为输出目录属性的值。 它包括尾随反斜杠“\\”。|  
|`$(DevEnvDir)`|Visual Studio 的安装目录（使用驱动器和路径进行定义）；包括尾随反斜杠“\\”。|  
|`$(PlatformName)`|当前目标平台的名称。 例如，“AnyCPU”。|  
|`$(ProjectDir)`|项目的目录（使用驱动器和路径进行定义）；包括尾随反斜杠“\\”。|  
|`$(ProjectPath)`|项目的绝对路径名称（使用驱动器、路径、基名称和文件扩展名进行定义）。|  
|`$(ProjectName)`|项目的基名称。|  
|`$(ProjectFileName)`|项目的文件名称（使用基名称和文件扩展名进行定义）。|  
|`$(ProjectExt)`|项目的文件扩展名。 文件扩展名之前包括“.”。|  
|`$(SolutionDir)`|解决方案的目录（使用驱动器和路径进行定义）；包括尾随反斜杠“\\”。|  
|`$(SolutionPath)`|解决方案的绝对路径（使用驱动器、路径、基名称和文件扩展名进行定义）。|  
|`$(SolutionName)`|解决方案的基名称。|  
|`$(SolutionFileName)`|解决方案的文件名称（使用基名称和文件扩展名进行定义）。|  
|`$(SolutionExt)`|解决方案的文件扩展名。 文件扩展名之前包括“.”。|  
|`$(TargetDir)`|生成的主输出文件的目录（使用驱动器和路径进行定义）。 它包括尾随反斜杠“\\”。|  
|`$(TargetPath)`|生成的主输出文件的绝对路径名称（使用驱动器、路径、基名称和文件扩展名进行定义）。|  
|`$(TargetName)`|生成的主输出文件的基名称。|  
|`$(TargetFileName)`|生成的主输出文件的文件名称（使用基名称和文件扩展名进行定义）。|  
|`$(TargetExt)`|生成的主输出文件的文件扩展名。 文件扩展名之前包括“.”。|  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中指定自定义生成事件](../../ide/specifying-custom-build-events-in-visual-studio.md)   
 [“项目设计器”->“生成事件”页 (C#)](../../ide/reference/build-events-page-project-designer-csharp.md)   
 [如何：指定生成事件 (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)   
 [如何：指定生成事件 (C#)](../../ide/how-to-specify-build-events-csharp.md)
