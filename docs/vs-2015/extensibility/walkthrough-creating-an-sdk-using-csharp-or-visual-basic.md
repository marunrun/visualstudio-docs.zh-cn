---
title: 演练：使用C#或 VISUAL BASIC 创建 SDK |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a604e3500c0ea438c987c4cf07ded98a5e03dd61
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558203"
---
# <a name="walkthrough-creating-an-sdk-using-c-or-visual-basic"></a>演练：使用 C# 或 Visual Basic 创建 SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，你将学习如何使用视觉对象C#创建简单的数学库 sdk，然后将 SDK 打包为 Visual Studio 扩展（VSIX）。 你将完成以下过程：  
  
- [创建 SimpleMath Windows 运行时组件](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)  
  
- [创建 SimpleMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)  
  
- [创建使用类库的示例应用程序](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)  
  
## <a name="prerequisites"></a>必备条件  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="createClassLibrary"></a>创建 SimpleMath Windows 运行时组件  
  
1. 在菜单栏上，依次选择 "**文件**"、"**新建**"、"**新建项目**"。  
  
2. 在模板列表中，展开 "**视觉C#对象**" 或 " **Visual Basic**"，选择 " **Windows 应用商店**" 节点，然后选择 " **Windows 运行时组件**" 模板。  
  
3. 在 "**名称**" 框中，指定**SimpleMath**，然后选择 "**确定"** 按钮。  
  
4. 在**解决方案资源管理器**中，打开**SimpleMath**项目节点的快捷菜单，然后选择 "**属性**"。  
  
5. 将**Class1.cs**重命名为**Arithmetic.cs** ，并对其进行更新以匹配以下代码：  
  
     [!code-csharp[CreatingAnSDKUsingWinRT#3](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmath/arithmetic.cs#3)]
     [!code-vb[CreatingAnSDKUsingWinRT#3](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmath/arithmetic.vb#3)]  
  
6. 在**解决方案资源管理器**中，打开**解决方案 "SimpleMath"** 节点的快捷菜单，然后选择 " **Configuration Manager**"。  
  
     此时将打开 " **Configuration Manager** " 对话框。  
  
7. 在 "**活动解决方案配置**" 列表中，选择 "**发布**"。  
  
8. 在 "**配置**" 列中，验证 " **SimpleMath** " 行是否设置为 "**发布**"，然后选择 "**关闭**" 按钮接受更改。  
  
    > [!IMPORTANT]
    > SimpleMath 组件的 SDK 只包含一个配置。 此配置必须是发布版本，否则使用组件的应用不会通过[!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)]的认证。  
  
9. 在**解决方案资源管理器**中，打开**SimpleMath**项目节点的快捷菜单，然后选择 "**生成**"。  
  
## <a name="createVSIX"></a>创建 SimpleMathVSIX 扩展项目  
  
1. 在**解决方案 "SimpleMath"** 节点的快捷菜单上，选择 "**添加**"、"**新建项目**"。  
  
2. 在模板列表中，展开 "**视觉C#对象**" 或 " **Visual Basic**"，选择 "**扩展性**" 节点，然后选择 " **VSIX 项目**" 模板。  
  
3. 在 "**名称**" 框中，指定**SimpleMathVSIX**，然后选择 "**确定"** 按钮。  
  
4. 在**解决方案资源管理器**中，选择**source.extension.vsixmanifest**项。  
  
5. 在菜单栏上，依次选择 **“视图”**、 **“代码”**。  
  
6. 将现有的 XML 替换为以下 XML：  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]
  
7. 在**解决方案资源管理器**中，选择 " **SimpleMathVSIX** " 项目。  
  
8. 在菜单栏上，依次选择 "**项目**"、"**添加新项**"。  
  
9. 在**常见项**列表中，展开 "**数据**"，然后选择 " **XML 文件**"。  
  
10. 在 "**名称**" 框中，指定 `SDKManifest.xml`，然后选择 "**添加**" 按钮。  
  
11. 在**解决方案资源管理器**中，打开 `SDKManifest.xml`的快捷菜单，选择 "**属性**"，然后将 "**包括在 VSIX 中**" 属性的值更改为 " **True**"。  
  
12. 用下列 XML 替换该文件的内容：  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmathvsix/sdkmanifest.xml#1)]
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmathvsix/sdkmanifest.xml#1)]  
  
13. 在**解决方案资源管理器**中，打开**SimpleMathVSIX**项目的快捷菜单，选择 "**添加**"，然后选择 "**新建文件夹**"。  
  
14. 将文件夹重命名为 `references`。  
  
15. 打开 "**引用**" 文件夹的快捷菜单，选择 "**添加**"，然后选择 "**新建文件夹**"。  
  
16. 将子文件夹重命名为 "`commonconfiguration`"，在其中创建子文件夹，并将子文件夹命名为 `neutral`。  
  
17. 重复前面的四个步骤，这次将第一个文件夹重命名为 `redist`。  
  
     该项目现在包含以下文件夹结构：  
  
    ```  
    references\commonconfiguration\neutral  
    redist\commonconfiguration\neutral  
    ```  
  
18. 在**解决方案资源管理器**中，打开**SimpleMath**项目的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**"。  
  
19. 在**文件资源管理器**中，导航到 bin\Release 文件夹，打开 SimpleMath 文件的快捷菜单，然后选择 "**复制**"。  
  
20. 在**解决方案资源管理器**中，将该文件粘贴到**SimpleMathVSIX**项目的 references\commonconfiguration\neutral 文件夹中。  
  
21. 重复上一步，将 SimpleMath 文件粘贴到**SimpleMathVSIX**项目中的 redist\commonconfiguration\neutral 文件夹。  
  
22. 在**解决方案资源管理器**中，选择 " **SimpleMath**"。  
  
23. 在菜单栏上，依次选择 "**视图**"、"**属性**" （键盘：选择 F4 键）。  
  
24. 在 "**属性**" 窗口中，将 "**生成操作**" 属性更改为 "**内容**"，然后将 "**包括在 VSIX 中**" 属性更改为**True**。  
  
25. 在**解决方案资源管理器**中，对**SimpleMath**重复此过程。  
  
26. 在**解决方案资源管理器**中，选择 " **SimpleMathVSIX** " 项目。  
  
27. 在菜单栏上，依次选择 "**生成**"、"**生成 SimpleMathVSIX**"。  
  
28. 在**解决方案资源管理器**中，打开**SimpleMathVSIX**项目的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**"。  
  
29. 在**文件资源管理器**中，导航到 \bin\Release 文件夹，然后运行 SimpleMathVSIX 安装。  
  
30. 选择 "**安装**" 按钮，等待安装完成，然后重启 Visual Studio。  
  
## <a name="createSample"></a>创建使用类库的示例应用程序  
  
1. 在菜单栏上，依次选择 "**文件**"、"**新建**"、"**新建项目**"。  
  
2. 在模板列表中，展开 "**视觉C#对象**" 或 " **Visual Basic**"，然后选择 " **Windows 应用商店**" 节点。  
  
3. 选择 "**空白应用**" 模板，将项目命名为 " **ArithmeticUI**"，然后选择 **"确定"** 按钮。  
  
4. 在**解决方案资源管理器**中，打开**ArithmeticUI**项目的快捷菜单，然后选择 "**添加**"、"**引用**"。  
  
5. 在引用类型列表中，展开 " **Windows**"，然后选择 "**扩展**"。  
  
6. 在详细信息窗格中，选择 "**简单数学 SDK**扩展"。  
  
    此时会显示有关 SDK 的更多信息。 你可以选择 "**详细信息**" 链接以打开 https://docs.microsoft.com，如本演练前面的 sdkmanifest.xml 文件中所述。  
  
7. 在 "**引用管理器**" 对话框中，选中 "**简单数学 SDK** " 复选框，然后选择 **"确定"** 按钮。  
  
8. 在菜单栏上，依次选择 "**视图**"、"**对象浏览器**"。  
  
9. 在 "**浏览**" 列表中，选择 "**简单数学**"。  
  
     你现在可以浏览 SDK 中的内容。  
  
10. 在**解决方案资源管理器**中，打开 MainPage，并将其内容替换为以下 xaml：  
  
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml#1)]
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml#1)]  
  
11. 更新 MainPage.xaml.cs 以匹配以下代码：  
  
     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml.cs#2)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml.vb#2)]  
  
12. 选择 F5 键以运行应用。  
  
13. 在应用程序中，输入任意两个数字，选择一个操作，然后选择 " **=** " 按钮。  
  
     显示正确的结果。  
  
    你已成功创建并使用了扩展 SDK。  
  
## <a name="see-also"></a>另请参阅  
 [演练：使用C++  创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)  
 [演练：使用 JavaScript 创建 SDK](walkthrough-creating-an-sdk-using-javascript.md)   
 [获取软件开发工具包](../extensibility/creating-a-software-development-kit.md)
