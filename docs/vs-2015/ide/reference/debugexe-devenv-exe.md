---
title: /DebugExe (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ac542ded884e922028c6cbc16447fb2a3241613b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193810"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

打开要调试的指定可执行文件。  
  
## <a name="syntax"></a>语法  
  
```  
Devenv /debugexe ExecutableFile  
```  
  
## <a name="arguments"></a>自变量  
 `ExecutableFile`  
 必需。 .exe 文件的路径和文件名称。  
  
 如果找不到 .exe 文件或不存在，不会显示任何警告或错误，并且 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 启动正常。  
  
## <a name="remarks"></a>备注  
 `ExecutableFile` 形式参数后的任何字符串都作为实际参数传递到此文件。  
  
## <a name="example"></a>示例  
 以下示例打开文件 `MyApplication.exe` 进行调试。  
  
```  
Devenv.exe /debugexe MyApplication.exe  
```  
  
## <a name="see-also"></a>另请参阅  
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
