---
title: 为控件启用编码的 UI 测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 5ef1188f-89dc-413d-801d-0efdaf9b0427
caps.latest.revision: 24
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 331dabfe8e219383fdc04187482b17b9048886a9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302572"
---
# <a name="enable-coded-ui-testing-of-your-controls"></a>启用控件的编码的 UI 测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果实现对编码的 UI 测试框架的支持，则可以更轻松地测试你的控件。 您能够以增量方式增加支持级别。 您可以先从支持录制、播放和属性验证开始。 在此基础上，您可以允许编码的 UI 测试生成器识别控件的自定义属性，并提供自定义类以便从生成的代码访问这些属性。 你还可以帮助编码的 UI 测试生成器，使之以一种与所录制操作的目的更为接近的方法来捕获操作。

 **本主题内容：**

1. [通过实现可访问性来支持录制和播放以及属性验证](../test/enable-coded-ui-testing-of-your-controls.md#recordandplayback)

2. [通过实现属性提供程序来支持自定义属性验证](../test/enable-coded-ui-testing-of-your-controls.md#customproprties)

3. [通过实现用于访问自定义属性的类来支持代码生成](../test/enable-coded-ui-testing-of-your-controls.md#codegeneration)

4. [通过实现操作筛选器来支持意向感知操作](../test/enable-coded-ui-testing-of-your-controls.md#intentawareactions)

   ![CUIT&#95;Full](../test/media/cuit-full.png "CUIT_Full")

## <a name="recordandplayback"></a>通过实现可访问性来支持录制和播放以及属性验证
 编码的 UI 测试生成器可捕获与它在录制期间所遇到的控件有关的信息，然后生成代码以重播该会话。 如果控件不支持辅助功能，则编码的 UI 测试生成器将使用屏幕坐标来捕获操作（例如，鼠标单击）。 播放测试时，生成的代码将在同一屏幕坐标释放这些鼠标单击操作。 在播放测试时，如果控件出现在屏幕上的其他位置，则生成的代码将无法对控件执行该操作。 如果在不同的屏幕配置下、在不同的环境中，或者在 UI 布局发生更改之后播放测试，则这可能会导致失败。

 ![CUIT&#95;RecordNoSupport](../test/media/cuit-recordnosupport.png "CUIT_RecordNoSupport")

 不过，如果实现辅助功能，则它在录制测试并生成代码时，将使用这一辅助功能来捕获有关控件的信息。 然后，当您运行测试时，生成的代码将针对您的控件重播这些事件，即使它位于用户界面中的其他位置。 测试作者还可以使用控件的基本属性创建断言。

 ![CUIT&#95;Record](../test/media/cuit-record.png "CUIT_Record")

### <a name="to-support-record-and-playback-property-validation-and-navigation-for-a-windows-forms-control"></a>支持录制和播放、属性验证以及 Windows 窗体控件的导航
 根据以下过程中的概述和 <xref:System.Windows.Forms.AccessibleObject> 中的详细介绍，为您的控件实现辅助功能。

 ![CUIT&#95;Accessible](../test/media/cuit-accessible.png "CUIT_Accessible")

1. 实现一个从 <xref:System.Windows.Forms.Control.ControlAccessibleObject> 派生的类，并重写 <xref:System.Windows.Forms.Control.AccessibilityObject%2A> 属性以便返回类的对象。

    ```csharp
    public partial class ChartControl : UserControl
    {
        // Overridden to return the custom AccessibleObject for the control.
        protected override AccessibleObject CreateAccessibilityInstance()
        {
            return new ChartControlAccessibleObject(this);
        }

        // Inner class ChartControlAccessibleObject represents accessible information
        // associated with the ChartControl and is used when recording tests.
        public class ChartControlAccessibleObject : ControlAccessibleObject
        {
            ChartControl myControl;
            public ChartControlAccessibleObject(ChartControl ctrl)
                : base(ctrl)
            {
                myControl = ctrl;
            }
        }
    }
    ```

2. 重写可访问对象的 <xref:System.Windows.Forms.AccessibleObject.Role%2A>、<xref:System.Windows.Forms.AccessibleObject.State%2A>、<xref:System.Windows.Forms.AccessibleObject.GetChild%2A> 属性和 <xref:System.Windows.Forms.AccessibleObject.GetChildCount%2A> 方法。

3. 实现子控件的另一个辅助功能对象并重写子控件的 <xref:System.Windows.Forms.Control.AccessibilityObject%2A> 属性，以便返回该辅助功能对象。

4. 重写子控件辅助功能对象的 <xref:System.Windows.Forms.AccessibleObject.Bounds%2A>、<xref:System.Windows.Forms.AccessibleObject.Name%2A>、<xref:System.Windows.Forms.AccessibleObject.Parent%2A>、<xref:System.Windows.Forms.AccessibleObject.Role%2A>、<xref:System.Windows.Forms.AccessibleObject.State%2A>、<xref:System.Windows.Forms.AccessibleObject.Navigate%2A> 和 <xref:System.Windows.Forms.AccessibleObject.Select%2A> 属性及方法。

> [!NOTE]
> 本主题在此过程中从 <xref:System.Windows.Forms.AccessibleObject> 辅助功能示例开始，然后在此基础上完成剩余过程。 如果要创建辅助功能示例的可行版本，请创建一个控制台应用程序，然后用示例代码替换 Program.cs 中的代码。 您需要添加对辅助功能、System.Drawing 和 System.Windows.Forms 的引用。 若要消除生成警告，应将可访问性的“嵌入互操作类型”更改为“False”。 可以将项目的输出类型从“控制台应用”更改为“Windows 应用”，这样就不会在运行应用时看到控制台窗口了。

## <a name="customproprties"></a>通过实现属性提供程序来支持自定义属性验证
 在实现对录制、播放和属性验证的基本支持后，您可以通过实现 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> 插件，使控件的自定义属性可供编码的 UI 测试使用。 例如，下面的过程将创建一个属性提供程序，该程序允许编码的 UI 测试访问图表控件 CurveLegend 子控件的 State 属性。

 ![CUIT&#95;CustomProps](../test/media/cuit-customprops.png "CUIT_CustomProps")

### <a name="to-support-custom-property-validation"></a>支持自定义属性验证
 ![CUIT&#95;Props](../test/media/cuit-props.png "CUIT_Props")

1. 重写曲线图例可访问对象的 <xref:System.Windows.Forms.AccessibleObject.Description%2A> 属性，以便传递说明字符串中丰富的属性值，并通过分号 (;) 与主说明分隔开来（如果要实现多个属性，则每个属性之间也相互分隔）。

    ```csharp
    public class CurveLegendAccessibleObject : AccessibleObject
    {
        // add the state property value to the description
        public override string Description
        {
            get
            {
                // Add “;” and the state value to the end
                // of the curve legend’s description
                return "CurveLegend; " + State.ToString();
            }
        }
    }
    ```

2. 通过创建一个类库项目并添加对辅助功能、Microsoft.VisualStudio.TestTools.UITesting、Microsoft.VisualStudio.TestTools.UITest.Common 和 Microsoft.VisualStudio.TestTools.Extension 的引用，为你的控件创建一个 UI 测试扩展包。 将可访问性的“嵌入互操作类型”更改为“False”。

3. 添加一个从 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> 派生的属性提供程序类。

    ```csharp
    using System;
    using System.Collections.Generic;
    using Accessibility;
    using Microsoft.VisualStudio.TestTools.UITesting;
    using Microsoft.VisualStudio.TestTools.UITest.Extension;
    using Microsoft.VisualStudio.TestTools.UITesting.WinControls;
    using Microsoft.VisualStudio.TestTools.UITest.Common;

    namespace ChartControlExtensionPackage
    {
        public class ChartControlPropertyProvider : UITestPropertyProvider
        {
        }
    }
    ```

4. 通过将属性名称和属性描述符放在 <xref:System.Collections.Generic.Dictionary%602> 中，实施此属性提供程序。

    ```csharp
    // Define a map of property descriptors for CurveLegend
    private static Dictionary<string, UITestPropertyDescriptor> curveLegendPropertiesMap = null;
    private static Dictionary<string, UITestPropertyDescriptor> CurveLegendPropertiesMap
    {
        get
        {
            if (curveLegendPropertiesMap == null)
            {
                UITestPropertyAttributes read =
                    UITestPropertyAttributes.Readable |
                    UITestPropertyAttributes.DoNotGenerateProperties;
                curveLegendPropertiesMap =
                    new Dictionary<string, UITestPropertyDescriptor>
                        (StringComparer.OrdinalIgnoreCase);
                curveLegendPropertiesMap.Add("State",
                    new UITestPropertyDescriptor(typeof(string), read));
            }
            return curveLegendPropertiesMap;
        }
    }

    // return the property descriptor
    public override UITestPropertyDescriptor GetPropertyDescriptor(UITestControl uiTestControl, string propertyName)
    {
        return CurveLegendPropertiesMap[propertyName];
    }

    // return the property names
    public override ICollection<string> GetPropertyNames(UITestControl uiTestControl)
    {
        if (uiTestControl.ControlType.NameEquals("Chart") || uiTestControl.ControlType.NameEquals("Text"))
        {
            // the keys of the property map are the collection of property names
            return CurveLegendPropertiesMap.Keys;
        }

        // this is not my control
        throw new NotSupportedException();
    }

    // Get the property value by parsing the accessible description
    public override object GetPropertyValue(UITestControl uiTestControl, string propertyName)
    {
        if (String.Equals(propertyName, "State", StringComparison.OrdinalIgnoreCase))
        {
            object[] native = uiTestControl.NativeElement as object[];
            IAccessible acc = native[0] as IAccessible;

            string[] descriptionTokens = acc.accDescription.Split(new char[] { ';' });
            return descriptionTokens[1];
        }

        // this is not my control
        throw new NotSupportedException();
    }
    ```

5. 重写 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A?displayProperty=fullName>，指明您的程序集为控件及其子控件提供特定于控件的支持。

    ```csharp
    public override int GetControlSupportLevel(UITestControl uiTestControl)
    {
        // For MSAA, check the control type
        if (string.Equals(uiTestControl.TechnologyName, "MSAA",
            StringComparison.OrdinalIgnoreCase) &&
            (uiTestControl.ControlType == "Chart"||uiTestControl.ControlType == "Text"))
        {
            return (int)ControlSupport.ControlSpecificSupport;
        }

        // This is not my control, so return NoSupport
        return (int)ControlSupport.NoSupport;
    }
    ```

6. 重写 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider?displayProperty=fullName> 的剩余抽象方法。

    ```csharp
    public override string[] GetPredefinedSearchProperties(Type specializedClass)
    {
        throw new NotImplementedException();
    }

    public override Type GetSpecializedClass(UITestControl uiTestControl)
    {
        throw new NotImplementedException();
    }

    public override Type GetPropertyNamesClassType(UITestControl uiTestControl)
    {
        throw new NotImplementedException();
    }

    public override void SetPropertyValue(UITestControl uiTestControl, string propertyName, object value)
    {
        throw new NotImplementedException();
    }

    public override string GetPropertyForAction(UITestControl uiTestControl, UITestAction action)
    {
        throw new NotImplementedException();
    }

    public override string[] GetPropertyForControlState(UITestControl uiTestControl, ControlStates uiState, out bool[] stateValues)
    {
        throw new NotImplementedException();
    }

    ```

7. 添加一个从 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> 派生的扩展包类。

    ```csharp
    using System;
    using Microsoft.VisualStudio.TestTools.UITesting;
    using Microsoft.VisualStudio.TestTools.UITest.Extension;
    using Microsoft.VisualStudio.TestTools.UITest.Common;

    namespace ChartControlExtensionPackage
    {
        internal class ChartControlExtensionPackage : UITestExtensionPackage
        {
        }
    }
    ```

8. 定义程序集的 `UITestExtensionPackage` 特性。

    ```csharp
    [assembly: Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage(
                    "ChartControlExtensionPackage",
                    typeof(ChartControlExtensionPackage.ChartControlExtensionPackage))]
    namespace ChartControlExtensionPackage
    {
       …
    ```

9. 在扩展包类中，重写 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A?displayProperty=fullName>，以便在请求属性提供程序时返回属性提供程序类。

    ```csharp
    internal class ChartControlExtensionPackage : UITestExtensionPackage
    {
        public override object GetService(Type serviceType)
        {
            if (serviceType == typeof(UITestPropertyProvider))
            {
                if (propertyProvider == null)
                {
                    propertyProvider = new ChartControlPropertyProvider();
                }
                return propertyProvider;
            }
            return null;
        }

        private UITestPropertyProvider propertyProvider = null;
    }
    ```

10. 重写 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> 的剩余抽象方法和属性。

    ```csharp

    public override void Dispose() { }

    public override string PackageDescription
    {
        get { return "Supports coded UI testing of ChartControl"; }
    }

    public override string PackageName
    {
        get { return "ChartControl Test Extension"; }
    }

    public override string PackageVendor
    {
        get { return "Microsoft (sample)"; }
    }

    public override Version PackageVersion
    {
        get { return new Version(1, 0); }
    }

    public override Version VSVersion
    {
        get { return new Version(10, 0); }
    }
    ```

11. 生成二进制文件，然后将其复制到 **%ProgramFiles%\Common\Microsoft Shared\VSTT\10.0\UITestExtensionPackages**。

> [!NOTE]
> 此扩展包将应用于类型为“Text”的所有控件。 如果测试同一类型的多个控件，则需要分别进行测试，并管理在录制测试时要部署哪些扩展包。

## <a name="codegeneration"></a>通过实现用于访问自定义属性的类来支持代码生成
 当编码的 UI 测试时生成器生成会话录制的代码时，它将使用 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl> 类来访问您的控件。

```csharp

      UITestControl uIAText = this.UIItemWindow.UIChartControlWindow.UIAText;
Assert.AreEqual(this.AssertMethod3ExpectedValues.UIATextState, uIAText.GetProperty("State").ToString());
```

 如果已实现一个属性提供程序来访问控件的自定义属性，则可以添加一个用于访问这些属性的专用化类，以便简化所生成的代码。

```csharp

      ControlLegend uIAText = this.UIItemWindow.UIChartControlWindow.UIAText;
Assert.AreEqual(this.AssertMethod3ExpectedValues.UIATextState, uIAText.State);
```

### <a name="to-add-a-specialized-class-to-access-your-control"></a>添加专用类以访问您的控件
 ![CUIT&#95;CodeGen](../test/media/cuit-codegen.png "CUIT_CodeGen")

1. 实现从 <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinControl> 派生的类，并将控件的类型添加到构造函数中的搜索属性集合。

    ```csharp
    public class CurveLegend:WinControl
    {
       public CurveLegend(UITestControl c) : base(c)
       {
          // The curve legend control is a “text” type of control
          SearchProperties.Add(
             UITestControl.PropertyNames.ControlType, "Text");
       }
    }
    ```

2. 实现控件的自定义属性，作为类的属性。

    ```csharp
    public virtual string State
    {
        get
        {
            return (string)GetProperty("State");
        }
    }
    ```

3. 重写属性提供程序的 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetSpecializedClass%2A?displayProperty=fullName> 方法，以便返回曲线图例子控件的新类的类型。

    ```csharp
    public override Type GetSpecializedClass(UITestControl uiTestControl)
    {
       if (uiTestControl.ControlType.NameEquals("Text"))
       {
          // This is text type of control. For my control,
          // that means it’s a curve legend control.
          return typeof(CurveLegend);
       }

       // this is not a curve legend control
       return null;
    }
    ```

4. 重写属性提供程序的 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetPropertyNamesClassType%2A> 方法，以便返回新类的 PropertyNames 方法的类型。

    ```csharp
    public override Type GetPropertyNamesClassType(UITestControl uiTestControl)
    {
        if (uiTestControl.ControlType.NameEquals("Text"))
        {
          // This is text type of control. For my control,
          // that means it’s a curve legend control.
            return typeof(CurveLegend.PropertyNames);
        }

        // this is not a curve legend control
        return null;
    }
    ```

## <a name="intentawareactions"></a>通过实现操作筛选器来支持意向感知操作
 当 Visual Studio 录制测试时，它会捕获鼠标和键盘事件。 但是，在某些情况下，在一系列鼠标和键盘事件中可能会丢失操作的目的。 例如，如果控件支持自动完成，则在其他环境中播放测试时，同一组鼠标和键盘事件可能会产生不同的值。 您可以添加一个操作筛选器插件，将一系列键盘和鼠标事件替换为单一操作。 这样一来，您就可以将结果为选择某一值的一系列鼠标和键盘事件替换为设置值的单一操作。 当从一个环境转到另一个环境时，这样可以保护编码的 UI 测试，使之不受自动完成差异的影响。

### <a name="to-support-intent-aware-actions"></a>支持目的感知操作
 ![CUIT&#95;Actions](../test/media/cuit-actions.png "CUIT_Actions")

1. Implement an action filter class that’s derived from [UITestActionFilter](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110)), overriding the properties [ApplyTimeout](/previous-versions/visualstudio/visual-studio-2012/dd984649%28v%3dvs.110%29), [Category](/previous-versions/visualstudio/visual-studio-2012/dd986905(v=vs.110)), [Enabled](/previous-versions/visualstudio/visual-studio-2012/dd985633(v=vs.110)), [FilterType](/previous-versions/visualstudio/visual-studio-2012/dd778726(v=vs.110)), [Group](/previous-versions/visualstudio/visual-studio-2012/dd779219(v=vs.110)) and [Name](/previous-versions/visualstudio/visual-studio-2012/dd998334(v=vs.110)).

    ```csharp
    internal class MyActionFilter : UITestActionFilter
    {
       // If the user actions we are aggregating exceeds the time allowed,
       // this filter is not applied. (The timeout is configured when the
       // test is run.)
       public override bool ApplyTimeout
       {
          get { return true; }
       }

       // Gets the category of this filter. Categories of filters
       // are applied in priority order.
       public override UITestActionFilterCategory Category
       {
          get { return UITestActionFilterCategory.PostSimpleToCompoundActionConversion; }
       }

       public override bool Enabled
       {
          get { return true; }
       }

       public override UITestActionFilterType FilterType
       {
          // This action filter operates on a single action
          get { return UITestActionFilterType.Unary; }
       }

       // Gets the name of the group to which this filter belongs.
       // A group can be enabled/disabled using configuration file.
       public override string Group
       {
          get { return "ChartControlActionFilters"; }
       }

       // Gets the name of this filter.
       public override string Name
       {
          get { return "Convert Double-Click to Single-Click"; }
       }
    ```

2. 重写 `UITestActionFilter.ProcessRule`。 此示例将一个双击操作替换成了单击操作。

    ```csharp
    public override bool ProcessRule(IUITestActionStack actionStack)
    {
        if (actionStack.Count > 0)
        {
            MouseAction lastAction = actionStack.Peek() as MouseAction;
            if (lastAction != null)
            {
                if (lastAction.UIElement.ControlTypeName.Equals(
                     ControlType.Text.ToString(),
                     StringComparison.OrdinalIgnoreCase))
                {
                    if(lastAction.ActionType == MouseActionType.DoubleClick)
                    {
                        // Convert to single click
                        lastAction.ActionType = MouseActionType.Click;
                    }
                }
            }
        }
        // Do not stop aggregation
        return false;
    }
    ```

3. 将操作筛选器添加到扩展包的 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> 方法。

    ```csharp
    public override object GetService(Type serviceType)
    {
       if (serviceType == typeof(UITestPropertyProvider))
       {
          if (propertyProvider == null)
          {
             propertyProvider = new PropertyProvider();
          }
          return propertyProvider;
       }
       else if (serviceType == typeof(UITestActionFilter))
       {
          if (actionFilter == null)
          {
             actionFilter = new RadGridViewActionFilter();
          }
          return actionFilter;
       }
       return null;
    }
    ```

4. 生成二进制文件，然后将其复制到 %ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages。

> [!NOTE]
> 操作筛选器不依赖于辅助功能实现或属性提供程序。

## <a name="debug-your-property-provider-or-action-filter"></a>调试您的属性提供程序或操作筛选器
 您的属性提供程序和操作筛选器在一个扩展包中实现，此扩展包在一个与应用程序分离的进程中，由编码的 UI 测试生成器来加载和运行。

#### <a name="to-debug-your-property-provider-or-action-filter"></a>调试属性提供程序或操作筛选器

1. 生成扩展包的调试版本，然后将 .dll 和 .pdb 文件复制到 %ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages。

2. 运行您的应用程序（不在调试器中）。

3. 运行编码的 UI 测试生成器。

     `codedUITestBuilder.exe  /standalone`

4. 将调试器附加到 codedUITestBuilder 进程。

5. 在代码中设置断点。

6. 在编码的 UI 测试生成器中，创建断言以执行您的属性提供程序，并录制操作以运用您的操作筛选器。

## <a name="external-resources"></a>外部资源

### <a name="guidance"></a>指导
 [使用 Visual Studio 2012 对连续交付进行测试 - 第 2 章：单元测试：测试内部](https://go.microsoft.com/fwlink/?LinkID=255188)

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.AccessibleObject>
- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
