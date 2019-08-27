---
title: 向域特定语言定义中添加跟踪属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- tracking properties [Domain-Specific Language Tools], walkthrough
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
ms.assetid: 4aa47777-de75-4897-a423-a3c4426b4125
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 814327befe538bfaa102b198988e76dbd52090bb
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705688"
---
# <a name="adding-a-tracking-property-to-a-domain-specific-language-definition"></a>向域特定语言定义中添加跟踪属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何将跟踪属性添加到域模型。  
  
 一个*跟踪域*属性是用户可以更新，但具有一个默认值，通过使用其他域属性或元素的值计算的属性。  
  
 例如，在域特定语言工具 （DSL 工具），域类的属性具有默认值通过使用域类中，而是用户的名称的显示名称可以在设计时更改值或其重置为计算的值。  
  
 在本演练中，创建域特定语言 (DSL) 具有 Namespace 跟踪基于模型的默认 Namespace 属性的默认值的属性。 有关跟踪属性的详细信息，请参阅[定义跟踪属性](https://msdn.microsoft.com/0538b0e4-6221-4e7d-911a-b92cd622f0be)。  
  
- 跟踪属性说明符 DSL 工具支持。 但是，在 DSL 设计器不能用于向语言添加跟踪属性。 因此，必须添加自定义代码来定义和实现的跟踪属性。  
  
  跟踪属性有两种状态： 跟踪，并更新用户。 跟踪属性具有以下功能：  
  
- 中的跟踪状态，当计算跟踪属性的值，和的值更新为模型更改中的其他属性。  
  
- 当在更新用户状态的跟踪属性的值将保留到的用户上次设置该属性的值。  
  
- 在中**属性**窗口中，**重置**命令对于在更新属性时，仅启用了跟踪属性的用户状态。 **重置**命令的跟踪属性设置为跟踪状态。  
  
- 在中**属性**以常规字体显示窗口中，当跟踪属性处于跟踪状态，其值。  
  
- 在中**属性**窗口中，在更新跟踪属性时通过用户状态，以粗体显示其值。  
  
## <a name="prerequisites"></a>系统必备  
 在开始本演练之前，必须首先安装这些组件：  
  
|||  
|-|-|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185579](http://go.microsoft.com/fwlink/?LinkID=185579)|  
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185580](http://go.microsoft.com/fwlink/?LinkID=185580)|  
|[!INCLUDE[dsl](../includes/dsl-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185581](http://go.microsoft.com/fwlink/?LinkID=185581)|  
  
## <a name="creating-the-dsl-project"></a>创建 DSL 项目  
 创建域特定语言的项目。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
1. 创建域特定语言设计器项目。 将其命名为 `TrackingPropertyDSL`。  
  
2. 在中**域特定语言设计器向导**，设置以下选项：  
  
    1. 选择**MinimalLanguage**模板。  
  
    2. 使用域特定语言的默认名称`TrackingPropertyDSL`。  
  
    3. 设置到的模型文件的扩展名为`trackingPropertyDsl`。  
  
    4. 模型文件使用默认模板图标。  
  
    5. 设置到产品的名称`Product Name`。  
  
    6. 设置为公司名称`Company Name`。  
  
    7. 使用解决方案中项目的根命名空间的默认值`CompanyName.ProductName.TrackingPropertyDSL`。  
  
    8. 允许向导为您的程序集创建强名称密钥文件。  
  
    9. 查看解决方案的详细信息，然后单击**完成**创建 DSL 定义项目。  
  
## <a name="customizing-the-default-dsl-definition"></a>自定义默认 DSL 定义  
 在本部分中，您自定义 DSL 定义中包含以下各项：  
  
- 跟踪每个元素的模型属性的 Namespace。  
  
- 一个布尔 IsNamespaceTracking 属性，为模型的每个元素的。 此属性将指示跟踪属性是否在跟踪状态或已更新的用户状态。  
  
- 该模型默认 Namespace 属性。 此属性将用于计算 Namespace 跟踪属性的默认值。  
  
- CustomElements 计算模型的属性。 此属性将指示具有自定义的命名空间的元素的比例。  
  
#### <a name="to-add-the-domain-properties"></a>若要添加的域属性  
  
1. 在 DSL 设计器中，右键单击**ExampleModel**域类中，依次指向**添加**，然后单击**DomainProperty**。  
  
    1. 命名新属性`DefaultNamespace`。  
  
    2. 在中**属性**窗口中的为新属性，设置**默认值**到`DefaultNamespace`，并设置**类型**到**字符串**。  
  
2. 向**ExampleModel**域类中，添加名为的域属性`CustomElements`。  
  
     在中**属性**窗口中的为新属性，设置**种类**到**计算**。  
  
3. 向**ExampleElement**域类中，添加名为的域属性`Namespace`。  
  
     在中**属性**窗口中的为新属性，设置**是可浏览**到**False**，并设置**类型**到**CustomStorage**.  
  
4. 向**ExampleElement**域类中，添加名为的域属性`IsNamespaceTracking`。  
  
     中**属性**窗口中的为新属性，设置**是可浏览**到**False**，将**Default Value**到`true`，并设置**类型**到**布尔**。  
  
#### <a name="to-update-the-diagram-elements-and-dsl-details"></a>若要更新的关系图元素和 DSL 详细信息  
  
1. 在 DSL 设计器中，右键单击**ExampleShape**几何形状，依次指向**添加**，然后单击**文本修饰器**。  
  
    1. 命名新文本修饰器`NamespaceDecorator`。  
  
    2. 在中**属性**窗口中的文本修饰器，设置**位置**到**InnerBottomLeft**。  
  
2. 在 DSL 设计器中，选择连接的线**ExampleElement**类来**ExampleShape**形状。  
  
    1. 在中**DSL 详细信息**窗口中，选择**修饰器映射**选项卡。  
  
    2. 在中**修饰器**列表中，选择**NamespaceDecorator**，选中其复选框，然后在**显示属性**列表中，选择**Namespace**.  
  
3. 在中**DSL 资源管理器**，展开**域类**文件夹中，右键单击**ExampleElement**节点，并单击**添加新域类型描述符**.  
  
    1. 展开**ExampleElement**节点，然后选择**自定义类型描述符 （域类型描述符）** 节点。  
  
    2. 在中**属性**窗口中的域类型描述符，将**自定义编码**到**True**。  
  
4. 在中**DSL 资源管理器**，选择**Xml 序列化行为**节点。  
  
    1. 在中**属性**窗口中，将**自定义发布加载**到**True**。  
  
## <a name="transforming-templates"></a>转换模板  
 现在，已经为你的 DSL 定义的域类和属性，可以验证，DSL 定义经过转换可以正确地重新生成你的项目的代码。  
  
#### <a name="to-transform-the-text-templates"></a>转换文本模板  
  
1. 上**解决方案资源管理器**工具栏上，单击**转换所有模板**。  
  
2. 系统将重新生成解决方案的代码，并将保存 DslDefinition.dsl。 有关定义文件的 XML 格式的信息，请参阅[DslDefinition.dsl 文件](../modeling/the-dsldefinition-dsl-file.md)。  
  
## <a name="creating-files-for-custom-code"></a>创建自定义代码的文件  
 当转换所有模板时，系统将生成在 Dsl 和 DslPackage 项目中定义特定于域的语言的源代码。 这样可以避免干扰生成的文本，不同于生成的代码文件的文件中编写自定义代码。  
  
 用于维护的值和跟踪属性的状态，必须提供代码。 若要帮助你区分从生成的代码中，自定义代码并避免命名冲突的文件，将你的自定义代码的文件放在单独的子文件夹中。  
  
#### <a name="to-create-the-code-files"></a>若要创建的代码文件  
  
1. 在中**解决方案资源管理器**，右键单击**DSL**项目，指向**添加**，然后单击**新文件夹**。 将新文件夹命名为`CustomCode`。  
  
2. 右键单击新**独特**文件夹，指向**添加**，然后单击**新项**。  
  
3. 选择**代码文件**模板，将**名称**到`NamespaceTrackingProperty.cs`，然后单击**确定**。  
  
     创建 NamespaceTrackingProperty.cs 文件并将其打开以进行编辑。  
  
4. 在文件夹中，创建以下的代码文件： `ExampleModel.cs,``HelperClasses.cs`， `Serialization.cs`，和`TypeDescriptor.cs`。  
  
5. 在中**DslPackage**项目中，还创建`CustomCode`文件夹，并向其添加`Package.cs`代码文件。  
  
## <a name="adding-helper-classes-to-support-tracking-properties"></a>添加帮助器类，以支持跟踪属性  
 HelperClasses.cs 文件中，添加`TrackingHelper`和`CriticalException`类，如下所示。 将引用这些类在此演练的后面。  
  
#### <a name="to-add-the-helper-classes"></a>若要添加的帮助程序类  
  
1. 将以下代码添加到 HelperClasses.cs 文件。  
  
    ```csharp  
    using System;  
    using System.Collections;  
    using System.Diagnostics;  
    using Microsoft.VisualStudio.Modeling;  
  
    namespace CompanyName.ProductName.TrackingPropertyDSL  
    {  
        internal static class TrackingHelper  
        {  
            /// <summary>Notify each model element in a collection that a tracked  
            /// property has changed.</summary>  
            /// <param name="store">The store for the model.</param>  
            /// <param name="collection">The collection of model elements that  
            /// contain the tracking property.</param>  
            /// <param name="propertyId">The ID of the tracking property.</param>  
            /// <param name="trackingPropertyId">The ID of the property that  
            /// indicates whether the tracking property is tracking.</param>  
            internal static void UpdateTrackingCollectionProperty(  
                Store store,  
                IEnumerable collection,  
                Guid propertyId,  
                Guid trackingPropertyId)  
            {  
                DomainPropertyInfo propInfo =  
                    store.DomainDataDirectory.GetDomainProperty(propertyId);  
  
                DomainPropertyInfo trackingPropInfo =  
                    store.DomainDataDirectory.GetDomainProperty(trackingPropertyId);  
  
                Debug.Assert(propInfo != null);  
                Debug.Assert(trackingPropInfo != null);  
                Debug.Assert(trackingPropInfo.PropertyType.Equals(typeof(bool)),  
                    "Tracking property not specified as a boolean");  
  
                foreach (ModelElement element in collection)  
                {  
                    // If the tracking property is currently tracking, then notify  
                    // it that the tracked property has changed.  
                    bool isTracking = (bool)trackingPropInfo.GetValue(element);  
                    if (isTracking)  
                    {  
                        propInfo.NotifyValueChange(element);  
                    }  
                }  
            }  
        }  
  
        /// <summary>Helper class to flag critical exceptions from ones that are  
        /// safe to ignore.</summary>  
        internal static class CriticalException  
        {  
            /// <summary>Gets whether an exception is critical and can not be  
            /// ignored.</summary>  
            /// <param name="ex">The exception to check.</param>  
            /// <returns>True if the exception is critical.</returns>  
            internal static bool IsCriticalException(Exception ex)  
            {  
                if (ex is NullReferenceException  
                    || ex is StackOverflowException  
                    || ex is OutOfMemoryException  
                    || ex is System.Threading.ThreadAbortException)  
                    return true;  
  
                if (ex.InnerException != null)  
                    return IsCriticalException(ex.InnerException);  
  
                return false;  
            }  
        }  
    }  
    ```  
  
## <a name="adding-custom-code-for-the-custom-type-descriptor"></a>自定义类型描述符添加自定义代码  
 实现`GetCustomProperties`方法的类型描述符`ExampleModel`域类。  
  
> [!NOTE]
> DSL 工具生成的自定义类型描述符的代码`ExampleModel`调用`GetCustomProperties`; 但是，DSL 工具不会生成实现该方法的代码。  
  
 定义此方法将创建跟踪的跟踪属性的 Namespace 属性描述符。 此外，跟踪属性提供属性使**属性**窗口以正确显示属性。  
  
#### <a name="to-modify-the-type-descriptor-for-the-examplemodel-domain-class"></a>若要修改 ExampleModel 域类的类型描述符  
  
1. 将以下代码添加到 TypeDescriptor.cs 文件。  
  
    ```csharp  
    using System;  
    using System.ComponentModel;  
    using Microsoft.VisualStudio.Modeling;  
    using Microsoft.VisualStudio.Modeling.Design;  
  
    namespace CompanyName.ProductName.TrackingPropertyDSL  
    {  
        // To the custom type descriptor for the ExampleElement domain class, add  
        // the GetCustomProperties method.  
        public partial class ExampleElementTypeDescriptor  
        {  
            /// <summary>Returns the property descriptors for the described  
            /// ExampleElement domain class.</summary>  
            /// <remarks>This method adds the tracking property descriptor.  
            /// </remarks>  
            private PropertyDescriptorCollection GetCustomProperties(  
                Attribute[] attributes)  
            {  
                // Get the default property descriptors from the base class  
                PropertyDescriptorCollection propertyDescriptors =  
                    base.GetProperties(attributes);  
  
                // Get a reference to the model element that is being described.  
                ExampleElement source = this.ModelElement as ExampleElement;  
  
                //Add the descriptor for the tracking property.  
                if (source != null)  
                {  
                    DomainPropertyInfo domainProperty =  
                        source.Store.DomainDataDirectory.GetDomainProperty(  
                            ExampleElement.NamespaceDomainPropertyId);  
  
                    DomainPropertyInfo trackingProperty =  
                        source.Store.DomainDataDirectory.GetDomainProperty(  
                            ExampleElement.IsNamespaceTrackingDomainPropertyId);  
  
                    // Define attributes for the tracking property so that the  
                    // Properties window displays the property correctly.  
                    Attribute[] attr = new Attribute[] {  
                        new DisplayNameAttribute("Element Namespace"),  
                        new DescriptionAttribute("The namespace of the element."),  
                        new CategoryAttribute("Tracking Properties"),  
                    };  
  
                    propertyDescriptors.Add(new TrackingPropertyDescriptor(  
                        source, domainProperty, trackingProperty, attr));  
                }  
  
                // Return the property descriptors for this element  
                return propertyDescriptors;  
            }  
        }  
    }  
    ```  
  
## <a name="adding-custom-code-for-the-package"></a>包中添加自定义代码  
 生成的代码定义 ExampleElement 域类; 的类型说明提供程序但是，必须添加代码以指示要使用此类型说明提供程序的 DSL。  
  
#### <a name="to-update-the-dsl-package-to-use-your-custom-type-descriptor"></a>若要更新 DSL 包以使用自定义类型描述符  
  
1. 将以下代码添加到 Package.cs 文件。  
  
    ```csharp  
    using System.ComponentModel;  
  
    namespace CompanyName.ProductName.TrackingPropertyDSL  
    {  
        // Override the default Initialize method.  
        internal sealed partial class TrackingPropertyDSLPackage  
        {  
            protected override void Initialize()  
            {  
                // Add the custom type descriptor for the ExampleElement type.  
                TypeDescriptor.AddProvider(  
                    new ExampleElementTypeDescriptionProvider(),  
                    typeof(ExampleElement));  
  
                base.Initialize();  
            }  
        }  
    }  
    ```  
  
## <a name="adding-custom-code-for-the-model"></a>添加自定义代码模型  
 实现`GetCustomElementsValue`方法`ExampleModel`域类。  
  
> [!NOTE]
> DSL 工具生成的代码`ExampleModel`调用`GetCustomElementsValue`; 但是，DSL 工具不会生成实现该方法的代码。  
  
 定义`GetCustomElementsValue`方法提供逻辑的 CustomElements 计算属性`ExampleModel`。 此方法进行计数的`ExampleElement`具有跟踪属性有一个用户更新的值，并返回一个字符串，表示此计数为模型中的总元素的一定比例 Namespace 的域类。  
  
 此外，添加`OnDefaultNamespaceChanged`方法`ExampleModel`，并重写`OnValueChanged`方法`DefaultNamespacePropertyHandler`嵌套的类`ExampleModel`调用`OnDefaultNamespaceChanged`。  
  
 因为 DefaultNamespace 属性用于计算跟踪属性，Namespace`ExampleModel`必须通知所有`ExampleElement`DefaultNamespace 值已更改的域类。  
  
#### <a name="to-modify-the-property-handler-for-the-tracked-property"></a>若要修改的属性处理程序被跟踪属性  
  
1. 将以下代码添加到 ExampleModel.cs 文件。  
  
    ```csharp  
    using System.Linq;  
  
    namespace CompanyName.ProductName.TrackingPropertyDSL  
    {  
        public partial class ExampleModel  
        {  
            public string GetCustomElementsValue()  
            {  
                if (this.Elements.Count == 0) return "0/0";  
  
                int number = this.Elements.Count(e => !e.IsNamespaceTracking);  
                return string.Format("{0}/{1}", number, this.Elements.Count);  
            }  
  
            #region Value changed handler for the tracked property  
  
            // When a tracked property changes, it needs to notify all of the properties  
            // that track it.  
  
            /// <summary>Called by the DefaultNamespace property value handler when the  
            /// DefaultNamespace property changes.</summary>  
            /// <param name="oldValue">The previous value of the property.</param>  
            /// <param name="newValue">The new value of the property.</param>  
            protected virtual void OnDefaultNamespaceChanged(  
                string oldValue, string newValue)  
            {  
                // Use the helper class to notify all of the elements in the model  
                // that the default namespace has changed.  
                TrackingHelper.UpdateTrackingCollectionProperty(  
                    this.Store,  
                    this.Elements,  
                    ExampleElement.NamespaceDomainPropertyId,  
                    ExampleElement.IsNamespaceTrackingDomainPropertyId);  
            }  
  
            // Update the change handler for the DefaultNamespace property.  
            internal sealed partial class DefaultNamespacePropertyHandler  
            {  
                /// <summary>Called when the DefaultNamespace property changes.</summary>  
                /// <param name="element">The model element that has the property that  
                /// changed.</param>  
                /// <param name="oldValue">The previous value of the property.</param>  
                /// <param name="newValue">The new value of the property.</param>  
                protected override void OnValueChanged(  
                    ExampleModel element, string oldValue, string newValue)  
                {  
                    base.OnValueChanged(element, oldValue, newValue);  
  
                    if (!element.Store.InUndoRedoOrRollback)  
                    {  
                        element.OnDefaultNamespaceChanged(oldValue, newValue);  
                    }  
                }  
            }  
  
            #endregion  
        }  
    }  
    ```  
  
## <a name="adding-custom-code-for-the-tracking-property"></a>将自定义代码添加跟踪属性  
 添加`CalculateNamespace`方法`ExampleElement`域类。  
  
 定义此方法提供逻辑的 CustomElements 计算属性`ExampleModel`。 此方法进行计数的`ExampleElement`具有 Namespace 跟踪是在更新的属性的域类通过用户状态，并返回一个字符串，表示此计数为模型中的总元素的一定比例。  
  
 此外，添加的存储和方法来获取和设置的 Namespace 自定义存储属性`ExampleElement`域类。  
  
> [!NOTE]
> DSL 工具生成的代码`ExampleModel`调用 get 和 set 方法; 但是，DSL 工具不会生成实现方法的代码。  
  
#### <a name="to-add-the-method-for-the-custom-type-descriptor"></a>若要添加的自定义类型描述符的方法  
  
1. 将以下代码添加到 NamespaceTrackingProperty.cs 文件。  
  
    ```csharp  
    using System;  
    using Microsoft.VisualStudio.Modeling;  
  
    namespace CompanyName.ProductName.TrackingPropertyDSL  
    {  
        // To the domain class that has the tracking property, add the caluclation  
        // for when the property is tracking.  
        public partial class ExampleElement  
        {  
            /// <summary>Calculates the actual value of the property when it is  
            /// tracking.</summary>  
            /// <returns>The value of the tracking property when it is  
            /// tracking.</returns>  
            /// <remarks>Making this method virtual allows child classes to modify  
            /// the calculation. This method does not need to perform validation, as  
            /// its caller handles validation prior to calling this method.  
            /// <para>In this case, the tracking value depends on the default namespace  
            /// property of the parent model.</para></remarks>  
            protected virtual string CalculateNamespace()  
            {  
                return this.ExampleModel.DefaultNamespace;  
            }  
  
            #region Tracking property implementation  
  
            // Implement the Namespace domain property of the ExampleElement domain class,  
            // and update the IsNamespaceTracking domain property value handler.  
  
            /// <summary>Storage for the Namespace property.</summary>  
            private string namespaceStorage;  
  
            /// <summary>Gets the value of the Namespace property.</summary>  
            /// <returns>The value of the Namespace property.</returns>  
            private string GetNamespaceValue()  
            {  
                // Only retrieve the tracked value if the store is not in the  
                // middle of a serialization transaction.  
                bool loading = this.Store.TransactionManager.InTransaction  
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;  
  
                if (!loading && this.IsNamespaceTracking)  
                {  
                    try  
                    {  
                        return this.CalculateNamespace();  
                    }  
                    catch (NullReferenceException)  
                    {  
                        return default(string);  
                    }  
                    catch (Exception e)  
                    {  
                        if (CriticalException.IsCriticalException(e))  
                        {  
                            throw;  
                        }  
                        else  
                        {  
                            return default(string);  
                        }  
                    }  
                }  
  
                return namespaceStorage;  
            }  
  
            /// <summary>Sets the value of the Namespace property.</summary>  
            /// <param name="value">The new value for the property.</param>  
            private void SetNamespaceValue(string value)  
            {  
                namespaceStorage = value;  
  
                // Only update the state of the tracking property if the store is  
                // not in the middle of a serialization transaction.  
                bool loading = this.Store.TransactionManager.InTransaction  
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;  
  
                if (!this.Store.InUndoRedoOrRollback && !loading)  
                {  
                    this.IsNamespaceTracking = false;  
                }  
            }  
  
            // Update the default behavior of the ExampleElement.IsNamespaceTracking  
            // domain property value handler.  
            internal sealed partial class IsNamespaceTrackingPropertyHandler  
            {  
                /// <summary>Called after the IsNamespaceTracking property changes.  
                /// </summary>  
                /// <param name="element">The model element that has the property  
                /// that changed.</param>  
                /// <param name="oldValue">The previous value of the property.  
                /// </param>  
                /// <param name="newValue">The new value of the property.</param>  
                protected override void OnValueChanged(  
                    ExampleElement element, Boolean oldValue, Boolean newValue)  
                {  
                    base.OnValueChanged(element, oldValue, newValue);  
                    if (!element.Store.InUndoRedoOrRollback && newValue)  
                    {  
                        DomainPropertyInfo propInfo =  
                            element.Store.DomainDataDirectory.GetDomainProperty(  
                                ExampleElement.NamespaceDomainPropertyId);  
                        propInfo.NotifyValueChange(element);  
                    }  
                }  
  
                /// <summary>Performs the reset operation for the IsNamespaceTracking  
                /// property for a model element.</summary>  
                /// <param name="element">The model element that has the property  
                /// to reset.</param>  
                internal void ResetValue(ExampleElement element)  
                {  
                    object calculatedValue = null;  
  
                    try  
                    {  
                        calculatedValue = element.CalculateNamespace();  
                    }  
                    catch (NullReferenceException)  
                    {  
                    }  
                    catch (System.Exception e)  
                    {  
                        if (CriticalException.IsCriticalException(e))  
                        {  
                            throw;  
                        }  
                    }  
  
                    if ((calculatedValue != null  
                        && object.Equals(element.Namespace, calculatedValue)))  
                    {  
                        element.isNamespaceTrackingPropertyStorage = true;  
                    }  
                }  
  
                /// <summary>Method to set IsNamespaceTracking to false so that this  
                /// instance of this tracking property is not storage-based.  
                /// </summary>  
                /// <param name="element">The element on which to reset the property  
                /// value.</param>  
                internal void PreResetValue(ExampleElement element)  
                {  
                    // Force the IsNamespaceTracking property to false so that the value  
                    // of the Namespace property is retrieved from storage.  
                    element.isNamespaceTrackingPropertyStorage = false;  
                }  
            }  
  
            #endregion  
        }  
    }  
    ```  
  
## <a name="adding-custom-code-to-support-serialization"></a>添加自定义代码以支持序列化  
 添加代码以支持 XML 序列化自定义的后期加载行为。  
  
> [!NOTE]
> DSL 工具生成调用的代码`OnPostLoadModel`和`OnPostLoadModelAndDiagram`方法; 但是，DSL 工具不会生成实现这些方法的代码。  
  
#### <a name="to-add-code-to-support-the-custom-post-load-behavior"></a>若要添加代码以支持自定义的后期加载行为  
  
1. 将以下代码添加到 Serialization.cs 文件。  
  
    ```csharp  
    using System;  
    using System.Diagnostics;  
    using Microsoft.VisualStudio.Modeling;  
  
    namespace CompanyName.ProductName.TrackingPropertyDSL  
    {  
        #region Helper classes for maintaining state while the store is serializing.  
  
        public abstract partial class TrackingPropertyDSLSerializationHelperBase  
        {  
            /// <summary>Reset the tracking state properties to their natural values  
            /// based on comparing storage with calculation.</summary>  
            /// <param name="store">The store that contains this model.</param>  
            internal static void ResetTrackingProperties(Store store)  
            {  
                // Two passes required - one to set all elements to storage-based  
                // then another to set some back to being tracking.  
                foreach (ModelElement element in store.ElementDirectory.AllElements)  
                {  
                    ExampleElement myElementInstance = element as ExampleElement;  
                    if (myElementInstance != null)  
                    {  
                        myElementInstance.PreResetIsTrackingProperties();  
                        continue;  
                    }  
                }  
                foreach (ModelElement element in store.ElementDirectory.AllElements)  
                {  
                    ExampleElement myElementInstance = element as ExampleElement;  
                    if (myElementInstance != null)  
                    {  
                        myElementInstance.ResetIsTrackingProperties();  
                        continue;  
                    }  
                }  
            }  
        }  
  
        // Add the pre-reset and reset methods for the model element.  
        public partial class ExampleElement  
        {  
            /// <summary>Calls the pre-reset method on the associated property value  
            /// handler for each tracking property of this model element.</summary>  
            internal virtual void PreResetIsTrackingProperties()  
            {  
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.PreResetValue(this);  
            }  
  
            /// <summary>Calls the reset method on the associated property value  
            /// handler for each tracking property of this model element.</summary>  
            internal virtual void ResetIsTrackingProperties()  
            {  
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.ResetValue(this);  
            }  
        }  
  
        #endregion  
  
        #region Custom serialization code  
  
        // To the serialization helper for the TrackingPropertyDSL class, add post  
        // load handlers to bind the tracking property to the serialization process.  
        // These handlers manage the tracking states and property values when the  
        // model is serialized and deserialized.  
        public partial class TrackingPropertyDSLSerializationHelperBase  
        {  
            /// <summary>Customize model loading.</summary>  
            /// <param name="serializationResult">The serialization result from the  
            /// load operation.</param>  
            /// <param name="partition">The partition in which the new  
            /// instance was created.</param>  
            /// <param name="fileName">The name of the file from which the  
            /// instance was deserialized.</param>  
            /// <param name="modelRoot">The root of the file that was loaded.  
            /// </param>  
            private void OnPostLoadModel(  
                SerializationResult serializationResult,  
                Partition partition,  
                string fileName,  
                ExampleModel modelRoot)  
            {  
            }  
  
            /// <summary>Customize model and diagram loading.</summary>  
            /// <param name="serializationResult">Stores serialization result from  
            /// the load operation.</param>  
            /// <param name="modelPartition">Partition in which the new  
            /// instance will be created.</param>  
            /// <param name="modelFileName">Name of the file from which the  
            /// instance will be deserialized.</param>  
            /// <param name="diagramPartition">Partition in which the new  
            /// diagram instance will be created.</param>  
            /// <param name="diagramFileName">Name of the file from which the  
            /// diagram instance will be deserialized.</param>  
            /// <param name="modelRoot">The root of the file that was loaded.</param>  
            /// <param name="diagram">The diagram matching the modelRoot.</param>  
            private void OnPostLoadModelAndDiagram(  
                SerializationResult serializationResult,  
                Partition modelPartition,  
                string modelFileName,  
                Partition diagramPartition,  
                string diagramFileName,  
                ExampleModel modelRoot,  
                TrackingPropertyDSLDiagram diagram)  
            {  
                Debug.Assert(modelPartition != null);  
                Debug.Assert(modelPartition.Store != null);  
  
                // Tracking properties need to be set up according to whether the  
                // serialization matches the calculated values.  
                TrackingPropertyDSLSerializationHelperBase.ResetTrackingProperties(  
                    modelPartition.Store);  
            }  
        }  
  
        #endregion  
    }  
    ```  
  
## <a name="testing-the-language"></a>测试语言  
 下一步是生成并运行 DSL 设计器中的新实例[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]，以便您可以验证跟踪属性工作正常。  
  
#### <a name="to-exercise-the-language"></a>若要执行的语言  
  
1. 在“生成”菜单上，单击“重新生成解决方案”。  
  
2. 在“调试”菜单上，单击“启动调试”。  
  
     实验性生成[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]将打开**调试**解决方案，其中包含一个空测试文件。  
  
3. 在中**解决方案资源管理器**，双击 Test.trackingPropertyDsl 文件以在设计器中打开它，然后单击设计图面。  
  
     请注意，在**属性**关系图中，窗口**Default Namespace**属性是**DefaultNamespace**，和**自定义元素**属性是**0/0**。  
  
4. 拖动**ExampleElement**从元素**工具箱**到关系图图面。  
  
5. 在**属性**窗口中的元素，选择**元素 Namespace**属性，并将值从**DefaultNamespace**到**OtherNamespace**。  
  
     请注意，值**元素 Namespace**现在以粗体显示。  
  
6. 在中**属性**窗口中，右键单击**元素 Namespace**，然后单击**重置**。  
  
     属性的值更改为**DefaultNamespace**，并以常规字体显示值。  
  
     右键单击**元素 Namespace**试。 **重置**现已禁用命令，因为该属性目前是在其跟踪状态。  
  
7. 将另一个**ExampleElement**从**工具箱**到关系图图面，并更改其**元素 Namespace**到**OtherNamespace**。  
  
8. 单击设计图面。  
  
     在中**属性**窗口中为关系图的值**自定义元素**现在**1/2**。  
  
9. 更改**默认 Namespace**从关系图**DefaultNamespace**到**NewNamespace**。  
  
     **Namespace**的第一个元素跟踪**Default Namespace**属性，而**Namespace**第二个元素保持其用户更新值**OtherNamespace**。  
  
10. 保存的解决方案，然后关闭实验性生成。  
  
## <a name="next-steps"></a>后续步骤  
 如果你打算使用多个跟踪属性，或在多个 DSL 中实现跟踪属性，可以创建文本模板生成支持每个跟踪属性的常用代码。 有关文本模板的详细信息，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Modeling.Design.TrackingPropertyDescriptor>   
 <xref:Microsoft.VisualStudio.Modeling.Design.ElementTypeDescriptor>   
 [如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)   
 [如何：创建域特定语言解决方案](../modeling/how-to-create-a-domain-specific-language-solution.md)   
 [演练：自定义的域特定语言定义](../misc/walkthrough-customizing-the-domain-specific-language-definition.md)
