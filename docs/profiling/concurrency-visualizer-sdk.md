---
title: 并发可视化工具 SDK | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.sdk.about
ms.assetid: 4b22cdf9-59b1-4c88-a6d8-1644a4a11e08
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33b8f0215e09dd43c265c7eb8ba08613132fabbc
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68870312"
---
# <a name="concurrency-visualizer-sdk"></a>并发可视化工具 SDK
可通过使用并发可视化工具 SDK 检测源代码，以在并发可视化工具中显示附加信息。 可以在代码中将其他数据与阶段和事件关联。 这些其他的可视化被称为标记  。  有关介绍性演练，请参阅 [Introducing the Concurrency Visualizer SDK](http://go.microsoft.com/fwlink/?LinkId=235405)（并发可视化工具 SDK 简介）。

## <a name="properties"></a>属性
 标志、范围和消息都具有两个属性：类别和重要性。 在[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框中，可以使用以下属性来筛选显示的标记集。 此外，这些属性还会影响标记的视觉表示形式。 例如，标志的大小用于表示重要性。 此外，颜色用于指示类别。

## <a name="basic-usage"></a>基本用法
 并发可视化工具公开可用于生成标记的默认提供程序。 提供程序已与并发可视化工具一起注册，无需执行其他操作即可使标记显示在 UI 中。

### <a name="c-and-visual-basic"></a>C# 和 Visual Basic
 通过调用 [Markers](/previous-versions/hh694099(v=vs.140)) 类中的方法，在 C#、Visual Basic 和其他托管代码中使用默认提供程序。 它将公开四种方法，用于生成标记：[WriteFlag](/previous-versions/hh694185%28v%3dvs.140%29)、[EnterSpan](/previous-versions/hh694205(v=vs.140))、[WriteMessage](/previous-versions/hh694161(v=vs.140)) 和 [WriteAlert](/previous-versions/hh694180(v=vs.140))。 有多个用于这些函数的重载，具体取决于是否想要使用这些属性的默认值。  最简单的重载仅采用指定事件说明的字符串参数。 该说明显示在并发可视化工具报表中。

##### <a name="to-add-sdk-support-to-a-c-or-visual-basic-project"></a>向 C# 或 Visual Basic 项目添加 SDK 支持

1. 在菜单栏上，选择“分析”  、“并发可视化工具”  和“将 SDK 添加到项目中”  。

2. 选择想要在其中访问 SDK 的项目，然后选择“将 SDK 添加到所选项目中”  按钮。

3. 向代码添加 Imports 或 Using 语句。

    ```csharp
    using Microsoft.ConcurrencyVisualizer.Instrumentation;
    ```

    ```VB
    Imports Microsoft.ConcurrencyVisualizer.Instrumentation
    ```

### <a name="c"></a>C++
 在 C++ 中，创建 [marker_series 类](../profiling/marker-series-class.md)对象，并使用它来调用函数。  `marker_series` 类将公开三个用于生成标记的函数：[marker_series:: write_flag 方法](../profiling/marker-series-write-flag-method.md)、[marker_series:: write_message 方法](../profiling/marker-series-write-message-method.md)和 [marker_series:: write_alert 方法](../profiling/marker-series-write-alert-method.md)。

##### <a name="to-add-sdk-support-to-a-c-or-c-project"></a>向 C++ 或 C 项目添加 SDK 支持

1. 在菜单栏上，选择“分析”  、“并发可视化工具”  和“将 SDK 添加到项目中”  。

2. 选择想要在其中访问 SDK 的项目，然后选择“将 SDK 添加到所选项目中”  按钮。

3. 对于 C++，请包括 `cvmarkersobj.h`。 对于 C，请包括 `cvmarkers.h`。

4. 向代码添加 Using 语句。

    ```cpp
    using namespace Concurrency::diagnostic;
    ```

5. 创建 `marker_series` 对象，并将其传递给 `span` 构造函数。

    ```C++

    marker_series mySeries;
    span s(mySeries, _T("Span description"));

    ```

## <a name="custom-usage"></a>自定义用法
 对于高级方案，并发可视化工具 SDK 将公开更多的控件。  两个主要概念与更多高级方案相关联：标记提供程序和标记序列。 标记提供程序是不同的 ETW 提供程序（每个都具有不同的 GUID）。 标记序列是由一个提供程序生成的事件的串行通道。 可以使用它们组织由标记提供程序生成的事件。

#### <a name="to-use-a-new-marker-provider-in-a-c-or-visual-basic-project"></a>在 C# 或 Visual Basic 项目中使用新的标记提供程序

1. 创建 [MarkerWriter](/previous-versions/hh694138(v=vs.140)) 对象。  构造函数采用一个 GUID。

2. 若要注册该提供程序，请打开并发可视化工具的[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框。  选择“标记”  选项卡，然后选择“添加新提供程序”  按钮。 在[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框中，输入用于创建该提供程序和该提供程序说明的 GUID。

#### <a name="to-use-a-new-marker-provider-in-a-c-or-c-project"></a>在 C++ 或 C 项目中使用新的标记提供程序

1. 使用 `CvInitProvider` 函数初始化 PCV_PROVIDER。  构造函数采用 GUID* 和 PCV_PROVIDER\*。

2. 若要注册该提供程序，请打开[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框。  选择“标记”  选项卡，然后选择“添加新提供程序”  按钮。 在此对话框中，输入用于创建该提供程序和该提供程序说明的 GUID。

#### <a name="to-use-a-marker-series-in-a-c-or-visual-basic-project"></a>在 C# 或 Visual Basic 项目中使用标记系列

1. 要使用新的 [MarkerSeries](/previous-versions/hh694127(v=vs.140))，首先使用 [MarkerWriter](/previous-versions/hh694138(v=vs.140)) 对象来创建它，然后直接从新系列中生成标记事件。

    ```csharp
    MarkerSeries series1 = myMarkerWriter.CreateMarkerSeries("Series 1");
    series1.WriteFlag("My flag");
    ```

    ```VB
    Dim series1 As New myMarkerWriter.CreateMarkerSeries("Series 1")
    series1.WriteFlag("My flag")
    ```

#### <a name="to-use-a-marker-series-in-a-c-project"></a>在 C++ 项目中使用标记系列

1. 创建 `marker_series` 对象。  可以从此新系列生成事件。

    ```scr
    marker_series series;
    series.write_flag(_T("Hello world!"));
    ```

#### <a name="to-use-a-marker-series-in-a-c-project"></a>在 C 项目中使用标记系列

1. 使用 `CvCreateMarkerSeries` 函数创建 PCV_MARKERSERIES。

    ```C++
    PCV_MARKERSERIES series;
    CvCreatemarkerSeries(myProvider, _T("My Series"), &series);
    CvWriteFlag(series, _T("Writing a flag"));
    ```

## <a name="see-also"></a>请参阅

|Title|说明|
|-----------|-----------------|
|[C++ 库参考](../profiling/cpp-library-reference.md)|介绍用于 C++ 的并发可视化工具 API。|
|[C 库参考](../profiling/c-library-reference.md)|介绍用于 C 的并发可视化工具 API。|
|[检测](/previous-versions/hh694104(v=vs.140))|介绍用于托管代码的并发可视化工具 API。|
|[并发可视化工具](../profiling/concurrency-visualizer.md)|有关使用并发方法生成和包含线程执行数据的分析数据文件的视图和报表的参考信息。|