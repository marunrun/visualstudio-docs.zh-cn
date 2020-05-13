---
title: 创建基本项目系统，第 1 部分 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ff969a905d48ef16b3cb036fa897bf0307b929d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739722"
---
# <a name="create-a-basic-project-system-part-1"></a>创建基本项目系统，第 1 部分
在 Visual Studio 中，项目是开发人员用来组织源代码文件和其他资产的容器。 项目在**解决方案资源管理器**中显示为解决方案的子级。 项目允许您组织、构建、调试和部署源代码，并创建对 Web 服务、数据库和其他资源的引用。

 项目在项目文件中定义，例如 Visual C++ 项目的 *.csproj*文件。 您可以创建自己的项目类型，该类型具有自己的项目文件名扩展名。 有关项目类型的详细信息，请参阅[项目类型](../extensibility/internals/project-types.md)。

> [!NOTE]
> 如果您需要使用自定义项目类型扩展 Visual Studio，我们强烈建议利用[Visual Studio 项目系统](https://github.com/Microsoft/VSProjectSystem)（VSPS），该系统比从头开始构建项目系统具有许多优势：
>
> - 更容易上船。  即使是基本的项目系统也需要数万行代码。  利用 VSPS 可将载入成本降低到几下，然后再准备好根据您的需求进行自定义。
> - 更轻松的维护。  通过利用 VSPS，您只需要维护自己的方案。  我们处理所有项目系统基础结构的维护。
>
>   如果您需要定位比 Visual Studio 2013 更老的 Visual Studio 版本，您将无法在 Visual Studio 扩展中利用 VSPS。  如果是这样的话，这个演练是一个很好的开始的地方。

 本演练演示如何创建具有项目文件名扩展名 *.myproj*的项目类型。 本演练借用了现有的 Visual C++ 项目系统。

> [!NOTE]
> 有关扩展项目的更多示例，请参阅[VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

 本演练将介绍如何完成这些任务：

- 创建基本项目类型。

- 创建基本项目模板。

- 向可视化工作室注册项目模板。

- 通过打开 **"新项目"** 对话框，然后使用模板创建项目实例。

- 为项目系统创建项目工厂。

- 为项目系统创建项目节点。

- 为项目系统添加自定义图标。

- 实现基本模板参数替换。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

 您还必须下载[项目的托管包框架的](https://github.com/tunnelvisionlabs/MPFProj10)源代码。 将文件提取到要创建的解决方案可访问的位置。

## <a name="create-a-basic-project-type"></a>创建基本项目类型
 创建名为 **"简单项目"的**C# VSIX 项目。 （**文件** > **新项目** > **Project**，然后**可视化 C#** > **可扩展性** > **VSIX 项目**）。 添加可视化工作室包项目模板（在**解决方案资源管理器**上，右键单击项目节点并选择 **"添加新** > **项目**"，然后转到 **"扩展可视化** > **工作室"包**）。 命名文件*简单项目包*。

## <a name="creating-a-basic-project-template"></a>创建基本项目模板
 现在，您可以修改此基本 VS 包以实现新的 *.myproj*项目类型。 要创建基于 *.myproj*项目类型的项目，Visual Studio 必须知道要添加到新项目的文件、资源和引用。 要提供此信息，请将项目文件放在项目模板文件夹中。 当用户使用 *.myproj*项目创建项目时，文件将复制到新项目。

### <a name="to-create-a-basic-project-template"></a>创建基本项目模板

1. 向项目添加三个文件夹，另一个文件夹位于另一个文件夹下：*模板\项目\简单项目*。 （在**解决方案资源管理器**中，右键单击 **"简单项目项目**"节点，指向 **"添加**"，然后单击 **"新建文件夹**"。 命名文件夹*模板*。 在 *"模板"* 文件夹中，添加名为 *"项目"的*文件夹。 在 *"项目"* 文件夹中，添加名为 *"简单项目*"的文件夹。

2. 在*模板\项目\简单项目*文件夹中，添加一个位图图像文件，用作名为 *"简单项目.ico"* 的图标。 单击"**添加**"时，图标编辑器将打开。

3. 使图标与众不同。 此图标将显示在演练后面的"**新项目**"对话框中。

    ![“简单项目”图标](../extensibility/media/simpleprojicon.png "简单图标")

4. 保存图标并关闭图标编辑器。

5. 在*模板\项目\简单项目*文件夹中，添加名为*Program.cs***的类**项目。

6. 将现有代码替换为以下行。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Text;

   namespace $nameSpace$
   {
       public class $className$
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

   > [!IMPORTANT]
   > 这不是Program.cs代码的最终形式;但是，这不是*代码*的最终形式。替换参数将在后面的步骤中处理。 您可能会看到编译错误，但只要文件的**BuildAction**是**内容**，您应该能够像往常一样生成和运行项目。

7. 保存文件。

8. 将*AssemblyInfo.cs*文件从 *"属性*"文件夹复制到 *"项目"_简单项目*文件夹。

9. 在 *"项目_简单项目"* 文件夹中添加名为*SimpleProject.myproj*的 XML 文件。

   > [!NOTE]
   > 此类型的所有项目的文件名扩展名是 *.myproj*。 如果要更改它，则必须在演练中提及的任何地方更改它。

10. 将现有内容替换为以下行。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid></ProjectGuid>
        <OutputType>Exe</OutputType>
        <RootNamespace>MyRootNamespace</RootNamespace>
        <AssemblyName>MyAssemblyName</AssemblyName>
        <EnableUnmanagedDebugging>false</EnableUnmanagedDebugging>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        <DebugSymbols>true</DebugSymbols>
        <OutputPath>bin\Debug\</OutputPath>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
        <DebugSymbols>false</DebugSymbols>
        <OutputPath>bin\Release\</OutputPath>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="mscorlib" />
        <Reference Include="System" />
        <Reference Include="System.Data" />
        <Reference Include="System.Xml" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="AssemblyInfo.cs">
          <SubType>Code</SubType>
        </Compile>
        <Compile Include="Program.cs">
          <SubType>Code</SubType>
        </Compile>
      </ItemGroup>
      <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
    </Project>
    ```

11. 保存文件。

12. **Include in VSIX**在 **"属性"** 窗口中，将*AssemblyInfo.cs、Program.cs、**简单项目.ico*和*SimpleProject.myproj*的**生成操作**设置为*Program.cs***"true"。** **Content**

    此项目模板描述了具有调试配置和发布配置的基本 Visual C++ 项目。 该项目包括两个源文件 *，AssemblyInfo.cs**和Program.cs*，以及多个程序集引用。 从模板创建项目时，ProjectGuid 值将自动替换为新的 GUID。

    在**解决方案资源管理器**中，展开**的模板**文件夹应如下所示：

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>创建基本项目工厂
 您必须告诉 Visual Studio 项目模板文件夹的位置。 为此，向实现项目工厂的 VSPackage 类添加一个属性，以便在生成 VSPackage 时将模板位置写入系统注册表。 首先创建项目工厂 GUID 标识的基本项目工厂。 使用<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>属性将项目工厂连接到类`SimpleProjectPackage`。

### <a name="to-create-a-basic-project-factory"></a>创建基本项目工厂

1. 为项目工厂创建 GUID（在 **"工具"** 菜单上，单击"创建 GUID"）或使用以下示例中的**GUID。** 将 GUID 添加到具有`SimpleProjectPackage`已定义的`PackageGuidString`节附近的类。 GUID 必须同时使用 GUID 形式和字符串形式。 生成的代码应类似于以下示例。

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. 将类添加到名为*SimpleProjectFactory.cs*的顶部*简单项目*文件夹。

3. 添加以下 using 指令：

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. 向`SimpleProjectFactory`类添加 GUID 属性。 属性的值是新项目工厂 GUID。

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   现在，您可以注册项目模板。

### <a name="to-register-the-project-template"></a>注册项目模板

1. 在*SimpleProjectPackage.cs*中<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>，向`SimpleProjectPackage`类添加属性，如下所示。

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. 重建解决方案并验证其生成时是否没有错误。

    重建注册项目模板。

   参数`defaultProjectExtension`并`possibleProjectExtensions`设置为项目文件名扩展名 *（.myproj*）。 参数`projectTemplatesDirectory`设置为*模板*文件夹的相对路径。 在生成期间，此路径将转换为完整生成并添加到注册表以注册项目系统。

## <a name="test-the-template-registration"></a>测试模板注册
 模板注册告诉 Visual Studio 项目模板文件夹的位置，以便 Visual Studio 可以在 **"新项目"** 对话框中显示模板名称和图标。

### <a name="to-test-the-template-registration"></a>测试模板注册

1. 按**F5**开始调试 Visual Studio 的实验实例。

2. 在实验实例中，创建新创建的项目类型的新项目。 在 **"新项目"** 对话框中，应看到 **"已安装模板**"下的 **"简单项目**"。

   现在，您有一个已注册的项目工厂。 但是，它还不能创建项目。 项目包和项目工厂协同工作以创建和初始化项目。

## <a name="add-the-managed-package-framework-code"></a>添加托管包框架代码
 实现项目包和项目工厂之间的连接。

- 导入托管包框架的源代码文件。

    1. 卸载简单项目项目（在**解决方案资源管理器**中，选择项目节点，并在上下文菜单上单击 **"卸载项目**"），并在 XML 编辑器中打开项目文件。

    2. 将以下块添加到项目文件（略高于\<"导入>块）。 在`ProjectBasePath`刚刚下载的托管包框架代码中设置为*ProjectBase.file 文件*的位置。 您可能需要向路径名称添加反斜杠。 如果不这样做，项目可能无法找到托管包框架源代码。

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > 不要忘记路径末尾的斜杠。

    3. 重新加载项目。

    4. 添加对下列程序集的引用：

        - `Microsoft.VisualStudio.Designer.Interfaces`（在*\<VSSDK 中安装>_VisualStudio集成\公共_程序集\v2.0*）

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>初始化项目工厂

1. 在*SimpleProjectPackage.cs*文件中，添加以下`using`指令。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. 从`Microsoft.VisualStudio.Package.ProjectPackage``SimpleProjectPackage`派生类。

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. 注册项目工厂。 将以下行添加到`SimpleProjectPackage.Initialize`方法，只是在`base.Initialize`之后。

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. 实现抽象属性`ProductUserContext`：

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. 在*SimpleProjectFactory.cs*，在现有`using`指令`using`之后添加以下指令。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. 从`ProjectFactory``SimpleProjectFactory`派生类。

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. 将以下虚拟方法添加到`SimpleProjectFactory`类。 您将在后面的一节中实现此方法。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. 将以下字段和构造函数添加到`SimpleProjectFactory`类。 此`SimpleProjectPackage`引用缓存在专用字段中，以便可用于设置服务提供商站点。

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. 重建解决方案并验证其生成时是否没有错误。

## <a name="test-the-project-factory-implementation"></a>测试项目工厂实施
 测试是否调用项目工厂实现的构造函数。

### <a name="to-test-the-project-factory-implementation"></a>测试项目工厂实施

1. 在*SimpleProjectFactory.cs*文件中，在`SimpleProjectFactory`构造函数中的下一行设置断点。

    ```csharp
    this.package = package;
    ```

2. 按**F5**启动可视化工作室的实验实例。

3. 在实验实例中，开始创建新项目。 在 **"新项目**"对话框中，选择 **"简单项目**项目"类型，然后单击"**确定**"。 执行在断点处停止。

4. 清除断点并停止调试。 由于我们尚未创建项目节点，因此项目创建代码仍引发异常。

## <a name="extend-the-projectnode-class"></a>扩展 ProjectNode 类
 现在，您可以实现从`SimpleProjectNode`类派生的`ProjectNode`类。 基`ProjectNode`类处理以下项目创建任务：

- 将项目模板文件*SimpleProject.myproj 复制到*新项目文件夹。 根据在 **"新项目"** 对话框中输入的名称重命名副本。 属性`ProjectGuid`值替换为新的 GUID。

- 遍历项目模板文件的 MSBuild 元素 *，SimpleProject.myproj*，并查找`Compile`元素。 对于每个`Compile`目标文件，将文件复制到新的项目文件夹。

  派生`SimpleProjectNode`类处理以下任务：

- 启用创建或选择**解决方案资源管理器**中项目和文件节点的图标。

- 启用指定其他项目模板参数替换。

### <a name="to-extend-the-projectnode-class"></a>扩展 ProjectNode 类

1. 添加名为的 `SimpleProjectNode.cs` 的类。

2. 用下面的代码替换现有代码。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Project;

   namespace SimpleProject
   {
       public class SimpleProjectNode : ProjectNode
       {
           private SimpleProjectPackage package;

           public SimpleProjectNode(SimpleProjectPackage package)
           {
               this.package = package;
           }
           public override Guid ProjectGuid
           {
               get { return SimpleProjectPackage.guidSimpleProjectFactory; }
           }
           public override string ProjectType
           {
               get { return "SimpleProjectType"; }
           }

           public override void AddFileFromTemplate(
               string source, string target)
           {
               this.FileTemplateProcessor.UntokenFile(source, target);
               this.FileTemplateProcessor.Reset();
           }
       }
   }
   ```

   此类`SimpleProjectNode`实现具有以下重写方法：

- `ProjectGuid`返回项目工厂 GUID。

- `ProjectType`返回项目类型的本地化名称。

- `AddFileFromTemplate`将所选文件从模板文件夹复制到目标项目。 此方法在后面的一节中进一步实现。

  构造`SimpleProjectNode`函数与`SimpleProjectFactory`构造函数一`SimpleProjectPackage`样，在私有字段中缓存引用，以便以后使用。

  要将`SimpleProjectFactory`类连接到类，`SimpleProjectNode`必须在`SimpleProjectNode``SimpleProjectFactory.CreateProject`方法中实例化新，并将其缓存在私有字段中，以便以后使用。

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>连接项目工厂类和节点类

1. 在*SimpleProjectFactory.cs*文件中，添加以下`using`指令：

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. 使用以下`SimpleProjectFactory.CreateProject`代码替换方法。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. 重建解决方案并验证其生成时是否没有错误。

## <a name="test-the-projectnode-class"></a>测试 ProjectNode 类
 测试项目工厂以查看它是否创建了项目层次结构。

### <a name="to-test-the-projectnode-class"></a>测试 ProjectNode 类

1. 按 **F5** 开始调试。 在实验实例中，创建新的简单项目。

2. Visual Studio 应调用项目工厂以创建项目。

3. 关闭 Visual Studio 的实验实例。

## <a name="add-a-custom-project-node-icon"></a>添加自定义项目节点图标
 前面部分中的项目节点图标是默认图标。 您可以将其更改为自定义图标。

### <a name="to-add-a-custom-project-node-icon"></a>添加自定义项目节点图标

1. 在 **"资源"** 文件夹中，添加名为*SimpleProjectNode.bmp*的位图文件。

2. 在 **"属性"** 窗口中，将位图减小到 16 x 16 像素。 使位图与众不同。

    ![简单项目命令](../extensibility/media/simpleprojprojectcomm.png "简单专业项目通信")

3. 在 **"属性"** 窗口中，将位图的**生成操作**更改为 **"嵌入资源**"。

4. 在*SimpleProjectNode.cs*中，添加`using`以下指令：

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. 将以下静态字段和构造函数添加到`SimpleProjectNode`类。

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. 将以下属性添加到类的`SimpleProjectNode`开头。

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. 将实例构造函数替换为以下代码。

   ```csharp
   public SimpleProjectNode(SimpleProjectPackage package)
   {
       this.package = package;

       imageIndex = this.ImageHandler.ImageList.Images.Count;

       foreach (Image img in imageList.Images)
       {
           this.ImageHandler.AddImage(img);
       }
   }
   ```

   在静态构造期间`SimpleProjectNode`，从程序集清单资源检索项目节点位图，并将其缓存在专用字段中，以便以后使用。 请注意图像路径的<xref:System.Reflection.Assembly.GetManifestResourceStream%2A>语法。 要查看嵌入在程序集中的清单资源的名称，请使用 方法<xref:System.Reflection.Assembly.GetManifestResourceNames%2A>。 将此方法应用于程序集时`SimpleProject`，结果应如下所示：

- *简单项目.资源.资源*

- *可视化工作室.项目资源*

- *简单项目.VS包.资源*

- *资源.图像.bmp*

- *微软.VisualStudio.项目.不要再次显示对话.资源*

- *微软.VisualStudio.项目.安全警告对话.资源*

- *简单项目.资源.简单项目节点.bmp*

  在实例构造期间，`ProjectNode`基类加载*Resources.imagelis.bmp*，其中嵌入了资源 *_imagelis.bmp*中常用的 16 x 16 位图。 此位图列表可供`SimpleProjectNode`作为`ImageHandler.ImageList`。 `SimpleProjectNode`将项目节点位图追加到列表中。 图像列表中的项目节点位图的偏移量将缓存，供以后用作公共`ImageIndex`属性的值。 Visual Studio 使用此属性来确定要显示为项目节点图标的位图。

## <a name="test-the-custom-project-node-icon"></a>测试自定义项目节点图标
 测试项目工厂以查看它是否创建具有自定义项目节点图标的项目层次结构。

### <a name="to-test-the-custom-project-node-icon"></a>测试自定义项目节点图标

1. 开始调试，并在实验实例中创建新的 SimpleProject。

2. 在新创建的项目中，请注意*SimpleProjectNode.bmp*用作项目节点图标。

     ![简单项目“新建项目节点”](../extensibility/media/simpleprojnewprojectnode.png "简单专业项目节点")

3. 在代码编辑器中打开“Program.cs”**。 您应该会看到类似于以下代码的源代码。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace $nameSpace$
    {
        public class $className$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

     请注意，模板参数$nameSpace$和 $className$没有新值。 您将在下一节中了解如何实现模板参数替换。

## <a name="substitute-template-parameters"></a>替换模板参数
 在前面的一节中，您可以使用 属性`ProvideProjectFactory`向 Visual Studio 注册项目模板。 以这种方式注册模板文件夹的路径，可以通过重写和扩展`ProjectNode.AddFileFromTemplate`类来启用基本的模板参数替换。 有关详细信息，请参阅[新项目生成：在引擎盖下，第二部分](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 现在向`AddFileFromTemplate`类添加替换代码。

### <a name="to-substitute-template-parameters"></a>替换模板参数

1. 在*SimpleProjectNode.cs*文件中，添加以下`using`指令。

   ```csharp
   using System.IO;
   ```

2. 使用以下`AddFileFromTemplate`代码替换方法。

   ```csharp
   public override void AddFileFromTemplate(
       string source, string target)
   {
       string nameSpace =
           this.FileTemplateProcessor.GetFileNamespace(target, this);
       string className = Path.GetFileNameWithoutExtension(target);

       this.FileTemplateProcessor.AddReplace("$nameSpace$", nameSpace);
       this.FileTemplateProcessor.AddReplace("$className$", className);

       this.FileTemplateProcessor.UntokenFile(source, target);
       this.FileTemplateProcessor.Reset();
   }
   ```

3. 在`className`赋值语句之后，在 方法中设置断点。

   赋值语句确定命名空间和新类名称的合理值。 使用这些新`ProjectNode.FileTemplateProcessor.AddReplace`值，两个方法调用替换相应的模板参数值。

## <a name="test-the-template-parameter-substitution"></a>测试模板参数替换
 现在，您可以测试模板参数替换。

### <a name="to-test-the-template-parameter-substitution"></a>测试模板参数替换

1. 开始调试，并在实验实例中创建新的 SimpleProject。

2. 执行停止在`AddFileFromTemplate`方法的断点处。

3. 检查 和`nameSpace``className`参数的值。

   - `nameSpace`在\<*[模板\项目]简单项目_简单项目.myproj*项目模板文件中给出 rootNamespace> 元素的值。 在本例中，该值为 `MyRootNamespace`。

   - `className`给定类源文件名的值，而不提供文件名扩展名。 在这种情况下，要复制到目标文件夹的第一个文件*AssemblyInfo.cs*。因此，类名称的值为`AssemblyInfo`。

4. 删除断点，然后按**F5**继续执行。

    可视化工作室应完成项目创建。

5. 在代码编辑器中打开“Program.cs”**。 您应该会看到类似于以下代码的源代码。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;

   namespace MyRootNamespace
   {
       public class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

    请注意，命名空间现在是`MyRootNamespace`，类名称现在是。 `Program`

6. 开始调试项目。 新项目应编译、运行并显示"您好 VSX !!!" 显示文本字符串“Hello World!”。

    ![简单项目命令](../extensibility/media/simpleprojcommand.png "简单专业命令")

   祝贺你！ 您已经实现了基本的托管项目系统。
