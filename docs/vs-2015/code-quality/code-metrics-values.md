---
title: 代码度量值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code metrics
- code analysis
- measure code quality
ms.assetid: bc38831e-2083-4ea4-8527-ee41499a342f
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 23dba7b7c29c05b55af2c461f36bdaa4b46b948f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667724"
---
# <a name="code-metrics-values"></a>代码度量值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码度量是一组软件度量值，使开发人员可以更好地了解他们正在开发的代码。 通过利用代码度量，开发人员可以了解应该改编哪些类型和/或方法或对这些方法进行更全面的测试。 开发团队可以确定潜在风险、了解项目的当前状态以及在软件开发过程中跟踪进度。

## <a name="software-measurements"></a>软件度量
 以下列表显示了用于计算的代码度量结果 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ：

- 可**维护性索引**–计算0到100之间的索引值，它表示维护代码的相对轻松程度。 较高的值表示更好的可维护性。 颜色编码分级可用于快速标识代码中的问题点。 绿色评级介于20和100之间，表示代码具有良好的可维护性。 黄色评分介于10和19之间，表示代码适度维护。 红色评分是0到9之间的评分，表示可维护性低。

- **圈复杂度** –测量代码的结构复杂性。 它通过计算程序流中的不同代码路径的数目来创建。 具有复杂控制流的程序将需要更多测试才能实现良好的代码覆盖率，并将降低维护性。

    > [!NOTE]
    > 在某些情况下，方法的圈复杂度计算 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 与早期版本不同。 有关详细信息，请参阅 [疑难解答代码度量值问题](../code-quality/troubleshooting-code-metrics-issues.md)中的 "Visual Studio 2010 代码复杂性计算中的更改" 部分。

- **继承深度** –指示扩展到类层次结构的根的类定义的数量。 层次结构越深层，就越难以理解在何处定义或/和重定义特定的方法和字段。

- **类耦合** –通过参数、局部变量、返回类型、方法调用、泛型或模板实例化、基类、接口实现、在外部类型上定义的字段和特性修饰来度量与唯一类的耦合。 优秀的软件设计要求类型和方法应具有较高的聚合和低耦合。 高耦合性表明，由于它对其他类型的互依关系，难于重复使用和维护的设计。

- **代码行** –指示代码中的近似行数。 计数基于 IL 代码，因此不是源代码文件中的准确行数。 非常高的计数可能表示某个类型或方法正在尝试执行过多的工作并且应拆分。 它还可能指示可能难以维护类型或方法。

## <a name="anonymous-methods"></a>匿名方法
 *匿名方法*只是没有名称的方法。 匿名方法经常用于将代码块作为委托参数进行传递。 在成员中声明的匿名方法（如方法或访问器）的指标结果与声明该方法的成员相关联。 它们不与调用方法的成员相关联。

 有关代码度量如何处理匿名方法的详细信息，请参阅 [匿名方法和代码分析](../code-quality/anonymous-methods-and-code-analysis.md)。

## <a name="generated-code"></a>生成的代码
 某些软件工具和编译器会生成添加到项目中的代码，并且项目开发人员不会查看或不应更改。 通常，当代码度量值计算指标值时，它会忽略生成的代码。 这样，指标值就可以反映开发人员可以查看和更改的内容。

 为 Windows 窗体生成的代码不会被忽略，因为它是开发人员可以查看和更改的代码。

## <a name="see-also"></a>另请参阅
 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
