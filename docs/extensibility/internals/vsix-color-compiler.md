---
title: VSIX 颜色编译器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f414a56bb05a23b6efef19aa7c99292b8a40038a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703900"
---
# <a name="vsix-color-compiler"></a>VSIX 颜色编译器
Visual Studio 扩展颜色编译器工具是一个控制台应用程序，它采用一个表示现有 Visual Studio 主题颜色的 .xml 文件，并将其隐藏到 .pkgdef 文件中，以便这些颜色可以在 Visual Studio 中使用。 由于很容易比较 .xml 文件之间的差异，此工具可用于管理源代码管理中的自定义颜色。 还可以将其连接到生成环境，以便生成的输出是有效的 .pkgdef 文件。

 **主题 XML 架构**

 完整的主题 .xml 文件如下所示：

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

 \<主题>元素定义整个主题。 主题必须至少包含一个\<类别>元素。 主题元素的定义如下：

```xml
<Theme Name="name" GUID="guid">
      <!-- one or more Category elements -->
</Theme>
```

|||
|-|-|
|**特性**|**定义**|
|名称|[必需]主题的名称|
|GUID|[必需]主题的 GUID（必须匹配 GUID 格式）|

 为 Visual Studio 创建自定义颜色时，需要为以下主题定义这些颜色。 如果特定主题不存在颜色，Visual Studio 会尝试从"灯光"主题加载缺失的颜色。

|||
|-|-|
|**主题名称**|**主题 GUID**|
|浅色|[de3dbbcd-f642-433c-8353-8f1df4370aba]|
|深色|{1ded0138-47ce-435e-84ef-9ec1f439b749}|
|蓝色|[a4d6a176-b948-4b29-8c66-53c97a1ed7d0]|
|高对比度|[a4d6a176-b948-4b29-8c66-53c97a1ed7d0]|

 **类别**

 类别\<>元素定义主题中的颜色集合。 类别名称提供逻辑分组，并且应尽可能狭义地定义。 类别必须至少包含一个\<颜色>元素。 类别元素的定义如下：

```xml
<Category Name="name" GUID="guid">
      <!-- one or more Color elements -->
 </Category>
```

|||
|-|-|
|**特性**|**定义**|
|名称|[必需]类别的名称|
|GUID|[必需]类别的 GUID（必须匹配 GUID 格式）|

 **彩色**

 颜色\<>元素定义 UI 的组件或状态的颜色。 颜色的首选命名方案是 [UI 类型] [状态]。 不要使用"颜色"一词，因为它是多余的。 颜色应清楚地指示要应用颜色的元素类型和情况或"状态"。 颜色不能为空，并且必须包含\<背景>和\<前景>元素的一个或两个。 颜色元素的定义如下：

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

 **背景和/或前景**

 背景\<>和\<前景>元素为 UI 元素的背景或前景定义颜色的值和类型。 这些元素没有子元素。

```xml
<Background Type="type" Source="int" />
<Foreground Type="type" Source="int" />
```

|||
|-|-|
|**特性**|**定义**|
|类型|[必需]颜色的类型。 该参数可以是下列值之一：<br /><br /> *CT_INVALID：* 颜色无效或未设置。<br /><br /> *CT_RAW：* 原始 ARGB 值。<br /><br /> *CT_COLORINDEX：* 请勿使用。<br /><br /> *CT_SYSCOLOR：* 来自 SysColor 的 Windows 系统颜色。<br /><br /> *CT_VSCOLOR：*__VSSYSCOLOREX的视觉工作室颜色。<br /><br /> *CT_AUTOMATIC：* 自动颜色。<br /><br /> *CT_TRACK_FOREGROUND：* 请勿使用。<br /><br /> *CT_TRACK_BACKGROUND：* 请勿使用。|
|源|[必需]十六进制表示的颜色值|

 __VSCOLORTYPE枚举支持的所有值都由 Type 属性中的架构支持。 但是，我们建议您仅使用CT_RAW和CT_SYSCOLOR。

 **一起**

 这是一个有效主题 .xml 文件的简单示例：

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

 VsixColor编译器\<XML文件> \<PkgDef\<文件>可选 Args>

 **自变量**

||||
|-|-|-|
|**切换名称**|**说明**|**必需或可选**|
|未命名 （.xml 文件）|这是第一个未命名的参数，是要转换的 XML 文件的路径。|必选|
|未命名（.pkgdef 文件）|这是第二个未命名的参数，是生成的 .pkgdef 文件的输出路径。<br /><br /> 默认值：XML\<文件名>.pkgdef|可选|
|/noLogo|设置此标志将停止打印产品和版权信息。|可选|
|/?|打印帮助信息。|可选|
|/help|打印帮助信息。|可选|

 **示例**

- VsixColor 编译器 D：\xml_颜色.xml D：\pkgdef_colors.pkgdef

- VsixColor 编译器 D：\xml_颜色.xml/noLogo

## <a name="notes"></a>说明

- 此工具要求安装最新版本的 VC++ 运行时。

- 仅支持单个文件。 不支持通过文件夹路径进行批量转换。

## <a name="sample-output"></a>示例输出
 该工具生成的 .pkgdef 文件将类似于以下键：

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff

[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff
```
