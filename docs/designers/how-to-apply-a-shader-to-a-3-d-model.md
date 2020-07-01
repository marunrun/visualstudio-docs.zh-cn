---
title: 如何：向三维模型应用着色器
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a3877bd6-abd8-4a9d-842c-6848b6c2f335
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1f1ae981704287a74bb4e37117190b8b6111d0a9
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769241"
---
# <a name="how-to-apply-a-shader-to-a-3d-model"></a>如何：向三维模型应用着色器

本文演示如何使用模型编辑器将定向关系图着色器语言 (DGSL) 着色器应用于三维模型。

## <a name="apply-a-shader-to-a-3d-model"></a>向三维模型应用着色器

可对三维模型应用着色效果，使其具有有趣的外观。

开始前，请确保显示“属性”  窗口”。

1. 从包含一个或多个模型的三维场景开始。 如果没有合适的三维场景，请按照[如何：创建基本三维模型](../designers/how-to-create-a-basic-3-d-model.md)中所述进行创建。 还必须具有可应用于模型的 DGSL 着色器。 如果没有合适的着色器，请按照[如何：创建基本颜色着色器](../designers/how-to-create-a-basic-color-shader.md)中所述进行创建，并在继续操作前确保已将其保存至文件中。

2. 在“选择”模式中，选择要应用着色器的模型，然后在“属性”窗口的“效果”属性组中的“文件名”属性中，指定要应用到模型的 DGSL 着色器     。

以下模型应用了基本颜色效果：

![显示基本颜色效果的三维场景](../designers/media/digit-3d-model-effect.png)

将着色器应用到模型后，可在着色器设计器中打开它，方式是选择模型，然后在“属性”窗口的“效果”属性组的 **(Advanced)** 属性中选择省略号 ( **...** ) 按钮。

## <a name="see-also"></a>另请参阅

- [如何：创建基本 3D 模型](../designers/how-to-create-a-basic-3-d-model.md)
- [如何：创建基本颜色着色器](../designers/how-to-create-a-basic-color-shader.md)
- [模型编辑器](../designers/model-editor.md)
- [着色器设计器](../designers/shader-designer.md)
