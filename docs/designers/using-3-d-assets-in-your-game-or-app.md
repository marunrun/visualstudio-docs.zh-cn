---
title: 在游戏或应用中使用三维资产
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- VC.Project.ImageContentTask.ContentOutput
- VC.Project.MeshContentTask.ContentOutput
- VC.Project.ImageContentTask.GeneratePremultipliedAlpha
- VC.Project.ImageContentTask.Compress
- VC.Project.ShaderGraphContentTask.ContentOutput
- VC.Project.ImageContentTask.GenerateMips
ms.assetid: ea587909-e434-46a8-abf8-9b3e95a58b4f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3821262a456f9e3e764555fce5fc883b42d4ae9e
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768653"
---
# <a name="how-to-use-3d-assets-in-your-game-or-app"></a>如何：在游戏或应用中使用三维资产

本文介绍如何使用 Visual Studio 处理三维资产并将其包含在生成中。

在使用 Visual Studio 中的工具创建三维资产后，下一步是在应用中使用它们。 但是在使用它们之前，你的资产必须转换为 DirectX 可以解读的格式。 为帮助转换资产，Visual Studio 将为它可产生的每种资产提供生成自定义。 若要将资产包含在生成中，你只需将项目配置为使用生成自定义、将资产添加到你的项目，然后将资产配置为使用正确的生成自定即可。 此后，你可以将资产加载到应用中，然后通过创建并填充 DirectX 资源来使用它们，正如你在任何其他 DirectX 应用中一样。

## <a name="configure-your-project"></a>配置项目

在可将三维资产部署为生成的一部分之前，Visual Studio 必须了解所需部署的资产种类。 Visual Studio 已了解了很多常见的文件种类，但是因为仅某些种类的应用可使用三维资产，因此 Visual Studio 不会假设项目将生成这些种类的文件。 使用为每种资产类型提供的生成自定义（告知 Visual Studio 如何以有用的方式处理不同类型文件的文件），可告知 Visual Studio 应用使用这些种类的资产  。 因为这些自定义可基于每个项目而进行应用，因此你只需向你的项目添加相应的自定义即可。

### <a name="to-add-the-build-customizations-to-your-project"></a>将生成自定义添加到你的项目

1. 在“解决方案资源管理器”中，打开项目的快捷菜单，然后选择“生成依赖项” > “生成自定义”    。

   随即显示“Visual C++ 生成自定义文件”对话框  。

2. 在“可用的生成自定义文件”下，选中希望在项目中使用的资产类型对应的复选框，如下表中所述  ：

    |资产类型|生成自定义名称|
    |----------------| - |
    |纹理和图像|ImageContentTask（.targets、.props） |
    |三维模型|MeshContentTask（.targets、.props） |
    |着色器|ShaderGraphContentTask（.targets、.props） |

3. 选择“确定”  按钮。

## <a name="include-assets-in-your-build"></a>将资产包含在生成中

现在你的项目已了解你希望使用的不同种类的三维资产，下一步是告知它哪些文件是三维资产及其所属的资产种类。

### <a name="to-add-an-asset-to-your-build"></a>将资产添加到生成

1. 在“解决方案资源管理器”中，在项目中打开资产的快捷菜单，然后选择“属性”   。

   随即显示资产的“属性页”对话框  。

2. 请确保将“配置”和“平台”属性设置为你希望更改应用的值   。

3. 在“配置属性”下，选择“常规”，然后在“常规”下的属性网格中，将“项目类型”属性设置为相应的内容管道项目类型     。 例如，对于图像或纹理文件，请选择“图像内容管道”  。

    > [!IMPORTANT]
    > 默认情况下，Visual Studio 假设应使用内置于 Visual Studio 中“图像”项目类型对很多种类的图像文件进行分类  。 因此，必须更改你希望通过图像内容管道处理的每个图像的“项目类型”属性  。 三维模型和视觉着色器图形的内容管道源文件的其他类型默认为正确的“项目类型”  。

4. 选择“确定”  按钮。

下面是三种内容管道项目类型及其关联的源文件类型和输出文件类型。

|项目类型|源文件类型|输出文件格式|
|---------------| - | - |
|图像内容管道 |可移植网络图形 (.png) <br /><br /> JPEG（.jpg、.jpeg、.jpe、.jfif）    <br /><br /> 直接绘画表面 (.dds) <br /><br /> 图形交换格式 (.gif) <br /><br /> 位图（.bmp、.dib）  <br /><br /> 标记图像文件格式（.tif、.tiff）  <br /><br /> Targa (.tga) |直接绘画表面 (.dds) |
|网格内容管道 |Autodesk FBX 交换文件 (.fbx) <br /><br /> Collada DAE 文件 (.dae) <br /><br /> Wavefront OBJ 文件 (.obj) |三维网格文件 (.cmo) |
|着色器内容管道 |视觉对象着色器图 (.dgsl) |编译着色器输出 (.cso) |

## <a name="configure-asset-content-pipeline-properties"></a>配置资产内容管道属性

你可以设置每个资产文件的内容管道属性，以便它将以特定的方式生成。

### <a name="to-configure-content-pipeline-properties"></a>配置内容管道属性

1. 在“解决方案资源管理器”中，在你的项目中打开资产文件的快捷菜单，然后选择“属性”   。

   随即显示资产的“属性页”对话框  。

2. 请确保将“配置”和“平台”属性设置为你希望更改应用到的值   。

3. 在“配置属性”下，选择内容管道节点（例如，纹理和图像资产的“图像内容管道”），然后在属性网格中，将属性设置为相应的值   。 例如，若要在生成时为纹理资产生成 mipmap，请将“生成 Mip”属性设置为“是”   。

4. 选择“确定”  按钮。

### <a name="image-content-pipeline-configuration"></a>图像内容管道配置

使用图像内容管道工具生成纹理资产时，你可以采用各种方式压缩纹理、指示生成时是否应该生成 MIP 级别，以及更改输出文件的名称。

|Property|描述|
|--------------|-----------------|
|压缩 |指定用于输出文件的压缩类型。<br /><br /> 可用选项为：<br /><br /> -   不进行压缩 <br />-   BC1_UNORM 压缩 <br />-   BC1_UNORM_SRGB 压缩 <br />-   BC2_UNORM 压缩 <br />-   BC2_UNORM_SRGB 压缩 <br />-   BC3_UNORM 压缩 <br />-   BC3_UNORM_SRGB 压缩 <br />-   BC4_UNORM 压缩 <br />-   BC4_SNORM 压缩 <br />-   BC5_UNORM 压缩 <br />-   BC5_SNORM 压缩 <br />-   BC6H_UF16 压缩 <br />-   BC6H_SF16 压缩 <br />-   BC7_UNORM 压缩 <br />-   BC7_UNORM_SRGB 压缩 <br /><br /> 有关不同版本的 DirectX 中支持哪些压缩格式的信息，请参阅 [DXGI 编程指南](/windows/win32/direct3ddxgi/dx-graphics-dxgi-overviews)。|
|转换为预乘 alpha 格式|若要将输出文件中的图像转换为预乘 alpha 格式，则为“是”；否则为“否”   。 仅更改输出文件，源图像未发生更改。|
|**生成 Mip**|若要在生成时生成完整的 MIP 链并将它包含在输出文件中，则为“是”；否则为“否”   。 如果为“否”且源文件已经包含 mipmap 链，则输出文件将具有 MIP 链；否则，输出文件将没有 MIP 链  。|
|内容输出 |指定输出文件的名称。 **重要提示：** 更改输出文件的文件扩展名不会影响其文件格式。|

### <a name="mesh-content-pipeline-configuration"></a>网格内容管道配置

使用网格内容管道工具生成网格资产时，你可以更改输出文件的名称。

|Property|描述|
|--------------|-----------------|
|内容输出 |指定输出文件的名称。 **重要提示：** 更改输出文件的文件扩展名不会影响其文件格式。|

### <a name="shader-content-pipeline-configuration"></a>着色器内容管道配置

使用着色器内容管道工具生成着色器资产时，你可以更改输出文件的名称。

|Property|描述|
|--------------|-----------------|
|内容输出 |指定输出文件的名称。 **重要提示：** 更改输出文件的文件扩展名不会影响其文件格式。|

## <a name="load-and-use-3d-assets-at-run-time"></a>在运行时加载和使用三维资产

### <a name="use-textures-and-images"></a>使用纹理和图像

Direct3D 提供了用于创建纹理资源的功能。 在 Direct3D 11 中，D3DX11 实用工具库提供了用于直接从图像文件创建纹理资源和资源视图的其他功能。 有关如何在 Direct3D 11 中创建纹理资源的详细信息，请参阅[纹理](/windows/win32/direct3d11/overviews-direct3d-11-resources-textures)。 有关如何使用 D3DX11 库从图像文件创建纹理资源或资源视图的详细信息，请参阅[如何：从文件初始化纹理](/windows/win32/direct3d11/overviews-direct3d-11-resources-textures-how-to)。

### <a name="use-3d-models"></a>使用三维模型

Direct3D 11 不提供用于从三维模型创建资源的功能。 相反，必须编写代码，该代码读取三维模型文件并创建表示三维模型和该模型所需的任何资源（例如，纹理或着色器）的顶点和索引缓冲区。

### <a name="use-shaders"></a>使用着色器

Direct3D 提供了用于创建着色器资源并将其绑定到可编程的图形管道的功能。 有关如何在 Direct3D 中创建着色器资源并将其绑定到管道的详细信息，请参阅 [HLSL 编程指南](/windows/win32/direct3dhlsl/dx-graphics-hlsl-pguide)。

在可编程的图形管道中，每个管道阶段都必须为下一个管道阶段提供一个以它可理解的方式进行格式化的结果。 因为着色器设计器仅可创建像素着色器，所以这意味着你的应用应确保它接收的数据将采用所预期的格式。 以下几个可编程的着色器阶段可在像素着色器之前出现并执行几何变换：顶点着色器、外壳着色器、域着色器和几何着色器。 不可编程的分割阶段也可在像素着色器之前出现。 无论那些阶段直接出现在像素着色器之前，它都必须采用以下格式提供其结果：

```hlsl
struct PixelShaderInput
{
    float4 pos : SV_POSITION;
    float4 diffuse : COLOR;
    float2 uv : TEXCOORD0;
    float3 worldNorm : TEXCOORD1;
    float3 worldPos : TEXCOORD2;
    float3 toEye : TEXCOORD3;
    float4 tangent : TEXCOORD4;
    float3 normal : TEXCOORD5;
};
```

根据你在着色器中使用的着色器设计器节点，你可能还必须提供采用遵循以下定义的格式的其他数据：

```hlsl
Texture2D Texture1 : register( t0 );
Texture2D Texture2 : register( t1 );
Texture2D Texture3 : register( t2 );
Texture2D Texture4 : register( t3 );
Texture2D Texture5 : register( t4 );
Texture2D Texture6 : register( t5 );
Texture2D Texture7 : register( t6 );
Texture2D Texture8 : register( t7 );

TextureCube CubeTexture1 : register( t8 );
TextureCube CubeTexture2 : register( t9 );
TextureCube CubeTexture3 : register( t10 );
TextureCube CubeTexture4 : register( t11 );
TextureCube CubeTexture5 : register( t12 );
TextureCube CubeTexture6 : register( t13 );
TextureCube CubeTexture7 : register( t14 );
TextureCube CubeTexture8 : register( t15 );

SamplerState TexSampler : register( s0 );

cbuffer MaterialVars : register (b0)
{
    float4 MaterialAmbient;
    float4 MaterialDiffuse;
    float4 MaterialSpecular;
    float4 MaterialEmissive;
    float MaterialSpecularPower;
};

cbuffer LightVars : register (b1)
{
    float4 AmbientLight;
    float4 LightColor[4];
    float4 LightAttenuation[4];
    float3 LightDirection[4];
    float LightSpecularIntensity[4];
    uint IsPointLight[4];
    uint ActiveLights;
}

cbuffer ObjectVars : register(b2)
{
    float4x4 LocalToWorld4x4;
    float4x4 LocalToProjected4x4;
    float4x4 WorldToLocal4x4;
    float4x4 WorldToView4x4;
    float4x4 UVTransform4x4;
    float3 EyePosition;
};

cbuffer MiscVars : register(b3)
{
    float ViewportWidth;
    float ViewportHeight;
    float Time;
};
```

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[如何：导出包含 mipmap 的纹理](../designers/how-to-export-a-texture-that-contains-mipmaps.md)|描述如何使用“图像内容管道”导出包含预计算 mipmap 的纹理。|
|[如何：导出包含预乘 Alpha 的纹理](../designers/how-to-export-a-texture-that-has-premultiplied-alpha.md)|描述如何使用“图像内容管道”导出包含预乘 alpha 值的纹理。|
|[如何：使用 Direct2D 或 JavaScript 应用导出纹理以供使用](../designers/how-to-export-a-texture-for-use-with-direct2d-or-javascipt-apps.md)|描述如何使用“图像内容管道”导出可在 Direct2D 或 JavaScript 应用中使用的纹理。|
|[处理游戏和应用的三维资产](../designers/working-with-3-d-assets-for-games-and-apps.md)|描述 Visual Studio 提供的用于创建和操作三维资产（包括纹理和图像、三维模型和着色器）的编辑工具。|
|[如何：导出着色器](../designers/how-to-export-a-shader.md)|描述如何从着色器设计器中导出着色器。|
