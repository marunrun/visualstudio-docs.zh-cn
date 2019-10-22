---
title: -Updateconfiguration (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /updateconfiguration Devenv switch
- Devenv, /updateconfiguration switch
- updateconfiguration Devenv switch
ms.assetid: 9a1084cc-8b68-4ccc-aaea-f95939164338
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 50773821b328ea81381744bc6f32b3907cd1c5bc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657918"
---
# <a name="updateconfiguration-devenvexe"></a>/Updateconfiguration (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通知 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 合并系统上的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 包，并检查 MEF 缓存中是否有任何更改。

## <a name="syntax"></a>语法

```
devenv /updateconfiguration
```

## <a name="remarks"></a>备注
 安装 VSIX 包时，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 会自动运行此命令。 应在修补文件后运行 `devenv.exe /updateconfiguration`，以便 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 更新 MEF 缓存。 这样便于评估是否进行了适当的修补。

## <a name="example"></a>示例
 以下命令行会使 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 合并系统上的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 包，并检查 MEF 缓存中是否有任何更改。

```
Devenv.exe /updateconfiguration
```

## <a name="see-also"></a>另请参阅
 在 Visual Studio [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)[中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)
