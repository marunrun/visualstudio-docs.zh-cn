---
title: 分析托管代码的代码缺陷演练 |Microsoft Docs
ms.date: 01/29/2018
ms.topic: conceptual
helpviewer_keywords:
- code analysis [Visual Studio]
- managed code, analyzing
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 4a00fdb2a41a03554113f2ecb626185aab2c74d5
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547996"
---
# <a name="walkthrough-use-static-code-analysis-to-find-code-defects"></a>演练：使用静态代码分析查找代码缺陷

在本演练中, 您将使用旧代码分析来分析托管项目的代码缺陷。

本文将指导你完成使用旧式分析来分析 .NET 托管代码程序集是否符合 .NET 设计准则的过程。

## <a name="create-a-class-library"></a>创建类库

### <a name="to-create-a-class-library"></a>创建类库

1. 在“文件”菜单上，选择“新建” > “项目”。

1. 在 "**新建项目**" 对话框中, 展开 "**已安装** > **视觉对象C#** ", 然后选择 " **Windows 桌面**"。

1. 选择 "类库 **(.NET Framework)** " 模板。

1. 在 "**名称**" 文本框中, 键入**CodeAnalysisManagedDemo** , 然后单击 **"确定"** 。

1. 创建项目后, 打开*Class1.cs*文件。

1. 将 Class1.cs 中的现有文本替换为以下代码:

   ```csharp
   using System;

   namespace testCode
   {
       public class demo : Exception
       {
           public static void Initialize(int size) { }
           protected static readonly int _item;
           public static int item { get { return _item; } }
       }
   }
   ```

1. 保存 Class1.cs 文件。

## <a name="analyze-the-project"></a>分析项目

### <a name="to-analyze-a-managed-project-for-code-defects"></a>分析托管项目的代码缺陷

1. 在**解决方案资源管理器**中选择 "CodeAnalysisManagedDemo" 项目。

1. 在“项目”菜单上，单击“属性”。

     将显示 CodeAnalysisManagedDemo 属性页。

1. 选择 "**代码分析**" 选项卡。

1. 请确保选中 **"对生成启用代码分析"** 。

1. 从 "**运行此规则集**" 下拉列表中, 选择 " **Microsoft 所有规则**"。

1. 在 "**文件**" 菜单上, 单击 "**保存选定项**", 然后关闭 "属性" 页。

1. 在 "**生成**" 菜单上, 单击 "**生成 CodeAnalysisManagedDemo**"。

    "**错误列表**" 和 "**输出**" 窗口中显示 CodeAnalysisManagedDemo 项目生成警告。

## <a name="correct-the-code-analysis-issues"></a>更正代码分析问题

### <a name="to-correct-code-analysis-rule-violations"></a>更正代码分析规则冲突

1. 在 "**视图**" 菜单上, 选择 "**错误列表**"。

    根据所选的开发人员配置文件, 可能需要指向 "**视图**" 菜单上的 "**其他窗口**", 然后选择 "**错误列表**"。

1. 在“解决方案资源管理器”中，选择“显示所有文件”。

1. 展开 "属性" 节点, 然后打开*AssemblyInfo.cs*文件。

1. 使用以下提示来更正警告:

   [CA1014用 CLSCompliantAttribute](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md)标记程序集:Microsoft. Design: 应将 "demo" 标记为 CLSCompliantAttribute, 并且其值应为 true。

   1. 将代码`using System;`添加到 AssemblyInfo.cs 文件。

   1. 接下来, 将代码`[assembly: CLSCompliant(true)]`添加到 AssemblyInfo.cs 文件的末尾。

   [CA1032实现标准异常构造](../code-quality/ca1032-implement-standard-exception-constructors.md)函数:Microsoft. Design:将以下构造函数添加到此类: 公共演示 (String)

   1. 将构造函数`public demo (String s) : base(s) { }`添加到类`demo`。

   [CA1032实现标准异常构造](../code-quality/ca1032-implement-standard-exception-constructors.md)函数:Microsoft. Design:将以下构造函数添加到此类: 公共演示 (String, Exception)

   1. 将构造函数`public demo (String s, Exception e) : base(s, e) { }`添加到类`demo`。

   [CA1032实现标准异常构造](../code-quality/ca1032-implement-standard-exception-constructors.md)函数:Microsoft. Design:将以下构造函数添加到此类: protected demo (SerializationInfo, StreamingContext)

   1. 将代码`using System.Runtime.Serialization;`添加到 Class1.cs 文件的开头。

   1. 接下来, 添加构造函数`protected demo (SerializationInfo info, StreamingContext context) : base(info, context) { } to the class demo.`

   [CA1032实现标准异常构造](../code-quality/ca1032-implement-standard-exception-constructors.md)函数:Microsoft. Design:将以下构造函数添加到此类: 公共演示 ()

   1. 将构造函数`public demo () : base() { }`添加到类`demo` **。**

   [CA1709标识符应采用正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)的大小写:Microsoft。命名:更正命名空间名称 "testCode" 的大小写, 将其改为 "TestCode"。

   1. 更改命名空间`testCode` `TestCode`的大小写。

   [CA1709标识符应采用正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)的大小写:Microsoft。命名:更正类型名称 "demo" 的大小写, 将其改为 "Demo"。

   1. 将成员的名称更改为`Demo`。

   [CA1709标识符应采用正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)的大小写:Microsoft。命名:更正成员名称 "item" 的大小写, 将其更改为 "Item"。

   1. 将成员的名称更改为`Item`。

   [CA1710标识符应具有正确的](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)后缀:Microsoft。命名:重命名 "testCode" 以在 "Exception" 中结束。

   1. 将类及其构造函数的名称更改为`DemoException`。

   [CA2210程序集应具有有效的](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)强名称:使用强名称密钥对 "CodeAnalysisManagedDemo" 进行签名。

   1. 在 "**项目**" 菜单上, 选择 " **CodeAnalysisManagedDemo 属性**"。

      项目属性随即出现。

   1. 选择 **“签名”** 选项卡。

   1. 选中 "为**程序集签名**" 复选框。

   1. 在 "**选择字符串名称密钥文件**" 列表中, 选择 **\<"新建 ...">** 。

      此时将显示 "**创建强名称密钥**" 对话框。

   1. 在 "**密钥文件名称**" 中, 键入为 testkey。

   1. 输入密码, 然后选择 **"确定"** 。

   1. 在 "**文件**" 菜单上, 选择 "**保存选定项**", 然后关闭属性页。

   [CA2237：用 SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)标记 ISerializable 类型:Microsoft。用法:将 [Serializable] 特性添加到类型 "demo", 因为此类型实现了 ISerializable。

   1. 将属性添加到类`demo`。 `[Serializable ()]`

   在完成更改后，Class1.cs 文件应如下所示：

   ```csharp
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

1. 重新生成项目。

## <a name="exclude-code-analysis-warnings"></a>排除代码分析警告

1. 对于每一个剩余警告，请执行以下操作：

    1. 选择**错误列表**中的警告。

    1. 从右键单击菜单 (上下文菜单) 中, 选择 "**在禁止显示文件中** **取消** > "。

1. 重新生成项目。

     项目生成时不会出现任何警告或错误。

## <a name="see-also"></a>请参阅

[托管代码的代码分析](../code-quality/code-analysis-for-managed-code-overview.md)