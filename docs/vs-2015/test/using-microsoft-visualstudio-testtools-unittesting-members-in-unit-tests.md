---
title: 在单元测试中使用 Microsoft.VisualStudio.TestTools.UnitTesting 成员| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 0fa335fd-e442-448f-913f-25a19df90a93
caps.latest.revision: 8
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e8b3ea10b96a63bd18098030dc884ac3f3383353
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657184"
---
# <a name="using-microsoftvisualstudiotesttoolsunittesting-members-in-unit-tests"></a>在单元测试中使用 Microsoft.VisualStudio.TestTools.UnitTesting 成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
单元测试框架支持 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的单元测试。 在编写单元测试的代码时使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting> 命名空间中的类和成员。 如果从头开始编写了单元测试，或是优化从进行测试的代码生成的单元测试，则可以使用它们。

## <a name="groups-of-elements"></a>元素组
 为了帮助提供更清晰的单元测试框架概述，本节将 UnitTesting 命名空间的元素组织为相关功能组。

> [!NOTE]
> 属性元素（其名称以字符串 Attribute 结束）可以在带有或不带字符串 Attribute 的情况下使用。 例如，以下两个代码示例的功能相同：
>
> `[TestClass()]`
>
> `[TestClassAttribute()]`

### <a name="elements-used-for-data-driven-testing"></a>用于数据驱动的测试的元素
 使用以下元素可设置数据驱动的单元测试。 有关详细信息，请参阅[如何：创建数据驱动的单元测试](../test/how-to-create-a-data-driven-unit-test.md)和[演练：使用配置文件定义数据源](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataAccessMethod>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElement>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElementCollection>

## <a name="attributes-used-to-establish-a-calling-order"></a>用于建立调用顺序的属性
 使用以下属性之一进行修饰的代码元素在指定时间进行调用。 有关详细信息，请参阅[单元测试的剖析](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)。

### <a name="for-assemblies"></a>对于程序集
 AssemblyInitialize 和 AssemblyCleanup 恰好在加载程序集之后以及恰好在卸载程序集之前进行调用。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyCleanupAttribute>

### <a name="for-classes"></a>对于类
 ClassInitialize 和 ClassCleanup 恰好在加载类之后以及恰好在卸载类之前进行调用。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassCleanupAttribute>

### <a name="for-test-methods"></a>对于测试方法

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>

## <a name="attributes-used-to-identify-test-classes-and-methods"></a>用于标识测试类和方法的属性
 每个测试类都必须具有 TestClass 属性，每个测试方法都必须具有 TestMethod 属性。 有关详细信息，请参阅[单元测试的剖析](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute>

## <a name="assert-classes-and-related-exceptions"></a>Assert 类和相关异常
 单元测试可以按特定应用程序对不同类型的断言语句、异常和属性的使用来验证应用程序。 有关详细信息，请参阅[使用 Assert 类](../test/using-the-assert-classes.md)。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute>

## <a name="the-testcontext-class"></a>TestContext 类
 以下特性和分配给它们的值会出现在特定测试方法的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 属性窗口中。 这些属性不旨在通过单元测试的代码进行访问。 相反，它们会影响使用或运行单元测试的方法（由你通过 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 使用或运行，或由 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 测试引擎测试或运行）。例如，其中一些属性在“测试管理器”窗口和“测试结果”窗口中显示为列，这意味着可以使用它们对测试和测试结果进行分组和排序。 这样一个属性是 TestPropertyAttribute，可用于将任意元数据添加到单元测试。 例如，可以通过使用 `[TestProperty("TestPass", "Accessibility")]` 标记单元测试，来使用该属性存储此测试所涵盖的测试轮次的名称。 还可以使用它存储它属于的测试类型的指示器： `[TestProperty("TestKind", "Localization")]`。 使用此特性创建的属性以及分配的属性值都会显示在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 属性窗口中的标题“测试特定的”**** 下。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DescriptionAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.WorkItemAttribute>

## <a name="test-configuration-classes"></a>测试配置类

- [ObjectTypes](/previous-versions/visualstudio/visual-studio-2013/dd987428(v=vs.120))

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection>

## <a name="attributes-used-for-generating-reports"></a>用于生成报告的属性
 本节中的属性将它们修饰的测试方法与 [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] 团队项目的项目层次结构中的实体相关。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssIterationAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssProjectStructureAttribute>

## <a name="classes-used-with-private-accessors"></a>与专用访问器一起使用的类
 如[使用 Publicize 创建专用访问器](https://msdn.microsoft.com/2056c6a7-6672-42a7-8f53-fead33c56deb)中所述，可以为私有方法生成单元测试。 这生成会创建专用访问器类，它会实例化 PrivateObject 类的对象。 PrivateObject 类是包装类，它在专用访问器进程中使用反射。 PrivateType 类非常相似，但是用于调用私有静态方法而不是调用私有实例方法。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType>

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting>