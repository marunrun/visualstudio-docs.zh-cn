---
title: SccBeginBatch 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 264d9057bf4f17281d6d8a16ed3a6794004e0e21
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189558"
---
# <a name="sccbeginbatch-function"></a>SccBeginBatch 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数将启动批处理序列的源代码管理操作。 [SccEndBatch](../extensibility/sccendbatch-function.md)将调用以结束该批处理。 这些批不能嵌套。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccBeginBatch(void);  
```  
  
#### <a name="parameters"></a>Parameters  
 无。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|SCC_OK|一批操作已成功开始。|  
|SCC_E_UNKNOWNERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 使用源控制批处理以跨多个项目或多个上下文中执行相同操作。 若要在批处理操作期间消除冗余的每个项目对话框从用户体验，可以使用批处理。 `SccBeginBatch`函数和[SccEndBatch](../extensibility/sccendbatch-function.md)作为函数对用于指示的开头和结尾的操作。 它们不能嵌套。 `SccBeginBatch` 设置一个标志，指示批处理操作正在进行。  
  
 批处理操作生效时，源代码管理插件应为用户提供最多一个对话框中的任何问题，并对所有后续操作应用来自该对话框中的响应。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccEndBatch](../extensibility/sccendbatch-function.md)
