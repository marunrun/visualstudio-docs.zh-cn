---
title: -LCID (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- language default
- locale IDs, setting for IDE
- Devenv, /LCID switch
- locale IDs
- /l Devenv switch
- LCID devenv switch
- /lcid Devenv switch
ms.assetid: 3a3f4e70-ea66-4351-9d62-acb1dec30e8e
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0b1d83cca1da917a08b8765dae66fb240ca1dc75
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199213"
---
# <a name="lcid-devenvexe"></a>/LCID (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

设置集成开发环境 (IDE) 内文本、货币和其他值使用的默认语言。  
  
## <a name="syntax"></a>语法  
  
```  
devenv {/LCID|/l} LocaleID  
```  
  
## <a name="arguments"></a>自变量  
 `LocaleID`  
 必需。 指定的语言的 LCID（区域设置 ID）。  
  
## <a name="remarks"></a>备注  
 加载 IDE 并设置环境的默认自然语言。 此更改保留在会话中，并反映在 IDE 的“选项”对话框中“环境”选项的“国际设置”窗格上    。  
  
 如果指定的语言在用户的系统上不可用，则忽略 /LCID 开关。  
  
 下表列出了受 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 支持的语言的 LCID。  
  
|语言|LCID|  
|--------------|----------|  
|中文（简体）|2052|  
|和 SharePoint 2010 显示的“中文(繁体)”|1028|  
|英语|1033|  
|法语|1036|  
|德语|1031|  
|意大利语|1040|  
|日语|1041|  
|朝鲜语|1042|  
|西班牙语|3082|  
  
## <a name="example"></a>示例  
 此示例加载具有英语资源字符串的 IDE。  
  
```  
devenv /LCID 1033  
```  
  
## <a name="see-also"></a>另请参阅  
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)   
 [“选项”对话框 ->“环境”->“区域设置”](../../ide/reference/international-settings-environment-options-dialog-box.md)   
 [自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)
