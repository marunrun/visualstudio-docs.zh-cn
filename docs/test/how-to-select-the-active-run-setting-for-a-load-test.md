---
title: 为负载测试选择运行设置
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, run settings, active
ms.assetid: ed6ff546-acfa-4dd8-b3a2-6e7455930ca4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 91ac811c1f55fdb9a662db679ebd2d038ecdd5dd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75588975"
---
# <a name="how-to-select-the-active-run-setting-for-a-load-test"></a>如何：为负载测试选择活动运行设置

在用“新建负载测试向导”创建负载测试之后，可以使用“负载测试编辑器”来更改方案属性以满足测试需求和目标   。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

一个负载测试可以包含一个或多个运行设置，运行设置是会影响负载测试运行方式的一组属性  。 在“属性”窗口中，运行设置按类别进行组织  。 当负载测试运行时，它会使用当前设置为活动的运行设置。

> [!NOTE]
> 有关运行设置属性及其说明的完整列表，请参见[负载测试运行设置属性](../test/load-test-run-settings-properties.md)。

如果负载测试只包含“运行设置”文件夹下的一个运行设置节点，那么该节点始终为活动节点  。 如果负载测试包含多个运行测试节点，则可以选择一个在运行负载测试时要使用的节点。 请参阅[如何：向负载测试中添加额外的运行设置](../test/how-to-add-additional-run-settings-to-a-load-test.md)。

在负载测试编辑器中，以“[Active]”后缀来标识活动运行设置  。

## <a name="select-the-active-run-setting"></a>选择活动运行设置

1. 打开一个负载测试。

2. 展开“运行设置”文件夹  。

3. 右键单击要使其成为活动节点的运行设置节点，然后选择“设置为活动的”  。

     在“负载测试编辑器”中，受影响的运行设置节点将用“[Active]”后缀来更新  。

     选定的运行设置将变为活动状态，并一直保持活动状态，直到您选择了其他要处于活动状态的运行设置。

> [!NOTE]
> 可以通过设置名为 `Test.UseRunSetting=<run setting name>` 的环境变量来重写活动的运行设置。 此方法在从命令行或批处理文件运行负载测试时非常有用。 您无需打开负载测试便可以选择不同的运行设置。

## <a name="specify-the-run-setting-to-use-from-the-command-line"></a>从命令行指定要使用的运行设置

通过从命令行设置环境变量，可以重写负载测试中的默认运行设置：

**设置 Test.UseRunSetting=PreProdEnvironment**

并运行测试：

**mstest /testcontainer:loadtest1.loadtest**

## <a name="see-also"></a>另请参阅

- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [如何：向负载测试添加额外的运行设置](../test/how-to-add-additional-run-settings-to-a-load-test.md)
