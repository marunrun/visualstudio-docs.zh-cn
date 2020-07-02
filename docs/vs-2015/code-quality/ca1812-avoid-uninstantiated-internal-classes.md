---
title: CA1812：避免未实例化的内部类 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1812
- AvoidUninstantiatedInternalClasses
helpviewer_keywords:
- AvoidUninstantiatedInternalClasses
- CA1812
ms.assetid: 1bb92a42-322a-44cc-98a8-8858212c1e1f
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 401fbfbccfeeeeec5cbdc0e791b110d1b5f0201b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543970"
---
# <a name="ca1812-avoid-uninstantiated-internal-classes"></a>CA1812:避免未实例化的内部类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AvoidUninstantiatedInternalClasses|
|CheckId|CA1812|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 程序集级别类型的实例不是由程序集中的代码创建的。

## <a name="rule-description"></a>规则描述
 此规则尝试查找对该类型的一个构造函数的调用，并在找不到调用时报告冲突。

 此规则不检查以下类型：

- 值类型

- 抽象类型

- 枚举

- 委托

- 编译器发出的数组类型

- 不能实例化并 `static` 仅定义（ `Shared` 在 Visual Basic 中）方法的类型。

  如果你将应用 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute?displayProperty=fullName> 到正在分析的程序集，则将不会在标记为的任何构造函数上出现此规则， `internal` 因为你无法判断某个字段是否正由其他 `friend` 程序集使用。

  即使在代码分析中无法解决此限制 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，在 `friend` 分析中有每个程序集时，外部独立的 FxCop 也将在内部构造函数上发生。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除该类型或添加使用它的代码。 如果类型仅包含静态方法，请将以下内容之一添加到类型中，以防止编译器发出默认的公共实例构造函数：

- 面向版本1.0 和1.1 的类型的私有构造函数 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

- `static`面向的类型的（ `Shared` 在 Visual Basic）修饰符 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告。 建议在以下情况下禁止显示此警告：

- 类是通过后期绑定反射方法（如）创建的 <xref:System.Activator.CreateInstance%2A?displayProperty=fullName> 。

- 类是由运行时或 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 自动创建的。 例如，用于实现 <xref:System.Configuration.IConfigurationSectionHandler?displayProperty=fullName> 或 <xref:System.Web.IHttpHandler?displayProperty=fullName> 的类。

- 类作为具有新约束的泛型类型参数进行传递。 例如，下面的示例将引发此规则。

  ```csharp
  internal class MyClass
  {
      public DoSomething()
      {
      }
  }
  public class MyGeneric<T> where T : new()
  {
      public T Create()
      {
          return new T();
      }
  }
  // [...]
  MyGeneric<MyClass> mc = new MyGeneric<MyClass>();
  mc.Create();
  ```

  在这些情况下，我们建议禁止显示此警告。

## <a name="related-rules"></a>相关规则
 [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1801:检查未使用的参数](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804:移除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)
