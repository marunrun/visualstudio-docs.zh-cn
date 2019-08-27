---
title: VSIX 颜色编译器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f706cc0c84f4329e0e4e8ad9545a31d8f3c31ed4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332801"
---
# <a name="vsix-color-compiler"></a>VSIX 颜色编译器
Visual Studio 扩展颜色编译器工具是采用一个表示颜色的现有 Visual Studio 主题的.xml 文件的控制台应用程序并将其向.pkgdef 文件，以便可以在 Visual Studio 中使用这些颜色。 因为可以轻松比较.xml 文件之间的差异，此工具可用于管理源控件中的自定义颜色。 它还可以挂接到生成环境，以便生成的输出是一个有效的.pkgdef 文件。

 **主题的 XML 架构**

 完成主题.xml 文件如下所示：

```xml
<Themes>
      <!—one or Theme elements -->
      <Theme>
        <!-- one or more Category elements -->
        <Category>
          <!-- one or more Color elements -->
          <Color>
            <!-- zero or one Background element -->
            <Background />
            <!-- zero or one Foreground element -->
            <Foreground />
          </Color>
        </Category>
      </Theme>
</Themes>
```

 **主题**

 \<主题 > 元素定义整个主题。 主题必须包含至少一个\<类别 > 元素。 主题元素的定义如下：

```xml
<Theme Name="name" GUID="guid">
      <!-- one or more Category elements -->
</Theme>
```

|||
|-|-|
|**特性**|**定义**|
|名称|[必需]主题的名称|
|GUID|[必需]主题的 GUID （必须匹配 GUID 格式）|

 为 Visual Studio 中创建自定义颜色时, 这些颜色需要定义有关以下主题。 如果没有颜色存在于特定主题，Visual Studio 将尝试从浅色主题中加载缺失的颜色。

|||
|-|-|
|**主题名称**|**主题 GUID**|
|浅|{de3dbbcd-f642-433c-8353-8f1df4370aba}|
|深|{1ded0138-47ce-435e-84ef-9ec1f439b749}|
|蓝色|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|
|高对比度|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|

 **类别**

 \<类别 > 元素定义在主题中的颜色的集合。 类别名称提供逻辑分组，而应定义为窄越好。 类别必须包含至少一个\<颜色 > 元素。 类别元素的定义如下：

```xml
<Category Name="name" GUID="guid">
      <!-- one or more Color elements -->
 </Category>
```

|||
|-|-|
|**特性**|**定义**|
|名称|[必需]类别的名称|
|GUID|[必需]该类别的 GUID （必须匹配 GUID 格式）|

 **Color**

 \<颜色 > 元素定义的组件或 UI 的状态的颜色。 一种颜色的首选命名方案是 [UI 类型] [State]。 不要使用"颜色"一词，因为它是冗余。 一种颜色应清楚地指示元素类型和的情况下，或"状态，"将为其应用颜色。 一种颜色不能为空，并且必须包含一个或两个\<背景 > 和\<前台 > 元素。 颜色元素的定义如下：

```xml
<Color Name="name">
        <Background /> <!-- zero or one Background element -->
        <Foreground /> <!-- zero or one Foreground element -->
 </Color>
```

|||
|-|-|
|**特性**|**定义**|
|名称|[必需]颜色的名称|

 **背景和/或前台**

 \<背景 > 和\<前台 > 元素定义的颜色值和背景或前景的 UI 元素的类型。 这些元素具有任何子级。

```xml
<Background Type="type" Source="int" />
<Foreground Type="type" Source="int" />
```

|||
|-|-|
|**特性**|**定义**|
|类型|[必需]颜色的类型。 它可以是以下值之一：<br /><br /> *CT_INVALID:* 颜色是无效或未设置。<br /><br /> *CT_RAW:* 原始的 ARGB 值。<br /><br /> *CT_COLORINDEX:* 不要使用。<br /><br /> *CT_SYSCOLOR:* 一种从 SysColor Windows 系统颜色。<br /><br /> *CT_VSCOLOR:* __VSSYSCOLOREX 从 Visual Studio 颜色。<br /><br /> *CT_AUTOMATIC:* 自动的颜色。<br /><br /> *CT_TRACK_FOREGROUND:* 不要使用。<br /><br /> *CT_TRACK_BACKGROUND:* 不要使用。|
|Source|[必需]以十六进制表示颜色的值|

 类型属性中的架构支持由 __VSCOLORTYPE 枚举支持的所有值。 但是，我们建议使用仅限 CT_RAW 和 CT_SYSCOLOR。

 **所有内容**

 这是有效的主题.xml 文件的一个简单示例：

```xml
<Themes>
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">
    <Category Name="MyCategory" GUID="{0A96238B-70CE-4479-9170-EECEAA3FCD58}">
      <Color Name="MyActiveBorder">
        <Background Type="CT_RAW" Source="FFCCCEDB" />
      </Color>
    </Category>
  </Theme>
</Themes>
```

## <a name="how-to-use-the-tool"></a>如何使用该工具
 **语法**

 VsixColorCompiler \<XML 文件 > \<PkgDef 文件 >\<可选参数 >

 **参数**

||||
|-|-|-|
|**交换机名称**|**备注**|**必需或可选**|
|未命名 （.xml 文件）|这是第一个未命名的参数，是要转换的 XML 文件的路径。|必需|
|未命名 （.pkgdef 文件）|这是第二个未命名的参数，生成的.pkgdef 文件的输出路径。<br /><br /> 默认：\<XML 文件名 >.pkgdef|Optional|
|/noLogo|设置此标志会停止打印的产品和版权信息。|Optional|
|/?|打印帮助信息。|Optional|
|/help|打印帮助信息。|Optional|

 **示例**

- VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef

- VsixColorCompiler D:\xml\colors.xml /noLogo

## <a name="notes"></a>说明

- 此工具需要安装 VC + + 运行时的最新版本。

- 支持仅单个文件。 不支持通过文件夹路径的批量转换。

## <a name="sample-output"></a>示例输出
 由工具生成.pkgdef 文件将类似于以下键：

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff

[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff
```