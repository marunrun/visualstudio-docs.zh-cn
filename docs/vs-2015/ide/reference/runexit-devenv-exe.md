---
title: -Runexit (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- runexit Devenv switch
- Devenv, /runexit switch
- /runexit Devenv switch
ms.assetid: bfc94875-5fc0-4110-b961-d59c0b403790
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6d1158a12de8b8adfe20fa6d045b756abf8d7b3c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665498"
---
# <a name="runexit-devenvexe"></a>/Runexit (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

编译和运行指定的项目或解决方案，然后关闭集成开发环境 (IDE)。

## <a name="syntax"></a>语法

```
devenv /runexit {SolutionName|ProjectName}
```

## <a name="arguments"></a>自变量
 `SolutionName`（必需）。 解决方案文件的完整路径和名称。

 `ProjectName`（必需）。 项目文件的完整路径和名称。

## <a name="remarks"></a>备注
 根据为活动解决方案配置指定的设置编译并运行指定项目或解决方案。 此开关会在项目或解决方案处于运行状态时最小化 IDE，会在项目或解决方案完成运行后关闭 IDE。

- 用双引号将含有空格的字符串引起来。

- “命令”窗口或使用 `/out` 开关指定的任何日志文件中都可显示摘要信息（包括错误）  。

## <a name="example"></a>示例
 此示例会在最小化的 IDE 中使用活动部署配置运行解决方案 `MySolution`，然后关闭 IDE。

```
devenv /runexit "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln"
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md) [/Run （devenv）](../../ide/reference/run-devenv-exe.md) [/Build （node.js）](../../ide/reference/build-devenv-exe.md) [/Rebuild （](../../ide/reference/rebuild-devenv-exe.md) devenv） [/out （devenv](../../ide/reference/out-devenv-exe.md) ）
