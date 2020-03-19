---
title: 向用于负载测试的计数器集添加计数器
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- counters, counter sets
- counter sets
- load tests, counter sets
ms.assetid: e17d0e71-f982-4fc1-a2df-a1065d37473d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b83d9c3624a4a268bfeba8a02b224fb9813ad7d1
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594323"
---
# <a name="how-to-add-counters-to-counter-sets-using-the-load-test-editor"></a>如何：使用负载测试编辑器向计数器集中添加计数器

使用“负载测试向导”创建负载测试时，会添加一个初始的计数器集。  该计数器集为您的负载测试提供了一组预定义计数器集。 有关详细信息，请参阅[为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 如果负载测试分布在多台远程计算机之间，则会将控制器和代理计数器映射到控制器和代理计数器集中。 有关如何在负载测试中使用远程计算机的详细信息，请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

在“负载测试编辑器”中管理计数器  。 已添加到测试中的计数器集会出现在负载测试的“计数器集”节点中。  创建负载测试后，可以向现有的计数器集中添加新的计数器。

## <a name="to-add-counters-to-a-counter-set"></a>向计数器集添加计数器

1. 打开一个负载测试。

2. 展开“计数器集”节点。  添加到负载测试中的所有计数器集都会显示出来。

    > [!NOTE]
    > 负载测试的层次结构树中还包含“运行设置”节点。  此节点包含“计数器集映射”节点，其中显示了所有计算机以及映射到这些计算机的计数器集。 

3. 右键单击一个现有的计数器集，然后选择“添加计数器”。 

     将显示“选取性能计数器”对话框。 

4. 在“计算机”下拉组合框中，键入要映射到的计算机的名称。  或者，也可以从下拉列表中选择一台计算机。

    > [!NOTE]
    > 因为在收集性能数据之前计数器集必须映射到一台计算机，所以必须指定收集性能数据的计算机。

5. 选择“性能类别”来筛选性能数据计数器的类别。  您将会看到两列数据供您从中选择性能计数器。

    > [!NOTE]
    > 有些计数器类别还会要求您选择一个实例。 例如，如果选择一个 SQL 计数器，还必须选择一个 SQL 实例，因为在目标计算机上可能会安装多个 SQL 实例。

6. 选择一个计数器和一个实例以添加到您的自定义计数器集中。

     \- 或 -

     选择“所有计数器”单选按钮来选择所有可用的计数器。 

7. 选择 **“确定”** 。

    > [!NOTE]
    > 还可以通过选择现有计数器或计数器类别，选择“复制”，然后将它粘贴到另一计数器集节点，从而向计数器集添加计数器。 可以删除那些复制了但不需要的多余计数器。

## <a name="see-also"></a>另请参阅

- [为负载测试中的计算机指定计数器集和阈值规则](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
