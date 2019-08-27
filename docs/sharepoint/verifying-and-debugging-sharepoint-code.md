---
title: 验证和调试 SharePoint 代码 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- unit testing [SharePoint development in Visual Studio]
- IntelliTrace [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, IntelliTrace
- SharePoint development in Visual Studio, unit testing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7b57e07245631d37594d66ea7907b16efd817b2b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008233"
---
# <a name="verify-and-debug-sharepoint-code"></a>验证和调试 SharePoint 代码
通过使用 IntelliTrace 和单元测试，您可以更轻松地调试 SharePoint 解决方案，并确保解决方案中的每个方法都正常运行。 按照与其他类型的项目的相同过程，可以在 Visual Studio 中的 SharePoint 项目中使用这些功能。

## <a name="intellitrace"></a>Intellitrace
通过使用 IntelliTrace，您不仅能确定 SharePoint 解决方案的当前状态，还能确定过去发生的事件以及这些事件发生的上下文。 您可在 SharePoint 解决方案中记录了感兴趣的事件的不同时间点来回切换，并可查看变量在每个时间点的状态和值。 通过使用此动态导航，您可以快捷方便地调试 SharePoint 解决方案，而不必设置很多断点。 你可以调试会话保存到 IntelliTrace 日志 (*.iTrace*) 文件，更高版本中 Visual Studio Enterprise 中，将其打开并执行崩溃后调试。 *.ITrace*文件包括有关何时何地特定 SharePoint 错误的发生，详细的信息，以便您可以更轻松地找出导致错误的原因。 中的信息 *.iTrace*文件是统一记录系统 (ULS) 在 SharePoint 中创建的完整的错误日志的子集。 此信息包括特定于 SharePoint 的事件，例如打开或关闭用户配置文件的时间，以及加载、读取或更改 SharePoint 项目中的属性的时间。 您可以配置 IntelliTrace 记录的事件。 有关详细信息，请参阅[使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)。

当 SharePoint 发生错误时，错误对话框将显示该特定错误的“相关 ID”标识符。 此外可以获取关联 Id 中列出的事件 *.iTrace*文件。 若要显示所有的事件所发生的具有给定的相关 ID 的列表，可以输入中的 ID**分析**IntelliTrace 摘要页部分。 在此部分中，可以选择是仅显示所发生事件的名称，还是显示事件名称及其调用信息（例如函数名、出口点和入口点、参数及返回值）。

可以在 IntelliTrace 中获得 Visual Studio 事件，通过选择**F5**密钥。 不过若要获得特定于 SharePoint 的事件，您必须使用 Microsoft Monitoring Agent 在 SharePoint 解决方案中收集 IntelliTrace 数据。 此工具可收集 IntelliTrace 数据并创建 *.iTrace*部署 Visual Studio 外部的应用程序的文件。 有关详细信息，请参阅[IntelliTrace 功能](../debugger/intellitrace-features.md)并[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。

## <a name="unit-test"></a>单元测试
通过执行单元测试，在代码编写和运行测试的测试方法代码中，可以更轻松地找到错误。 这些方法包含空变量和一个断言语句，可用于验证逻辑和项目根据 SharePoint 对象模型的功能。 有关详细信息，请参阅[单元测试代码](../test/unit-test-your-code.md)。

### <a name="support-for-microsoft-fakes-framework"></a>对 Microsoft Fakes 框架的支持
SharePoint 项目支持 Microsoft Fakes，Microsoft Fakes 是一种隔离框架，在其中你可以在基于 .NET Framework 的应用程序中创建基于委托的测试存根和填充码。 使用 Fakes 框架，你可以在单元测试中创建、维护和注入虚拟实现。 这些存根和填充码会将你的单元测试与环境隔离。 您可以创建存根，以测试使用接口或具有可重写方法的非密封类的代码。 你可以创建填充码，以将对具有静态或不可重写方法的密封类的硬编码调用重定向到另一填充码实现。 您还可以使用存根类型和填充码类型的委托，动态自定义各个存根成员的行为。 有关详细信息，请参阅[隔离受测代码使用 Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md)。

## <a name="related-articles"></a>相关文章

|标题|描述|
|-----------|-----------------|
|[IntelliTrace](../debugger/intellitrace.md)|说明如何使用 IntelliTrace 更轻松地调试 Visual Studio 解决方案。|
|[演练：使用 IntelliTrace 调试 SharePoint 应用程序](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)|演示如何使用 IntelliTrace 找出 SharePoint 项目中的编码错误。|
|[单元测试代码](../test/unit-test-your-code.md)|介绍如何使用单元测试在代码中查找逻辑错误。|

## <a name="see-also"></a>请参阅

- [提高代码质量](../test/improve-code-quality.md)