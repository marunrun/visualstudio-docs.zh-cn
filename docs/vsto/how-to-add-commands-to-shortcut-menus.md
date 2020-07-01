---
title: 如何：向快捷菜单中添加命令
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office menus, creating
- Office development in Visual Studio, context menus
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1ad27481799718d9d2b0872d7a43837fc822ca40
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546193"
---
# <a name="how-to-add-commands-to-shortcut-menus"></a>如何：向快捷菜单中添加命令
  本主题演示如何使用 VSTO 外接程序将命令添加到 Office 应用程序的快捷菜单中。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

### <a name="to-add-commands-to-shortcut-menus-in-office"></a>将命令添加到 Office 的快捷菜单中

1. 将“功能区 XML” **** 项添加到文档级项目或 VSTO 外接程序项目中。 有关详细信息，请参阅[如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。 In

2. 在“解决方案资源管理器”**** 中，选择“” **** 或“” ****。

3. 在菜单栏上，选择 "**查看**  >  **代码**"。

     “ThisAddin” **** 类文件随即在代码编辑器中打开。

4. 将下面的代码添加到 **ThisAddin** 类中。 此代码可替代 `CreateRibbonExtensibilityObject` 方法，并将功能区 XML 类返回到 Office 应用程序。

     [!code-csharp[Trin_WordAddIn_Menus#1](../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs#1)]
     [!code-vb[Trin_WordAddIn_Menus#1](../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb#1)]

5. 在“解决方案资源管理器” **** 中，选择功能区 XML 文件。 默认情况下，功能区 XML 文件命名为*Ribbon1.xml*。

6. 在菜单栏上，选择 "**查看**  >  **代码**"。

     功能区 XML 文件随即在代码编辑器中打开。

7. 在代码编辑器中添加 XML，该 XML 描述快捷菜单以及要添加到快捷菜单的控件。

     下面的示例将向 Word 文档的快捷菜单添加按钮、菜单和库控件。 此快捷菜单的控件 ID 是 ContextMenuText。 有关 Office 2010 快捷方式控件 ID 的完整列表，请参阅[office 2010 帮助文件： office 熟知用户界面控件标识符](https://www.microsoft.com/download/details.aspx?id=6627)。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="MyButton" label="My Button" insertBeforeMso="HyperlinkInsert" onAction="GetButtonID" />
          <menu id="MySubMenu" label="My Submenu" >
            <button id="MyButton2" label="Button on submenu" />
          </menu>
          <gallery id="galleryOne" label="My Gallery">
            <item id="item1" imageMso="HappyFace" />
            <item id="item2" imageMso="HappyFace" />
            <item id="item3" imageMso="HappyFace" />
            <item id="item4" imageMso="HappyFace" />
          </gallery>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

8. 在“解决方案资源管理器” **** 中，选择“MyRibbon.cs” **** 或“MyRibbon.vb” ****。

9. 向 `Ribbon1` 要处理的每个控件的类添加一个回叫方法。

     下面的回叫方法将处理“我的按钮” **** 按钮。 此代码会在光标当前位置向活动文档添加一个字符串。

     [!code-vb[Trin_WordAddIn_Menus#2](../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/ribbon1.vb#2)]
     [!code-csharp[Trin_WordAddIn_Menus#2](../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/ribbon1.cs#2)]

## <a name="see-also"></a>另请参阅
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [演练：创建书签的快捷菜单](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [在 Office 2010 中自定义上下文菜单](/previous-versions/office/developer/office-2010/ee691832(v=office.14))
