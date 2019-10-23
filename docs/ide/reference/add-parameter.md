---
title: “向方法添加参数”快速操作
ms.date: 09/28/2018
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d1edc9d38ff4476a9fe76886676bfce1c80a61db
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658806"
---
# <a name="add-a-parameter-to-a-method-using-a-quick-action"></a>使用快速操作向方法添加参数

此代码生成适用于：

- C#

- Visual Basic

**功能：** 便于用户根据使用情况，自动向方法添加参数。

**使用时机：** 需要向方法添加参数，并希望以适当方式自动声明它。

操作原因：  虽然可以在调用方法前向方法声明添加参数，但此功能可根据方法调用自动添加参数。

## <a name="how-to-use-it"></a>使用方法

1. 向方法调用添加额外参数。

   调用的方法的名称下方显示红色波形曲线。

2. 将指针悬停在红色波形曲线上，直到显示“快速操作”菜单。 选择“快速操作”菜单中的“向下箭头”  ，再选择“向 [方法] 添加参数”  。

   ![Visual Studio 中的“向方法添加参数”快速操作](media/add-parameter-to-method.png)

   > [!TIP]
   > 也可以通过下列方式访问“快速操作”菜单：将光标悬停在方法调用行上，再按 Ctrl  +.  ， （句点）或选择文件边距中的灯泡图标。

   此时，Visual Studio 会向方法声明添加新参数。

> [!NOTE]
> 如果对相应方法有其他调用，可能会在使用此快速操作后看到错误消息，因为其他调用没有为新添加的形参指定实参。

## <a name="see-also"></a>请参阅

- [向构造函数添加参数](generate-constructor.md#addparameter)