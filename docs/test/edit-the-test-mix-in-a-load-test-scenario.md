---
title: 负载测试方案的测试组合
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, adding tests
- test mix
- load tests, test mix
- load tests, removing tests
ms.assetid: 303e1d70-5d98-424a-b51e-e0898e16d3f8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f28a9be17bba0bf7fc8fa4ea2198a255a2cbde53
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68918306"
---
# <a name="edit-the-test-mix-to-specify-which-web-performance-unit-and-coded-ui-tests-to-include-in-a-load-test-scenario"></a>编辑测试组合以指定在负载测试方案中包括的 Web 性能、单元和编码的 UI 测试

方案的测试组合  是方案中包含的 Web 性能测试和单元测试的选择以及这些测试在方案中的分布的组合。 分布方案是可为虚拟用户在负载测试运行期间选择的特定测试的概率指定的设置。

向负载测试添加一组测试之后，“测试组合”可像其他组合选项一样工作。  虚拟用户根据在组合中指定的概率随机选择测试。 例如，如果有两个测试，在组合中各占 50% 的概率，则新虚拟用户选择运行第一个测试大约占一半时间。 在 50/50 组合中，如果一个测试较长，另一个较短，则负载更多来自于较长的测试。

可以移除已添加到组合中的测试。 还可以使用组合控件来更改测试组合的分布。 通过组合控件，您可以轻松地调整方案中测试的分布。

> [!NOTE]
> 分发方案是虚拟用户在负载测试运行期间选择特定测试的概率的衡量方式。 分发方案用百分比表示。 因此，一个方案中包含的所有测试的总分发方案数为 100。 例如，如果一个方案仅包含一个测试，则该测试的分发方案为 100%。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="add-new-tests-to-a-test-mix-in-an-existing-scenario"></a>将新测试添加到现有方案中的测试组合

使用“新建负载测试向导”  创建新方案时，可以指定要添加到新方案的测试组合的 Web 性能测试和单元测试。

可使用“负载测试编辑器”  将更多 Web 性能测试和单元测试添加到方案的测试组合。

![向现有负载测试中添加测试](../test/media/ltest_addingtests.png)

### <a name="to-add-more-tests-to-an-existing-scenario"></a>向现有方案添加更多测试

1. 打开一个负载测试。

2. 在“负载测试编辑器”  中，右键单击现有方案，然后选择“添加测试”  。

     随即出现“添加测试”对话框。  解决方案中尚未包含在方案中的所有 Web 性能测试、单元测试和编码的 UI 测试都可以添加到方案中。

3. 在“可用测试”  窗格中选择要添加的 Web 性能测试、单元测试或编码的 UI 测试。 选择右箭头将测试添加到“选定的测试”窗格。 

4. 添加完测试后，选择“确定”。 

     测试被添加到测试组合中。 新的分布方案将自动分配给测试组合中的测试。

5. （可选）调整混合控件以指定测试分布。 有关详细信息，请参阅[关于混合控件](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)。

## <a name="remove-tests-from-a-scenario"></a>从方案中移除测试
![从现有负载测试中移除测试](../test/media/ltest_removetest.png)

### <a name="to-remove-tests-from-a-scenario"></a>从方案中移除测试

1. 打开一个负载测试。

2. 在“负载测试编辑器”  的负载测试树中，右键单击要从中删除测试的方案，然后选择“编辑测试组合”  。 随即出现“编辑测试组合”对话框。 

3. 在网格中选择 Web 性能测试、单元测试或编码的 UI 测试，然后选择“删除”  。

    > [!NOTE]
    > 移除测试之后，将测试组合调整为您的首选分发方案。

4. 删除完测试后，选择“确定”。 

## <a name="EditingTestMixAboutMixControl"></a>关于混合控件
通过组合控件，可以调整负载测试方案中在测试、浏览器类型或网络类型之间分布的负载百分比。 可以通过移动滑块来调整百分比值。 调整测试组合可指定虚拟用户在负载测试方案中运行特定测试的概率。

移动滑块时，所有可用项的百分比值都会发生变化。 如果移动两个以上的项，则添加或移除的量在其他项中均匀分布。 可以重写此行为。 对于某个特定项，如果选中锁定列中的复选框，则将锁定该项的指定百分比值。 随后移动滑块时，添加或移除的量只能应用于其余所有取消锁定的项。

“分布”按钮用于在所有项中平均分配百分比。  例如，如果有三个项，则选择“分布”会将百分比值设置为 34、33 和 33。 

> [!WARNING]
> “分布”按钮会重写任意锁定的项  。

还可以不使用滑块而直接在“%”列中键入百分比值  。 如果直接输入百分比值，则其他项将不会自动调整。

> [!NOTE]
> 当总数达不到 100% 或者在“%”列中输入的百分比值为小数时，滑块处于禁用状态  。

手动输入百分比值时，应该确保所有项的总和为 100%。 保存组合时，如果总和不是 100%，则系统会提示您或者接受现有的百分比值，或者返回并调整它们。 如果选择接受现有百分比，则会按比例分配这些百分比以达到 100%。  例如，如果有两个项，并且手动将它们设置为 80% 和 40%，则第一个项将设置为 66.67%（80 除以 120），第二个项将设置为 33.33%（40 除以 120）。

## <a name="see-also"></a>请参阅

- [编辑负载测试方案](../test/edit-load-test-scenarios.md)