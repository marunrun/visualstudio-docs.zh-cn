---
title: 类型可视化器和自定义查看器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b8def9d28279f601ff488fca457982806629c0b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712468"
---
# <a name="type-visualizer-and-custom-viewer"></a>类型可视化器和自定义查看器
类型可视化工具是以特定格式显示数据片段的组件。 格式完全取决于实现可视化工具的人员，无论是最终用户还是可视化工具的第三方供应商。

 自定义查看器是自定义表达式赋值器的一部分，该计算器以特定格式显示数据片段。 此格式完全由自定义查看器的实现者决定，这意味着该格式由表达式赋值器 （EE） 的实现者决定。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>支持表达式赋值器中的类型可视化器
 EE 支持一组可视化工具可访问的接口，支持类型可视化器[：IEE 可视化服务](../../extensibility/debugger/reference/ieevisualizerservice.md)接口和[IEE 可视化数据提供程序](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)等接口。 但是，EE 不负责实现类型可视化工具本身：EE 仅允许外部可视化工具访问其类型信息。 此类可视化工具可能随 EE 一起运输，并安装在 Visual Studio 的相应位置，由其他第三方供应商甚至最终用户提供。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>支持表达式赋值器中的自定义查看器
 EE 还可以支持自定义查看器，其中 EE 本身提供用于查看数据类型的代码。 自定义查看器实现[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)接口，该接口处理以所需的任何格式显示数据的所有职责;查看器可以完全控制显示，甚至可以修改数据。 产品发货时，EE 提供的任何自定义查看器都随 EE 一起使用。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算器](../../extensibility/debugger/expression-evaluator.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
