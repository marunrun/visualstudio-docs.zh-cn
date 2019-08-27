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
ms.openlocfilehash: 8b59a3de88403300a46b7992a2dad72e3d6b59e0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563305"
---
# <a name="profile-the-performance-of-sharepoint-applications"></a>配置文件的 SharePoint 应用程序性能

如果您的 SharePoint 应用程序正在执行速度缓慢或效率低下，你可以使用 Visual Studio 中的分析功能以确定有问题的代码和其他元素。 通过使用负载测试功能，可以确定 SharePoint 应用程序在负载下，如多个用户同时访问该应用程序时的执行方式。 通过运行 web 性能测试，可以测量应用程序在 web 上找到的执行方式。 通过使用编码的 UI 测试，可以验证整个 SharePoint 应用程序，包括其用户界面，是否工作正常。 一起使用这些测试时，它们可以帮助你部署应用程序之前识别性能问题。

## <a name="profile-tools-overview"></a>配置文件工具概述

分析参考观察和记录您的应用程序的性能行为，在运行的过程。 通过分析应用程序，可以找到问题，例如瓶颈、 低效代码和内存分配问题，这导致应用程序运行缓慢或占用太多内存。 例如，可以使用分析来识别你的代码，其中一些代码片段的频繁调用，并可能会降低您的应用程序的整体性能的热点。 确认作用点后，通常可以优化或消除这些问题。

在集成的开发环境 (IDE) 中，可以使用若干分析工具来识别和查找这些类型的性能问题。 对于其他类型的 Visual Studio 项目一样，这些工具适用相同的方式对 SharePoint 项目。 分析工具性能向导将引导您完成创建使用指定的测试的性能会话。 性能会话是一组用于从应用程序，以及一个或多个分析运行的结果收集性能信息的配置数据。 性能会话存储在项目文件夹，并可以查看它们**性能资源管理器**。 有关详细信息，请参阅[了解性能收集方法](../profiling/understanding-performance-collection-methods.md)。

创建并在应用程序上运行的配置文件分析后，报表将提供有关其性能的详细信息。 此报表可随时间、 层次结构函数调用堆栈或调用树包含诸如的 CPU 使用率关系图。 报表的确切内容因测试运行，例如采样或检测的类型而异。 有关详细信息，请参阅[分析工具报告概述](http://go.microsoft.com/fwlink/?LinkId=224689)。

## <a name="performance-session-process"></a>性能会话进程

若要分析的应用程序，启动时通过使用分析工具性能向导创建性能会话。 在菜单栏上依次选择**分析**，**启动性能向导**。 完成向导，您输入到性能会话，例如所需的配置文件方法和要分析的应用程序所需的信息。 有关详细信息，请参阅[如何：配置文件的网站或 Web 应用程序使用性能向导](http://go.microsoft.com/fwlink/?LinkId=224692)。 或者，可以使用命令行选项来设置和运行性能会话。 有关详细信息，请参阅[分析工具从命令行使用](http://go.microsoft.com/fwlink/?LinkId=224703)。 如果你想要手动配置性能会话的各个方面，请参阅[如何：使用分析工具手动创建性能会话](http://go.microsoft.com/fwlink/?LinkId=224691)。 您还可以创建性能会话从单元测试，通过在**测试结果**窗口中，打开单元测试的快捷菜单，然后选择**创建性能会话**。

设置性能会话后，保存的会话配置、 服务器配置为提供分析数据和应用程序运行。 使用应用程序时，性能数据写入日志文件。 中列出了性能会话**性能资源管理器**下**目标**文件夹。 在性能会话完成后，其报表中出现**报表**中的文件夹**性能资源管理器**。 若要显示报表，请打开在**性能资源管理器**。 若要查看或配置性能会话的属性，请打开其快捷菜单中的**性能资源管理器**，然后选择**属性**。 性能会话的特定属性的详细信息，请参阅[分析工具配置性能会话](http://go.microsoft.com/fwlink/?LinkId=224694)。 有关如何解释结果的性能会话的信息，请参阅[对分析工具数据](http://go.microsoft.com/fwlink/?LinkId=224704)。

## <a name="stress-test"></a>压力测试

你可以通过在 Visual Studio 中创建负载测试和 web 性能测试分析您的应用程序的压力性能。 当在 Visual Studio 中创建负载测试时，您指定因素，名为的情况下，若要针对测试应用程序的组合。 这些因素包括负载模式、 测试组合模型、 测试组合、 网络组合和 web 浏览器组合。 负载测试方案可以包含单元测试和 web 性能测试。

图 1：负载测试结果的示例

![运行负载测试关系图视图](../sharepoint/media/load-webgraphs.png "运行负载测试关系图视图")

Web 性能测试模拟最终用户可能与 SharePoint 应用程序中进行交互。 您可以通过在浏览器会话中记录 HTTP 请求，或创建 web 性能测试**Web 性能测试记录器**。 中显示 web 请求**Web 性能测试编辑器**浏览器会话结束后。 你可以调试中的结果**Web 性能测试结果查看器**。 您可以通过使用手动生成 web 性能测试**Web 性能测试编辑器**。

## <a name="test-user-interfaces"></a>测试用户界面

编码的 UI 测试自动驱动通过其用户界面 (UI) 的 SharePoint 应用程序。 这些测试涵盖 UI 控件，如按钮和菜单，以验证它们正常。 此类测试不执行验证或其他逻辑是在 UI 中，例如在网页中的情况特别有用。 此外可以使用编码的 UI 测试来自动手动测试。 你创建编码的 UI 测试 SharePoint 应用程序相同的方式创建其他类型的应用程序的测试。 有关详细信息，请参阅[测试 SharePoint 2010 应用程序使用编码的 UI 测试](../test/testing-sharepoint-2010-applications-with-coded-ui-tests.md)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[演练：分析 SharePoint 应用程序](../sharepoint/walkthrough-profiling-a-sharepoint-application.md)|演示如何对 SharePoint 应用程序执行采样配置文件分析。|
|[发布前对应用进行性能测试](/azure/devops/test/load-test/run-performance-tests-app-before-release?view=vsts)|介绍如何创建负载测试，帮助您进行压力测试 SharePoint 应用程序。|
|[单元测试代码](../test/unit-test-your-code.md)|介绍如何使用单元测试在代码中查找逻辑错误。|
|[使用编码的 UI 测试来测试 SharePoint 2010 应用程序](../test/testing-sharepoint-2010-applications-with-coded-ui-tests.md)|介绍如何测试 SharePoint 应用程序的用户界面。|

## <a name="see-also"></a>请参阅

- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [提高代码质量](../test/improve-code-quality.md)