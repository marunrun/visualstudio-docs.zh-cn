---
title: 演练：对托管代码进行代码缺陷分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, walkthroughs
- managed code, analyzing
- code analysis tool, walkthroughs
ms.assetid: 22b99f49-1924-4fb5-a421-c8b23e5d5cd4
caps.latest.revision: 47
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9478394162051fc08c33047cf1ac24275aff75e2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72609322"
---
# <a name="walkthrough-analyzing-managed-code-for-code-defects"></a>演练：对托管代码进行代码缺陷分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，您将使用代码分析工具来分析托管项目的代码缺陷。

 本演练将指导你完成使用代码分析来分析 .NET 托管代码程序集是否符合 Microsoft .NET 框架设计准则的过程。

 在本演练中，你将：

- 分析和更正代码缺陷警告。

## <a name="prerequisites"></a>Prerequisites

- [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]

## <a name="create-a-class-library"></a>创建类库

#### <a name="to-create-a-class-library"></a>创建类库

1. 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 的 "**文件**" 菜单上，单击 "**新建**"，然后单击 "**项目**"。

2. 在 "**新建项目**" 对话框中的 "**项目类型**" 下，单击 "**视觉对象C#** "。

3. 在 "**模板**" 下 **，选择 "类库"** 。

4. 在 "**名称**" 文本框中，键入**CodeAnalysisManagedDemo** ，然后单击 **"确定"** 。

5. 创建项目后，打开 Class1.cs 文件。

6. 将 Class1.cs 中的现有文本替换为以下代码：

     `//CodeAnalysisManagedDemo //Class1.cs using System;  namespace testCode {          public class demo : Exception     {                  public static void Initialize(int size) { }         protected static readonly int _item;         public static int item { get { return _item; } }     } }`

7. 保存 Class1.cs 文件。

## <a name="analyze-the-project"></a>分析项目

#### <a name="to-analyze-a-managed-project-for-code-defects"></a>分析托管项目的代码缺陷

1. 在**解决方案资源管理器**中选择 "CodeAnalysisManagedDemo" 项目。

2. 在“项目”菜单上，单击“属性”。

     将显示 CodeAnalysisManagedDemo 属性页。

3. 单击 " **CodeAnalysis**"。

4. 请确保选中 **"生成时启用代码分析（定义 CODE_ANALYSIS 常量）"** 。

5. 从 "**运行此规则集**" 下拉列表中，选择 " **Microsoft 所有规则**"。

6. 在 "**文件**" 菜单上，单击 "**保存选定项**"，然后关闭 ManagedDemo 属性页。

7. 在 "**生成**" 菜单上，单击 "**生成 ManagedDemo**"。

     "**代码分析**" 和 "**输出**" 窗口中将报告 CodeAnalysisManagedDemo 项目生成警告。

     如果未显示 "**代码分析**" 窗口，请在 "**分析**" 菜单上选择 "**窗口**"，然后**选择 "代码分析**"。

## <a name="correct-the-code-analysis-issues"></a>更正代码分析问题

#### <a name="to-correct-code-analysis-rule-violations"></a>更正代码分析规则冲突

1. 在 "**视图**" 菜单上，单击**错误列表**。

     根据所选的开发人员配置文件，可能需要指向 "**视图**" 菜单上的 "**其他窗口**"，然后单击 "**错误列表**"。

2. 在**解决方案资源管理器**中，单击 "**显示所有文件**"。

3. 接下来，展开 "属性" 节点，然后打开 AssemblyInfo.cs 文件。

4. 使用以下内容来更正警告：

- [CA1014：用 CLSCompliantAttribute 标记程序集](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md)： CLSCompliantAttribute： "demo" 应标记为，其值应为 true。

  - 将代码 `using``System;` 添加到 AssemblyInfo.cs 文件。

       接下来，将代码 `[assembly: CLSCompliant(true)]` 添加到 AssemblyInfo.cs 文件的末尾。

       重新生成项目。

- [CA1032：实现标准异常构造函数](../code-quality/ca1032-implement-standard-exception-constructors.md)： Microsoft. Design：将以下构造函数添加到此类：公共演示（String）

  - 将构造函数 `public demo (String s) : base(s) { }` 添加到类 `demo`。

- [CA1032：实现标准异常构造函数](../code-quality/ca1032-implement-standard-exception-constructors.md)： Microsoft. Design：将以下构造函数添加到此类：公共演示（String，exception）

  - 将构造函数 `public demo (String s, Exception e) : base(s, e) { }` 添加到类 `demo`。

- [CA1032：实现标准异常构造函数](../code-quality/ca1032-implement-standard-exception-constructors.md)： Microsoft. Design：将以下构造函数添加到此类： protected Demo （SerializationInfo，StreamingContext）

  - 将代码 `using System.Runtime.Serialization;` 添加到 Class1.cs 文件的开头。

       接下来，添加构造函数 `protected demo (SerializationInfo info, StreamingContext context) : base(info, context) { } to the class demo.`

       重新生成项目。

- [CA1032：实现标准异常构造函数](../code-quality/ca1032-implement-standard-exception-constructors.md)： Microsoft. Design：将以下构造函数添加到此类：公共演示（）

  - 将构造函数 `public demo () : base() { }` 添加到类 `demo` **。**

       重新生成项目。

- [CA1709：标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)： Microsoft。命名：更正命名空间名称 "testCode" 的大小写，将其改为 "testCode"。

  - 将命名空间 `testCode` 的大小写更改为 `TestCode`。

- [CA1709：标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)： Microsoft。命名：更正类型名称 "demo" 的大小写，将其改为 "demo"。

  - 将成员的名称更改为 `Demo`。

- [CA1709：标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)： Microsoft。命名：更正成员名称 "item" 的大小写，将其改为 "item"。

  - 将成员的名称更改为 `Item`。

- [CA1710：标识符应具有正确的后缀：。请将](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)"TestCode" 重命名为以 "Exception" 结尾。

  - 将类及其构造函数的名称更改为 `DemoException`。

- [CA2210：程序集应具有有效的强名称](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)：使用强名称密钥对 "ManagedDemo" 进行签名。

  - 在 "**项目**" 菜单上，单击 " **ManagedDemo 属性**"。

       项目属性随即出现。

       单击 "**签名**"。

       选中 "为**程序集签名**" 复选框。

       在 "**选择字符串名称密钥文件**" 列表中，选择 **\<New 。>** 。

       此时将显示 "**创建强名称密钥**" 对话框。

       在 "**密钥文件名称**" 中，键入为 testkey。

       输入密码，然后单击 **"确定"** 。

       在 "**文件**" 菜单上，单击 "**保存选定项**"，然后关闭属性页。

       重新生成项目。

- [CA2237：使用 SerializableAttribute： Microsoft 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)。用法：将 [Serializable] 特性添加到类型 "demo"，因为此类型实现了 iserializable。

  - 将 `[Serializable ()]` 特性添加到类 `demo`。

       重新生成项目。

  在完成更改后，Class1.cs 文件应如下所示：

```
//CodeAnalysisManagedDemo
//Class1.cs
using System;
using System.Runtime.Serialization;

namespace TestCode
{

    [Serializable()]
    public class DemoException : Exception
    {
        public DemoException () : base() { }
        public DemoException(String s) : base(s) { }
        public DemoException(String s, Exception e) : base(s, e) { }
        protected DemoException(SerializationInfo info, StreamingContext context) : base(info, context) { }

        public static void Initialize(int size) { }
        protected static readonly int _item;
        public static int Item { get { return _item; } }
    }
}
```

## <a name="exclude-code-analysis-warnings"></a>排除代码分析警告

#### <a name="to-exclude-code-defect-warnings"></a>排除代码缺陷警告

1. 对于每一个剩余警告，请执行以下操作：

   1. 在“代码分析”窗口中，选择警告。

   2. 选择 "**操作**"，然后选择 "**取消消息**"，然后选择 **"在项目禁止显示文件**"。

      有关详细信息，请参阅[如何：使用菜单项禁止显示警告](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)

2. 重新生成项目。

    项目生成时不会出现任何警告或错误。
