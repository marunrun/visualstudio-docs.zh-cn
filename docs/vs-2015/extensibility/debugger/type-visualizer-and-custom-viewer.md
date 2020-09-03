---
title: 类型可视化工具和自定义查看器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a85be2978abe35e91096b55fba5ec5281be25fbe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185312"
---
# <a name="type-visualizer-and-custom-viewer"></a>类型可视化工具和自定义查看器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

类型可视化工具是一个组件，它以非常特定的格式显示一段数据。 此格式完全由可视化工具的实施者决定，是最终用户还是可视化工具的第三方供应商。  
  
 自定义查看器是自定义表达式计算器的一部分，它以非常特定的格式显示一段数据。 此格式完全取决于自定义查看器的实施者，这意味着该格式由表达式计算器的实施者决定 (EE) 。  
  
## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>对表达式计算器中的类型可视化工具的支持  
 通过支持可视化工具可访问的一组接口（如 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) 和 [IEEVISUALIZERDATAPROVIDER](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)），EE 可支持类型可视化工具。 但请注意，EE 并不负责实现类型可视化工具本身： EE 只允许外部可视化工具访问其类型信息。 此类可视化工具可能随 EE 一起提供，并安装在 Visual Studio 中的适当位置，由其他第三方供应商提供，甚至由最终用户提供。  
  
## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>表达式计算器中的自定义查看器支持  
 EE 还可以支持自定义查看器，在该查看器中，EE 本身提供查看数据类型的代码。 自定义查看器实现了 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) 接口，该接口可处理以任意格式显示数据的所有职责;查看器可以完全控制显示，甚至可以允许修改数据。 EE 提供的任何自定义查看器在产品发布时均随附于 EE。  
  
## <a name="see-also"></a>另请参阅  
 [调试器组件](../../extensibility/debugger/debugger-components.md)   
 [表达式计算器](../../extensibility/debugger/expression-evaluator.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
