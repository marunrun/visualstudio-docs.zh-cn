---
title: 如何：取消显示编译器警告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 31827b17-f933-413d-b28a-b19f903b64ca
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aeb404c479edec5dec89f28e80584d435f5c370a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670646"
---
# <a name="how-to-suppress-compiler-warnings"></a>如何：取消显示编译器警告

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以清理生成日志，方法是指定一个或多个不希望包含的编译器警告类型。 例如，将生成日志的详细级别设置为一般、详细或诊断时，可以使用此方法查看自动生成的部分信息，而不是所有信息。 有关详细级别的更多信息，请参阅[如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)。

### <a name="to-suppress-specific-warnings-for-visual-c-or-f"></a>抑制视觉对象C#或 F \# 的特定警告

1. 在**解决方案资源管理器**中，选择想要取消显示警告的项目。

2. 在菜单栏上，依次选择 **“查看”** 、 **“属性页”** 。

3. 选择“生成”页。

4. 在“取消显示警告”框中，指定想要取消显示的警告的错误代码，使用分号分隔，然后重新生成解决方案。

### <a name="to-suppress-specific-warnings-for-visual-c"></a>要取消显示特定的 Visual C++ 警告

1. 在**解决方案资源管理器**中，选择想要取消显示警告的项目或源文件。

2. 在菜单栏上，依次选择 **“查看”** 、 **“属性页”** 。

3. 依次选择“配置属性”类别、“C/C++”类别和“高级”页。

4. 执行以下步骤之一：

    - 在“禁用特定警告”框中，指定想要取消显示的警告的错误代码，并使用分号分隔。

    - 在“禁用特定警告”框中，选择“编辑”以显示更多选项。

5. 选择“确定”按钮，然后重新生成解决方案。

## <a name="suppressing-warnings-for-visual-basic"></a>取消显示 Visual Basic 警告

可以通过编辑项目的 .vbproj 文件，隐藏 Visual Basic 的特定编译器警告。 你还可以使用[编译页，项目设计器](../ide/reference/compile-page-project-designer-visual-basic.md)来按类别取消显示警告。 有关详细信息，请参阅[在 Visual Basic 中配置警告](../ide/configuring-warnings-in-visual-basic.md)。

#### <a name="to-suppress-specific-warnings-for-visual-basic"></a>要取消显示特定的 Visual Basic 警告

1. 在**解决方案资源管理器**中，选择想要取消显示警告的项目。

2. 在菜单栏上，依次选择“项目”、“卸载项目”。

3. 在“解决方案资源管理器”中，打开项目的快捷菜单，然后选择“编辑_ProjectName_.vbproj”。

    此项目文件在代码编辑器中打开。

4. 找到生成所使用的生成配置中的 `<NoWarn></NoWarn>` 元素。

    以下示例显示在 x86 平台上的调试生成配置中的使用粗体文本的 `<NoWarn></NoWarn>` 元素：

   ```xml
   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
       <PlatformTarget>x86</PlatformTarget>
       <DebugSymbols>true</DebugSymbols>
       <DebugType>full</DebugType>
       <Optimize>false</Optimize>
       <OutputPath>bin\Debug\</OutputPath>
       <DefineDebug>true</DefineDebug>
       <DefineTrace>true</DefineTrace>
       <ErrorReport>prompt</ErrorReport>
       <NoWarn></NoWarn>
       <WarningLevel>1</WarningLevel>
     </PropertyGroup>
   ```

5. 添加一个或多个警告编号作为 `<NoWarn>` 元素的值。 如果指定多个警告编号，请使用逗号分隔，如以下示例所示。

   ```xml
   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
       <PlatformTarget>x86</PlatformTarget>
       <DebugSymbols>true</DebugSymbols>
       <DebugType>full</DebugType>
       <Optimize>false</Optimize>
       <OutputPath>bin\Debug\</OutputPath>
       <DefineDebug>true</DefineDebug>
       <DefineTrace>true</DefineTrace>
       <ErrorReport>prompt</ErrorReport>
       <NoWarn>40059,42024</NoWarn>
       <WarningLevel>1</WarningLevel>
     </PropertyGroup>
   ```

6. 保存对 .vbproj 文件所做的更改。

7. 在菜单栏上，依次选择“项目”、“重载项目”。

8. 在菜单栏上，依次选择“生成”、“重新生成解决方案”。

    “输出”窗口不再显示指定的警告。

   有关详细信息，请参阅 [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83)。

## <a name="see-also"></a>请参阅

- [演练：生成应用程序](../ide/walkthrough-building-an-application.md)
- [如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
