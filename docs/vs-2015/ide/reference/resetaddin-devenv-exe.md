---
title: -ResetAddin (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- disable addin
- addin state
- reset addin
ms.assetid: 9e339c8d-d768-4d86-8f45-2f479fc8255b
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6321433b506d41df57150b5a135a800a16cef0ab
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65689679"
---
# <a name="resetaddin-devenvexe"></a>/ResetAddin (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

移除与指定外接程序关联的命令和命令用户界面。  
  
## <a name="syntax"></a>语法  
  
```  
Devenv /ResetAddin AddIn  
```  
  
## <a name="arguments"></a>自变量  
 `AddIn`  
 可选。 外接程序的命令名称。  
  
## <a name="remarks"></a>备注  
 默认情况下，外接程序的命令名称等于 *\<AddInSolutionName>*.Connect<em>.\<AddInSolutionName></em>，并在 Connect.cs 中显示为 `Exec` 方法的 `commandName` 参数。 还可以通过开始在 Visual Studio 的“命令”窗口中键入外接程序的名称并使用 Intellisense 填充其余部分来验证命令名称。  
  
## <a name="example"></a>示例  
 以下示例启动 Visual Studio 并阻止 `MyAddin` 外接程序在启动时运行。  
  
```  
Devenv.exe /ResetAddin MyAddin.Connect.MyAddin  
```  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)   
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
