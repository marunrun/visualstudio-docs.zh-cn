---
title: 创建 SharePoint 解决方案包使用 MSBuild 任务
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 432daff22616950e0a97164190a94082bf2db354
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401498"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>如何：使用 MSBuild 任务创建 SharePoint 解决方案包
  可以生成、 清除和验证 SharePoint 包 ( *.wsp*) 在开发计算机上使用命令行 MSBuild 任务。 这些命令还可用于生成计算机上使用 Team Foundation Server 自动生成过程。

## <a name="build-a-sharepoint-package"></a>生成 SharePoint 包

#### <a name="to-build-a-sharepoint-package"></a>若要生成 SharePoint 包

1. 在 Windows 上**启动**菜单中，选择**所有程序** > **附件** > **命令提示符下**。

2. 将更改为您的 SharePoint 项目所在的目录。

3. 输入以下命令以创建项目包。 替换*ProjectFileName*与项目的名称。

    ```cmd
    msbuild /t:Package ProjectFileName
    ```

     例如，可以运行以下命令，包名为 ListDefinition1 的 SharePoint 项目。

    ```cmd
    msbuild /t:Package ListDefinition1.vbproj
    msbuild /t:Package ListDefinition1.csproj
    ```

## <a name="clean-a-sharepoint-package"></a>清除 SharePoint 包

#### <a name="to-clean-a-sharepoint-package"></a>若要清理的 SharePoint 包

1. 打开命令提示符窗口。

2. 将更改为您的 SharePoint 项目所在的目录。

3. 输入以下命令以清理项目的包。 替换*ProjectFileName*与项目的名称。

    ```cmd
    msbuild /t:CleanPackage ProjectFileName
    ```

     例如，可以运行以下命令以清除一个名为 ListDefinition1 的 SharePoint 项目之一。

    ```cmd
    msbuild /t:CleanPackage ListDefinition1.vbproj
    msbuild /t:CleanPackage ListDefinition1.csproj
    ```

## <a name="validate-a-sharepoint-package"></a>验证 SharePoint 包

#### <a name="to-validate-a-sharepoint-package"></a>若要验证 SharePoint 包

1. 打开命令提示符窗口。

2. 将更改为您的 SharePoint 项目所在的目录。

3. 输入以下命令以验证该项目的包。 替换*ProjectFileName*与项目的名称。

    ```cmd
    msbuild /t:ValidatePackage ProjectFileName
    ```

     例如，可以运行以下命令来验证名为 ListDefinition1 的 SharePoint 项目之一。

    ```cmd
    msbuild /t:ValidatePackage ListDefinition1.vbproj
    msbuild /t:ValidatePackage ListDefinition1.csproj
    ```

## <a name="set-properties-in-a-sharepoint-package"></a>在 SharePoint 包中设置属性

#### <a name="to-set-a-property-in-a-sharepoint-package"></a>若要设置的 SharePoint 包中的属性

1. 打开命令提示符窗口。

2. 将更改为您的 SharePoint 项目所在的目录。

3. 输入以下命令以设置项目的包中的属性。 替换*PropertyName*与你想要设置的属性。

    ```cmd
    msbuild /property:PropertyName=Value
    ```

     例如，可以运行以下命令以设置警告等级。

    ```cmd
    msbuild /property:WarningLevel = 2
    ```

## <a name="see-also"></a>请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：添加和删除项 SharePoint 功能](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
