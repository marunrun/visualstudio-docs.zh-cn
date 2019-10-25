---
title: -DoNotLoadProjects (devenv.exe)
ms.date: 04/30/2019
ms.topic: reference
helpviewer_keywords:
- Devenv, /DoNotLoadProjects switch
- /DoNotLoadProjects Devenv switch
- DoNotLoadProjects Devenv switch
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34fe7dfed2774eace7d32b1c9041355b566d4e76
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654496"
---
# <a name="donotloadprojects-devenvexe"></a>/DoNotLoadProjects (devenv.exe)

**Visual Studio 2019 版本 16.1 中的新增功能**

打开指定的解决方案，而不加载任何项目。 有关详细信息，请参阅 [Visual Studio 中筛选的解决方案](../filtered-solutions.md)。

## <a name="syntax"></a>语法

```shell
devenv /DoNotLoadProjects SolutionName
```

## <a name="arguments"></a>自变量

*SolutionName*

必需。 要打开的解决方案的完整路径和名称。

## <a name="example"></a>示例

该示例将打开解决方案 MySln.sln 而不加载任何项目。

```shell
devenv /donotloadprojects MySln.sln
```

## <a name="see-also"></a>请参阅

- [Visual Studio 中筛选的解决方案](../filtered-solutions.md)
- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
