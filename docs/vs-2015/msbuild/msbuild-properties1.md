---
title: MSBuild Properties1 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- MSBuild, properties
ms.assetid: 962912ac-8931-49bf-a88c-0200b6e37362
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2399ff36639732f20babef368a1d9e2f6758a1c4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437875"
---
# <a name="msbuild-properties1"></a>MSBuild Properties1
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

属性是可用于配置生成的名称/值对。 属性可用于将值传递给任务，评估条件和存储将在整个项目文件中引用的值。  
  
## <a name="defining-and-referencing-properties-in-a-project-file"></a>在项目文件中定义和引用属性  
 属性的声明方式是：创建一个与属性同名的元素，将其指定为 [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) 元素的子元素。 例如，下面的 XML 将创建一个名为 `BuildDir` 的属性，其值为 `Build`。  
  
```  
<PropertyGroup>  
    <BuildDir>Build</BuildDir>  
</PropertyGroup>  
```  
  
 在整个项目文件中，可使用语法 $(`PropertyName`) 来引用各个属性。 例如，上一示例中的属性是使用 $(BuildDir) 引用的。  
  
 属性值可通过重新定义属性进行更改。 使用以下 XML可赋予 `BuildDir` 属性新值：  
  
```  
<PropertyGroup>  
    <BuildDir>Alternate</BuildDir>  
</PropertyGroup>  
```  
  
 属性按其在项目中的显示顺序进行评估。 分配旧值后，必须声明 `BuildDir` 的新值。  
  
## <a name="reserved-properties"></a>保留属性  
 MSBuild 保留了一些属性名称，用于存储有关项目文件和 MSBuild 二进制文件的信息。 与其他属性一样，可使用 $ 符号引用这些属性。 例如，$(MSBuildProjectFile) 会返回项目文件的完整文件名，包括文件扩展名。  
  
 有关详细信息，请参阅[如何：引用的名称或项目文件的位置](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)并[MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)。  
  
## <a name="environment-properties"></a>环境属性  
 可以引用项目文件中的环境变量，方法与引用保留属性相同。 例如，若要使用项目文件中的 `PATH` 环境变量，可使用 $(Path)。 如果项目包含与环境属性具有相同名称的属性定义，则项目中的属性将覆盖环境变量的值。  
  
 每个 MSBuild 项目都有一个独立环境块：它只能识别对自己块的读写操作。  在计算或生成项目文件之前，MSBuild 只在初始化属性集合时读取环境变量。 在此之后，环境属性是静态的，也就是说，每个生成工具使用相同的名称和值启动。  
  
 若要从生成工具中获取环境变量的当前值，请使用[属性函数](../msbuild/property-functions.md) System.Environment.GetEnvironmentVariable。 不过，首选方法是使用任务参数 <xref:Microsoft.Build.Utilities.ToolTask.EnvironmentVariables%2A>。 可将此字符串数组中的环境属性集传递给生成工具，而不影响系统环境变量。  
  
> [!TIP]
> 并非所有的环境变量都被读入并成为初始属性。 系统将忽略变量名称不是有效 MSBuild 属性名称的所有环境变量（例如“386”）。  
  
 有关详细信息，请参阅[如何：在生成中使用环境变量](../msbuild/how-to-use-environment-variables-in-a-build.md)。  
  
## <a name="registry-properties"></a>注册表属性  
 可使用以下语法读取系统注册表值，其中 `Hive` 是注册表配置单元（例如 HKEY_LOCAL_MACHINE），`Key` 是密钥名称，`SubKey` 是子密钥名称，`Value` 是子密钥的值。  
  
```  
$(registry:Hive\MyKey\MySubKey@Value)  
```  
  
 若要获取默认的子密钥值，请省略 `Value`。  
  
```  
$(registry:Hive\MyKey\MySubKey)  
```  
  
 可以使用此注册表值初始化生成属性。 例如，若要创建一个表示 Visual Studio web 浏览器主页的生成属性，请使用此代码：  
  
```  
<PropertyGroup>  
  <VisualStudioWebBrowserHomePage>  
    $(registry:HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\12.0\WebBrowser@HomePage)  
  </VisualStudioWebBrowserHomePage>  
<PropertyGroup>  
```  
  
## <a name="global-properties"></a>全局属性  
 通过 MSBuild，可在命令行中使用 **/property**（或 **/p**）开关设置属性。 这些全局属性值会覆盖项目文件中设置的属性值。 这包括环境属性，但不包括不能更改的保留属性。  
  
 以下示例将全局 `Configuration` 属性设置为 `DEBUG`。  
  
```  
msbuild.exe MyProj.proj /p:Configuration=DEBUG  
```  
  
 还可使用 MSBuild 任务的 `Properties` 属性为多项目生成中的子项目设置或修改全局属性。 有关详细信息，请参阅 [MSBuild 任务](../msbuild/msbuild-task.md)。  
  
 如果您在项目标记中使用 `TreatAsLocalProperty` 特性指定一个属性，则全局属性值不会重写项目文件中设置的属性值。 有关详细信息，请参阅[Project 元素 (MSBuild)](../msbuild/project-element-msbuild.md)和[如何：生成相同的源文件使用不同选项](../msbuild/how-to-build-the-same-source-files-with-different-options.md)。  
  
## <a name="property-functions"></a>属性函数  
 从 .NET Framework 版本 4 开始，可以使用属性函数来计算 MSBuild 脚本。 可在生成脚本中读取系统时间、比较字符串、匹配正则表达式及执行其他操作，而无需使用 MSBuild 任务。  
  
 可使用字符串（实例）方法来操作任何属性值，并且还可调用许多系统类的静态方法。 例如，可按如下所示将生成属性设置为当天的日期。  
  
```  
<Today>$([System.DateTime]::Now.ToString("yyyy.MM.dd"))</Today>  
```  
  
 有关详细信息，以及属性函数的列表，请参阅[属性函数](../msbuild/property-functions.md)。  
  
## <a name="creating-properties-during-execution"></a>在执行过程中创建属性  
 在生成的评估阶段会为 `Target` 元素外的属性分配值。 在后续执行阶段中，可按以下方式创建或修改属性：  
  
- 任何任务都可以发出属性。 若要发出属性，[Task](../msbuild/task-element-msbuild.md) 元素必须具有含有 `PropertyName` 属性的 [Output](../msbuild/output-element-msbuild.md) 子元素。  
  
- [CreateProperty](../msbuild/createproperty-task.md) 任务可发出属性。 此用法已弃用。  
  
- 从 .NET Framework 3.5 起，`Target` 元素可能会包含 `PropertyGroup` 元素，后者可能会包含属性声明。  
  
## <a name="storing-xml-in-properties"></a>在属性中存储 XML  
 属性可包含任意 XML，这有助于将值传递给任务或显示日志记录信息。 以下示例介绍了 `ConfigTemplate` 属性，它具有一个包含 XML 和其他属性引用的值。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 使用其相应属性值来替换属性引用。 属性值按其显示顺序进行分配。 因此，在此示例中，`$(MySupportedVersion)`、`$(MyRequiredVersion)` 和 `$(MySafeMode)` 应已定义。  
  
```  
  
<PropertyGroup>  
    <ConfigTemplate>  
        <Configuration>  
            <Startup>  
                <SupportedRuntime  
                    ImageVersion="$(MySupportedVersion)"  
                    Version="$(MySupportedVersion)"/>  
                <RequiredRuntime  
                    ImageVersion="$(MyRequiredVersion)  
                    Version="$(MyRequiredVersion)"  
                    SafeMode="$(MySafeMode)"/>  
            </Startup>  
        </Configuration>  
    </ConfigTemplate>  
</PropertyGroup>  
```  
  
## <a name="see-also"></a>请参阅  
 [MSBuild 概念](../msbuild/msbuild-concepts.md)  
 [MSBuild](msbuild.md)  
 [如何：在生成中使用环境变量](../msbuild/how-to-use-environment-variables-in-a-build.md)   
 [如何：引用的名称或项目文件的位置](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)   
 [如何：生成相同的源文件使用不同选项](../msbuild/how-to-build-the-same-source-files-with-different-options.md)   
 [MSBuild 保留属性和常见属性](../msbuild/msbuild-reserved-and-well-known-properties.md)   
 [Property 元素 (MSBuild)](../msbuild/property-element-msbuild.md)
