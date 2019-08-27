---
title: 键入可视化工具和自定义查看器 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185312"
---
# <a name="type-visualizer-and-custom-viewer"></a>类型可视化工具和自定义查看器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

类型可视化工具是非常特定的格式显示一段数据的组件。 此格式是完全取决于该可视化工具的实施者，无论是最终用户或第三方供应商的可视化工具。  
  
 自定义查看器是非常特定的格式显示一段数据自定义表达式计算器的一部分。 此格式是完全取决于自定义查看器中，这意味着格式是由表达式计算器 (EE) 实现的实施者。  
  
## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>表达式计算器中的类型可视化工具的支持  
 EE 可以通过支持一套可视化工具可以访问接口支持类型可视化工具： 接口如[IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)并[IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)。 但请注意，EE 概不负责实现类型可视化工具本身： EE 只允许外部可视化工具对其类型信息的访问。 此类可视化工具可能会随 EE 并安装在由其他第三方供应商或甚至最终用户提供的 Visual Studio 中的适当位置。  
  
## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>表达式计算器中的自定义查看器的支持  
 EE 还可以支持自定义查看器在其中 EE 本身提供了用于查看数据类型的代码。 自定义查看器实现[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)所需接口，处理的任何格式显示数据的所有任务; 查看器可以完全控制如何显示，并且甚至还可以允许要修改的数据。 在产品发布时提供 EE 的任何自定义查看器随附 EE。  
  
## <a name="see-also"></a>请参阅  
 [调试器组件](../../extensibility/debugger/debugger-components.md)   
 [表达式计算器](../../extensibility/debugger/expression-evaluator.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
