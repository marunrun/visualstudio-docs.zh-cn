---
title: Exec 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Exec
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, Exec task
ms.assetid: c9b7525a-b1c9-40fc-8bce-77a5b8f960d8
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2a69fc64c3371a2970c03ec0129d4c733f5ae9cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201753"
---
# <a name="exec-task"></a>Exec 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用指定的参数来运行指定程序或命令。  
  
## <a name="parameters"></a>参数  
 下表描述了 `Exec` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`Command`|必选 `String` 参数。<br /><br /> 要运行的命令。 可以是系统命令（例如 attrib），也可以是可执行文件（例如 program.exe、runprogram.bat 或 setup.msi）。<br /><br /> 此参数可包含多行命令。 或者，可将多个命令放在批文件中，然后使用此参数运行文件。|  
|`CustomErrorRegularExpression`|可选 `String` 参数。<br /><br /> 指定用于查找工具输入中错误行的正则表达式。 这对会生成不常见格式的输出的工具非常有用。|  
|`CustomWarningRegularExpression`|可选 `String` 参数。<br /><br /> 指定用于查找工具输入中警告行的正则表达式。 这对会生成不常见格式的输出的工具非常有用。|  
|`ExitCode`|可选 `Int32` 输出只读参数。<br /><br /> 指定执行的命令提供的退出代码。|  
|`IgnoreExitCode`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则任务会忽略执行的命令所提供的退出代码。 否则，如果执行的命令返回一个非零退出代码，那么该任务将返回 `false`。|  
|`IgnoreStandardErrorWarningFormat`|可选 `Boolean` 参数。<br /><br /> 如果为 `false`，则会选择输出中与标准错误/警告格式相匹配的行，并将其记录为错误/警告。 如果为 `true`，则会禁用此行为。|  
|`Outputs`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含任务的输出项。 `Exec` 任务自身不会设置这些项。 相反，你可以提供这些项，使得任务看似已对其进行了设置，以便于稍后在项目中使用。|  
|`StdErrEncoding`|可选 `String` 输出参数。<br /><br /> 指定捕获的任务标准错误流的编码。 默认值为当前控制台输出编码。|  
|`StdOutEncoding`|可选 `String` 输出参数。<br /><br /> 指定捕获的任务标准输出流的编码。 默认值为当前控制台输出编码。|  
|`WorkingDirectory`|可选 `String` 参数。<br /><br /> 指定要在其中运行命令的目录。|  
  
## <a name="remarks"></a>备注  
 在要执行的作业的特定 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务不可用时，此任务会非常有用。 但是，与更具体化的任务不同，`Exec` 任务无法从工具或其运行的命令中收集输出。  
  
 `Exec` 任务调用 cmd.exe 而不是直接调用进程。  
  
 除本文档列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类。 有关这些其他参数及其说明的列表，请参阅 [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例使用 `Exec` 任务来运行命令。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Binaries Include="*.dll;*.exe"/>  
    </ItemGroup>  
  
    <Target Name="SetACL">  
        <!-- set security on binaries-->  
        <Exec Command="echo y| cacls %(Binaries.Identity) /G everyone:R"/>  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
