---
title: 分析 SharePoint 应用程序的性能 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Profiling.SilverlightWebPartOnly
- VS.SharePointTools.Profiling.DotNetTrustLevel
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 72739cd1063298a2dafc71976fd45360bc2d6ec2
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189206"
---
# <a name="profile-the-performance-of-sharepoint-applications"></a>分析 SharePoint 应用程序的性能

如果您的 SharePoint 应用程序的运行速度缓慢或效率低下，则可以使用 Visual Studio 中的分析功能来确定有问题的代码和其他元素。 通过使用负载测试功能，你可以确定 SharePoint 应用程序在压力下的执行方式，例如，许多用户同时访问应用程序时。 通过运行 web 性能测试，你可以衡量应用程序在 web 上的执行方式。 通过使用编码的 UI 测试，您可以验证整个 SharePoint 应用程序（包括其用户界面）是否正常工作。 将这些测试一起使用时，它们可以帮助你在部署应用程序之前确定性能问题。

## <a name="profile-tools-overview"></a>配置文件工具概述

分析是指观察和记录应用程序在运行时的性能行为的过程。 通过分析你的应用程序，你可以发现一些问题，如瓶颈、低效的代码和内存分配问题，这会导致应用程序运行缓慢或占用太多内存。 例如，你可以使用分析来识别代码中的热点，代码段是经常调用的代码段，并可能会降低应用程序的总体性能。 确定热点后，通常可以优化或消除它们。

您可以在集成开发环境（IDE）中使用多个分析工具来确定和查找这些类型的性能问题。 对于 SharePoint 项目，这些工具的工作方式与其他同类 Visual Studio 项目相同。 分析工具性能向导将引导你完成创建使用指定测试的性能会话的过程。 性能会话是一组用于从应用程序收集性能信息的配置数据，以及一个或多个分析运行的结果。 性能会话存储在项目文件夹中，您可以在**性能资源管理器**中查看它们。 有关详细信息，请参阅[了解性能收集方法](../profiling/understanding-performance-collection-methods.md)。

在应用程序上创建并运行配置文件分析后，报表将提供有关其性能的详细信息。 此报表可以包括诸如一段时间内的 CPU 使用情况图、分层函数调用堆栈或调用关系图等项。 报表的确切内容可能会有所不同，具体取决于所运行的测试类型，如采样或检测。 有关详细信息，请参阅[分析工具报表概述](../profiling/performance-report-overview.md)。

## <a name="performance-session-process"></a>性能会话进程

若要分析应用程序，请首先使用分析工具性能向导来创建性能会话。 在菜单栏上，选择 "**分析**"、"**启动性能向导**"。 完成向导时，请输入性能会话所需的信息，例如所需的配置文件方法和要分析的应用程序。 有关详细信息，请参阅[如何：使用性能向导分析网站或 Web 应用程序](../profiling/how-to-collect-performance-data-for-a-web-site.md)。 作为替代方法，可以使用命令行选项来设置和运行性能会话。 有关详细信息，请参阅[从命令行使用分析工具](../profiling/using-the-profiling-tools-from-the-command-line.md)。 如果要手动配置性能会话的每个方面，请参阅[如何：使用分析工具手动创建性能会话](../profiling/how-to-manually-create-performance-sessions.md)。 还可以通过单元测试创建性能会话，方法是在 "**测试结果**" 窗口中打开单元测试的快捷菜单，然后选择 "**创建性能会话**"。

设置性能会话后，将保存会话配置，并将服务器配置为提供分析数据，并运行应用程序。 使用应用程序时，会将性能数据写入日志文件。 性能会话在 "**目标**" 文件夹下**性能资源管理器**中列出。 性能会话完成后，其报表将显示在**性能资源管理器**的 "**报表**" 文件夹中。 若要显示报表，请在**性能资源管理器**中打开它。 若要查看或配置性能会话的属性，请在**性能资源管理器**中打开其快捷菜单，然后选择 "**属性**"。 有关性能会话的特定属性的详细信息，请参阅[配置分析工具的性能会话](../profiling/configuring-performance-sessions.md)。 有关如何解释性能会话结果的信息，请参阅[分析分析工具数据](../profiling/analyzing-performance-tools-data.md)。

## <a name="stress-test"></a>压力测试

可以通过在 Visual Studio 中创建负载测试和 web 性能测试，来分析应用程序的压力性能。 当你在 Visual Studio 中创建负载测试时，可以指定用于测试应用程序的因素（称为方案）组合。 这些因素包括负载模式、测试组合模型、测试组合、网络组合和 web 浏览器组合。 负载测试方案可以包括单元测试和 web 性能测试。

图1：负载测试结果示例

![运行负载测试关系图视图](../sharepoint/media/load-webgraphs.png "运行负载测试图形视图")

Web 性能测试模拟最终用户可能与 SharePoint 应用程序交互的方式。 可以通过在浏览器会话中记录 HTTP 请求或使用**Web 性能测试记录器**来创建 web 性能测试。 浏览器会话完成后，web 请求将显示在**Web 性能测试编辑器**中。 然后，你可以在**Web 性能测试结果查看器**中调试结果。 你还可以使用**Web 性能测试编辑器**手动生成 web 性能测试。

## <a name="test-user-interfaces"></a>测试用户界面

编码的 UI 测试通过其用户界面（UI）自动驱动您的 SharePoint 应用程序。 这些测试涵盖了 UI 控件（如按钮和菜单）来验证它们是否正常工作。 如果在 UI 中执行验证或其他逻辑（例如在网页中），则这种测试特别有用。 你还可以使用编码的 UI 测试来自动执行手动测试。 为 SharePoint 应用程序创建编码的 UI 测试的方式与为其他类型的应用程序创建测试的方式相同。 有关详细信息，请参阅[通过编码的 UI 测试来测试 SharePoint 2010 应用程序](/visualstudio/test/testing-sharepoint-2010-applications-with-coded-ui-tests?view=vs-2015)。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[演练：分析 SharePoint 应用程序](../sharepoint/walkthrough-profiling-a-sharepoint-application.md)|演示如何对 SharePoint 应用程序执行采样分析分析。|
|[发布前对应用进行性能测试](/azure/devops/test/load-test/run-performance-tests-app-before-release?view=vsts)|介绍如何创建负载测试，从而帮助你对 SharePoint 应用程序进行压力测试。|
|[单元测试代码](../test/unit-test-your-code.md)|介绍如何使用单元测试在代码中查找逻辑错误。|
|[使用编码的 UI 测试来测试 SharePoint 2010 应用程序](/visualstudio/test/testing-sharepoint-2010-applications-with-coded-ui-tests?view=vs-2015)|介绍如何测试您的 SharePoint 应用程序的用户界面。|

## <a name="see-also"></a>请参阅

- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [提高代码质量](../test/improve-code-quality.md)