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
ms.openlocfilehash: ab1e0b890d6241742770ed38ff61fc1c2c0ed2f4
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535701"
---
# <a name="walkthrough-use-static-code-analysis-to-find-code-defects"></a>演练：使用静态代码分析查找代码缺陷

在本演练中，您将使用旧代码分析来分析托管项目的代码缺陷。

本文将指导你完成使用旧式分析来分析 .NET 托管代码程序集是否符合 .NET 设计准则的过程。

## <a name="create-a-class-library"></a>创建类库

1. 打开 Visual Studio，然后从 "类库 **（.NET Framework）** " 模板创建一个新项目。

1. 将项目命名为**CodeAnalysisManagedDemo**。

1. 创建项目后，打开*Class1.cs*文件。

1. 将 Class1.cs 中的现有文本替换为以下代码：

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

## <a name="analyze-the-project-for-code-defects"></a>对项目进行代码缺陷分析

1. 在**解决方案资源管理器**中选择 "CodeAnalysisManagedDemo" 项目。

2. 在“项目”菜单上，单击“属性”。

   将显示 CodeAnalysisManagedDemo 属性页。

3. 选择 "**代码分析**" 选项卡。

::: moniker range="vs-2017"

4. 请确保选中 **"生成时启用代码分析"** 。

5. 从 "**运行此规则集**" 下拉列表中，选择 " **Microsoft 所有规则**"。

::: moniker-end

::: moniker range=">=vs-2019"

4. 请确保在**二进制分析器**部分中选择了 **"生成时运行"** 。

5. 从 "**活动规则**" 下拉列表中，选择 " **Microsoft 所有规则**"。

::: moniker-end

6. 在 "**文件**" 菜单上，单击 "**保存选定项**"，然后关闭 "属性" 页。

7. 在 "**生成**" 菜单上，单击 "**生成 CodeAnalysisManagedDemo**"。

    "**错误列表**" 和 "**输出**" 窗口中显示 CodeAnalysisManagedDemo 项目生成警告。

## <a name="correct-the-code-analysis-issues"></a>更正代码分析问题

1. 在 "**视图**" 菜单上，选择 "**错误列表**"。

    根据所选的开发人员配置文件，可能需要指向 "**视图**" 菜单上的 "**其他窗口**"，然后选择 "**错误列表**"。

1. 在“解决方案资源管理器”中，选择“显示所有文件”。

1. 展开 "属性" 节点，然后打开*AssemblyInfo.cs*文件。

1. 使用以下提示来更正警告：

   [CA1014：用 CLSCompliantAttribute 标记程序集](../code-quality/ca1014.md)：向 AssemblyInfo.cs 文件的末尾添加代码 `[assembly: CLSCompliant(true)]`。

   [CA1032：实现标准异常构造函数](../code-quality/ca1032.md)：将构造函数 `public demo (String s) : base(s) { }` 添加到类 `demo`。

   [CA1032：实现标准异常构造函数](../code-quality/ca1032.md)：将构造函数 `public demo (String s, Exception e) : base(s, e) { }` 添加到类 `demo`。

   [CA1032：实现标准异常构造函数](../code-quality/ca1032.md)：将构造函数 `protected demo (SerializationInfo info, StreamingContext context) : base(info, context) { }` 添加到类演示。 还需要为 <xref:System.Runtime.Serialization?displayProperty=fullName> 添加 `using` 语句。

   [CA1032：实现标准异常构造函数](../code-quality/ca1032.md)：将构造函数 `public demo () : base() { }` 添加到类 `demo`。

   [CA1709：标识符应采用正确的大小](../code-quality/ca1709.md)写：将命名空间 `testCode` 的大小写更改为 `TestCode`。

   [CA1709：标识符应采用正确的大小写](../code-quality/ca1709.md)：将成员的名称更改为 `Demo`。

   [CA1709：标识符应采用正确的大小写](../code-quality/ca1709.md)：将成员的名称更改为 `Item`。

   [CA1710：标识符应具有正确的后缀](../code-quality/ca1710.md)：将类及其构造函数的名称更改为 `DemoException`。

   [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237.md)：向类 `demo` 添加 `[Serializable ()]` 特性。

   [CA2210：程序集应具有有效的强名称](../code-quality/ca2210.md)：使用强名称密钥签名 "CodeAnalysisManagedDemo"：

   1. 在 "**项目**" 菜单上，选择 " **CodeAnalysisManagedDemo 属性**"。

      项目属性随即出现。

   1. 选择 **“签名”** 选项卡。

   1. 选中 "为**程序集签名**" 复选框。

   1. 在 "**选择字符串名称密钥文件**" 列表中，选择 " **\<New >** "。

      此时将显示 "**创建强名称密钥**" 对话框。

   1. 对于 "**密钥文件名称**"，请输入**为 testkey**。

   1. 输入密码，然后选择 **"确定"** 。

   1. 在 "**文件**" 菜单上，选择 "**保存选定项**"，然后关闭属性页。

   完成所有更改后，Class1.cs 文件应如下所示：

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

    1. 从右键单击菜单（上下文菜单）中，选择 "**取消**隐藏**文件中**的  > "。

1. 重新生成项目。

     项目生成时不会出现任何警告或错误。

## <a name="see-also"></a>请参阅

[托管代码的代码分析](../code-quality/code-analysis-for-managed-code-overview.md)
