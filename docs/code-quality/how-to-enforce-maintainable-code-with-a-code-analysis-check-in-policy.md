---
title: 使用代码分析签入策略
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: d1b3b04f-4dd9-40e6-b2d4-b414d33fb647
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0924d3c7b6f39e4ec026a77ee8e0418361e311ba
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260925"
---
# <a name="how-to-enforce-maintainable-code-with-a-code-analysis-check-in-policy"></a>如何：强制执行可维护的代码使用代码分析签入策略

开发人员可以使用代码度量值工具来衡量的复杂性和可维护性的其代码，但你不能作为签入策略的一部分调用代码度量值。 但是，可以启用代码分析规则，验证你的代码符合代码度量标准，并强制实施通过签入策略的规则。 代码度量值的详细信息，请参阅[代码的指标值](../code-quality/code-metrics-values.md)。

可以启用继承深度、 类耦合、 可维护性指数和复杂性规则以强制实施通过代码分析签入策略可维护的代码。 这些规则的所有四个代码分析策略编辑器中找到"可维护性规则"类别下。

Team foundation 版本控制的管理员可以将代码分析可维护性规则添加到签入策略要求。 这些签入策略要求开发人员运行代码分析签入启动之前基于这些规则的更改。

## <a name="to-open-the-code-analysis-policy-editor"></a>若要打开代码分析策略编辑器

1. 在中**团队资源管理器**，右键单击项目，单击**项目设置**，然后单击**源代码管理**。

     **源代码管理**对话框随即出现。

2. 上**签入策略**选项卡，然后单击**添加**。

     **添加签入策略**对话框随即出现。

3. 在中**签入策略**列表中，选择**代码分析**复选框，然后依次**确定**。

     **代码分析策略编辑器**对话框随即出现。

## <a name="to-enable-code-analysis-maintainability-rules"></a>若要启用代码分析可维护性规则

1. 在中**代码分析策略编辑器**对话框中的**规则设置**，展开**可维护性规则**节点。

2. 选择以下规则对应的复选框：

   - 继承深度：**CA1501 AvoidExcessiveInheritance** -阈值：在 5 个以上级别深度警告

   - 复杂性：**CA1502 AvoidExcessiveComplexity** -阈值：在超过 25 种的警告

   - 可维护性索引：**CA1505 AvoidUnmaintainableCode** - Threshold:少于 20 发出警告

   - 类耦合度：**CA1506 AvoidExcessiveClassCoupling** -阈值：在多个类的 80 和多个方法，为 30 的警告

     此外，如果你想违反规则时阻止成功生成，则选择**将警告视为错误**规则说明旁边的复选框。

3. 单击 **“确定”** 。 新签入策略现在适用于未来的签入。

## <a name="see-also"></a>请参阅

- [代码度量值](../code-quality/code-metrics-values.md)
- [创建和使用代码分析签入策略](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)
