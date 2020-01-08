---
title: 从命令行设置负载测试运行设置
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, command line
- load tests, run settings, selecting
ms.assetid: 175d1d58-f09a-4449-b132-a29a394a7c8e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 760cf18062e607e9f9039c6cc5f4adf409134cb5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588988"
---
# <a name="how-to-select-a-load-test-run-setting-to-use-from-the-command-line"></a>如何：从命令行选择要使用的负载测试运行设置

负载测试包含运行设置，运行设置是会影响负载测试运行方式的属性  。 在“属性”  窗口中，运行设置按类别进行组织。 当负载测试运行时，它会使用当前设置为活动的运行设置。

如果负载测试只包含一个运行设置，则它始终为活动节点。 如果负载测试包含多个运行测试节点，则可以选择一个在从命令行运行负载测试时使用的节点。 请参阅[如何：向负载测试添加额外的运行设置](../test/how-to-add-additional-run-settings-to-a-load-test.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-change-the-run-setting-from-the-command-line"></a>从命令行更改运行设置

1. 如果要从命令行使用不同的运行设置来利用上下文参数策略，请使用以下命令：

    `Set Test.UseRunSetting= CorporateStagingWebServer`

2. 使用 mstest 运行负载测试：

    `mstest /testcontainer:loadtest1.loadtest`

## <a name="see-also"></a>请参阅

- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [如何：向负载测试添加额外的运行设置](../test/how-to-add-additional-run-settings-to-a-load-test.md)
- [如何：为负载测试选择活动运行设置](../test/how-to-select-the-active-run-setting-for-a-load-test.md)
