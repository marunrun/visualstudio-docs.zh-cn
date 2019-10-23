---
title: 编辑负载测试
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Load Test Editor
- load tests, Load Test Editor
ms.assetid: ba16ed02-137e-40bf-a4cb-45d87d922d37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 65cfdde84e0a0e2bb1aa28e9d4b96e2505a93a57
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665026"
---
# <a name="edit-load-tests"></a>编辑负载测试

负载测试运行 Web 性能测试或单元测试，以模拟多用户同时访问同一服务器。 负载测试用于获得应用程序的压力和性能数据。 可以将负载测试配置为模拟各种负载情况，如用户负载和网络类型。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

负载测试由“方案”、“计数器集”和“运行设置”定义    。 下图说明[方案](../test/edit-load-test-scenarios.md)、[计数器集](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)和[运行设置](../test/load-test-run-settings-properties.md)之间的差异：

![负载测试体系结构](../test/media/load_test_editor.png)

## <a name="software-requirements"></a>软件要求

Web 性能和负载测试项目仅在 Visual Studio Enterprise 中可用。

## <a name="edit-load-test-scenario-settings"></a>编辑负载测试方案设置

方案用于对用户组与服务器应用程序交互的方式进行建模。 方案由负载模式、测试组合模式、测试组合、浏览器组合和网络组合构成。 一个负载测试可以有多个方案，单个方案可以包含多个 Web 性能测试和多个单元测试。 通过对类似设置进行分组，方案允许对性质类似的测试进行分组并一起运行这些测试。

有关详细信息，请参阅[编辑负载测试方案](../test/edit-load-test-scenarios.md)和[负载测试方案属性面板](../test/load-test-scenario-properties.md)。

## <a name="configure-and-manage-performance-counter-sets"></a>配置和管理性能计数器集

负载测试提供了按不同的技术组织在一起的命名计数器集，这些计数器集在分析性能计数器数据时十分有用。 计数器集包括“负载测试”、“IIS”、“ASP.NET”和“SQL”。 在使用“新建负载测试向导”  创建负载测试时，会为被指定包含在负载测试中的计算机配置一组初始的且非常重要的预定义计数器。 在“负载测试编辑器”中管理计数器。 

有关详细信息，请参阅[为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)。

## <a name="configure-and-manage-load-test-run-settings"></a>配置和管理负载测试运行设置

“运行设置”是能影响负载测试的运行方式的属性。 在“属性”  窗口中，运行设置按类别进行组织。

有关详细信息，请参阅[配置负载测试运行设置](../test/configure-load-test-run-settings.md)和[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。

## <a name="see-also"></a>请参阅

- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [分析阈值规则冲突](../test/analyze-threshold-rule-violations-in-load-tests.md)