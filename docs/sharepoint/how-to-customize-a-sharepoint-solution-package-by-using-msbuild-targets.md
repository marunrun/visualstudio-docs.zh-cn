---
title: 使用 MSBuild 目标自定义 SharePoint 解决方案包
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e6570b1e3c16f1935813682e2c29051c4ac7d64a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016878"
---
# <a name="how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets"></a>如何：使用 MSBuild 目标自定义 SharePoint 解决方案包
  通过在命令提示符处使用 MSBuild 目标，可以自定义 Visual Studio 创建 SharePoint 包文件（*.wsp*）的方式。 例如，可以自定义 MSBuild 属性以更改打包中间目录，以及自定义 MSBuild 项组以指定枚举的文件。

## <a name="customize-and-run-msbuild-targets"></a>自定义和运行 MSBuild 目标
 如果自定义 BeforeLayout 和 AfterLayout 目标，您可以在布局包之前执行任务，例如，添加、移除或修改要打包的文件。

#### <a name="to-customize-the-beforelayout-target"></a>自定义 BeforeLayout 目标

1. 打开编辑器（如“记事本”），然后添加以下代码。

   ```xml
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <Target Name="BeforeLayout">
       <Message Importance="high" Text="In the BeforeLayout Target"></Message>
     </Target>
   </Project>
   ```

    此示例将在此目标打包之前显示一条消息。

2. 将该文件命名为**CustomLayout**，然后将其保存在 SharePoint 项目的文件夹中。

3. 打开项目，打开其快捷菜单，然后选择 "**卸载项目**"。

4. 在**解决方案资源管理器**中，打开项目的快捷菜单，**然后选择 "** * \<ProjectName> .vbproj* " 或 "**编辑** * \<ProjectName> .csproj*"。

5. 在临近项目文件末尾的 `Import` 行后面，添加以下行。

   ```xml
   <Import Project="CustomLayout.SharePoint.targets" />
   ```

6. 保存并关闭项目文件。

7. 在**解决方案资源管理器**中，打开项目的快捷菜单，然后选择 "**重新加载项目**"。

   发布项目时，此消息将在打包开始之前显示在输出中。

#### <a name="to-customize-the-afterlayout-target"></a>自定义 AfterLayout 目标

1. 在菜单栏上，选择 "**文件**" "  >  **打开**  >  **文件**"。

2. 在 "**打开文件**" 对话框中，导航到项目文件夹，选择 "CustomLayout" 文件，然后选择 "**打开**" 按钮。

3. 在 `</Project>` 标记的前面添加下列代码：

   ```xml
   <Target Name="AfterLayout">
     <Message Importance="high" Text="In the AfterLayout Target"></Message>
   </Target>
   ```

    此示例将在此目标打包后显示一条消息。

4. 保存并关闭目标文件。

5. 重新启动 Visual Studio，然后打开项目。

   在发布项目时，打包开始前将显示 BeforeLayout 消息，打包完成后将显示 AfterLayout 消息。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
