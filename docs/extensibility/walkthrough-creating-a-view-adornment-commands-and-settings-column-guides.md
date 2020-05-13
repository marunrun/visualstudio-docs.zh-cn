---
title: 创建视图修饰、命令和设置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4a2df0a3-42da-4f7b-996f-ee16a35ac922
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4aab9e0ede95eebe6f8f54cc3f01e7e7d5f98d1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697650"
---
# <a name="walkthrough-create-a-view-adornment-commands-and-settings-column-guides"></a>演练：创建视图装饰、命令和设置（列参考线）
您可以使用命令和视图效果扩展 Visual Studio 文本/代码编辑器。 本文介绍如何开始使用流行的扩展功能，列指南。 列参考线是在文本编辑器的视图上绘制的视觉光线，可帮助您将代码管理到特定的列宽度。 具体来说，格式化的代码对于包含在文档、博客文章或 Bug 报告中的示例非常重要。

本演练中的操作：
- 创建 VSIX 项目
- 添加编辑器视图修饰
- 添加对保存和获取设置的支持（在何处绘制列参考线及其颜色）
- 添加命令（添加/删除列参考线，更改其颜色）
- 将命令放在"编辑"菜单和文本文档上下文菜单上
- 添加从可视化工作室命令窗口调用命令的支持

  您可以使用此可视化工作室库[扩展名](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)试用列指南功能的版本。

  > [!NOTE]
  > 在本演练中，您将大量代码粘贴到 Visual Studio 扩展模板生成的几个文件中。 但是，很快本演练将参考 GitHub 上已完成的解决方案以及其他扩展示例。 已完成的代码略有不同，因为它具有真正的命令图标，而不是使用泛型模板图标。

## <a name="get-started"></a>入门
从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="set-up-the-solution"></a>设置解决方案
首先，创建 VSIX 项目，添加编辑器视图修饰，然后添加一个命令（该命令添加 VSPackage 来拥有该命令）。 基本体系结构如下所示：
- 您有一个文本视图创建侦听器`ColumnGuideAdornment`，用于创建每个视图的对象。 此对象根据需要侦听有关视图更改或设置更改、更新或重绘列参考线的事件。
- 有一个`GuidesSettingsManager`处理从 Visual Studio 设置存储读取和写入。 设置管理器还有用于更新支持用户命令的设置的操作（添加列、删除列、更改颜色）。
- 如果您有用户命令，则需要使用 VSIP 包，但只是初始化命令实现对象的样板代码。
- 有一个`ColumnGuideCommands`对象运行用户命令，并挂接*在 .vsct*文件中声明的命令的命令处理程序。

  **VSIX**. 使用**文件&#124; New ...** 命令创建项目。 在左侧导航窗格中选择**C#** 下的 **"扩展性节点"，** 并在右侧窗格中选择**VSIX 项目**。 输入名称 **"列指南**"并选择 **"确定"** 以创建项目。

  **查看修饰**。 按解决方案资源管理器中项目节点上的右指针按钮。 选择"**添加&#124;新项目 ...** 在左侧导航窗格中选择 **"可扩展性&#124;编辑器**"，并在右侧窗格中选择 **"编辑器视口装饰**"。 输入名称 **"列指南"** 作为项目名称，然后选择 **"添加**"以添加它。

  您可以看到此项模板向项目添加了两个文件（以及引用，等等 **）：ColumnGuideAdornment.cs**和**ColumnGuideAdornmentTextViewCreationListener.cs**。 模板在视图上绘制紫色矩形。 在以下部分中，您将更改视图创建侦听器中的几行，并替换**ColumnGuideAdornment.cs**的内容。

  **命令**. 在**解决方案资源管理器中**，按项目节点上的右指针按钮。 选择"**添加&#124;新项目 ...** 在左侧导航窗格**中选择"扩展性&#124; VSPackage"，** 并在右侧窗格中选择 **"自定义命令**"。 输入名称**列指南命令**作为项目名称，然后选择 **"添加**"。 除了几个引用，添加命令和包还添加了**ColumnGuideCommands.cs、ColumnGuideCommandsPackage.cs**和**ColumnGuideCommandsPackage.cs** **ColumnGuideCommandsPackage.vsct**。 在以下部分中，替换第一个和最后一个文件的内容，以定义和实现命令。

## <a name="set-up-the-text-view-creation-listener"></a>设置文本视图创建侦听器
在编辑器中打开*ColumnGuideAdornmentTextViewCreationListener.cs。* 每当 Visual Studio 创建文本视图时，此代码都会实现处理程序。 根据视图的特征，有一些属性可以控制调用处理程序。

代码还必须声明修饰层。 当编辑器更新视图时，它会获取视图的修饰图层，并从中获取修饰元素。 您可以使用属性声明图层相对于其他图层的顺序。 更换以下行：

```csharp
[Order(After = PredefinedAdornmentLayers.Caret)]
```

用这两行：

```csharp
[Order(Before = PredefinedAdornmentLayers.Text)]
[TextViewRole(PredefinedTextViewRoles.Document)]
```

替换的行位于声明修饰图层的一组属性中。 您更改的第一行仅更改列参考线显示的位置。 在视图中绘制"之前"的文本意味着它们显示在文本后面或下方。 第二行声明，列指南修饰适用于符合文档概念的文本实体，但您可以声明修饰（例如，仅适用于可编辑文本）。 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)中提供了更多信息

## <a name="implement-the-settings-manager"></a>实现设置管理器
将*GuidesSettingsManager.cs*的内容替换为以下代码（如下所述）：

```csharp
using Microsoft.VisualStudio.Settings;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Settings;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Media;

namespace ColumnGuides
{
    internal static class GuidesSettingsManager
    {
        // Because my code is always called from the UI thred, this succeeds.
        internal static SettingsManager VsManagedSettingsManager =
            new ShellSettingsManager(ServiceProvider.GlobalProvider);

        private const int _maxGuides = 5;
        private const string _collectionSettingsName = "Text Editor";
        private const string _settingName = "Guides";
        // 1000 seems reasonable since primary scenario is long lines of code
        private const int _maxColumn = 1000;

        static internal bool AddGuideline(int column)
        {
            if (! IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column",
                    "The paramenter must be between 1 and " + _maxGuides.ToString());
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            if (offsets.Count() >= _maxGuides)
                return false;
            // Check for duplicates
            if (offsets.Contains(column))
                return false;
            offsets.Add(column);
            WriteSettings(GuidesSettingsManager.GuidelinesColor, offsets);
            return true;
        }

        static internal bool RemoveGuideline(int column)
        {
            if (!IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column", "The paramenter must be between 1 and 10,000");
            var columns = GuidesSettingsManager.GetColumnOffsets();
            if (! columns.Remove(column))
            {
                // Not present.  Allow user to remove the last column
                // even if they're not on the right column.
                if (columns.Count != 1)
                    return false;

                columns.Clear();
            }
            WriteSettings(GuidesSettingsManager.GuidelinesColor, columns);
            return true;
        }

        static internal bool CanAddGuideline(int column)
        {
            if (!IsValidColumn(column))
                return false;
            var offsets = GetColumnOffsets();
            if (offsets.Count >= _maxGuides)
                return false;
            return ! offsets.Contains(column);
        }

        static internal bool CanRemoveGuideline(int column)
        {
            if (! IsValidColumn(column))
                return false;
            // Allow user to remove the last guideline regardless of the column.
            // Okay to call count, we limit the number of guides.
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            return offsets.Contains(column) || offsets.Count() == 1;
        }

        static internal void RemoveAllGuidelines()
        {
            WriteSettings(GuidesSettingsManager.GuidelinesColor, new int[0]);
        }

        private static bool IsValidColumn(int column)
        {
            // zero is allowed (per user request)
            return 0 <= column && column <= _maxColumn;
        }

        // This has format "RGB(<int>, <int>, <int>) <int> <int>...".
        // There can be any number of ints following the RGB part,
        // and each int is a column (char offset into line) where to draw.
        static private string _guidelinesConfiguration;
        static private string GuidelinesConfiguration
        {
            get
            {
                if (_guidelinesConfiguration == null)
                {
                    _guidelinesConfiguration =
                        GetUserSettingsString(
                            GuidesSettingsManager._collectionSettingsName,
                            GuidesSettingsManager._settingName)
                        .Trim();
                }
                return _guidelinesConfiguration;
            }

            set
            {
                if (value != _guidelinesConfiguration)
                {
                    _guidelinesConfiguration = value;
                    WriteUserSettingsString(
                        GuidesSettingsManager._collectionSettingsName,
                        GuidesSettingsManager._settingName, value);
                    // Notify ColumnGuideAdornments to update adornments in views.
                    var handler = GuidesSettingsManager.SettingsChanged;
                    if (handler != null)
                        handler();
                }
            }
        }

        internal static string GetUserSettingsString(string collection, string setting)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetReadOnlySettingsStore(SettingsScope.UserSettings);
            return store.GetString(collection, setting, "RGB(255,0,0) 80");
        }

        internal static void WriteUserSettingsString(string key, string propertyName,
                                                     string value)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetWritableSettingsStore(SettingsScope.UserSettings);
            store.CreateCollection(key);
            store.SetString(key, propertyName, value);
        }

        // Persists settings and sets property with side effect of signaling
        // ColumnGuideAdornments to update.
        static private void WriteSettings(Color color, IEnumerable<int> columns)
        {
            string value = ComposeSettingsString(color, columns);
            GuidelinesConfiguration = value;
        }

        private static string ComposeSettingsString(Color color,
                                                    IEnumerable<int> columns)
        {
            StringBuilder sb = new StringBuilder();
            sb.AppendFormat("RGB({0},{1},{2})", color.R, color.G, color.B);
            IEnumerator<int> columnsEnumerator = columns.GetEnumerator();
            if (columnsEnumerator.MoveNext())
            {
                sb.AppendFormat(" {0}", columnsEnumerator.Current);
                while (columnsEnumerator.MoveNext())
                {
                    sb.AppendFormat(", {0}", columnsEnumerator.Current);
                }
            }
            return sb.ToString();
        }

        // Parse a color out of a string that begins like "RGB(255,0,0)"
        static internal Color GuidelinesColor
        {
            get
            {
                string config = GuidelinesConfiguration;
                if (!String.IsNullOrEmpty(config) && config.StartsWith("RGB("))
                {
                    int lastParen = config.IndexOf(')');
                    if (lastParen > 4)
                    {
                        string[] rgbs = config.Substring(4, lastParen - 4).Split(',');

                        if (rgbs.Length >= 3)
                        {
                            byte r, g, b;
                            if (byte.TryParse(rgbs[0], out r) &&
                                byte.TryParse(rgbs[1], out g) &&
                                byte.TryParse(rgbs[2], out b))
                            {
                                return Color.FromRgb(r, g, b);
                            }
                        }
                    }
                }
                return Colors.DarkRed;
            }

            set
            {
                WriteSettings(value, GetColumnOffsets());
            }
        }

        // Parse a list of integer values out of a string that looks like
        // "RGB(255,0,0) 1, 5, 10, 80"
        static internal List<int> GetColumnOffsets()
        {
            var result = new List<int>();
            string settings = GuidesSettingsManager.GuidelinesConfiguration;
            if (String.IsNullOrEmpty(settings))
                return new List<int>();

            if (!settings.StartsWith("RGB("))
                return new List<int>();

            int lastParen = settings.IndexOf(')');
            if (lastParen <= 4)
                return new List<int>();

            string[] columns = settings.Substring(lastParen + 1).Split(',');

            int columnCount = 0;
            foreach (string columnText in columns)
            {
                int column = -1;
                // VS 2008 gallery extension didn't allow zero, so per user request ...
                if (int.TryParse(columnText, out column) && column >= 0)
                {
                    columnCount++;
                    result.Add(column);
                    if (columnCount >= _maxGuides)
                        break;
                }
            }
            return result;
        }

        // Delegate and Event to fire when settings change so that ColumnGuideAdornments
        // can update.  We need nothing special in this event since the settings manager
        // is statically available.
        //
        internal delegate void SettingsChangedHandler();
        static internal event SettingsChangedHandler SettingsChanged;

    }
}

```

大多数此代码创建并分析设置格式："RGB（>、int\<\<>、int\<>）int \<>、int \<>......"。  末尾的整数是需要列参考线的一个基于列的列。 列参考线扩展在单个设置值字符串中捕获其所有设置。

代码的某些部分值得突出显示。 以下代码行获取用于设置存储的 Visual Studio 托管包装器。 在大多数情况下，此摘要通过 Windows 注册表，但此 API 独立于存储机制。

```csharp
internal static SettingsManager VsManagedSettingsManager =
    new ShellSettingsManager(ServiceProvider.GlobalProvider);
```

Visual Studio 设置存储使用类别标识符和设置标识符来唯一标识所有设置：

```csharp
private const string _collectionSettingsName = "Text Editor";
private const string _settingName = "Guides";
```

您不必用作`"Text Editor"`类别名称。 你可以选择任何你喜欢的东西。

前几个函数是更改设置的入口点。 它们检查高级约束，如允许的最大参考线数。  然后，他们调用`WriteSettings`，它组成一个设置字符串并设置属性`GuideLinesConfiguration`。 设置此属性会将设置值保存到 Visual Studio 设置存储，并`SettingsChanged`触发事件以更新所有`ColumnGuideAdornment`对象，每个对象都与文本视图相关联。

有几个入口点函数，如`CanAddGuideline`，用于实现更改设置的命令。 当 Visual Studio 显示菜单时，它会查询命令实现以查看该命令当前是否启用、名称是什么，等等。  下面您将看到如何连接这些入口点以执行命令实现。 有关命令的详细信息，请参阅[扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。

## <a name="implement-the-columnguideadornment-class"></a>实现列指南修饰类
对于`ColumnGuideAdornment`每个可以具有修饰的文本视图，将实例化该类。 此类侦听有关视图更改或设置更改的事件，以及根据需要更新或重绘列参考线的事件。

将*ColumnGuideAdornment.cs*的内容替换为以下代码（如下所述）：

```csharp
using System;
using System.Windows.Media;
using Microsoft.VisualStudio.Text.Editor;
using System.Collections.Generic;
using System.Windows.Shapes;
using Microsoft.VisualStudio.Text.Formatting;
using System.Windows;

namespace ColumnGuides
{
    /// <summary>
    /// Adornment class, one instance per text view that draws a guides on the viewport
    /// </summary>
    internal sealed class ColumnGuideAdornment
    {
        private const double _lineThickness = 1.0;
        private IList<Line> _guidelines;
        private IWpfTextView _view;
        private double _baseIndentation;
        private double _columnWidth;

        /// <summary>
        /// Creates editor column guidelines
        /// </summary>
        /// <param name="view">The <see cref="IWpfTextView"/> upon
        /// which the adornment will be drawn</param>
        public ColumnGuideAdornment(IWpfTextView view)
        {
            _view = view;
            _guidelines = CreateGuidelines();
            GuidesSettingsManager.SettingsChanged +=
                new GuidesSettingsManager.SettingsChangedHandler(SettingsChanged);
            view.LayoutChanged +=
                new EventHandler<TextViewLayoutChangedEventArgs>(OnViewLayoutChanged);
            _view.Closed += new EventHandler(OnViewClosed);
        }

        void SettingsChanged()
        {
            _guidelines = CreateGuidelines();
            UpdatePositions();
            AddGuidelinesToAdornmentLayer();
        }

        void OnViewClosed(object sender, EventArgs e)
        {
            _view.LayoutChanged -= OnViewLayoutChanged;
            _view.Closed -= OnViewClosed;
            GuidesSettingsManager.SettingsChanged -= SettingsChanged;
        }

        private bool _firstLayoutDone;

        void OnViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
        {
            bool fUpdatePositions = false;

            IFormattedLineSource lineSource = _view.FormattedLineSource;
            if (lineSource == null)
            {
                return;
            }
            if (_columnWidth != lineSource.ColumnWidth)
            {
                _columnWidth = lineSource.ColumnWidth;
                fUpdatePositions = true;
            }
            if (_baseIndentation != lineSource.BaseIndentation)
            {
                _baseIndentation = lineSource.BaseIndentation;
                fUpdatePositions = true;
            }
            if (fUpdatePositions ||
                e.VerticalTranslation ||
                e.NewViewState.ViewportTop != e.OldViewState.ViewportTop ||
                e.NewViewState.ViewportBottom != e.OldViewState.ViewportBottom)
            {
                UpdatePositions();
            }
            if (!_firstLayoutDone)
            {
                AddGuidelinesToAdornmentLayer();
                _firstLayoutDone = true;
            }
        }

        private static IList<Line> CreateGuidelines()
        {
            Brush lineBrush = new SolidColorBrush(GuidesSettingsManager.GuidelinesColor);
            DoubleCollection dashArray = new DoubleCollection(new double[] { 1.0, 3.0 });
            IList<Line> result = new List<Line>();
            foreach (int column in GuidesSettingsManager.GetColumnOffsets())
            {
                Line line = new Line()
                {
                    // Use the DataContext slot as a cookie to hold the column
                    DataContext = column,
                    Stroke = lineBrush,
                    StrokeThickness = _lineThickness,
                    StrokeDashArray = dashArray
                };
                result.Add(line);
            }
            return result;
        }

        void UpdatePositions()
        {
            foreach (Line line in _guidelines)
            {
                int column = (int)line.DataContext;
                line.X2 = _baseIndentation + 0.5 + column * _columnWidth;
                line.X1 = line.X2;
                line.Y1 = _view.ViewportTop;
                line.Y2 = _view.ViewportBottom;
            }
        }

        void AddGuidelinesToAdornmentLayer()
        {
            // Grab a reference to the adornment layer that this adornment
            // should be added to
            // Must match exported name in ColumnGuideAdornmentTextViewCreationListener
            IAdornmentLayer adornmentLayer =
                _view.GetAdornmentLayer("ColumnGuideAdornment");
            if (adornmentLayer == null)
                return;
            adornmentLayer.RemoveAllAdornments();
            // Add the guidelines to the adornment layer and make them relative
            // to the viewport
            foreach (UIElement element in _guidelines)
                adornmentLayer.AddAdornment(AdornmentPositioningBehavior.OwnerControlled,
                                            null, null, element, null);
        }
    }

}
```

此类的实例保留到关联的<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>`Line`对象和在视图上绘制的对象列表。

构造函数（在`ColumnGuideAdornmentTextViewCreationListener`Visual Studio 创建新视图时调用）创建列指南`Line`对象。  构造函数`SettingsChanged`还添加事件（在 中`GuidesSettingsManager`定义）和视图事件`LayoutChanged`和`Closed`的处理程序。

由于`LayoutChanged`视图中的多种更改（包括 Visual Studio 创建视图时），事件将触发。 处理程序`OnViewLayoutChanged`调用`AddGuidelinesToAdornmentLayer`以执行。 中`OnViewLayoutChanged`的代码确定是否需要根据更改（如字体大小更改、视图排水沟、水平滚动等）更新行位置。 中的`UpdatePositions`代码会导致引导行在字符之间或文本列之后绘制，该列位于文本行中指定的字符偏移量中。

每当设置更改时`SettingsChanged`，函数只需使用任何新`Line`设置重新创建所有对象。 设置行位置后，代码将从`Line``ColumnGuideAdornment`修饰图层中删除所有以前的对象并添加新对象。

## <a name="define-the-commands-menus-and-menu-placements"></a>定义命令、菜单和菜单位置
声明命令和菜单、在各种其他菜单上放置命令或菜单组以及挂接命令处理程序可能有很多。 本演练重点介绍命令在此扩展中的工作方式，但有关更深入的信息，请参阅[扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。

### <a name="introduction-to-the-code"></a>代码简介
"列参考线"扩展名显示声明属于一组命令（添加列、删除列、更改行颜色），然后将该组放在编辑器上下文菜单的子菜单上。  "列参考线"扩展名还会将命令添加到**主编辑**菜单中，但使其不可见，下面是一个常见模式。

命令实现有三个部分：ColumnGuideCommandsPackage.cs、列指南命令包.vsct 和ColumnGuideCommands.cs。 模板生成的代码在 **"工具"** 菜单上放置一个命令，该命令弹出一个对话框作为实现。 您可以查看如何在 *.vsct*和*ColumnGuideCommands.cs*文件中实现，因为它非常简单。 替换下面这些文件中的代码。

包代码包含 Visual Studio 发现扩展提供命令并找到将命令放置位置所需的样板声明。 当包初始化时，它会实例化命令实现类。 有关与命令相关的包的详细信息，请参阅[扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。

### <a name="a-common-commands-pattern"></a>通用命令模式
列参考线扩展中的命令是可视化工作室中非常常见的模式的示例。 将相关命令放在组中，并将该组放在主菜单上，通常设置""`<CommandFlag>CommandWellOnly</CommandFlag>`使命令不可见。  在主菜单（如**Edit）** 上放置命令会为它们提供漂亮的名称（如**Edit.AddColumnGuide），** 这对于在**工具选项**中重新分配键绑定时查找命令非常有用。 当从**命令窗口**调用命令时，它对于完成也很有用。

然后，将命令组添加到上下文菜单或子菜单中，您希望用户使用这些命令。 Visual Studio`CommandWellOnly`仅视为主菜单的不可见标志。 将同一组命令放在上下文菜单或子菜单上时，这些命令是可见的。

作为常见模式的一部分，"列参考线"扩展将创建第二个组，该组包含单个子菜单。 子菜单依次包含具有四列引导命令的第一组。 保存子菜单的第二个组是放置在各种上下文菜单上的可重用资产，该资产在这些上下文菜单上放置了一个子菜单。

### <a name="the-vsct-file"></a>.vsct 文件
*.vsct*文件声明命令及其去向以及图标等。 将 *.vsct*文件的内容替换为以下代码（如下所述）：

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <!--  This is the file that defines the actual layout and type of the commands.
        It is divided in different sections (e.g. command definition, command
        placement, ...), with each defining a specific set of properties.
        See the comment before each section for more details about how to
        use it. -->

  <!--  The VSCT compiler (the tool that translates this file into the binary
        format that VisualStudio will consume) has the ability to run a preprocessor
        on the vsct file; this preprocessor is (usually) the C++ preprocessor, so
        it is possible to define includes and macros with the same syntax used
        in C++ files. Using this ability of the compiler here, we include some files
        defining some of the constants that we will use inside the file. -->

  <!--This is the file that defines the IDs for all the commands exposed by
      VisualStudio. -->
  <Extern href="stdidcmd.h"/>

  <!--This header contains the command ids for the menus provided by the shell. -->
  <Extern href="vsshlids.h"/>

  <!--The Commands section is where commands, menus, and menu groups are defined.
      This section uses a Guid to identify the package that provides the command
      defined inside it. -->
  <Commands package="guidColumnGuideCommandsPkg">
    <!-- Inside this section we have different sub-sections: one for the menus, another
    for the menu groups, one for the buttons (the actual commands), one for the combos
    and the last one for the bitmaps used. Each element is identified by a command id
    that is a unique pair of guid and numeric identifier; the guid part of the identifier
    is usually called "command set" and is used to group different command inside a
    logically related group; your package should define its own command set in order to
    avoid collisions with command ids defined by other packages. -->

    <!-- In this section you can define new menu groups. A menu group is a container for
         other menus or buttons (commands); from a visual point of view you can see the
         group as the part of a menu contained between two lines. The parent of a group
         must be a menu. -->
    <Groups>

      <!-- The main group is parented to the edit menu. All the buttons within the group
           have the "CommandWellOnly" flag, so they're actually invisible, but it means
           they get canonical names that begin with "Edit". Using placements, the group
           is also placed in the GuidesSubMenu group. -->
      <!-- The priority 0xB801 is chosen so it goes just after
           IDG_VS_EDIT_COMMANDWELL -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

      <!-- Group for holding the "Guidelines" sub-menu anchor (the item on the menu that
           drops the sub menu). The group is parented to
           the context menu for code windows. That takes care of most editors, but it's
           also placed in a couple of other windows using Placements -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_CTXT_CODEWIN" />
      </Group>

    </Groups>

    <Menus>
      <Menu guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" priority="0x1000"
            type="Menu">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup" />
        <Strings>
          <ButtonText>&Column Guides</ButtonText>
        </Strings>
      </Menu>
    </Menus>

    <!--Buttons section. -->
    <!--This section defines the elements the user can interact with, like a menu command or a button
        or combo box in a toolbar. -->
    <Buttons>
      <!--To define a menu group you have to specify its ID, the parent menu and its
          display priority.
          The command is visible and enabled by default. If you need to change the
          visibility, status, etc, you can use the CommandFlag node.
          You can add more than one CommandFlag node e.g.:
              <CommandFlag>DefaultInvisible</CommandFlag>
              <CommandFlag>DynamicVisibility</CommandFlag>
          If you do not want an image next to your command, remove the Icon node or
          set it to <Icon guid="guidOfficeIcon" id="msotcidNoIcon" /> -->

      <Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
              priority="0x0100" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicAddGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Add Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveColumnGuide"
              priority="0x0101" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicRemoveGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Remove Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidChooseGuideColor"
              priority="0x0103" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicChooseColor" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Column Guide &Color...</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveAllColumnGuides"
              priority="0x0102" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Remove A&ll Columns</ButtonText>
        </Strings>
      </Button>
    </Buttons>

    <!--The bitmaps section is used to define the bitmaps that are used for the
        commands.-->
    <Bitmaps>
      <!--  The bitmap id is defined in a way that is a little bit different from the
            others:
            the declaration starts with a guid for the bitmap strip, then there is the
            resource id of the bitmap strip containing the bitmaps and then there are
            the numeric ids of the elements used inside a button definition. An important
            aspect of this declaration is that the element id
            must be the actual index (1-based) of the bitmap inside the bitmap strip. -->
      <Bitmap guid="guidImages" href="Resources\ColumnGuideCommands.png"
              usedList="bmpPicAddGuide, bmpPicRemoveGuide, bmpPicChooseColor" />
    </Bitmaps>

  </Commands>

  <CommandPlacements>

    <!-- Define secondary placements for our groups -->

    <!-- Place the group containing the three commands in the sub-menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                      priority="0x0100">
      <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
    </CommandPlacement>

    <!-- The HTML editor context menu, for some reason, redefines its own groups
         so we need to place a copy of our context menu there too. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_HTML" />
    </CommandPlacement>

    <!-- The HTML context menu in Dev12 changed. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp_Dev12" id="IDMX_HTM_SOURCE_HTML_Dev12" />
    </CommandPlacement>

    <!-- Similarly for Script -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_SCRIPT" />
    </CommandPlacement>

    <!-- Similarly for ASPX  -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_ASPX" />
    </CommandPlacement>

    <!-- Similarly for the XAML editor context menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x0600">
      <Parent guid="guidXamlUiCmds" id="IDM_XAML_EDITOR" />
    </CommandPlacement>

  </CommandPlacements>

  <!-- This defines the identifiers and their values used above to index resources
       and specify commands. -->
  <Symbols>
    <!-- This is the package guid. -->
    <GuidSymbol name="guidColumnGuideCommandsPkg"
                value="{e914e5de-0851-4904-b361-1a3a9d449704}" />

    <!-- This is the guid used to group the menu commands together -->
    <GuidSymbol name="guidColumnGuidesCommandSet"
                value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
      <IDSymbol name="GuidesContextMenuGroup" value="0x1020" />
      <IDSymbol name="GuidesMenuItemsGroup" value="0x1021" />
      <IDSymbol name="GuidesSubMenu" value="0x1022" />
      <IDSymbol name="cmdidAddColumnGuide" value="0x0100" />
      <IDSymbol name="cmdidRemoveColumnGuide" value="0x0101" />
      <IDSymbol name="cmdidChooseGuideColor" value="0x0102" />
      <IDSymbol name="cmdidRemoveAllColumnGuides" value="0x0103" />
    </GuidSymbol>

    <GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
      <IDSymbol name="bmpPicAddGuide" value="1" />
      <IDSymbol name="bmpPicRemoveGuide" value="2" />
      <IDSymbol name="bmpPicChooseColor" value="3" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp_Dev12"
                value="{78F03954-2FB8-4087-8CE7-59D71710B3BB}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML_Dev12" value="0x1" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp" value="{d7e8c5e1-bdb8-11d0-9c88-0000f8040a53}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML" value="0x33" />
      <IDSymbol name="IDMX_HTM_SOURCE_SCRIPT" value="0x34" />
      <IDSymbol name="IDMX_HTM_SOURCE_ASPX" value="0x35" />
    </GuidSymbol>

    <GuidSymbol name="guidXamlUiCmds" value="{4c87b692-1202-46aa-b64c-ef01faec53da}">
      <IDSymbol name="IDM_XAML_EDITOR" value="0x103" />
    </GuidSymbol>
  </Symbols>

</CommandTable>

```

**GUIDS**. 对于 Visual Studio 查找命令处理程序并调用它们，您需要确保*在ColumnGuideCommandsPackage.cs*文件中声明的包 GUID（从项目项模板生成）与 *.vsct*文件中声明的包 GUID（从上面复制）匹配。 如果重复使用此示例代码，则应确保具有不同的 GUID，以便不与可能复制此代码的任何其他人发生冲突。

在*ColumnGuideCommandsPackage.cs*中查找此行，并在引号之间复制 GUID：

```csharp
public const string PackageGuidString = "ef726849-5447-4f73-8de5-01b9e930f7cd";
```

然后，将 GUID 粘贴到 *.vsct*文件中，以便在`Symbols`声明中具有以下行：

```xml
<GuidSymbol name="guidColumnGuideCommandsPkg"
            value="{ef726849-5447-4f73-8de5-01b9e930f7cd}" />
```

命令集的 GUID 和位图图像文件对于扩展也是唯一的：

```xml
<GuidSymbol name="guidColumnGuidesCommandSet"
            value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
<GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
```

但是，在本演练中，您不需要更改命令集和位图图像 GUID 即可使代码正常工作。 命令集 GUID 需要匹配*ColumnGuideCommands.cs*文件中的声明，但您也替换该文件的内容;因此，GUID 将匹配。

*.vsct*文件中的其他 GUID 标识将列指南命令添加到的预先存在的菜单，因此它们永远不会更改。

**文件部分**。 *.vsct*有三个外部部分：命令、位置和符号。 命令部分定义图标的命令组、菜单、按钮或菜单项以及位图。 放置部分声明组在菜单上或将其他放置位置转到预先存在的菜单的位置。 符号部分声明*在 .vsct*文件的其他位置使用的标识符，这使得 *.vsct*代码比随处都有 GUID 和十六进制数字更具可读性。

**命令部分，组定义**。 命令部分首先定义命令组。 命令组是您在菜单中看到的命令，这些命令带有分隔组的轻微灰色线条。 组还可以填充整个子菜单，如本示例所示，在这种情况下，您看不到灰色分隔线。 *.vsct*文件声明两个组，`GuidesMenuItemsGroup`一个组是父级`IDM_VS_MENU_EDIT`的（主**编辑**菜单）和`GuidesContextMenuGroup`父级组`IDM_VS_CTXT_CODEWIN`（代码编辑器的上下文菜单）。

第二组声明具有`0x0600`优先级：

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
```

其想法是将列参考线子菜单放在向其添加子菜单组的任何上下文菜单的末尾。 但是，您不应假定您最了解，并且使用`0xFFFF`的优先级强制子菜单始终为最后。 您必须尝试该数字，以查看子菜单位于放置该菜单的上下文菜单上的位置。 在这种情况下，`0x0600`足够高，可以尽可能将其放在菜单的末尾，但它为其他人留出空间来设计其扩展，使其低于列参考线扩展名（如果需要）。

**命令部分，菜单定义**。 接下来，命令部分定义子菜单，该子`GuidesSubMenu`菜单为 父菜单`GuidesContextMenuGroup`。 是`GuidesContextMenuGroup`添加到所有相关上下文菜单的组。 在放置部分中，代码将组在此子菜单上放置带有四列指南命令的组。

**命令部分，按钮定义**。 然后，命令部分定义菜单项或作为四列参考线命令的按钮。 `CommandWellOnly`，上面讨论，意味着命令是不可见的，当放置在主菜单上。 菜单项按钮声明的两个（添加指南和删除指南）也有一个`AllowParams`标志：

```xml
<CommandFlag>AllowParams</CommandFlag>
```

此标志启用在 Visual Studio 调用命令处理程序时接收参数的命令，以及具有主菜单位置的命令。  如果用户从命令窗口运行该命令，则参数将传递给事件参数中的命令处理程序。

**命令部分，位图定义**。 最后，命令部分声明用于命令的位图或图标。 本节是一个简单的声明，用于标识项目资源并列出已使用的图标的一个基于一个索引。 *.vsct*文件的符号部分声明用作索引的标识符的值。 本演练使用添加到项目的自定义命令项模板提供的位图条。

**放置部分**. 命令节后是放置部分。 第一个代码将上面讨论的第一组添加到出现命令的子菜单中，该组将四列引导命令保留到：

```xml
<CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                  priority="0x0100">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
</CommandPlacement>
```

所有其他位置将`GuidesContextMenuGroup`（包含`GuidesSubMenu`） 添加到其他编辑器上下文菜单。 当代码声明 时`GuidesContextMenuGroup`，它被父级声明到代码编辑器的上下文菜单。 这就是为什么您看不到代码编辑器上下文菜单的位置。

**符号部分**. 如上所述，符号部分声明*在 .vsct*文件的其他位置使用的标识符，这使得 *.vsct*代码比随处都有 GUID 和十六进制数字更具可读性。 本节的要点是包 GUID 必须同意包类中的声明。 而且，命令集 GUID 必须同意命令实现类中的声明。

## <a name="implement-the-commands"></a>实现命令
*ColumnGuideCommands.cs*文件实现命令并挂接处理程序。 当 Visual Studio 加载包并初始化包时，包反过来会`Initialize`调用命令实现类。 命令初始化只需实例化类，构造函数将连接所有命令处理程序。

将*ColumnGuideCommands.cs*文件的内容替换为以下代码（如下所述）：

```csharp
using System;
using System.ComponentModel.Design;
using System.Globalization;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;
using Microsoft.VisualStudio.TextManager.Interop;
using Microsoft.VisualStudio.Text.Editor;
using Microsoft.VisualStudio;

namespace ColumnGuides
{
    /// <summary>
    /// Command handler
    /// </summary>
    internal sealed class ColumnGuideCommands
    {

        const int cmdidAddColumnGuide = 0x0100;
        const int cmdidRemoveColumnGuide = 0x0101;
        const int cmdidChooseGuideColor = 0x0102;
        const int cmdidRemoveAllColumnGuides = 0x0103;

        /// <summary>
        /// Command menu group (command set GUID).
        /// </summary>
        static readonly Guid CommandSet =
            new Guid("c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e");

        /// <summary>
        /// VS Package that provides this command, not null.
        /// </summary>
        private readonly Package package;

        OleMenuCommand _addGuidelineCommand;
        OleMenuCommand _removeGuidelineCommand;

        /// <summary>
        /// Initializes the singleton instance of the command.
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        public static void Initialize(Package package)
        {
            Instance = new ColumnGuideCommands(package);
        }

        /// <summary>
        /// Gets the instance of the command.
        /// </summary>
        public static ColumnGuideCommands Instance
        {
            get;
            private set;
        }

        /// <summary>
        /// Initializes a new instance of the <see cref="ColumnGuideCommands"/> class.
        /// Adds our command handlers for menu (commands must exist in the command
        /// table file)
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        private ColumnGuideCommands(Package package)
        {
            if (package == null)
            {
                throw new ArgumentNullException("package");
            }

            this.package = package;

            // Add our command handlers for menu (commands must exist in the .vsct file)

            OleMenuCommandService commandService =
                this.ServiceProvider.GetService(typeof(IMenuCommandService))
                    as OleMenuCommandService;
            if (commandService != null)
            {
                // Add guide
                _addGuidelineCommand =
                    new OleMenuCommand(AddColumnGuideExecuted, null,
                                       AddColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidAddColumnGuide));
                _addGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_addGuidelineCommand);
                // Remove guide
                _removeGuidelineCommand =
                    new OleMenuCommand(RemoveColumnGuideExecuted, null,
                                       RemoveColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidRemoveColumnGuide));
                _removeGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_removeGuidelineCommand);
                // Choose color
                commandService.AddCommand(
                    new MenuCommand(ChooseGuideColorExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidChooseGuideColor)));
                // Remove all
                commandService.AddCommand(
                    new MenuCommand(RemoveAllGuidelinesExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidRemoveAllColumnGuides)));
            }
        }

        /// <summary>
        /// Gets the service provider from the owner package.
        /// </summary>
        private IServiceProvider ServiceProvider
        {
            get
            {
                return this.package;
            }
        }

        private void AddColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _addGuidelineCommand.Enabled =
                GuidesSettingsManager.CanAddGuideline(currentColumn);
        }

        private void RemoveColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _removeGuidelineCommand.Enabled =
                GuidesSettingsManager.CanRemoveGuideline(currentColumn);
        }

        private int GetCurrentEditorColumn()
        {
            IVsTextView view = GetActiveTextView();
            if (view == null)
            {
                return -1;
            }

            try
            {
                IWpfTextView textView = GetTextViewFromVsTextView(view);
                int column = GetCaretColumn(textView);

                // Note: GetCaretColumn returns 0-based positions. Guidelines are 1-based
                // positions.
                // However, do not subtract one here since the caret is positioned to the
                // left of
                // the given column and the guidelines are positioned to the right. We
                // want the
                // guideline to line up with the current caret position. e.g. When the
                // caret is
                // at position 1 (zero-based), the status bar says column 2. We want to
                // add a
                // guideline for column 1 since that will place the guideline where the
                // caret is.
                return column;
            }
            catch (InvalidOperationException)
            {
                return -1;
            }
        }

        /// <summary>
        /// Find the active text view (if any) in the active document.
        /// </summary>
        /// <returns>The IVsTextView of the active view, or null if there is no active
        /// document or the
        /// active view in the active document is not a text view.</returns>
        private IVsTextView GetActiveTextView()
        {
            IVsMonitorSelection selection =
                this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
                                                    as IVsMonitorSelection;
            object frameObj = null;
            ErrorHandler.ThrowOnFailure(
                selection.GetCurrentElementValue(
                    (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame, out frameObj));

            IVsWindowFrame frame = frameObj as IVsWindowFrame;
            if (frame == null)
            {
                return null;
            }

            return GetActiveView(frame);
        }

        private static IVsTextView GetActiveView(IVsWindowFrame windowFrame)
        {
            if (windowFrame == null)
            {
                throw new ArgumentException("windowFrame");
            }

            object pvar;
            ErrorHandler.ThrowOnFailure(
                windowFrame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView, out pvar));

            IVsTextView textView = pvar as IVsTextView;
            if (textView == null)
            {
                IVsCodeWindow codeWin = pvar as IVsCodeWindow;
                if (codeWin != null)
                {
                    ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
                }
            }
            return textView;
        }

        private static IWpfTextView GetTextViewFromVsTextView(IVsTextView view)
        {

            if (view == null)
            {
                throw new ArgumentNullException("view");
            }

            IVsUserData userData = view as IVsUserData;
            if (userData == null)
            {
                throw new InvalidOperationException();
            }

            object objTextViewHost;
            if (VSConstants.S_OK
                   != userData.GetData(Microsoft.VisualStudio
                                                .Editor
                                                .DefGuidList.guidIWpfTextViewHost,
                                       out objTextViewHost))
            {
                throw new InvalidOperationException();
            }

            IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
            if (textViewHost == null)
            {
                throw new InvalidOperationException();
            }

            return textViewHost.TextView;
        }

        /// <summary>
        /// Given an IWpfTextView, find the position of the caret and report its column
        /// number. The column number is 0-based
        /// </summary>
        /// <param name="textView">The text view containing the caret</param>
        /// <returns>The column number of the caret's position. When the caret is at the
        /// leftmost column, the return value is zero.</returns>
        private static int GetCaretColumn(IWpfTextView textView)
        {
            // This is the code the editor uses to populate the status bar.
            Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
                textView.Caret.ContainingTextViewLine;
            double columnWidth = textView.FormattedLineSource.ColumnWidth;
            return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                       / columnWidth));
        }

        /// <summary>
        /// Determine the applicable column number for an add or remove command.
        /// The column is parsed from command arguments, if present. Otherwise
        /// the current position of the caret is used to determine the column.
        /// </summary>
        /// <param name="e">Event args passed to the command handler.</param>
        /// <returns>The column number. May be negative to indicate the column number is
        /// unavailable.</returns>
        /// <exception cref="ArgumentException">The column number parsed from event args
        /// was not a valid integer.</exception>
        private int GetApplicableColumn(EventArgs e)
        {
            var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
            if (!string.IsNullOrEmpty(inValue))
            {
                int column;
                if (!int.TryParse(inValue, out column) || column < 0)
                    throw new ArgumentException("Invalid column");
                return column;
            }

            return GetCurrentEditorColumn();
        }

        /// <summary>
        /// This function is the callback used to execute a command when the a menu item
        /// is clicked. See the Initialize method to see how the menu item is associated
        /// to this function using the OleMenuCommandService service and the MenuCommand
        /// class.
        /// </summary>
        private void AddColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.AddGuideline(column);
            }
        }

        private void RemoveColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.RemoveGuideline(column);
            }
        }

        private void RemoveAllGuidelinesExecuted(object sender, EventArgs e)
        {
            GuidesSettingsManager.RemoveAllGuidelines();
        }

        private void ChooseGuideColorExecuted(object sender, EventArgs e)
        {
            System.Windows.Media.Color color = GuidesSettingsManager.GuidelinesColor;

            using (System.Windows.Forms.ColorDialog picker =
                new System.Windows.Forms.ColorDialog())
            {
                picker.Color = System.Drawing.Color.FromArgb(255, color.R, color.G,
                                                             color.B);
                if (picker.ShowDialog() == System.Windows.Forms.DialogResult.OK)
                {
                    GuidesSettingsManager.GuidelinesColor =
                        System.Windows.Media.Color.FromRgb(picker.Color.R,
                                                           picker.Color.G,
                                                           picker.Color.B);
                }
            }
        }

    }
}

```

**修复引用**。 此时缺少引用。 按解决方案资源管理器中的"参考"节点上的右指针按钮。 选择"**添加..."** 命令。 "**添加参考"** 对话框的右上角有一个搜索框。 输入"编辑器"（没有双引号）。 选择**Microsoft.VisualStudio.编辑器**项（您必须选中项目左侧的复选框，而不仅仅是选择该项目），然后选择 **"确定"** 以添加引用。

**初始化**。  当包类初始化时，它将调用`Initialize`命令实现类。 初始`ColumnGuideCommands`化实例化类，并将类实例和包引用保存在类成员中。

让我们看一下来自类构造函数的命令处理程序挂接：

```csharp
_addGuidelineCommand =
    new OleMenuCommand(AddColumnGuideExecuted, null,
                       AddColumnGuideBeforeQueryStatus,
                       new CommandID(ColumnGuideCommands.CommandSet,
                                     cmdidAddColumnGuide));

```

创建 一`OleMenuCommand`个 。 可视化工作室使用微软 Office 命令系统。 实例化时的关键参数`OleMenuCommand`是实现命令 （`AddColumnGuideExecuted`） 的函数，当 Visual Studio 显示具有命令 （`AddColumnGuideBeforeQueryStatus`） 和命令 ID 的菜单时要调用的函数。 Visual Studio 在菜单上显示命令之前调用查询状态函数，以便该命令可以使自身不可见或灰显，用于菜单的特定显示（例如，如果没有选择，则禁用**Copy）、** 更改其图标，甚至更改其名称（例如，从"添加内容到删除内容"）等。 命令 ID 必须与 *.vsct*文件中声明的命令 ID 匹配。 命令集和列参考线添加命令的字符串必须在 *.vsct*文件和*ColumnGuideCommands.cs*之间匹配。

以下行为用户通过命令窗口调用命令时提供帮助（如下所述）：

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";
```

 **查询状态**。 查询状态功能`AddColumnGuideBeforeQueryStatus`并`RemoveColumnGuideBeforeQueryStatus`检查某些设置（如参考线的最大数量或最大列），或者如果有要删除的列参考线。 如果条件合适，它们将启用命令。  查询状态函数需要高效，因为它们在每次 Visual Studio 显示菜单和菜单上的每个命令时都会运行。

 **添加列线指南执行函数**。 添加指南的有趣部分是找出当前编辑器视图和精心的位置。  首先，此函数调用`GetApplicableColumn`，它检查命令处理程序的事件参数中是否有用户提供的参数，如果没有，则函数检查编辑器的视图：

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

    return GetCurrentEditorColumn();
}

```

`GetCurrentEditorColumn`必须挖掘一点才能查看<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>代码。  如果遍通`GetActiveTextView`了`GetActiveView`，`GetTextViewFromVsTextView`可以看到如何执行此操作。 以下代码是抽象的相关代码，从当前选择开始，然后获取所选内容的帧，然后将帧的 DocView 作为 ，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>然后从 IVTextView 获取<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>， 然后获取视图主机，最后是 IWpfTextView：

```csharp
   IVsMonitorSelection selection =
       this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
           as IVsMonitorSelection;
   object frameObj = null;

ErrorHandler.ThrowOnFailure(selection.GetCurrentElementValue(
                                (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame,
                                out frameObj));

   IVsWindowFrame frame = frameObj as IVsWindowFrame;
   if (frame == null)
       <<do nothing>>;

...
   object pvar;
   ErrorHandler.ThrowOnFailure(frame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView,
                                                  out pvar));

   IVsTextView textView = pvar as IVsTextView;
   if (textView == null)
   {
       IVsCodeWindow codeWin = pvar as IVsCodeWindow;
       if (codeWin != null)
       {
           ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
       }
   }

...
   if (textView == null)
       <<do nothing>>

   IVsUserData userData = textView as IVsUserData;
   if (userData == null)
       <<do nothing>>

   object objTextViewHost;
   if (VSConstants.S_OK
           != userData.GetData(Microsoft.VisualStudio.Editor.DefGuidList
                                                            .guidIWpfTextViewHost,
                                out objTextViewHost))
   {
       <<do nothing>>
   }

   IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
   if (textViewHost == null)
       <<do nothing>>

   IWpfTextView textView = textViewHost.TextView;

```

获得 IWpfTextView 后，即可获取该选护符所在的列：

```csharp
private static int GetCaretColumn(IWpfTextView textView)
{
    // This is the code the editor uses to populate the status bar.
    Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
        textView.Caret.ContainingTextViewLine;
    double columnWidth = textView.FormattedLineSource.ColumnWidth;
    return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                / columnWidth));
}

```

当用户单击的当前列时，代码只需调用设置管理器来添加或删除列。 设置管理器触发所有`ColumnGuideAdornment`对象侦听的事件。 触发事件时，这些对象使用新的列指南设置更新其关联的文本视图。

## <a name="invoke-command-from-the-command-window"></a>从命令窗口调用命令
该列参考线示例使用户能够从命令窗口调用两个命令作为扩展形式。 如果使用 **"查看 &#124;其他窗口&#124;命令窗口"命令**，则可以看到命令窗口。 您可以通过输入"编辑"与命令窗口进行交互，并且在命令名称完成并提供参数 120 时，您有以下结果：

```csharp
> Edit.AddColumnGuide 120
>
```

启用此行为的示例部分位于 *.vsct*文件声明、`ColumnGuideCommands`连接命令处理程序时的类构造函数以及检查事件参数的命令处理程序实现中。

您在`<CommandFlag>CommandWellOnly</CommandFlag>`*.vsct*文件中看到""""""""""""""""""""**编辑**主菜单中的位置"，即使这些命令未显示在 **"编辑"** 菜单 UI 中。 将它们放在主**编辑**菜单上，可以给他们起像**Edit.AddColumnGuide**这样的名称。 保存四个命令的命令组声明将组直接放置在 **"编辑"** 菜单上：

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

```

按钮部分稍后声明命令`CommandWellOnly`，使其在主菜单上不可见，并声明它们与`AllowParams`：

```xml
<Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
        priority="0x0100" type="Button">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
  <Icon guid="guidImages" id="bmpPicAddGuide" />
  <CommandFlag>CommandWellOnly</CommandFlag>
  <CommandFlag>AllowParams</CommandFlag>

```

您看到命令处理程序在类构造函数中`ColumnGuideCommands`挂接代码提供了允许参数的说明：

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";

```

在检查当前`GetApplicableColumn`列的`OleMenuCmdEventArgs`编辑器视图之前，您看到函数检查值：

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

```

## <a name="try-your-extension"></a>尝试扩展
现在，您可以按**F5**执行列参考线扩展。 打开文本文件并使用编辑器的上下文菜单添加引导行、删除它们并更改其颜色。 单击文本（不是通过行末尾的空白）以添加列指南，或者编辑器将其添加到行的最后一列。 如果使用命令窗口并使用参数调用命令，则可以在任何地方添加列参考线。

如果要尝试不同的命令放置、更改名称、更改图标等，并且 Visual Studio 在菜单中显示最新代码时遇到任何问题，则可以重置正在调试的实验配置单元。 启动**Windows 开始菜单**并键入"重置"。 查找并运行该命令，**重置下一个可视化工作室实验实例**。 此命令清理所有扩展组件的实验注册表配置单元。 它不会清除组件中的设置，因此当您关闭 Visual Studio 的实验单元时，任何参考线都仍然存在，当您的代码在下次启动时读取设置存储时。

## <a name="finished-code-project"></a>已完成的代码项目
很快将有一个GitHub项目的视觉工作室扩展性示例，完成的项目将在那里。 本文将更新，以便发生此情况时指向该点。 已完成的示例项目可能具有不同的 guid，并且对于命令图标将有不同的位图条带。

您可以使用此可视化工作室库[扩展名](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)试用列指南功能的版本。

## <a name="see-also"></a>请参阅
- [编辑器内部](../extensibility/inside-the-editor.md)
- [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [向菜单添加子菜单](../extensibility/adding-a-submenu-to-a-menu.md)
- [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)
