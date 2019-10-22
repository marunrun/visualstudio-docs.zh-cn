---
title: 常规项目属性 (Android C++)| Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 65f4868b-b864-4989-a275-1e51869ef599
author: corob-msft
ms.author: corob
manager: jillfra
f1_keywords:
- VC.Project.VCConfiguration.OutputDirectory
- VC.Project.VCConfiguration.IntermediateDirectory
- VC.Project.VCConfiguration.TargetName
- VC.Project.VCConfiguration.TargetExt
- VC.Project.VCConfiguration.DeleteExtensionsOnClean
- VC.Project.VCConfiguration.BuildLogFile
- VC.Project.VCConfiguration.PlatformToolset
- VC.Project.VCConfiguration.ConfigurationType
- VC.Project.VCConfiguration.DeleteExtensionsOnClean
- VC.Project.VCConfiguration.UseOfSTL
- VC.Project.VCConfiguration.ThumbMode
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 4526a329b4e047a449995b7b5ef66362aff1cc8f
ms.sourcegitcommit: 6ae0a289f1654dec63b412bfa22035511a2ef5ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71950590"
---
# <a name="general-project-properties-android-c"></a>常规项目属性 (Android C++)

属性 | 说明 | 选项
--- | ---| ---
输出目录 | 指定输出文件目录的相对路径；可以包含环境变量。
中间目录 | 指定中间文件目录的相对路径；可以包含环境变量。
Target Name | 指定此项目将生成的文件名。
目标扩展名 | 指定此项目将生成的文件扩展名。 （示例：.exe 或 .dll   ）
清除时要删除的扩展名 | 分号分隔的通配符规范，指定在清除或重新生成时要删除中间目录中的哪些文件。
生成日志文件 | 指定启用生成日志时要写入的生成日志文件。
平台工具集 | 指定用于生成当前配置的工具集；如果未设置，则将使用默认工具集
配置类型 | 指定此配置生成的输出类型。 | 动态库 (.so) - 动态库 (.so   )<br>静态库 (.a) - 静态库 (.a   )<br>实用工具 - 实用程序 <br>生成文件 - 生成文件 <br>
目标 API 级别 | 被此配置当作目标的 Android NDK API 级别。
STL 的使用 | 指定要用于此配置的 C++ 标准库。 | 最小 C++ 运行时库 (system) <br>C++ 运行时静态库 (gabi++_static) <br>C++ 运行时共享库 (gabi++_shared) <br>STLport 运行时静态库 (stlport_static) <br>STLport 运行时共享库 (stlport_shared) <br>GNU STL 静态库 (gnustl_static) <br>GNU STL 共享库 (gnustl_shared) <br>LLVM libc++ 静态库 (c++_static) <br>LLVM libc++ 共享库 (c++_shared) <br>
Thumb 模式 | 生成执行 Thumb 微架构的代码。 仅适用于 ARM 架构。 | Thumb <br>ARM <br>已禁用 <br>
