---
title: Microsoft Fakes 中的代码生成、编译和命名约定 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 20221de4-2a9e-4787-b99a-b5855bb90872
caps.latest.revision: 18
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: df937d43c196193593bcfb1244bcc9e59a3c634a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660677"
---
# <a name="code-generation-compilation-and-naming-conventions-in-microsoft-fakes"></a>Microsoft Fakes 中的代码生成、编译和命名约定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题讨论 Fakes 代码生成和编译中的选项和问题，并介绍了 Fakes 生成的类型、成员和参数的命名约定。

 **要求**

- Visual Studio Enterprise

## <a name="BKMK_In_this_topic"></a> 在本主题中
 [代码生成和编译](#BKMK_Code_generation_and_compilation)

- [配置存根的代码生成](#BKMK_Configuring_code_generation_of_stubs) • [类型筛选](#BKMK_Type_filtering) • [将实际类和虚拟方法用作存根](#BKMK_Stubbing_concrete_classes_and_virtual_methods) • [内部类型](#BKMK_Internal_types) • [优化生成时间](#BKMK_Optimizing_build_times) • [避免程序集名称冲突](#BKMK_Avoiding_assembly_name_clashing)

  [Fakes 命名约定](#BKMK_Fakes_naming_conventions)

- [填充码类型和存根类型命名约定](#BKMK_Shim_type_and_stub_type_naming_conventions) • [填充码委托属性或存根委托字段命名约定](#BKMK_Shim_delegate_property_or_stub_delegate_field_naming_conventions) • [参数类型命名约定](#BKMK_Parameter_type_naming_conventions) • [递归规则](#BKMK_Recursive_rules)

  [外部资源](#BKMK_External_resources)

- [指南](#BKMK_Guidance)

## <a name="BKMK_Code_generation_and_compilation"></a>代码生成和编译

### <a name="BKMK_Configuring_code_generation_of_stubs"></a>配置存根的代码生成
 存根类型的生成在具有 .fakes 文件扩展名的 XML 文件中配置。 Fakes 框架通过自定义 MSBuild 任务在生成进程中集成并在生成时检测这些文件。 Fakes 代码生成器将存根类型编译为程序集并添加对项目的引用。

 下面的示例说明了 FileSystem.dll 中定义的存根类型：

```xml
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">
    <Assembly Name="FileSystem"/>
</Fakes>

```

### <a name="BKMK_Type_filtering"></a>类型筛选
 可在 .fakes 文件中设置筛选器以限制应用作存根的类型。 你可以在 StubGeneration 元素下添加数量不限的清除、添加、删除元素以生成所选类型的列表。

 例如，此 .fakes 文件会在 System 和 System.IO 命名空间下生成类型的存根，但是排除系统中包含“Handle”的任何类型：

```xml
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">
  <Assembly Name="mscorlib" />
  <!-- user code -->
  <StubGeneration>
    <Clear />
    <Add Namespace="System!" />
    <Add Namespace="System.IO!"/>
    <Remove TypeName="Handle" />
  </StubGeneration>
  <!-- /user code -->
</Fakes>
```

 筛选器字符串使用简单语法定义如何完成匹配：

- 默认情况下筛选器不区分大小写；筛选器可执行子字符串匹配：

     `el` 匹配“hello”

- 将 `!` 添加到筛选器的末尾，使其成为精确区分大小写匹配：

     `el!` 不匹配“hello”

     `hello!` 匹配“hello”

- 将 `*` 添加到筛选器的末尾，使其匹配字符串前缀：

     `el*` 不匹配“hello”

     `he*` 匹配“hello”

- 以分号分隔的列表中的多个筛选器已合并为析取：

     `el;wo` 匹配“hello”和“world”

### <a name="BKMK_Stubbing_concrete_classes_and_virtual_methods"></a>将具体类和虚拟方法用作存根
 默认情况下，为所有非密封类生成存根类型。 可通过 .fakes 配置文件将存根类型限制为抽象类：

```xml
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">
  <Assembly Name="mscorlib" />
  <!-- user code -->
  <StubGeneration>
    <Types>
      <Clear />
      <Add AbstractClasses="true"/>
    </Types>
  </StubGeneration>
  <!-- /user code -->
</Fakes>
```

### <a name="BKMK_Internal_types"></a>内部类型
 Fakes 代码生成器将为对生成的 Fakes 程序集可见的类型生成填充码类型和存根类型。 要使已填充的程序集的内部类型对 Fakes 和你的测试程序集可见，请将 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性添加到向生成的 Fakes 程序集和测试程序集提供可见性的已填充的程序集代码中。 以下是一个示例：

```csharp
// FileSystem\AssemblyInfo.cs
[assembly: InternalsVisibleTo("FileSystem.Fakes")]
[assembly: InternalsVisibleTo("FileSystem.Tests")]
```

 **强名称程序集中的内部类型**

 如果已填充的程序集具有强名称，并且你希望访问该程序集的内部类型：

- 测试程序集和 Fakes 程序集都必须具有强名称。

- 必须将测试的公钥和 Fakes 程序集添加到已填充的程序集的“InternalsVisibleToAttribute”  属性中。 这是当已填充的程序集具有强名称时，在已填充的程序集代码中我们的示例属性所呈现的效果：

  ```csharp
  // FileSystem\AssemblyInfo.cs
  [assembly: InternalsVisibleTo("FileSystem.Fakes",
      PublicKey=<Fakes_assembly_public_key>)]
  [assembly: InternalsVisibleTo("FileSystem.Tests",
      PublicKey=<Test_assembly_public_key>)]
  ```

  如果已填充的程序集具有强名称，则 Fakes 框架将自动对生成的 Fakes 程序集进行强签名。 你需要对测试程序集进行强签名。 请参阅[创建和使用具有强名称的程序集](https://msdn.microsoft.com/library/ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9)。

  Fakes 框架使用相同的密钥为所有生成的程序集签名，因此，你可以将此代码片段用作起点以将 Fakes 程序集的“InternalsVisibleTo”  属性添加到已填充的程序集代码中。

```csharp
[assembly: InternalsVisibleTo("FileSystem.Fakes, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e92decb949446f688ab9f6973436c535bf50acd1fd580495aae3f875aa4e4f663ca77908c63b7f0996977cb98fcfdb35e05aa2c842002703cad835473caac5ef14107e3a7fae01120a96558785f48319f66daabc862872b2c53f5ac11fa335c0165e202b4c011334c7bc8f4c4e570cf255190f4e3e2cbc9137ca57cb687947bc")]
```

 通过指定 **.snk** 文件（包含作为 **.fakes** 文件的 `Fakes`\\`Compilation` 元素中 `KeyFile` 属性值的替换密钥）的完整路径，可以为 Fakes 程序集指定不同的公钥，比如为已填充的程序集创建的密钥。 例如:

```xml
<-- FileSystem.Fakes.fakes -->
<Fakes ...>
  <Compilation KeyFile="full_path_to_the_alternate_snk_file" />
</Fakes>

```

 然后需要使用备用 **.snk** 文件的公钥作为已填充程序集代码中 Fakes 程序集的 InternalVisibleTo 属性的第二个参数：

```csharp
// FileSystem\AssemblyInfo.cs
[assembly: InternalsVisibleTo("FileSystem.Fakes",
    PublicKey=<Alternate_public_key>)]
[assembly: InternalsVisibleTo("FileSystem.Tests",
    PublicKey=<Test_assembly_public_key>)]
```

 在上面的示例中，`Alternate_public_key` 值和 `Test_assembly_public_key` 值可以相同。

### <a name="BKMK_Optimizing_build_times"></a>优化生成时间
 Fakes 程序集的编译可极大地加快生成时间。 通过为独立集中项目中的 .NET 系统程序集和第三方程序集生成 Fakes 程序集，可以最大程度地缩短生成时间。 由于你的计算机很少更改这种程序集，因此你可以在其他项目中重新使用生成的 Fakes 程序集。

 从单元测试项目中，可以轻松引用放置在项目文件夹 FakesAssemblies 下的已编译的 Fakes 程序集。

1. 使用与你的测试项目匹配的 .NET 运行时版本创建新的类库。 我们称之为 Fakes.Prebuild。 从项目中删除不需要的 class1.cs 文件。

2. 添加对需要 Fakes 的所有系统和第三方程序集的引用。

3. 为每个程序集和生成添加一个 .fakes 文件。

4. 从测试项目

    - 确保具有对 Fakes 运行时 DLL 的引用：

         C:\Program Files\Microsoft Visual Studio 12.0\Common7\IDE\PublicAssemblies\Microsoft.QualityTools.Testing.Fakes.dll

    - 对于每个已为其创建 Fakes 的程序集，请添加对相应 DLL 文件的引用，该文件位于项目文件夹的 Fakes.Prebuild\FakesAssemblies 中。

### <a name="BKMK_Avoiding_assembly_name_clashing"></a>避免程序集名称冲突
 在团队生成环境中，所有生成输出合并到一个目录中。 如果出现多个使用 Fakes 的项目，可能发生不同版本的 Fakes 程序集相互覆盖的情况。 例如，来自 .NET Framework 2.0 的 TestProject1 fakes mscorlib.dll 和 .NET Framework 4 的 TestProject2 fakes mscorlib.dll 都会产生一个 mscorlib.Fakes.dll Fakes 程序集。

 要避免出现此问题，在添加 .fakes 文件时，Fakes 应自动为非项目引用创建版本限定的 Fakes 程序集名称。 在创建 Fakes 程序集名称时，版本限定的 Fakes 程序集名称将嵌入版本号：

 假定程序集为 MyAssembly，版本为 1.2.3.4，则 Fakes 程序集名称为 MyAssembly.1.2.3.4.Fakes。

 你可以通过在 .fakes 中编辑程序集元素的版本属性来更改或删除此版本：

```xml
attribute of the Assembly element in the .fakes:
<Fakes ...>
  <Assembly Name="MyAssembly" Version="1.2.3.4" />
  ...
</Fakes>

```

## <a name="BKMK_Fakes_naming_conventions"></a>Fakes 命名约定

### <a name="BKMK_Shim_type_and_stub_type_naming_conventions"></a>填充类型和存根类型命名约定
 **命名空间**

- 向命名空间添加 .Fakes 后缀。

   例如，`System.Fakes` 命名空间包含系统命名空间的填充码类型。

- Global.Fakes 包含空命名空间的填充码类型。

  **类型名称**

- 向类型名称添加填充码前缀可生成填充码类型名称。

   例如，ShimExample 是 Example 类型的填充码类型。

- 向类型名称添加存根前缀可生成存根类型名称。

   例如，StubIExample 是 IExample 类型的存根类型。

  **类型参数和嵌套类型结构**

- 复制泛型类型参数。

- 根据填充码类型复制嵌套类型结构。

### <a name="BKMK_Shim_delegate_property_or_stub_delegate_field_naming_conventions"></a>填充委托属性或存根委托字段命名约定
 字段命名的**基本规则**，从空的名称开始：

- 追加方法名称。

- 如果方法名称是显式接口实现，则删除点。

- 如果是泛型方法，则追加 `Of`*n*，其中 *n* 是泛型方法自变量的数量。

  **特殊方法名称**（比如属性 getter 或 setter）将按下表所述方式处理。

|如果方法是…|示例|追加的方法名称|
|-------------------|-------------|--------------------------|
|**构造函数**|`.ctor`|`Constructor`|
|静态**构造函数**|`.cctor`|`StaticConstructor`|
|方法名称由以“_”分隔的两部分组成（比如属性 getter）的**取值函数**|*kind_name*（通常情况下，但不是由 ECMA 强制执行）|*NameKind*，两部分均首字母大写且进行交换|
||属性 `Prop` 的 getter|`PropGet`|
||属性 `Prop` 的 setter|`PropSet`|
||事件 adder|`Add`|
||事件 remover|`Remove`|
|由两部分组成的**运算符**|`op_name`|`NameOp`|
|例如：+ 运算符|`op_Add`|`AddOp`|
|对于**转换运算符**，追加返回类型。|`T op_Implicit`|`ImplicitOpT`|

 **备注**

- **索引器的 getter 和 setter** 的处理方式类似于属性。 索引器的默认名称为 `Item`。

- **参数类型**名称已转换并串联。

- 除非具有重载多义性，否则将忽略**返回类型**。 如果是这样，将在名称末尾追加返回类型

### <a name="BKMK_Parameter_type_naming_conventions"></a>参数类型命名约定

|假定为|追加的字符串是…|
|-----------|-------------------------|
|**类型**`T`|T<br /><br /> 已放置命名空间、嵌套结构和泛型 tic。|
|**out 参数**`out T`|`TOut`|
|**ref 参数**`ref T`|`TRef`|
|**数组类型**`T[]`|`TArray`|
|**多维数组**类型 `T[ , , ]`|`T3`|
|**指针**类型 `T*`|`TPtr`|
|**泛型类型**`T<R1, …>`|`TOfR1`|
|类型 `C<TType>` 的**泛型类型参数**`!i`|`Ti`|
|方法 `M<MMethod>` 的**泛型方法自变量**`!!i`|`Mi`|
|**嵌套类型**`N.T`|先追加 `N`，然后追加 `T`|

### <a name="BKMK_Recursive_rules"></a>递归规则
 下面的规则按递归方式应用：

- 由于 Fakes 使用 C# 生成 Fakes 程序集，因此，生成无效 C# 标记的所有字符都将转义为“_”（下划线）。

- 如果生成的名称与声明类型的任何成员发生冲突，则通过追加一个两位数的计数器（从 01 开始）来使用编号方案。

## <a name="BKMK_External_resources"></a>外部资源

### <a name="BKMK_Guidance"></a> 指导
 [使用 Visual Studio 2012 对连续交付进行测试 - 第 2 章：单元测试：测试内部](http://go.microsoft.com/fwlink/?LinkID=255188)

## <a name="see-also"></a>另请参阅
 [用 Microsoft Fakes 隔离测试代码](../test/isolating-code-under-test-with-microsoft-fakes.md)
