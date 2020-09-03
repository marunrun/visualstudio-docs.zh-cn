---
title: 跨多个项目连接应用设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bca17fdc440fc373d0d4811ed57cd5d27a6c201a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203846"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>跨多个项目连接应用设置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用源代码管理插件 API 1.2 生成的源代码管理插件可以使用批处理操作在多个项目或多个连接上下文中执行相同的源代码管理操作。 批处理可用于从用户体验中消除冗余的、每个项目的对话框。  
  
 如果用户在使用源代码管理插件 API 1.1 生成的源代码管理插件中选择属于多个连接的多个项， (例如，不同的文件共享计算机上的两个 Web 项目) 并将其签出，则用户会反复看到同一个对话框。 即使用户在对话框中单击 " **应用到所有** 项" 复选框，也会发生这种情况，因为 IDE 会重置每个连接上下文的状态。  
  
## <a name="new-capability-flag"></a>新建功能标志  
 `SccBeginBatch` 函数设置 `SCC_CAP_BATCH` 标志以指示正在进行批处理操作  
  
## <a name="new-functions"></a>新函数  
 以下新函数支持批处理操作：  
  
- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)  
  
- [SccEndBatch](../../extensibility/sccendbatch-function.md)  
  
  `SCCBeginBatch`函数启动一组源代码管理操作。 `SccEndBatch` 关闭组。 这些组可能不是嵌套的。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
