---
title: 如何：指定要启动的二进制文件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.itemlaunch
helpviewer_keywords:
- profiling tools, launching
- performance tools, launching
- performance sessions, launching
ms.assetid: ba77fcf4-8d78-49f1-b8f3-7dd0acf84306
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 919e84393cf4aef929a504aadbefe905afe24bfb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203428"
---
# <a name="how-to-specify-the-binary-to-start"></a>如何：指定要启动的二进制文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要分析二进制文件（如 DLL），必须在“\<目标> 属性页”对话框中输入信息  。 这些信息指示 DLL 项目查找调用应用程序的位置。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
### <a name="to-specify-the-executable-to-start"></a>指定要启动的可执行文件  
  
1. 在“性能资源管理器”  中，右键单击目标二进制文件，然后单击“属性”  。  
  
2. 在“属性页”对话框中单击“启动”属性   。  
  
3. 选中“重写项目属性”复选框  。  
  
4. 在“要启动的可执行文件”文本框中，指定文件的位置  。  
  
5. 在“参数”文本框中，指定启动应用程序所需的参数  。  
  
6. 在“工作目录”文本框中  ，指定目录的位置。  
  
7. 单击 **“确定”** 。  
  
## <a name="see-also"></a>请参阅  
 [配置性能会话](../profiling/configuring-performance-sessions.md)
