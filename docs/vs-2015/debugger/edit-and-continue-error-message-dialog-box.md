---
title: "\"编辑并继续\" 错误消息对话框 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.ENC.SupportedButNotAvailable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5437ef982309ef8595f08283f2685e93d346e764
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62428262"
---
# <a name="edit-and-continue-error-message-dialog-box"></a>“编辑并继续”错误消息对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你使用支持 "编辑并继续" 的语言进行调试时，将显示此对话框，但 " **编辑并继续** " 不能用于所做的代码更改类型。 此框中的错误消息提供了更加详细的说明。 此对话框出现的可能原因包括：  
  
- 尝试在启用非托管调试时编辑托管代码。 “编辑并继续”不可用于混合模式调试。  
  
- 尝试编辑 SQL Server 代码。  
  
- 尝试在调试 Dr. Watson 转储时编辑代码。  
  
- 您尝试在发生未经处理的异常之后编辑代码，但未选择 "**在未经处理的异常上展开调用堆栈**" 选项。  
  
- 尝试在调试嵌入的运行时应用程序时编辑代码。  
  
- 尝试在附加到的程序中编辑代码，而不是从 " **调试** " 菜单启动。  
  
- 尝试编辑优化的代码。  
  
- 尝试在目标为 64 位应用程序时编辑托管代码。 如果希望使用“编辑并继续”，必须将目标平台设置为 x86  (*项目***属性**、"**编译**" 选项卡、"**高级编译器**" 设置。 ) 。  
  
- 尝试编辑在调试过程中修改过并已重新加载的程序集中的代码。  
  
- 尝试编辑尚未加载的程序集中的代码。  
  
- 开始调试旧版本的应用程序（由于新版本具有生成错误）。  
  
- 尝试在代码运行时编辑代码。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **正常**  
 退出对话框并取消之前的编辑尝试。  
  
## <a name="see-also"></a>另请参阅  
 [受支持的代码更改 (C++)](../debugger/supported-code-changes-cpp.md)
