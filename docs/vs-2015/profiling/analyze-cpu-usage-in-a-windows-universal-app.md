---
title: 分析 Windows 通用应用中的 CPU 使用率 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c122b08e-e3bf-43e6-bd6c-e776e178fd9a
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 8d296c8803127cdbc2e6c72f86dcfba968e2b940
ms.sourcegitcommit: bdccab4c2dbd50ea8adaaf88c69c9ca32db88099
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73144783"
---
# <a name="analyze-cpu-usage-in-a-windows-universal-app"></a>分析 Windows 通用应用中的 CPU 使用率
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 和 Windows Phone] （.。。/Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 如需调查应用中的性能问题，最好从了解其使用 CPU 的方式开始。 **CPU 使用率**工具可显示 CPU 耗用时间执行代码的位置。 若要专注于特定的方案，可使用[XAML UI 响应能力](https://msdn.microsoft.com/library/4ff84cd1-4e63-4fda-b34f-3ef862a6e480)工具、 [cpu 使用率工具](../profiling/cpu-usage.md)工具或单个诊断会话中的两个工具来运行 cpu 使用情况。  
  
> [!NOTE]
> **CPU 使用率**工具不能与 Windows Phone Silverlight 8.1 应用一起使用。  
  
 本演练介绍如何收集和分析简单 Windows 通用 XAML 应用的 CPU 使用率。  
  
## <a name="BKMK_Create_the_CpuUseDemo_project"></a>创建 CpuUseDemo 项目  
 **CpuUseDemo** 是为演示如何收集和分析 CPU 使用率数据而创建的应用。 通过调用方法（该方法从对函数的多次调用中选择最大值），按钮将生成一个数字。 被调用的函数将创建大量的随机值，然后将返回最后一个随机值。 数据将显示在文本框中。  
  
1. 使用 **BlankApp** 模板创建名为 **CpuUseDemo** 的新 C# Windows 通用应用项目。  
  
     ![创建 CpuUseDemoProject](../profiling/media/cpu-use-newproject.png "CPU_USE_NewProject")  
  
2. 使用[此代码](#BKMK_MainPage_xaml)替换 MainPage.xaml。  
  
3. 使用[此代码](#BKMK_MainPage_xaml_cs)替换 MainPage.xaml.cs。  
  
4. 构建应用程序并试用。此应用程序非常简单，足以说明 CPU 使用情况数据分析的一些常见情况。  
  
## <a name="BKMK_Collect_CPU_usage_data"></a> 收集 CPU 使用量数据  
 ![在模拟器中运行应用程序的发布版本](../profiling/media/cpu-use-wt-setsimulatorandretail.png "CPU_USE_WT_SetSimulatorAndRetail")  
  
1. 在 Visual Studio 中，将部署目标设置为“模拟器”并将解决方案配置设置为“发布”。  
  
   - 通过在模拟器中运行该应用，你可以在该应用和 Visual Studio IDE 之间轻松切换。  
  
   - 在“发布”模式下运行此应用能更清晰地看到应用的实际性能。  
  
2. 在“调试” 菜单上，选择“性能探查器...”。  
  
3. 在“性能和诊断”中心中，选择“CPU 使用率”，然后选择“启动”。  
  
    ![启动 CpuUsage 诊断会话](../profiling/media/cpu-use-wt-perfdiaghub.png "CPU_USE_WT_PerfDiagHub")  
  
4. 启动应用时，单击“获取最大数”。 显示输出后等待约 1 秒时间，然后选择“获取最大数，异步”。 在单击按钮之间进行停顿有助于更轻松地隔离诊断报告中的按钮单击例程。  
  
5. 在第二个输出行显示之后，在性能和诊断中心中选择 **“停止收集”** 。  
  
   ![停止 CpuUsage 数据收集](../profiling/media/cpu-use-wt-stopcollection.png "CPU_USE_WT_StopCollection")  
  
   CPU 使用量工具可分析数据并显示报告。  
  
   ![CpuUsage 报表](../profiling/media/cpu-use-wt-report.png "CPU_USE_WT_Report")  
  
## <a name="BKMK_Analyze_the_CPU_Usage_report"></a>分析 CPU 使用率报告  
  
### <a name="BKMK_CPU_utilization_timeline_graph"></a>CPU 使用率时间线关系图  
 ![Cpu 利用率&#40;%&#41; timeline 图](../profiling/media/cpu-use-wt-timelinegraph.png "CPU_USE_WT_TimelineGraph")  
  
 CPU 使用量关系图借助设备上的所有处理器内核，以所有 CPU 时间的百分比形式显示应用的 CPU 活动。 在双核计算机上收集此报告的数据。 两个较大的峰值表示两次按钮单击事件的 CPU 活动。 `GetMaxNumberButton_Click` 将在单核上同步执行，因此方法的关系图高度永远不超过 50% 是合理的。 `GetMaxNumberAsycButton_Click` 跨两个内核异步运行，因此其峰值接近于同时在这两个内核上使用的所有 CPU 资源量，这看起来也是合理的。  
  
#### <a name="BKMK_Select_timeline_segments_to_view_details"></a>选择时间线段以查看详细信息  
 使用“诊断会话”时间线上的选择栏以专注于 GetMaxNumberButton_Click 数据：  
  
 ![已&#95;单击所选](../profiling/media/cpu-use-wt-getmaxnumberreport.png "CPU_USE_WT_GetMaxNumberReport")  
  
 现在，“诊断会话”时间线将显示选定时间线段（根据该报告，应稍大于 2 秒）内花费的时间，并筛选在选定时间段中运行的这些方法的调用关系树。  
  
 现在选择 `GetMaxNumberAsyncButton_Click` 段。  
  
 ![GetMaxNumberAsyncButton&#95;单击报表选择](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 完成此方法的速度比完成 `GetMaxNumberButton_Click` 的速度快了一秒钟，然而调用关系树项的含义却不太明显。  
  
### <a name="BKMK_The_CPU_Usage_call_tree"></a>CPU 使用率调用关系树  
 若要开始了解调用关系树的信息，重新选择 `GetMaxNumberButton_Click` 段，查看调用关系树的详细信息。  
  
#### <a name="BKMK_Call_tree_structure"></a>调用关系树结构  
 ![已&#95;单击调用树](../profiling/media/cpu-use-wt-getmaxnumbercalltree-annotated.png "CPU_USE_WT_GetMaxNumberCallTree_annotated")  
  
|||  
|-|-|  
|![步骤1](../profiling/media/procguid-1.png "ProcGuid_1")|CPU 使用量调用关系树中的顶级节点是一个伪节点|  
|![步骤2](../profiling/media/procguid-2.png "ProcGuid_2")|在大多数应用中，当禁用 **“显示外部代码”** 选项时，二级节点是 **[外部代码]** 节点，该节点包含系统和框架代码，它可以启动和停止应用、绘制 UI、控制线程计划以及向应用提供其他低级服务。|  
|![步骤3](../profiling/media/procguid-3.png "ProcGuid_3")|二级节点的子级为用户代码方法和异步例程，它们由二级系统和框架代码进行调用或创建。|  
|![步骤4](../profiling/media/procguid-4.png "ProcGuid_4")|方法的子节点仅包含用于父方法调用的数据。 禁用“显示外部代码” 后，应用方法只能包含 **[外部代码]** 节点。|  
  
#### <a name="BKMK_External_Code"></a>外部代码  
 外部代码由编写的代码执行的系统和框架组件中的函数组成。 外部代码包含的部分函数，可启动和停止应用、绘制 UI、控制线程以及向应用提供其他低级别服务。 在大多数情况下，你不会对外部代码感兴趣，因此 CPU 使用率调用关系树可将用户方法的外部函数收集到一个 **[外部代码]** 节点中。  
  
 若要查看外部代码的调用路径，请从 **“筛选器视图”** 列表中选择 **“显示外部代码”** ，然后选择 **“应用”** 。  
  
 ![选择 "筛选器视图"，然后单击 "显示外部代码"](../profiling/media/cpu-use-wt-filterview.png "CPU_USE_WT_FilterView")  
  
 请注意，许多外部代码调用链已深度嵌套，因此函数名列的宽度可能超过所有计算机监视器（最大的计算机监视器除外）的显示宽度。 发生这种情况时，函数名将显示为 **[…]** ：  
  
 ![调用关系树中的嵌套外部代码](../profiling/media/cpu-use-wt-showexternalcodetoowide.png "CPU_USE_WT_ShowExternalCodeTooWide")  
  
 使用搜索框以找到你正在查找的节点，然后使用水平滚动条以使数据在视图中显示：  
  
 ![搜索嵌套的外部代码](../profiling/media/cpu-use-wt-showexternalcodetoowide-found.png "CPU_USE_WT_ShowExternalCodeTooWide_Found")  
  
### <a name="BKMK_Call_tree_data_columns"></a>调用关系树数据列  
  
|||  
|-|-|  
|**总 CPU (%)**|![总数据量 % 等式](../profiling/media/cpu-use-wt-totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> 所选时间范围内应用的 CPU 活动百分比（函数调用和函数调用的函数使用的）。 请注意，这不同于“CPU 利用率” 时间线图，后者是将时间范围内的应用总活动量与可用的 CPU 总容量相比较。|  
|**自测 CPU (%)**|![自测 % 等式](../profiling/media/cpu-use-wt-selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> 所选时间范围内应用的 CPU 活动百分比（函数调用使用，不包括函数调用的函数活动）。|  
|**总 CPU(毫秒)**|所选时间范围内函数调用以及该函数调用函数所耗用的毫秒数。|  
|**自 CPU(毫秒)**|所选时间范围内函数调用以及该函数调用函数所耗用的毫秒数。|  
|**模块**|包含函数的模块的名称或包含 [外部代码] 节点中的函数的模块数。|  
  
### <a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a>CPU 使用率调用关系树中的异步函数  
 当编译器遇到异步方法时，它会创建一个隐藏的类以控制方法的执行。 从概念上讲，此类是一个状态机，包括编译器生成的函数（以异步方式调用原始方法的操作）的列表、回调、计划程序和所需的相应迭代器。 当由父方法调用原始方法时，运行时将从父方法的执行上下文中移除该原始方法，并且将在控制系统和框架代码的上下文中运行隐藏类的方法，以控制应用的执行。 异步方法通常（但不总是）在一个或多个不同线程上执行。 此代码将显示在 CPU 使用率调用关系树中，作为树的顶层节点正下方的 **[外部代码]** 节点的子级。  
  
 若要在我们的示例中查看该示例，请在时间线中重新选择 `GetMaxNumberAsyncButton_Click` 段。  
  
 ![GetMaxNumberAsyncButton&#95;单击报表选择](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 **[外部代码]** 下方的前两个节点是状态机类的编译器生成的方法。 第三个节点是对原始方法的调用。 通过展开生成的方法，可显示当前进行的操作。  
  
 ![展开的&#95;GetMaxNumberAsyncButton 单击调用树](../profiling/media/cpu-use-wt-getmaxnumberasync-expandedcalltree.png "CPU_USE_WT_GetMaxNumberAsync_ExpandedCallTree")  
  
- `MainPage::GetMaxNumberAsyncButton_Click` 执行的内容很少；主要管理任务值列表、计算结果最大值以及显示输出。  
  
- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` 显示用于计划和启动 48 个任务所需的活动，这些任务将包装对 `GetNumberAsync`的调用。  
  
- `MainPage::<GetNumberAsync>b__b` 显示调用 `GetNumber` 的任务的活动。  
  
## <a name="BKMK_Next_steps"></a> 后续步骤  
 CpuUseDemo 应用并非最出色的应用，但你可以在性能和诊断中心中，使用异步操作和其他工具对其进行实验，以扩展它的实用功能。  
  
- 请注意，`MainPage::<GetNumberAsync>b__b` 在[外部代码]中花费的时间多于其执行 GetNumber 方法所需的时间。 异步操作占用了其中大部分时间。 尝试增加任务（在 MainPage.xaml.cs 的 `NUM_TASKS` 常量中设置的任务）的数量，并尝试减少 `GetNumber` 中的迭代数（更改 `MIN_ITERATIONS` 值）。 运行收集方案，并将 `MainPage::<GetNumberAsync>b__b` 的 CPU 活动与原始 CPU 使用量诊断会话中的 CPU 活动进行比较。 尝试减少任务并增加迭代。  
  
- 用户通常不会关心应用的实际性能；他们在意的是应用的感知性能和响应能力。 XAML UI 响应能力工具显示影响感知响应能力的 UI 线程上的活动详细信息。  
  
     在诊断和性能中心中创建新会话，并同时添加 XAML UI 响应能力工具和 CPU 使用量工具。 运行收集方案。 如果已阅读了前面的内容，该报告显示的内容可能你早已了解，但前两个方法的“UI 线程使用率”时间线图中的差异却令人印象深刻。 在复杂且真实的应用中，工具的组合使用将很有帮助。  
  
## <a name="BKMK_MainPage_xaml"></a> MainPage.xaml  
  
```csharp  
<Page  
    x:Class="CpuUseDemo.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:local="using:CpuUseDemo"  
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    mc:Ignorable="d">  
  
    <Page.Resources>  
        <Style TargetType="TextBox">  
            <Setter Property="FontFamily"  Value="Lucida Console" />  
        </Style>  
    </Page.Resources>  
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">  
        <Grid.RowDefinitions>  
            <RowDefinition Height="Auto" />  
            <RowDefinition Height="*" />  
        </Grid.RowDefinitions>  
        <StackPanel Grid.Row="0" Orientation="Horizontal"  Margin="0,40,0,0">  
            <Button Name="GetMaxNumberButton" Click="GetMaxNumberButton_Click"  Content="Get Max Number" />  
            <Button Name="GetMaxNumberAsyncButton" Click="GetMaxNumberAsyncButton_Click"  Content="Get Max Number Async" />  
        </StackPanel>  
        <StackPanel Grid.Row="1">  
            <TextBox Name="TextBox1" AcceptsReturn="True" />  
        </StackPanel>  
    </Grid>  
  
</Page>  
  
```  
  
## <a name="BKMK_MainPage_xaml_cs"></a> MainPage.xaml.cs  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.IO;  
using System.Linq;  
using System.Runtime.InteropServices.WindowsRuntime;  
using Windows.Foundation;  
using Windows.Foundation.Collections;  
using Windows.UI.Xaml;  
using Windows.UI.Xaml.Controls;  
using Windows.UI.Xaml.Controls.Primitives;  
using Windows.UI.Xaml.Data;  
using Windows.UI.Xaml.Input;  
using Windows.UI.Xaml.Media;  
using Windows.UI.Xaml.Navigation;  
using Windows.Foundation.Diagnostics;  
using System.Threading;  
using System.Threading.Tasks;  
using System.Collections.Concurrent;  
  
// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238  
  
namespace CpuUseDemo  
{  
    /// <summary>  
    /// An empty page that can be used on its own or navigated to within a Frame.  
    /// </summary>  
    public sealed partial class MainPage : Page  
    {  
        public MainPage()  
        {  
            this.InitializeComponent();  
        }  
  
        const int NUM_TASKS = 48;  
        const int MIN_ITERATIONS = int.MaxValue / 1000;  
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;  
  
        long m_totalIterations = 0;  
        readonly object m_totalItersLock = new object();  
  
        private void GetMaxNumberButton_Click(object sender, RoutedEventArgs e)  
        {  
            GetMaxNumberAsyncButton.IsEnabled = false;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations = 0;  
            }  
            List<int> tasks = new List<int>();  
            for (var i = 0; i < NUM_TASKS; i++)  
            {  
                var result = 0;  
                result = GetNumber();  
                tasks.Add(result);  
            }  
            var max = tasks.Max();  
            var s = GetOutputString("GetMaxNumberButton_Click", NUM_TASKS, max, m_totalIterations);  
            TextBox1.Text += s;  
            GetMaxNumberAsyncButton.IsEnabled = true;  
        }  
  
        private async void GetMaxNumberAsyncButton_Click(object sender, RoutedEventArgs e)  
        {  
            GetMaxNumberButton.IsEnabled = false;  
            GetMaxNumberAsyncButton.IsEnabled = false;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations = 0;  
            }  
            var tasks = new ConcurrentBag<Task<int>>();  
            for (var i = 0; i < NUM_TASKS; i++)  
            {  
                tasks.Add(GetNumberAsync());  
            }  
            await Task.WhenAll(tasks.ToArray());  
            var max = 0;  
            foreach (var task in tasks)  
            {  
                max = Math.Max(max, task.Result);  
            }  
            var func = "GetMaxNumberAsyncButton_Click";  
            var outputText = GetOutputString(func, NUM_TASKS, max, m_totalIterations);  
            TextBox1.Text += outputText;  
            this.GetMaxNumberButton.IsEnabled = true;  
            GetMaxNumberAsyncButton.IsEnabled = true;  
        }  
  
        private int GetNumber()  
        {  
            var rand = new Random();  
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);  
            var result = 0;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations += iters;  
            }  
            // we're just spinning here  
            // and using Random to frustrate compiler optimizations  
            for (var i = 0; i < iters; i++)  
            {  
                result = rand.Next();  
            }  
            return result;  
        }  
  
        private Task<int> GetNumberAsync()  
        {  
            return Task<int>.Run(() =>  
            {  
                return GetNumber();  
            });  
        }  
  
        string GetOutputString(string func, int cycles, int max, long totalIters)  
        {  
            var fmt = "{0,-35}Tasks:{1,3}    Maximum:{2, 12}    Iterations:{3,12}\n";  
            return String.Format(fmt, func, cycles, max, totalIters);  
        }  
  
    }  
}  
  
```
