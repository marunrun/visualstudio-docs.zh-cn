---
title: 特定于 Visual C++ 的 MSBuild 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks specific to Visual C++
ms.assetid: 05410f0c-7356-4692-bc00-20664421c9ff
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 452c3b408ab6471963124e61bc803e99eb6be80d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686911"
---
# <a name="msbuild-tasks-specific-to-visual-c"></a>特定于 Visual C++ 的 MSBuild 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

任务提供在生成过程中运行的代码。 安装 Visual C++ 后，除了随 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 安装的任务外，以下任务也可用。 有关详细信息，请参阅 [MSBuild (Visual C++) 概述](https://msdn.microsoft.com/library/dd258f6f-ab51-48d9-b274-f7ba911d05ca)。  
  
 除了特定于每个任务的参数外，每个任务还具有以下参数。  
  
|参数|描述|  
|---------------|-----------------|  
|`Condition`|可选 `String` 参数。<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 引擎使用 `Boolean` 表达式来确定是否执行此任务。 有关 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 支持的条件的信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
|`ContinueOnError`|可选参数。 可以包含下列值之一：<br /><br /> -   **WarnAndContinue** 或 **true**。 当任务失败时，[Target](../msbuild/target-element-msbuild.md) 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为警告<br />-   **ErrorAndContinue**。 当任务失败时，`Target` 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为错误。<br />-   **ErrorAndStop** 或 **false**（默认值）。 当任务失败时，将不会执行 `Target` 元素中的剩余任务和生成，并且整个 `Target` 元素和生成都被视为已失败。<br /><br /> 4\.5 之前的 .NET Framework 版本仅支持 `true` 和 `false` 值。<br /><br /> 有关详细信息，请参阅[如何：忽略任务中的错误](../msbuild/how-to-ignore-errors-in-tasks.md)。|  
  
## <a name="related-topics"></a>相关主题  
  
|Title|描述|  
|-----------|-----------------|  
|[BscMake 任务](../msbuild/bscmake-task.md)|包装 Microsoft 浏览信息维护实用工具 (bscmake.exe)。|  
|[CL 任务](../msbuild/cl-task.md)|包装 Visual C++ 编译器工具 (cl.exe)。|  
|[CPPClean 任务](../msbuild/cppclean-task.md)|删除生成 Visual C++ 项目时 MSBuild 创建的临时文件。|  
|[LIB 任务](../msbuild/lib-task.md)|包装 Microsoft 32 位库管理器工具 (lib.exe)。|  
|[链接任务](../msbuild/link-task.md)|包装 Visual C++ 链接器工具 (link.exe)。|  
|[MIDL 任务](../msbuild/midl-task.md)|包装 Microsoft 接口定义语言 (MIDL) 编译器工具 (midl.exe)。|  
|[MT 任务](../msbuild/mt-task.md)|包装 Microsoft 清单工具 (mt.exe)。|  
|[RC 任务](../msbuild/rc-task.md)|包装 Microsoft Windows 资源编译器工具 (rc.exe)。|  
|[SetEnv 任务](../msbuild/setenv-task.md)|设置或删除指定环境变量的值。|  
|[VCMessage 任务](../msbuild/vcmessage-task.md)|记录生成期间的警告消息和错误消息。|  
|[XDCMake 任务](../msbuild/xdcmake-task.md)|包装 XML 文档工具 (xdcmake.exe)，它将 XML 文档注释 (.xdc) 文件合并到一个 .xml 文件中。|  
|[XSD 任务](../msbuild/xsd-task.md)|包装从源生成架构或类文件的 XML 架构定义工具 (Xsd.exe)。|  
|[MSBuild 引用](../msbuild/msbuild-reference.md)|介绍 MSBuild 系统的元素。|  
|[任务](../msbuild/msbuild-tasks.md)|介绍任务，这些任务是代码单元，可以组合起来以产生生成。|  
|[任务写入](../msbuild/task-writing.md)|描述如何创建任务。|
