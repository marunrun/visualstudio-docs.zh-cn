---
title: 使用 MSBuild 任务创建 SharePoint 解决方案包
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
ms.openlocfilehash: c59a38e1153a57c1bd886121eeac244075045a42
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86017007"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>如何：使用 MSBuild 任务创建 SharePoint 解决方案包
  可以在开发计算机上使用命令行 MSBuild 任务来生成、清理和验证 SharePoint 包 (*.wsp*) 。 你还可以使用这些命令通过在生成计算机上使用 Team Foundation Server 来自动执行生成过程。

## <a name="build-a-sharepoint-package"></a>生成 SharePoint 包

#### <a name="to-build-a-sharepoint-package"></a>生成 SharePoint 包

1. 在 Windows "**开始**" 菜单上，选择 "**所有程序**  >  **附件**"  >  **命令提示符**。

2. 更改为 SharePoint 项目所在的目录。

3. 输入以下命令为项目创建包。 将 *ProjectFileName* 替换为项目的名称。

    ```cmd
    msbuild /t:Package ProjectFileName
    ```

     例如，你可以运行以下命令之一来打包名为 ListDefinition1 的 SharePoint 项目。

    ```cmd
    msbuild /t:Package ListDefinition1.vbproj
    msbuild /t:Package ListDefinition1.csproj
    ```

## <a name="clean-a-sharepoint-package"></a>清理 SharePoint 包

#### <a name="to-clean-a-sharepoint-package"></a>清理 SharePoint 包

1. 打开命令提示符窗口。

2. 更改为 SharePoint 项目所在的目录。

3. 输入以下命令来清理项目的包。 将 *ProjectFileName* 替换为项目的名称。

    ```cmd
    msbuild /t:CleanPackage ProjectFileName
    ```

     例如，你可以运行以下命令之一来清理名为 ListDefinition1 的 SharePoint 项目。

    ```cmd
    msbuild /t:CleanPackage ListDefinition1.vbproj
    msbuild /t:CleanPackage ListDefinition1.csproj
    ```

## <a name="validate-a-sharepoint-package"></a>验证 SharePoint 包

#### <a name="to-validate-a-sharepoint-package"></a>验证 SharePoint 包

1. 打开命令提示符窗口。

2. 更改为 SharePoint 项目所在的目录。

3. 输入以下命令以验证项目的包。 将 *ProjectFileName* 替换为项目的名称。

    ```cmd
    msbuild /t:ValidatePackage ProjectFileName
    ```

     例如，你可以运行以下命令之一来验证名为 ListDefinition1 的 SharePoint 项目。

    ```cmd
    msbuild /t:ValidatePackage ListDefinition1.vbproj
    msbuild /t:ValidatePackage ListDefinition1.csproj
    ```

## <a name="set-properties-in-a-sharepoint-package"></a>设置 SharePoint 包中的属性

#### <a name="to-set-a-property-in-a-sharepoint-package"></a>在 SharePoint 包中设置属性

1. 打开命令提示符窗口。

2. 更改为 SharePoint 项目所在的目录。

3. 输入以下命令，为项目设置包中的属性。 将 *PropertyName* 替换为要设置的属性。

    ```cmd
    msbuild /property:PropertyName=Value
    ```

     例如，你可以运行以下命令来设置警告等级。

    ```cmd
    msbuild /property:WarningLevel = 2
    ```

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：在 SharePoint 功能中添加和移除项](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
