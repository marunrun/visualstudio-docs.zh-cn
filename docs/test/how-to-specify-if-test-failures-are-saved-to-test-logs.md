---
title: 保存测试失败的负载测试日志
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios
- load tests, logging
ms.assetid: 08a7fe98-a7f7-4b8d-94a3-ec82b65a2aaf
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ef80a10954e9cf58db04e46f11934ffd86974bea
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786099"
---
# <a name="how-to-specify-if-test-failures-are-saved-to-test-logs-using-the-load-test-editor"></a>如何：指定是否使用负载测试编辑器将测试失败保存到测试日志中

在用“新建负载测试向导”创建负载测试之后，可以使用“负载测试编辑器”更改负载测试属性，以满足测试需求和目标。 请参阅[演练：创建和运行负载测试](../test/walkthrough-create-and-run-a-load-test.md)。 通过更改“测试未通过时保存日志”属性，可以指定当负载测试中测试未通过时是否希望保存测试日志。

> [!NOTE]
> 有关运行设置属性及其说明的完整列表，请参见[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-specify-if-the-test-log-is-saved-when-a-test-fails-in-a-scenario"></a>指定当某个方案中测试未通过时是否保存测试日志

1. 打开一个负载测试。

     “负载测试编辑器”随即显示。 其中显示负载测试树。

2. 在负载测试树的“运行设置”文件夹中，选择要为其指定最大测试迭代数的运行设置节点。

3. 在“视图”菜单上选择“属性窗口”。

     该运行设置类别和属性将显示在“属性”窗口中。

4. 在“测试未通过时保存日志”属性中，选择 True 或 False 以指定当方案中的测试未通过时是否希望保存测试日志。

     更改完此属性后，请选择“文件”菜单上的“保存”。

     可以使用负载测试分析器的表视图来查看保存在日志中的数据。 有关详细信息，请参阅[在表视图中分析负载测试结果和错误](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)。

## <a name="see-also"></a>请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
- [演练：创建和运行负载测试](../test/walkthrough-create-and-run-a-load-test.md)