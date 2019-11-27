---
title: 对 UML 扩展运行单元测试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 745d74ae-e48c-4fd9-a755-4354b81b9f8a
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f634f028dafea3260a69537893513f13cc0ebe83
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74292546"
---
# <a name="run-unit-tests-on-uml-extensions"></a>对 UML 扩展运行单元测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

为了使代码在连续更改中保持稳定，建议你编写单元测试并将这些测试作为常规生成过程的一部分执行。 有关更多信息，请参见 [Unit Test Your Code](../test/unit-test-your-code.md)。 若要设置用于 Visual Studio 建模扩展的测试，你需要一些关键信息。 摘要：

- [设置用于 VSIX 扩展的单元测试](#Host)

   使用 VS IDE 主机适配器运行测试。 为每个测试方法添加 `[HostType("VS IDE")]`为前缀。 运行测试时，此主机适配器将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

- [访问 DTE 和 ModelStore](#DTE)

   通常，在测试初始化中，你必须打开模型及其关系图并访问 `IModelStore` 。

- [打开模型图](#Opening)

   可以在 `EnvDTE.ProjectItem` 和 `IDiagramContext`之间来回转换。

- [在 UI 线程中执行更改](#UiThread)

   必须在 UI 线程中执行用于更改模型存储的测试。 可以将 `Microsoft.VSSDK.Tools.VsIdeTesting.UIThreadInvoker` 用于此测试。

- [测试命令、笔势和其他 MEF 组件](#MEF)

   若要测试 MEF 组件，你必须将这些组件的导入属性显式连接到值。

  以下各节详述了这些内容。

## <a name="requirements"></a>要求
 请参阅 [要求](../modeling/extend-uml-models-and-diagrams.md#Requirements)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="Host"></a>设置用于 VSIX 扩展的单元测试
 建模扩展中的方法通常会使用已打开的关系图。 这些方法使用 MEF 导入，例如， **IDiagramContext** 和 **ILinkedUndoContext**。 测试环境必须先设置此上下文，然后你才能运行测试。

#### <a name="to-set-up-a-unit-test-that-executes-in-includevsprvsincludesvsprvs-mdmd"></a>设置在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中执行的单元测试

1. 创建 UML 扩展项目和单元测试项目。

    1. **UML 扩展项目。** 通常通过使用命令、笔势或验证项目模板创建此项目。 例如，请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

    2. **单元测试项目。** 有关更多信息，请参见 [Unit Test Your Code](../test/unit-test-your-code.md)。

2. 创建包含 UML 建模项目的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案。 将使用此解决方案作为测试的初始状态。 应当将它与写入 UML 扩展及其单元测试的解决方案分开。 有关详细信息，请参阅[创建 UML 建模项目和关系图](../modeling/create-uml-modeling-projects-and-diagrams.md)。

3. **在 UML 扩展项目中**，将 .csproj 文件编辑为文本并确保以下行显示 `true`：

    ```
    <CopyBuildOutputToOutputDirectory>true</CopyBuildOutputToOutputDirectory>
        <CopyOutputSymbolsToOutputDirectory>true</CopyOutputSymbolsToOutputDirectory>
    ```

     若要将 .csproj 文件编辑为文本，请在“解决方案资源管理器”中，从该项目的快捷菜单上选择 **“卸载项目”** 。 然后选择 **“编辑 .csproj”** 。 编辑文本后，请选择 **“重新加载项目”** 。

4. 在 UML 扩展项目中，将以下行添加到 **Properties\AssemblyInfo.cs**。 这将允许单元测试访问你想要测试的方法：

    ```csharp
    [assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.
    ```

5. **在单元测试项目中**，添加以下程序集引用：

    - *你的 UML 扩展项目*

    - **EnvDTE**

    - **VisualStudio. Microsoft.visualstudio.architecturetools.layer.validator。**

    - **VisualStudio. ComponentModelHost .dll**

    - **VisualStudio. "Microsoft.visualstudio.qualitytools.webtestframework. Microsoft.visualstudio.qualitytools.unittestframework.dll**

    - **VisualStudio （& e）**

    - **VSSDK. TestHostFramework .dll**

6. 将特性 `[HostType("VS IDE")]` 添加为每个测试方法（包括初始化方法）的前缀。

     这将确保测试将在 Visual Studio 的实验实例中运行。

## <a name="DTE"></a>访问 DTE 和 ModelStore
 编写一个方法以在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中打开建模项目。 通常，你只需在每个测试运行中打开一次解决方案。 若要仅运行此方法一次，请将 `[AssemblyInitialize]` 特性作为此方法的前缀。 不要忘记你还需要每个测试方法的 [HostType("VS IDE")] 特性。  例如:

```csharp
using EnvDTE;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.VSSDK.Tools.VsIdeTesting;

namespace UnitTests
{
  [TestClass]
  public static class TestSetup
  {

    // Location of a VS Solution that defines an initial state for your tests:
    private const string testSolutionFilePath = @"C:\MyTestFolder\TestModelSln\TestModel.sln";
    // Name of a modeling project within the test solution:
    private const string testModelingProjectName = "MyTestModel";

    // Make Solution and IModelStore available to test methods:
    public static Solution ModelSolution = null;
    public static IModelingProject ModelingProject = null;
    public static IModelStore ModelStore = null;

    // This method will be performed once to initialize tests for this assembly:
    [AssemblyInitialize]
    [HostType("VS IDE")]
    public static void OpenTestModelingProject(TestContext testContext)
    {
      // To make sure that we always start the tests in the same state,
      // copy the test solution from a read-only directory:
      // TODO: copy test solution folder.

      // Open a solution that is the initial state for your tests:
      ModelSolution = VsIdeTestHostContext.Dte.Solution;
      ModelSolution.Open(testSolutionFilePath);

      // Find the ModelingProject and IModelStore:
      foreach (Project project in ModelSolution.Projects)
      {
        // https://msdn.microsoft.com/library/ee791691.aspx
        ModelingProject = project as IModelingProject;
        if (ModelingProject != null)
        {
          // This is a modeling project.
          ModelStore = ModelingProject.Store;
          break;
        }
        // else this is another kind of project.
      }

      Assert.IsNotNull(ModelSolution, "VS solution not found");
      Assert.IsNotNull(ModelStore, "Modeling store not found");
    }
    [AssemblyCleanup]
    public static void RemoveTestSolution ()
    {
      // TODO: Remove copied test solution directory.
    }
  }
}

```

 如果 <xref:EnvDTE.Project?displayProperty=fullName> 的实例表示建模项目，则可以将其强制转换为[IModelingProject](/previous-versions/ee789474(v=vs.140))。

## <a name="Opening"></a>打开模型图
 对于每个测试或测试的类，你通常需要使用打开的关系图。 以下示例使用 `[ClassInitialize]` 特性，该特性在此测试类中先执行此方法，然后再执行其他方法。 同样，不要忘记你还需要每个测试方法的 [HostType("VS IDE")] 特性：

```csharp
//
private IDiagram diagram;
// This class contains unit tests:
[TestClass]
public class MyTestClass
{
  // Map filenames to open diagram files:
  private static Dictionary<string, IDiagram> diagrams = new Dictionary<string, IDiagram>();

  // This method will be called once for this test class:
  [ClassInitialize]
  [HostType("VS IDE")]
  public static void TestClassInitialize(TestContext testContext)
  {
    // Open all the diagrams in the model:
    foreach (ProjectItem item in (TestSetup.ModelingProject as Project).ProjectItems)
    {
      // Get the filename of the principal file (not the .layout subsidiary):
      string fileName = item.FileNames[0];
      // If this is a model diagram file, it can be cast to IDiagramContext:
      IDiagramContext modelingItem = item as IDiagramContext;
      if (modelingItem != null)
      {
        IDiagram diagram = modelingItem.CurrentDiagram;
        if (diagram == null)
        {
          // Diagram is closed. Open it:
          item.Open().Activate();
          diagram = modelingItem.CurrentDiagram;
        }
        diagrams[fileName] = diagram;
      }
      // else item is not a model diagram.
    }
    Assert.IsTrue(diagrams.Count>0, "UML diagram not found");
  }
// Insert test methods here ...
}

```

## <a name="UiThread"></a>在 UI 线程中执行模型更改
 如果测试或所测试的方法更改了模型存储，则你必须在用户界面线程中执行它们。 如果你不执行此操作，则可能会出现 `AccessViolationException`。 将测试方法的代码包含在对 Invoke 的调用中：

```
using System.Windows.Forms;
using Microsoft.VSSDK.Tools.VsIdeTesting;
 ...
    [TestMethod]
    [HostType("VS IDE")]
    public void MyTest1()
    {
      // Store operations must run in the UI thread:
      UIThreadInvoker.Invoke((System.Action)delegate()
      {
        SetupTestState(TestSetup.ModelStore, diagram);
        ExecuteMethodUnderTest(TestSetup.ModelStore, diagram);
      });
    }
```

## <a name="MEF"></a>测试命令、笔势和其他 MEF 组件
 MEF 组件使用的属性声明具有 `[Import]` 属性，并且其值由主机设置。 通常，此类属性包括 IDiagramContext、SVsServiceProvider 和 ILinkedUndoContext。 在测试使用上述任一属性的方法时，必须先设置这些属性的值，然后再执行所测试的方法。 例如，如果你编写了类似于此代码的命令扩展：

```

  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  class MyCommand : ICommandExtension
  {
    [Import] IDiagramContext context { get; set; }
    [Import]
Microsoft.VisualStudio.Shell.SVsServiceProvider
serviceProvider {get;set;}
    [Import] ILinkedUndoContext linkedUndoContext { get; set; }
    public void Execute(IMenuCommand command)
    {
      DoCommand();
    }
    private void DoCommand()
    {
      IDiagram diagram = context.CurrentDiagram;
      using (ILinkedUndoTransaction t = linkedUndoContext.BeginTransaction("go"))
      { ... }}}

```

 则可设置导入属性，如下所示：

```

using System.ComponentModel.Composition;
using Microsoft.VisualStudio.ComponentModelHost;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.VSSDK.Tools.VsIdeTesting;
...
    [TestMethod]
    [HostType("VS IDE")]
    public void Test1()
    {
      // Create an instance of the class under test:
      MyCommand myCommand = new MyCommand();
      // Get the components service:
      IComponentModel components = VsIdeTestHostContext.ServiceProvider
        .GetService(typeof(SComponentModel)) as IComponentModel;
      // Set the imported properties of the instance under test:
      // Extension requires "using System.ComponentModel.Composition;" :
      components.DefaultCompositionService.SatisfyImportsOnce(myCommand);
      // Call method(s) under test:
      UIThreadInvoker.Invoke((System.Action)delegate()
      {
        myCommand.DoCommand();
      });
...}
```

 如果要测试将某个导入属性作为参数的方法，则可以将该属性导入测试类，然后将 `SatisfyImportsOnce` 应用于测试实例。 例如:

```

using System.ComponentModel.Composition;
...
  [TestClass]
  public class MyTestClass
  {
    [Import] ILinkedUndoContext linkedUndoContext { get; set; }

    // Called before each test method:
    [TestInitialize, HostType("VS IDE")]
    public void TestInitializer()
    {
      IComponentModel components = VsIdeTestHostContext.ServiceProvider
            .GetService(typeof(SComponentModel)) as IComponentModel;
      // Extension requires "using System.ComponentModel.Composition;" :
      components.DefaultCompositionService.SatisfyImportsOnce(this);
    }
    [TestMethod, HostType("VS IDE")]
    public void Test2()
    {
     UIThreadInvoker.Invoke((System.Action)delegate()
      {
      // Pass context items to class under test:
      Class1 item1 = new Class1(this.linkedUndoContext);
      item1.Method1(); // Can use linkedUndoContext
     });
   }
}

```

 在本例中，为方便起见，将每个测试方法的两个特性合并到一行。

## <a name="access-from-tests-to-private-methods-and-variables"></a>从测试到私有方法和变量的访问
 有时，在执行所测试的方法之前和之后，你需要测试私有方法或验证私有字段的状态。 这会带来一些困难，因为测试与所测试的类在不同的程序集中。 可以考虑一些策略，其中包括以下方法：

 仅使用公共项和内部项进行测试编写测试，使其仅使用公共（或内部）类和成员。 这是最佳方法。 即使你重构所测试的程序集的内部实现，你的测试也可继续工作。 通过在做出更改之前和之后应用相同的测试，可以确保你所做的更改没有改变程序集的行为。

 若要做到这一点，你可能必须重构你的代码。 例如，你可能需要将一些方法归为另一个类。

 在仔细考虑此方法后，你通常会发现你的代码更易于读取和更改，并且在需要更改时不易出错。

 通过在要测试的项目中的 **Properties\AssemblyInfo.cs** 中添加特性，可以允许测试程序集访问内部项：

```csharp
[assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.
```

 定义测试接口定义一个接口，该接口包括要测试的类的公共成员，以及您希望测试能够使用的私有成员的其他属性和方法。 将此接口添加到要测试的项目中。 例如:

```csharp
internal interface MyClassTestInterface {
  void PublicMethod1();
  string PublicProperty1 { get; }
  string privateField1_Accessor { get; }
  int privateMethod1_Accessor (string p1);
 }
```

 将方法添加到要测试的类中，以显式实现访问器方法。 通过将这些附加方法写入到一个单独文件中的分部类定义中，使它们与主类分离开。 例如:

```csharp
partial public class MyClass
{
  string MyClassTestInterface.privateField1_Accessor
  { get { return privateField1; } }
  int MyClassTestInterface.privateMethod1_Accessor (string p1)
  { return privateMethod1(p1); }
}

```

 通过将此特性添加到正在测试的程序集中，允许测试程序集使用测试接口：

```csharp
[assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.
```

 在单元测试方法中，使用测试接口。 例如:

```csharp
MyClassTestInterface testInstance = new MyClass();
testInstance.PublicMethod1();
Assert.AreEqual("hello", testInstance.privateField1_Accessor);
```

 使用反射定义访问器这是我们建议的最小方法。 旧版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 提供了一个实用工具，可用于自动为每个私有方法创建一个访问器方法。 虽然此方法很方便，但我们的经验表明，此方法会生成与正在测试的应用程序的内部结构紧密耦合的单元测试。 当需求或体系结构发生更改时，这会产生额外的工作量，因为测试必须与实现一起更改。 此外，实现设计中的任何错误假设也会带入到测试中，使得测试无法发现错误。

## <a name="see-also"></a>请参阅
 [单元测试剖析](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
