---
title: /Run (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /run Devenv
- run Devenv switch
- applications [Visual Studio], running
- /r Devenv switch
- Devenv, /run switch
- r Devenv switch (/r)
ms.assetid: b1f22f9d-39a5-4918-8a2a-4b5c1e872665
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b2716995e8ff3a318262284b5733a471086c68c1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665524"
---
# <a name="run-devenvexe"></a>/Run (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

编译并运行指定的项目或解决方案。

## <a name="syntax"></a>语法

```
devenv {/run|/r} {SolutionName|ProjectName}
```

## <a name="arguments"></a>自变量
 `SolutionName`（必需）。 解决方案文件的完整路径和名称。

 `ProjectName`（必需）。 项目文件的完整路径和名称。

## <a name="remarks"></a>备注
 根据为活动解决方案配置指定的设置编译并运行指定项目或解决方案。 此开关启动集成开发环境 (IDE) ，并在项目或解决方案已完成运行后让该环境保持活动状态。

- 用双引号将含有空格的字符串引起来。

- “命令”窗口或使用 `/out` 开关指定的任何日志文件中都可显示摘要信息（包括错误）  。

## <a name="example"></a>示例
 该示例使用活动部署配置运行解决方案 `MySolution`。

```
devenv /run "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln"
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md) [/Runexit （devenv）](../../ide/reference/runexit-devenv-exe.md) [/Build （node.js）](../../ide/reference/build-devenv-exe.md) [/Rebuild （](../../ide/reference/rebuild-devenv-exe.md) devenv） [/out （devenv](../../ide/reference/out-devenv-exe.md) ）
