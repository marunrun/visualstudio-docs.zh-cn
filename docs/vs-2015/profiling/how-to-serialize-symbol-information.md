---
title: 如何：序列化符号信息 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Performance.General
helpviewer_keywords:
- profiling tools, serializing symbol information
- performance tools, serializing symbol information
ms.assetid: 9e0da706-6325-4073-83d1-aeab3b7c137a
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c4ea056c48525014fffad0243dfeb4dd40a8daa3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687012"
---
# <a name="how-to-serialize-symbol-information"></a>如何：序列化符号信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以序列化分析应用程序所需的符号。 符号序列化的作用是将符号添加到 .vsp 文件中。 通过向 .vsp 文件添加符号信息，其他人可以在没有原始符号访问权限的情况下分析性能报告。 如果未序列化符号，则需要有受检测的原始 .exe 和 .pdb 文件才能分析 .vsp 文件。  
  
### <a name="to-automatically-serialize-symbol-information"></a>自动序列化符号信息  
  
1. 在 **“工具”** 菜单上，单击 **“选项”**。  
  
     随即出现“选项”对话框。  
  
2. 单击“性能工具”。  
  
3. 在“常规设置”下，选择“自动序列化符号信息”。  
  
## <a name="see-also"></a>请参阅  
 [配置性能会话](../profiling/configuring-performance-sessions.md)   
 [如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)   
 [如何：保存已分析的报告文件](https://msdn.microsoft.com/0340ddde-caf4-48ac-8af3-d15dcdade556)
