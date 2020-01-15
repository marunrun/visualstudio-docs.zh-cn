---
title: 使用 .runsettings 文件配置单元测试
ms.date: 10/03/2019
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 3f6690c2443b6c084c3e876cbb1a4340247613e0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593247"
---
# <a name="configure-unit-tests-by-using-a-runsettings-file"></a>使用 .runsettings 文件配置单元测试 

通过使用 .runsettings 文件，可配置 Visual Studio 中的单元测试  。 例如，可更改正在运行测试的 .NET 版本、测试结果的目录，或者在测试运行期间收集的数据。

运行设置文件是可选的。 如果不需要执行任何特殊配置，则无需 .runsettings 文件  。 .runsettings 文件常见的用途是自定义[代码覆盖率分析](../test/customizing-code-coverage-analysis.md)  。

## <a name="specify-a-run-settings-file"></a>指定运行设置文件

运行设置文件可以用来在 IDE 中或者在使用 Azure Test Plans 或 Team Foundation Server (TFS) 的[生成工作流](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts)中，配置从[命令行](vstest-console-options.md)运行的测试。

### <a name="ide"></a>IDE

::: moniker range="vs-2017"

若要在 IDE 中指定一个运行设置文件，请选择“测试”  >“测试设置”  >“选择测试设置文件”  ，然后选择 .runsettings  文件。

![在 Visual Studio 2017 中选择测试设置文件菜单](media/select-test-settings-file.png)

该文件将显示在“测试设置”菜单上，你可以选择或取消选择它。 选择后，每当选择“分析代码覆盖率”时，都会应用运行设置文件  。

::: moniker-end

::: moniker range=">=vs-2019"

#### <a name="visual-studio-2019-version-163-and-earlier"></a>Visual Studio 2019 版本 16.3 及更早版本

若要在 IDE 中指定运行设置文件，请选择“测试”   > “选择设置文件”  。 浏览到并选择 .runsettings 文件  。

![在 Visual Studio 2019 中选择测试设置文件菜单](media/vs-2019/select-settings-file.png)

该文件将显示在“测试”菜单上，你可以选择或取消选择它。 选择后，每当选择“分析代码覆盖率”时，都会应用运行设置文件  。

#### <a name="visual-studio-2019-version-164-and-later"></a>Visual Studio 2019 版本 16.4 及更高版本

在 Visual Studio 2019 版本 16.4 及更高版本中，指定运行设置文件的方法有三种：

- 通过项目文件或 Directory.Build.props 文件将生成属性添加到项目。 项目的运行设置文件由 RunSettingsFilePath  属性指定。 

    - 当前 C#、VB、C++ 和 F# 项目中支持项目级运行设置。
    - 为项目指定的文件将替代解决方案中指定的任何其他运行设置文件。

     指定项目的 .runsettings 文件示例：
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <RunSettingsFilePath>$(SolutionDir)\example.runsettings</RunSettingsFilePath>
      </PropertyGroup>
      ...
    </Project>
    ```

- 将名为“.runsettings”的运行设置文件放在解决方案的根目录下。

  如果启用了自动检测运行设置文件，则此文件中的设置将应用到所有测试运行。 可以从以下两个位置打开 runsettings 文件自动检测：
  
    - “工具”  >“选项”  >“测试”  >“自动检测 runsettings 文件” 

      ![Visual Studio 2019 自动检测 runsettings 文件选项](media/vs-2019/auto-detect-runsettings-tools-window.png)
      
    - “测试”  >“配置运行设置”  >“自动检测 runsettings 文件” 
    
      ![Visual Studio 2019 自动检测 runsettings 文件菜单](media/vs-2019/auto-detect-runsettings-menu.png)

- 在 IDE 中，选择“测试”  >“配置运行设置”  >“选择解决方案范围的 runsettings 文件”  ，然后选择 .runsettings  文件。

   ![在 Visual Studio 2019 中选择测试解决方案范围的 runsettings 文件菜单](media/vs-2019/select-solution-settings-file.png)
      
   - 此文件替代解决方案根目录下的 “.runsettings”文件（如果存在），并应用于所有测试运行。  
   - 此文件选择仅在本地保留。 

::: moniker-end

### <a name="command-line"></a>命令行

若要从命令行运行测试，请使用 vstest.console.exe 并使用 /Settings 参数指定设置文件   。

1. 启动 Visual Studio 开发人员命令提示符：

   ::: moniker range="vs-2017"

   在 Windows“启动”  菜单中，选择“Visual Studio 2017”  >“VS 2017 的开发人员命令提示”  。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   在 Windows“启动”  菜单中，选择“Visual Studio 2019”  >“VS 2019 的开发人员命令提示”  。

   ::: moniker-end

2. 输入类似的命令：

   ```cmd
   vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage /Settings:CodeCoverage.runsettings
   ```

   or

   ```cmd
   vstest.console.exe --settings:test.runsettings test.dll
   ```

有关详细信息，请参阅 [VSTest.Console.exe 命令行选项](vstest-console-options.md)。

## <a name="customize-tests"></a>自定义测试

若要使用 .runsettings 文件自定义测试，请执行以下步骤  ：

1. 将 XML 文件添加到 Visual Studio 解决方案并将其另存为 test.runsettings  。

   > [!TIP]
   > 只要使用扩展名 .runsettings，文件名就无关紧要  。

2. 使用以下示例中的 XML 替换文件内容，并根据需要自定义。

::: moniker range="vs-2017"

3. 在“测试”  菜单上，依次选择“测试设置”  、“选择测试设置文件” >   。 浏览到创建的 .runsettings 文件，然后选择“确定”   。

::: moniker-end

::: moniker range=">=vs-2019"

3. 若要选择运行设置文件，请选择“测试”   > “选择设置文件”  。 浏览到创建的 .runsettings 文件，然后选择“确定”   。

::: moniker-end

   > [!TIP]
   > 可以在解决方案中创建多个 .runsettings 文件，然后按需选择一个作为活动测试设置文件  。

## <a name="example-runsettings-file"></a>.runsettings 文件示例 

以下 XML 显示典型 .runsettings 文件的内容  。 文件的每个元素都是可选的，因为它有默认值。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- Configurations that affect the Test Framework -->
  <RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <!-- Path relative to directory that contains .runsettings file-->
    <ResultsDirectory>.\TestResults</ResultsDirectory>

    <!-- x86 or x64 -->
    <!-- You can also change it from the Test menu; choose "Processor Architecture for AnyCPU Projects" -->
    <TargetPlatform>x86</TargetPlatform>

    <!-- Framework35 | [Framework40] | Framework45 -->
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>

    <!-- Path to Test Adapters -->
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>

    <!-- TestSessionTimeout was introduced in Visual Studio 2017 version 15.5 -->
    <!-- Specify timeout in milliseconds. A valid value should be greater than 0 -->
    <TestSessionTimeout>10000</TestSessionTimeout>
  </RunConfiguration>

  <!-- Configurations for data collectors -->
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
        <Configuration>
          <CodeCoverage>
            <ModulePaths>
              <Exclude>
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
              </Exclude>
            </ModulePaths>

            <!-- We recommend you do not change the following values: -->
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
            <CollectFromChildProcesses>True</CollectFromChildProcesses>
            <CollectAspDotNet>False</CollectAspDotNet>

          </CodeCoverage>
        </Configuration>
      </DataCollector>

      <DataCollector uri="datacollector://microsoft/VideoRecorder/1.0" assemblyQualifiedName="Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder.VideoRecorderDataCollector, Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder, Version=15.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" friendlyName="Screen and Voice Recorder">
        <!--Video data collector was introduced in Visual Studio 2017 version 15.5 -->
        <Configuration>
          <!-- Set "sendRecordedMediaForPassedTestCase" to "false" to add video attachments to failed tests only -->
          <MediaRecorder sendRecordedMediaForPassedTestCase="true"  xmlns="">           
            <ScreenCaptureVideo bitRate="512" frameRate="2" quality="20" />
          </MediaRecorder>
        </Configuration>
      </DataCollector>
    </DataCollectors>
  </DataCollectionRunSettings>

  <!-- Parameters used by tests at run time -->
  <TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="webAppUserName" value="Admin" />
    <Parameter name="webAppPassword" value="Password" />
  </TestRunParameters>

  <!-- Adapter Specific sections -->

  <!-- MSTest adapter -->
  <MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
  </MSTest>

</RunSettings>
```

## <a name="elements-of-a-runsettings-file"></a>.runsettings 文件的元素 

以下各节详细介绍了 .runsettings 文件的元素  。

### <a name="run-configuration"></a>运行配置

```xml
<RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <ResultsDirectory>.\TestResults</ResultsDirectory>
    <TargetPlatform>x86</TargetPlatform>
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>
    <TestSessionTimeout>10000</TestSessionTimeout>
</RunConfiguration>
```

RunConfiguration 元素可以包含下列元素  ：

|节点|默认|值|
|-|-|-|
|**ResultsDirectory**||在其中放置测试结果的目录。|
|**TargetFrameworkVersion**|Framework40|适用于 .NET Core 源的 `FrameworkCore10`、适用于基于 UWP 源的 `FrameworkUap10`、适用于 .NET Framework 4.5 及更高版本的 `Framework45`、适用于 .NET Framework 4.0 的 `Framework40` 以及适用于 .NET Framework 3.5 的 `Framework35`。<br /><br />此设置指定使用哪一版本的单元测试框架来查找并执行测试。 它可能与你在单元测试项目的生成属性中指定的 .NET 平台的版本不同。<br /><br />如果省略 .runsettings  文件中的 `TargetFrameworkVersion` 元素，平台会基于生成的二进制文件自动确定框架版本。|
|**TargetPlatform**|x86|x86、x64|
|**TreatTestAdapterErrorsAsWarnings**|false|false、true|
|**TestAdaptersPaths**||TestAdapters 所在目录的一个或多个路径|
|**MaxCpuCount**|1|此设置利用计算机上的可用内核，在运行单元测试时控制并行测试执行的程度。 测试执行引擎在每个可用内核上作为单独的进程启动，并为每个内核提供包含要运行的测试的容器。 容器可以是程序集、DLL 或相关项目。 测试容器即计划单位。 在每个容器中，测试将根据测试框架进行执行。 如果存在多个容器，进程在容器内完成测试执行时，系统会向它们提供下一个可用容器。<br /><br />MaxCpuCount 可以是：<br /><br />n，其中 1 <= n <= 内核数：最多启动 n 个进程<br /><br />n，其中 n = 任何其他值：启动的进程数最多可达可用内核数|
|**TestSessionTimeout**||当测试会话超过给定时间，允许用户终止测试会话。 设置超时可确保资源被充分利用，并且测试会话被限制在一个设定时间内。 Visual Studio 2017 版本 15.5  及更高版本中提供了此设置。|

### <a name="diagnostic-data-adapters-data-collectors"></a>诊断数据适配器（数据收集器）

DataCollectors 元素指定诊断数据适配器的设置  。 诊断数据适配器收集有关测试环境和受测的应用程序的其他信息。 每个适配器都具有默认设置，因此如果不希望使用默认值，只需提供设置。

#### <a name="code-coverage-adapter"></a>代码覆盖率适配器

```xml
<CodeCoverage>
    <ModulePaths>
        <Exclude>
            <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
        </Exclude>
    </ModulePaths>

    <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
    <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
    <CollectFromChildProcesses>True</CollectFromChildProcesses>
    <CollectAspDotNet>False</CollectAspDotNet>
</CodeCoverage>
```

代码覆盖率数据收集器创建应用程序代码的哪些部分已在测试中执行过的日志。 有关自定义代码覆盖率设置的详细信息，请参阅[自定义代码覆盖率分析](../test/customizing-code-coverage-analysis.md)。

#### <a name="video-data-collector"></a>视频数据收集器

视频数据收集器在运行测试时捕获屏幕录制。 此录制可用于对 UI 测试进行故障排除+。 视频数据收集器在 Visual Studio 2017 版本 15.5 及更高版本中可用  。

若要自定义任何其他类型的诊断数据适配器，请使用[测试设置文件](../test/collect-diagnostic-information-using-test-settings.md)。

### <a name="testrunparameters"></a>TestRunParameters

```xml
<TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="docsUrl" value="https://docs.microsoft.com" />
</TestRunParameters>
```

测试运行参数提供了一种可用于运行时测试的定义变量和值的方法。 使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.Properties%2A?displayProperty=nameWithType> 属性访问参数：

```csharp
[TestMethod]
public void HomePageTest()
{
    string appURL = TestContext.Properties["webAppUrl"];
}
```

若要使用测试运行参数，请将专用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> 字段和公共 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> 属性添加到测试类。

### <a name="mstest-run-settings"></a>MSTest 运行设置

```xml
<MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory Path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
</MSTest>
```

这些设置特定于运行具有 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 特性的测试方法的测试适配器。

|配置|默认|值|
|-|-|-|
|**ForcedLegacyMode**|false|在 Visual Studio 2012 中，对 MSTest 适配器进行了优化，使其变得更快且更具可伸缩性。 某些行为（如测试的运行顺序）可能不与 Visual Studio 早期版本中的完全一致。 将此值设置为 true 可使用旧测试适配器  。<br /><br />例如，如果为单元测试指定 app.config 文件，可能会用到此设置  。<br /><br />我们建议你考虑重构测试以便可以使用较新的适配器。|
|**IgnoreTestImpact**|false|当在 MSTest 中或从 Microsoft 测试管理器运行时，测试影响功能会设置受最近更改影响的测试的优先级。 此设置会停用该功能。 有关详细信息，请参阅[自上一个生成后应运行哪些测试？](https://msdn.microsoft.com/library/dd286589)。|
|**SettingsFile**||你可以指定测试设置文件以便与此处的 MSTest 适配器配合使用。 还可以[从设置菜单](#ide)指定测试设置文件。<br /><br />如果指定此值，则还必须将“ForcedlegacyMode”  设置为“true”  。<br /><br />`<ForcedLegacyMode>true</ForcedLegacyMode>`|
|**KeepExecutorAliveAfterLegacyRun**|false|测试运行完成后，MSTest 将关闭。 测试中启动的任何进程也将终止。 如果希望测试执行程序保持活动状态，请将此值设为 true  。 例如，可使用此设置让浏览器保持在编码的 UI 测试之间运行。|
|**DeploymentEnabled**|true|如果将此值设置为 false，则不会将已在测试方法中指定的部署项目复制到部署目录中  。|
|**CaptureTraceOutput**|true|你可以使用 <xref:System.Diagnostics.Trace.WriteLine%2A?displayProperty=nameWithType> 从测试方法写入调试跟踪。|
|**DeleteDeploymentDirectoryAfterTestRunIsComplete**|true|若要在测试运行后保留部署目录，请将此值设置为 false  。|
|**MapInconclusiveToFailed**|false|如果测试完成返回无结论的状态，则会映射到“测试资源管理器”中的已跳过状态  。 如果希望无结论的测试显示为失败，请将此值设为 true  。|
|**InProcMode**|false|如果希望测试在与 MSTest 适配器相同的进程中运行，请将此值设置为 true  。 此设置将提供较小的性能提升。 但是，如果测试存在异常，则剩余测试不会运行。|
|**AssemblyResolution**|false|查找和执行单元测试时，可以指定其他程序集的路径。 例如，对与测试程序集位于不同目录中的依赖程序集使用这些路径。 若要指定路径，请使用“Directory Path”元素  。 路径可以包括环境变量。<br /><br />`<AssemblyResolution>  <Directory Path="D:\myfolder\bin\" includeSubDirectories="false"/> </AssemblyResolution>`|

## <a name="see-also"></a>请参阅

- [配置测试运行](https://github.com/microsoft/vstest-docs/blob/master/docs/configure.md)
- [自定义代码覆盖率分析](../test/customizing-code-coverage-analysis.md)
- [Visual Studio 测试任务 (Azure Test Plans)](/azure/devops/pipelines/tasks/test/vstest?view=vsts)
