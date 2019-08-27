---
title: 1x1 视口大小变量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3dbc3247-00f5-4644-8ff9-72e9febcf09a
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 74e3bc706cb2df12aacddf9fbb77dec598bfc17a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157555"
---
# <a name="1x1-viewport-size-variant"></a>1x1 视口大小变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将所有呈现器目标上的视口尺寸缩小为 1x1 像素。  
  
## <a name="interpretation"></a>解释  
 较小的视口会减少必须着色的像素数，但是不会减少必须处理的顶点数。 将视口尺寸设置为 1x1 像素可有效地消除应用中的像素着色。  
  
 如果此变体显示较大的性能提升，则可能表示你的应用使用了太多填充率。 这可能表示你已经选择的分辨率对于目标平台而言太高，或者你的应用花费了大量时间来为之后覆盖（过度绘制）的像素着色。 结果表明，减小帧缓冲区的大小或减少过度绘制量将提升应用的性能。  
  
## <a name="remarks"></a>备注  
 在每次调用 `ID3D11DeviceContext::OMSetRenderTargets` 或 `ID3D11DeviceContext::RSSetViewports` 之后，视口尺寸将重置为 1x1 像素。  
  
## <a name="example"></a>示例  
 通过使用如下代码，可重现此变体：  
  
```  
D3D11_VIEWPORT viewport;  
viewport.TopLeftX = 0;  
viewport.TopLeftY = 0;  
viewport.Width = 1;  
viewport.Height = 1;  
d3d_context->RSSetViewports(1, &viewport);  
```
