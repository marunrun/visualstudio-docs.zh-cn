---
title: 演练：使用 c + + 创建 SDK |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15fa0714097efda31b52f1d389d3a26cf581e506
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905007"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>演练：使用 c + + 创建 SDK
本演练演示如何创建本机 c + + 数学库 SDK，将 SDK 打包为 Visual Studio 扩展（VSIX），并使用它创建应用。 本演练分为以下几个步骤：

- [创建本机和 Windows 运行时库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [创建 NativeMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [创建使用类库的示例应用程序](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>必备条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>创建本机和 Windows 运行时库

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板列表中，展开 " **Visual C++**  >  **Windows 通用**"，然后选择 " **DLL （Windows 通用应用）** " 模板。 在 "**名称**" 框中，指定 `NativeMath` ，然后选择 "**确定"** 按钮。

3. 更新*NativeMath*以匹配以下代码。

     [!code-cpp[CreatingAnSDKUsingCpp#1](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_1.h)]

4. 更新*NativeMath*以匹配以下代码：

     [!code-cpp[CreatingAnSDKUsingCpp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_2.cpp)]

5. 在**解决方案资源管理器**中，打开**解决方案 "NativeMath"** 的快捷菜单，然后选择 "**添加**  >  **新项目**"。

6. 在模板列表中，展开 " **Visual C++**"，然后选择 " **Windows 运行时组件**" 模板。 在 "**名称**" 框中，指定 `NativeMathWRT` ，然后选择 "**确定"** 按钮。

7. 更新*Class1*以匹配以下代码：

     [!code-cpp[CreatingAnSDKUsingCpp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_3.h)]

8. 更新*Class1*以匹配以下代码：

     [!code-cpp[CreatingAnSDKUsingCpp#4](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_4.cpp)]

9. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a>创建 NativeMathVSIX 扩展项目

1. 在**解决方案资源管理器**中，打开**解决方案 "NativeMath"** 的快捷菜单，然后选择 "**添加**  >  **新项目**"。

2. 在模板列表中，展开 " **Visual c #**  >  **扩展性**"，然后选择 " **VSIX 项目**"。 在 "**名称**" 框中，指定**NativeMathVSIX**，然后选择 "**确定"** 按钮。

3. 在**解决方案资源管理器**中，打开**source.extension.vsixmanifest**的快捷菜单，然后选择 "**查看代码**"。

4. 使用以下 XML 替换现有的 XML。

    [!code-xml[CreatingAnSDKUsingCpp#6](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]

5. 在**解决方案资源管理器**中，打开**NativeMathVSIX**项目的快捷菜单，然后选择 "**添加**  >  **新项**"。

6. 在**Visual c # 项**列表中，展开 "**数据**"，然后选择 " **XML 文件**"。 在 "**名称**" 框中，指定 `SDKManifest.xml` ，然后选择 "**确定"** 按钮。

7. 使用此 XML 替换文件的内容：

     [!code-xml[CreatingAnSDKUsingCpp#5](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_5.xml)]

8. 在**解决方案资源管理器**的**NativeMathVSIX**项目下，创建以下文件夹结构：

    ```xml
    \DesignTime
          \CommonConfiguration
                \Neutral
                      \Include
          \Debug
                \x86
    \Redist
          \Debug
                \x86
    \References
          \CommonConfiguration
                \Neutral
    ```

9. 在**解决方案资源管理器**中，打开**解决方案 "NativeMath"** 的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**"。

10. 在 "**文件资源管理器**" 中，复制 *$SolutionRoot $ \NativeMath\NativeMath.h*，然后在**解决方案资源管理器**中的 " **NativeMathVSIX** " 项目下，将其粘贴到 *$SolutionRoot $ \NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include \\ *文件夹中。

     复制 *$SolutionRoot $ \Debug\NativeMath\NativeMath.lib*，然后将其粘贴到 *$SolutionRoot $ \NativeMathVSIX\DesignTime\Debug\x86 \\ *文件夹中。

     将 *$SolutionRoot $\Debug\NativeMath\NativeMath.dll*复制并粘贴到 *$SolutionRoot $ \NativeMathVSIX\Redist\Debug\x86 \\ *文件夹中。

     将 *$SolutionRoot $\Debug\NativeMathWRT\NativeMathWRT.dll*复制并粘贴到 *$SolutionRoot $ \NativeMathVSIX\Redist\Debug\x86*文件夹中。
     复制 *$SolutionRoot $ \Debug\NativeMathWRT\NativeMathWRT.winmd*并将其粘贴到 *$SolutionRoot $ \NativeMathVSIX\References\CommonConfiguration\Neutral*文件夹中。

     复制 *$SolutionRoot $ \Debug\NativeMathWRT\NativeMathWRT.pri*并将其粘贴到 *$SolutionRoot $ \NativeMathVSIX\References\CommonConfiguration\Neutral*文件夹中。

11. 在 " *$SolutionRoot $ \NativeMathVSIX\DesignTime\Debug\x86 \\ * " 文件夹中，创建一个名为*NativeMathSDK*的文本文件，然后在其中粘贴以下内容：

    [!code-xml[CreatingAnSDKUsingCpp#7](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]

12. 在菜单栏上，选择 "**查看**  >  **其他窗口**  >  **属性" 窗口**（键盘：选择**F4**键）。

13. 在**解决方案资源管理器**中，选择**NativeMathWRT**文件。 在 "**属性**" 窗口中，将 "**生成操作**" 属性更改为 "**内容**"，然后将 "**包括在 VSIX 中**" 属性更改为**True**。

     为**NativeMath**文件重复此过程。

     为**NativeMathWRT**文件重复此过程。

     为**NativeMath**文件重复此过程。

     为**NativeMathSDK**文件重复此过程。

14. 在**解决方案资源管理器**中，选择**NativeMath**文件。 在 "**属性**" 窗口中，将 "**包括在 VSIX 中**" 属性更改为**True**。

     对**NativeMath.dll**文件重复此过程。

     对**NativeMathWRT.dll**文件重复此过程。

     对**SDKManifest.xml**文件重复此过程。

15. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

16. 在**解决方案资源管理器**中，打开**NativeMathVSIX**项目的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**"。

17. 在**文件资源管理器**中，导航到 *$SolutionRoot $ \NativeMathVSIX\bin\Debug*文件夹，然后运行*NativeMathVSIX*以开始安装。

18. 选择 "**安装**" 按钮，等待安装完成，然后打开 Visual Studio。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>创建使用类库的示例应用程序

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板列表中，展开 " **Visual C++**  >  **Windows 通用**"，然后选择 "**空白应用**"。 在 "**名称**" 框中，指定**NativeMathSDKSample**，然后选择 "**确定"** 按钮。

3. 在**解决方案资源管理器**中，打开**NativeMathSDKSample**项目的快捷菜单，然后选择 "**添加**  >  **引用**"。

4. 在 "**添加引用**" 对话框的 "引用类型" 列表中，展开 "**通用 Windows**"，然后选择 "**扩展**"。 最后，选中 "**本机数学 SDK** " 复选框，然后选择 "**确定"** 按钮。

5. 显示 NativeMathSDKSample 的项目属性。

    添加引用时，会应用在*NativeMathSDK*中定义的属性。 可以通过检查项目**配置属性**的 " **VC + + 目录**" 属性来验证是否已应用这些属性。

6. 在**解决方案资源管理器**中，打开**MainPage**，然后使用以下 xaml 替换其内容：

    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../extensibility/codesnippet/Xaml/walkthrough-creating-an-sdk-using-cpp_8.xaml)]

7. 更新*Mainpage*以匹配以下代码：

    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_9.h)]

8. 更新*MainPage*以匹配以下代码：

     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_10.cpp)]

9. 选择**F5**键以运行应用。

10. 在应用程序中，输入任意两个数字，选择一个操作，然后选择 **=** 按钮。

     显示正确的结果。

    本演练演示如何创建和使用扩展 SDK 来调入 [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] 库和非 [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] 库。

## <a name="next-steps"></a>后续步骤

## <a name="see-also"></a>另请参阅
- [演练：使用 c # 或 Visual Basic 创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
