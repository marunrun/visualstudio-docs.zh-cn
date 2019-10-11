---
title: 常规项目属性（Android C++ 生成文件）| Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: f76d717c-56ed-4373-8cf9-9bd1a053a4cd
author: corob-msft
ms.author: corob
manager: jillfra
f1_keywords:
- VC.Project.VCConfiguration.OutputDirectory
- VC.Project.VCConfiguration.IntermediateDirectory
- VC.Project.VCConfiguration.BuildLogFile
- VC.Project.VCConfiguration.ConfigurationType
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: b7fa1b91951e7a3fb145cc26275016037d1b5f2b
ms.sourcegitcommit: 6ae0a289f1654dec63b412bfa22035511a2ef5ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71950580"
---
# <a name="general-project-properties-android-c-makefile"></a>常规项目属性（Android C++ 生成文件）

Property | 说明 | 选项
--- | ---| ---
输出目录 | 指定输出文件目录的相对路径；可以包含环境变量。
中间目录 | 指定中间文件目录的相对路径；可以包含环境变量。
生成日志文件 | 指定启用生成日志时要写入的生成日志文件。
配置类型 | 指定此配置生成的输出类型。 | 动态库 (.so) - 动态库 (.so   )<br>静态库 (.a) - 静态库 (.a   )<br>实用工具 - 实用程序 <br>生成文件 - 生成文件 <br>
