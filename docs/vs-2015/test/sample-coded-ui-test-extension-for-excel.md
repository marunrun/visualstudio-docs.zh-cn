---
title: 用于 Excel 的编码的 UI 测试扩展示例 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests, extensions for Excel
ms.assetid: 451e4d14-7fac-42f9-af56-2bdc8414c6c7
caps.latest.revision: 15
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e0c6075f9f95f7dc1d21db91936cf35c76f9b2e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672232"
---
# <a name="sample-coded-ui-test-extension-for-excel"></a>适用于 Excel 的示例编码的 UI 测试扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此示例的扩展组件在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 编码的 UI 测试进程中运行，某种程度上和底层的 `ExtensionPackage` 类组成层次结构。 `TechnologyManager`、`ActionFilter` 和 `PropertyProvider` 类在下一层，而控件元素位于顶层。

 ![Excel 测试扩展体系结构](../test/media/excel-extarch.png "Excel_ExtArch")Excel 扩展体系结构

## <a name="extension-points"></a>扩展点
 这些类代表在该示例中实现的用于为 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 启用编码的 UI 测试的扩展点。

### <a name="extensionpackage"></a>ExtensionPackage
 继承自 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> 类，这是编码的 UI 测试扩展的入口点。 实现此抽象类使编码的 UI 测试框架可以从内部访问自定义的 UI 测试技术管理器、UI 测试属性提供程序，以及用于测试新的 UI 的 UI 测试操作筛选器。 有关详细信息，请参阅 [ExtensionPackage 类](../test/sample-excel-extension-extensionpackage-class.md)。

### <a name="technologymanager"></a>TechnologyManager
 继承自 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager> 类，该类提供用于测试录制和播放的技术管理器。 有关详细信息，请参阅 [TechnologyManager 类](../test/sample-excel-extension-technologymanager-class.md)。

### <a name="actionfilter"></a>ActionFilter
 该类继承自[microsoft.visualstudio.testtools.uitest.common.uitestactionfilter>](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110))类，此类提供一个基类，用于将相似的测试操作结果聚合到单个测试结果中。 有关详细信息，请参阅 [ActionFilter 类](../test/sample-excel-extension-actionfilter-class.md)。

### <a name="technology-elements"></a>技术元素
 继承自 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> 类的基类，它提供 UI 测试中可以录制和播放的技术元素的基础。 有关详细信息，请参阅[元素类](../test/sample-excel-extension-element-classes.md)。

### <a name="propertyprovider"></a>PropertyProvider
 继承自 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> 类，该类提供支持 UI 元素属性的、用于测试录制和播放的基类。 有关详细信息，请参阅 [PropertyProvider 类](../test/sample-excel-extension-propertyprovider-class.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>
- [ExtensionPackage 类](../test/sample-excel-extension-extensionpackage-class.md)
- [TechnologyManager 类](../test/sample-excel-extension-technologymanager-class.md)
- [ActionFilter 类](../test/sample-excel-extension-actionfilter-class.md)
- [Element 类](../test/sample-excel-extension-element-classes.md)
- [PropertyProvider 类](../test/sample-excel-extension-propertyprovider-class.md)
