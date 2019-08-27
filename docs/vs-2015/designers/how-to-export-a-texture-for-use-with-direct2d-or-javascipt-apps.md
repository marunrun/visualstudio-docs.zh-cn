---
title: 如何：导出纹理以用于 Direct2D 或 Javascipt 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 241c25fe-764e-4e1b-ad32-b1377dcbb605
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d73f24287c4acc38440767d84ae72e862a5e5c75
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823908"
---
# <a name="how-to-export-a-texture-for-use-with-direct2d-or-javascipt-apps"></a>如何：导出纹理以用于 Direct2D 或 Javascipt 应用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

图像内容管道可以生成与 Direct2D 的内部呈现约定相兼容的纹理。 这种类型的纹理适合在使用 Direct2D 的应用和使用 JavaScript 创建的 Windows 应用商店应用中使用。  
  
 本文档演示了这些活动：  
  
- 将源映像配置为由图像内容管道进行处理。  
  
- 配置图像内容管道以生成可在 Direct2D 或 JavaScript 应用中使用的纹理。  
  
  - 生成块压缩的 .dds 文件。  

  - 生成预乘的 Alpha。  

  - 禁用 mipmap 生成。  
  
## <a name="rendering-conventions-in-direct2d"></a>Direct2D 中的呈现约定  
 Direct2D 的上下文中使用的纹理必须符合这些 Direct2D 内部呈现约定：  
  
- Direct2D 通过使用预乘的 Alpha 实现透明度和半透明度。 与 Direct2D 一起使用的纹理必须包含预乘的 Alpha，即使该纹理不使用透明度或半透明度也是如此。 有关预乘 Alpha 的详细信息，请参阅[如何：导出包含自左乘的 Alpha 的纹理](../designers/how-to-export-a-texture-that-has-premultiplied-alpha.md)。  
  
- 必须通过使用以下块压缩格式之一以 .dds 格式应用纹理：  
  
  - BC1_UNORM 压缩  

  - BC2_UNORM 压缩  

  - BC3_UNORM 压缩  
  
- 不支持 mipmap。  
  
#### <a name="to-create-a-texture-thats-compatible-with-direct2d-rendering-conventions"></a>创建与 Direct2D 呈现约定相兼容的纹理  
  
1. 从基本纹理开始。 加载现有映像，或如[如何：创建基本纹理](../designers/how-to-create-a-basic-texture.md)。 若要支持 .dds 格式的块压缩，请指定宽度和高度为 4 的倍数（例如，100x100、128x128 或 256x192）的纹理。 由于不支持 mipmapping，因此纹理无需为正方形，并且大小无需为 2 的幂。  
  
2. 配置纹理文件，使其由图像内容管道进行处理。 在“解决方案资源管理器”  中，打开刚刚创建的纹理文件的快捷菜单，然后选择“属性”  。 在“配置属性”  ，常规”  页上，将“项目类型”  属性设置为“图像内容管道”  。 请确保将“内容”  属性设置为“是”  ，并且将“从生成中排除”  设置为“否”  ，然后选择“应用”  按钮。 将出现“图像内容管道”  配置属性页。  
  
3. 将输出格式设置为块压缩的格式之一。 在“配置属性”  、“图像内容管道”  、“常规”  页上，将“压缩”  属性设置为“BC3_UNORM 压缩(/compress:BC3_UNORM)”  。 根据具体需求，还可以选择任何其他的 BC1、BC2 或 BC3 格式。 Direct2D 当前不支持 BC4、BC5、BC6 或 BC7 纹理。 有关不同 BC 格式的详细信息，请参阅 [Block Compression (Direct3D 10)](https://msdn.microsoft.com/library/windows/desktop/bb694531.aspx)（块压缩 (Direct3D 10)）。  
  
   > [!NOTE]
   > 指定的压缩格式确定图像内容管道生成的文件的格式。 这不同于“图像编辑器”中源映像的“格式”  属性，该“格式”属性确定存储在磁盘上时源映像文件的格式 - 即工作格式  。 通常情况下，不需要已压缩的工作格式。  
  
4. 配置图像内容管道以生成使用预乘的 Alpha 的输出。 在“配置属性”  、“图像内容管道”  、“常规”  页上，将“转换为预乘 alpha 格式”  属性设置为“是(/generatepremultipliedalpha)”  。  
  
5. 配置图像内容管道，使其不生成 mipmap。 在“配置属性”  、“图像内容管道”  、“常规”  页上，将“生成 Mip”  属性设置为“否”  。  
  
6. 选择**确定**按钮。  
  
   生成项目时，图像内容管道会将源映像从工作格式转换为指定的输出格式（转换包括生成预乘的 Alpha），并且结果将被复制到项目的输出目录。
