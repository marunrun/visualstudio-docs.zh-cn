---
title: 如何：在部署 Visual Studio 2015 时自动应用产品密钥 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
ms.assetid: d79260be-6234-4fd3-89b5-a9756b4a93c1
caps.latest.revision: 11
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: ec050cf8f365bfae2290593a0c7f215dcb2f39cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185993"
---
# <a name="how-to-automatically-apply-product-keys-when-deploying-visual-studio"></a>How to: Automatically apply product keys when deploying Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[在部署 Visual Studio 时自动应用产品密钥](/visualstudio/install/automatically-apply-product-keys-when-deploying-visual-studio)。

可以采用编程方式将产品密钥作为用于自动化 Visual Studio 2015 的部署的脚本的一部分应用。 在安装 Visual Studio 期间或安装已完成后，产品密钥可以以编程方式在设备上设置。

## <a name="apply-the-license-during-installation"></a>在安装过程中应用许可证
 使用 /ProductKey 参数在 Visual Studio 的安装过程中应用产品密钥。 此安装程序参数可与 /Silent 参数一起使用，为最终用户安装处于已授权状态的 Visual Studio。 若要使用 /ProductKey 参数，请打开命令提示符。 运行安装程序（例如，vs_enterprise.exe 或 vs_professional.exe）并使用不包括短划线的产品密钥（25 个字符）设置 /ProductKey 参数：

 这是使用产品密钥 AAAAABBBBBCCCCCDDDDDEEEEEEE 安装 Visual Studio 2015 Enterprise 的示例命令：

 `vs_enterprise.exe [any other setup parameters] /ProductKey AAAAABBBBBCCCCCDDDDDDEEEEEE`

## <a name="apply-the-license-after-installation"></a>安装完成后应用许可证
 可以通过在无提示模式下使用目标计算机上的 storePID.exe 实用工具来使用产品密钥激活 Visual Studio 的已安装版本。 StorePID.exe 是一种实用程序，它使用 visual studio 安装** \<drive> ： \\ \Program Files (x86) \microsoft Visual studio 14.0\Common7\IDE\StorePID.exe**。

 通过使用“系统中心”代理或提升的命令提示符，后跟产品密钥（包含短划线）和 Microsoft 产品代码 (MPC)，运行具有提升的权限的 storePID.exe。 请务必在产品密钥中包含短划线！

 `StorePID.exe [product key including the dashes] [MPC]`

 这是用于安装 Visual Studio 2015 Enterprise 的示例命令行，具有 07060 的 MPC 和产品密钥“AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE”：

 `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\StorePID.exe AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 07060`

 下表列出了 Visual Studio 的每个版本的 MPC 代码：

|Visual Studio 版本|MPC|
|---------------------------|---------|
|Visual Studio Enterprise 2015|07060|
|Visual Studio Professional 2015|07062|
|Visual Studio Test Professional 2015|07066|
|Visual Studio Ultimate 2013|06181|
|Visual Studio Premium 2013|06191|
|Visual Studio Professional 2013|06177|
|Visual Studio Test Professional 2013|06194|

有关获取产品密钥的详细信息，请参阅[如何：找到 Visual Studio 产品密钥](../install/how-to-locate-the-visual-studio-product-key.md)。

如果 StorePID.exe 成功应用产品密钥，则它将返回 0。 如果遇到错误，它将返回 1 到 6 之间的一个数字。

## <a name="see-also"></a>请参阅

- [安装 Visual Studio](../install/install-visual-studio-2015.md)