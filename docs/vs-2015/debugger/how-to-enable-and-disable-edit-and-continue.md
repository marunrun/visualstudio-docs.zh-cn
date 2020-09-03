---
title: 如何：启用和禁用 "编辑并继续" |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- /INCREMENTAL linker option
- Apply Code Changes command
- Edit and Continue, disabling
- code changes, applying in break mode
- INCREMENTAL linker option
- Edit and Continue, enabling
- break mode, applying code changes
- Edit and Continue, applying code changes
- Step command
- Go command
ms.assetid: fd961a1c-76fa-420d-ad8f-c1a6c003b0db
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 70914da9be4046589a0ca3b8e5fd4ae13210ca51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65689262"
---
# <a name="how-to-enable-and-disable-edit-and-continue"></a>如何：启用和禁用“编辑并继续”
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以在设计时在 " **选项** " 对话框中禁用或启用 "编辑并继续"。 无法在调试过程中更改此设置。  
  
 “编辑并继续”仅在调试版本中起作用。 对于本机 C++，“编辑并继续”需要使用 /INCREMENTAL 选项。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-enabledisable-edit-and-continue"></a>启用/禁用“编辑并继续”  
  
1. 打开 "调试选项" 页 (**工具/选项/调试**) 。  
  
2. 向下滚动到 " **编辑并继续** " 类别。  
  
3. 若要启用，请选中 " **启用编辑并继续** " 复选框。 若要禁用它，请清除该复选框。  
  
   > [!NOTE]
   > 如果启用了 IntelliTrace 并且收集 IntelliTrace 事件和调用信息，则会禁用“编辑并继续”。 有关详细信息，请参阅 [配置 IntelliTrace](https://msdn.microsoft.com/7657ecab-e07e-4b1b-872d-f05d966be37e)。  
  
4. 单击“确定”。  
  
   有关这些选项的详细信息，请参阅 " [常规"、"调试"、"选项" 对话框](../debugger/general-debugging-options-dialog-box.md)。  
  
## <a name="see-also"></a>另请参阅  
 [编辑并继续](../debugger/edit-and-continue.md)
