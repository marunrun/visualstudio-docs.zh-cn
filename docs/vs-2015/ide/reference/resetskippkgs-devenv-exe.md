---
title: /ResetSkipPkgs (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /ResetSkipPkgs Devenv switch
- Devenv, /ResetSkipPkgs switch
- ResetSkipPkgs switch
ms.assetid: 7ece64f9-cfa4-4b34-b0d9-1c338b9557b3
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 207ceb92d84c2186aeec49c205d8d32f4d7aa969
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665574"
---
# <a name="resetskippkgs-devenvexe"></a>/ResetSkipPkgs (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

清除由希望避免 VSPackages 加载问题的用户添加到 VSPackages 的跳过加载选项，然后启动 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。

## <a name="syntax"></a>语法

```
Devenv /ResetSkipPkgs
```

## <a name="remarks"></a>备注
 SkipLoading 标记的状态禁用 VSPackage 加载，清除这些标记可重新启动 VSPackage 的加载。

## <a name="example"></a>示例
 以下示例清除了所有 SkipLoading 标记。

```
Devenv.exe /ResetSkipPkgs
```

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
