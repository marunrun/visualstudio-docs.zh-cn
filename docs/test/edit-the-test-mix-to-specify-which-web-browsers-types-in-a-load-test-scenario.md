---
title: 用于负载测试的浏览器测试组合
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, web browser types
- load tests, scenarios
- load tests, adding browsers
- load tests, removing browsers
ms.assetid: 47f981d9-3038-45cc-a486-82b9daf9a9a1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 394331ae06760e0547cfc2b5a37a6dcd357e3614
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114532"
---
# <a name="edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario"></a>编辑测试组合以指定在负载测试方案中包括哪些 Web 浏览器类型

浏览器组合提供了一种在负载测试方案中更真实地模拟负载的方法  。 负载是使用异类 Web 浏览器组合（而非单一种类的 Web 浏览器）生成的。 这样便创建了一种与你的应用程序所使用的 Web 浏览器更为接近的浏览器使用情形。

浏览器组合指定了虚拟用户在负载测试方案中运行特定 Web 浏览器类型的概率。 创建负载测试时，你可能希望模拟通过多个 Web 浏览器生成负载的情况。 从提供的 Web 浏览器集向浏览器组合中添加 Web 浏览器类型时，将在 Web 性能测试所提交的每个 HTTP 请求中添加一组与所选 Web 浏览器相关联的标头。

浏览器组合的工作方式与其他组合选项的工作方式相似。 Web 浏览器类型基于浏览器组合与虚拟用户随机关联。 该用户的测试基于你在组合中指定的概率在特定 Web 浏览器上运行。

指定了浏览器组合后，可以稍后向该组合中添加以及从中移除 Web 浏览器类型。 还可以使用组合控件来更改浏览器组合的分发方案。 通过组合控件，您可以轻松地调整方案中浏览器的分布。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="add-new-browsers-to-a-scenario"></a>向方案中添加新浏览器

### <a name="to-add-new-browsers-to-a-scenario"></a>向方案中添加新浏览器

1. 在为方案指定浏览器组合的过程中，选择“添加”  。

     新的浏览器项即添加到网格中。

    > [!NOTE]
    > 若要显示“编辑浏览器组合”对话框，请右键单击现有方案，然后选择“编辑浏览器组合”   。

2. 在“浏览器类型”列中，选择表示新项的箭头，然后选择所需的浏览器类型  。

3. （可选）调整混合控件以指定测试分布。

4. 完成浏览器的添加后，选择“确定”  。

## <a name="remove-browsers-from-a-scenario"></a>从方案中移除浏览器

### <a name="to-remove-browsers-from-a-scenario"></a>从方案中移除浏览器

1. 打开一个负载测试。

2. 右键单击要从中移除浏览器的方案，然后选择“编辑浏览器组合”  。

     将显示“编辑浏览器组合”对话框  。

3. 在网格中选择浏览器，然后选择“移除”  。

4. （可选）调整混合控件以指定测试分布。

5. 完成浏览器的移除后，选择“确定”  。

## <a name="about-the-mix-control"></a>关于混合控件

通过组合控件，可以调整负载测试方案中在测试、浏览器类型或网络类型之间分布的负载百分比。 可以通过移动滑块来调整百分比值。 调整浏览器类型的组合将指定虚拟用户在负载测试方案中运行特定浏览器类型的概率。

移动滑块时，所有可用项的百分比值都会发生变化。 如果移动两个以上的项，则添加或移除的量在其他项中均匀分布。 可以重写此行为。 对于某个特定项，如果选中锁定列中的复选框，则将锁定该项的指定百分比值。 随后移动滑块时，添加或移除的量只能应用于其余所有取消锁定的项。

“分布”按钮将用于在所有项之间平均分配百分比值  。 例如，如果有三个项，则选择“分布”会将百分比值设置为 34、33 和 33  。

> [!WARNING]
> “分布”按钮会重写任意锁定的项  。

还可以不使用滑块而直接在“%”列中键入百分比值。 如果直接输入百分比值，则其他项将不会自动调整。

> [!NOTE]
> 当总数达不到 100% 或者在“%”列中输入的百分比值为小数时，滑块处于禁用状态。

手动输入百分比值时，应该确保所有项的总和为 100%。 保存组合时，如果总和不是 100%，则系统会提示您或者接受现有的百分比值，或者返回并调整它们。 如果选择接受现有百分比，则会按比例分配这些百分比以达到 100%。  例如，如果有两个项，并且手动将它们设置为 80% 和 40%，则第一个项将设置为 66.67%（80 除以 120），第二个项将设置为 33.33%（40 除以 120）。

## <a name="see-also"></a>另请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)
