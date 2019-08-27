---
title: 定义锁定策略以创建只读段
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22eaa971035b4b202ecb76b3f1d29e286516a69b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445828"
---
# <a name="defining-a-locking-policy-to-create-read-only-segments"></a>定义锁定策略以创建只读段
Visual Studio 可视化和建模 SDK 的不可变性 API 允许程序锁定部分或全部域特定语言 (DSL) 模型，以便它可以读取但不是会更改。 无法使用此只读选项，例如，以便用户可以请求添加批注并查看 DSL 模型的同事，但可以禁止这些更改原始。

 此外，作为 DSL，作者可以定义*锁定策略。* 锁定策略定义哪些锁是允许、 不允许，或强制。 例如，当发布 DSL 时，您可以鼓励第三方开发人员能够扩展使用的新命令。 但也可以使用锁定策略以防止其更改模型的指定部分的只读状态。

> [!NOTE]
> 可以通过使用反射避开锁定策略。 它为第三方开发人员提供明确的边界，但不是提供强安全性。

 详细信息和示例都在 Visual Studio[可视化和建模 SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)网站。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="setting-and-getting-locks"></a>设置和获取锁
 在存储区、 一个分区，或某个元素上，可以设置锁。 例如，此语句将阻止模型元素被删除，并且还将阻止其属性正在更改：

```csharp
using Microsoft.VisualStudio.Modeling.Immutability; ...
element.SetLocks(Locks.Delete | Locks.Property);
```

 可以使用其他锁值以防止在关系、 创建元素时、 分区和角色中的重新排序链接之间移动数据的更改。

 锁将应用用户的操作以及程序代码。 如果程序代码尝试进行更改，`InvalidOperationException`将引发。 撤消或重做操作中，锁将被忽略。

 你可以发现是否元素通过使用给定的一组中具有的任何锁`IsLocked(Locks)`和可以使用来获取当前元素上的锁集`GetLocks()`。

 不使用事务的情况下，可以设置锁。 锁定数据库不是在存储区的一部分。 如果存储区中的值变化的响应中设置锁，例如在 OnValueChanged，您应允许是撤消操作的一部分的更改。

 这些方法是在中定义的扩展方法<xref:Microsoft.VisualStudio.Modeling.Immutability>命名空间。

### <a name="locks-on-partitions-and-stores"></a>锁分区和存储
 此外可以分区和应用商店应用锁。 设置分区的锁应用于分区中的所有元素。 因此，例如，以下语句将阻止在一个分区中的所有元素被删除，而不考虑其自己的锁的状态。 不过，其他锁如`Locks.Property`仍在单个元素上设置：

```csharp
partition.SetLocks(Locks.Delete);
```

 设置对存储区的锁将应用于其所有元素，而不考虑该锁的分区以及元素上的设置。

### <a name="using-locks"></a>使用锁
 可以使用锁来实现方案如下所示：

- 不允许对所有元素和关系，除非表示注释的那些更改。 这允许用户对模型进行批注而不更改它。

- 不允许更改中默认分区，但允许在关系图分区中进行更改。 用户可以重新排列关系图中，但不能更改基础模型。

- 不允许更改到存储在一个单独的数据库中注册的用户的组除外。 对于其他用户，关系图和模型是只读的。

- 不允许对模型进行更改，如果关系图的布尔属性设置为 true。 提供更改该属性的菜单命令。 这有助于确保它们无法表达的用户意外更改。

- 不允许添加和删除的元素和关系的特定类，但允许属性更改。 用户提供一个固定的窗体，它们可以在其中填充属性。

## <a name="lock-values"></a>锁值
 可以在应用商店、 分区或单独的模型元素上设置锁。 锁是`Flags`枚举： 可以使用其值进行组合&#124;。

- ModelElement 锁始终包含其分区锁。

- 锁分区始终包含在存储区的锁。

  无法设置锁分区上或存储并在同一时间禁用某个元素上的锁。

|“值”|这意味着如果`IsLocked(Value)`为 true|
|-|-|
|None|没有限制。|
|属性|不能更改域属性的元素。 这不适用于生成的域类在关系中的角色的属性。|
|添加|不能在分区中创建新元素和链接或存储。<br /><br /> 不适用于`ModelElement`。|
|移动|如果无法将元素移动各个分区之间`element.IsLocked(Move)`为 true，或者如果`targetPartition.IsLocked(Move)`为 true。|
|删除|无法删除一个元素，如果元素本身上设置此锁或任何元素上删除会传播，例如嵌入的元素和形状。<br /><br /> 可以使用`element.CanDelete()`发现是否可以删除某个元素。|
|重新排序|不能更改排序 roleplayer 方式的链接。|
|RolePlayer|不能更改来源于此元素的链接集。 例如，新元素不能嵌入此元素下。 这不会影响此元素是目标的链接。<br /><br /> 如果此元素是一个链接，其源和目标不受影响。|
|全部|其他值的按位 OR。|

## <a name="locking-policies"></a>锁定策略
 作为 DSL 的作者，你可以定义*锁定策略*。 锁定策略，以便可以防止特定的锁正在设置或强制要求使用特定的锁，必须设置减少 SetLocks()，该操作。 通常情况下，将使用锁定策略阻止用户或开发人员能够从意外地以相同的方式可以将变量声明 contravening DSL 的预期的用途`private`。

 锁定策略还可用于设置在所有元素上的锁依赖于该元素的类型。 这是因为`SetLocks(Locks.None)`时首次创建或从文件反序列化元素始终调用。

 但是，不能使用策略来改变其生命周期内的元素上的锁。 若要实现此效果，应使用调用`SetLocks()`。

 若要定义锁定策略，必须：

- 创建用于实现 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> 的类。

- 将此类添加到可通过你的 DSL 的 DocData 的服务。

### <a name="to-define-a-locking-policy"></a>若要定义锁定策略
 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> 具有以下定义：

```csharp
public interface ILockingPolicy
{
  Locks RefineLocks(ModelElement element, Locks proposedLocks);
  Locks RefineLocks(Partition partition, Locks proposedLocks);
  Locks RefineLocks(Store store, Locks proposedLocks);
}
```

 在调用时调用这些方法`SetLocks()`上应用商店、 分区或模型元素。 在每个方法中，则会一建议的锁。 您可以返回建议的组，也可以添加并减去锁。

 例如：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  public class MyLockingPolicy : ILockingPolicy
  {
    /// <summary>
    /// Moderate SetLocks(this ModelElement target, Locks locks)
    /// </summary>
    /// <param name="element">target</param>
    /// <param name="proposedLocks">locks</param>
    /// <returns></returns>
    public Locks RefineLocks(ModelElement element, Locks proposedLocks)
    {
      // In my policy, users can never delete an element,
      // and other developers cannot easily change that:
      return proposedLocks | Locks.Delete);
    }
    public Locks RefineLocks(Store store, Locks proposedLocks)
    {
      // Only one user can change this model:
      return Environment.UserName == "aUser"
           ? proposedLocks : Locks.All;
    }
```

 若要确保用户始终可以删除元素，即使其他代码调用 `SetLocks(Lock.Delete):`

 `return proposedLocks & (Locks.All ^ Locks.Delete);`

 若要禁用的 MyClass 的每个元素的所有属性中的行为更改：

 `return element is MyClass ? (proposedLocks | Locks.Property) : proposedLocks;`

### <a name="to-make-your-policy-available-as-a-service"></a>若要使策略可作为服务
 在你`DslPackage`项目中，添加新的文件，其中包含类似于下面的示例代码：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  // Override the DocData GetService() for this DSL.
  internal partial class YourDslDocData // Change
  {
    /// <summary>
    /// Custom locking policy cache.
    /// </summary>
    private ILockingPolicy myLockingPolicy = null;

    /// <summary>
    /// Called when a service is requested.
    /// </summary>
    /// <param name="serviceType">Service requested</param>
    /// <returns>Service implementation</returns>
    public override object GetService(System.Type serviceType)
    {
      if (serviceType == typeof(SLockingPolicy)
       || serviceType == typeof(ILockingPolicy))
      {
        if (myLockingPolicy == null)
        {
          myLockingPolicy = new MyLockingPolicy();
        }
        return myLockingPolicy;
      }
      // Request is for some other service.
      return base.GetService(serviceType);
    }
}
```
