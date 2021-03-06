---
title: vtordisp
ms.date: 10/18/2018
f1_keywords:
- vc-pragma.vtordisp
- vtordisp_CPP
helpviewer_keywords:
- pragmas, vtordisp
- vtordisp pragma
ms.assetid: 05b7d73c-43fa-4b62-8c8a-170a9e427391
ms.openlocfilehash: 67c6c329bcee75012f6075334760925eca945501
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62179447"
---
# <a name="vtordisp"></a>vtordisp

**C++特定**

控制隐藏的 vtordisp 构造函数/析构函数置换成员的添加。

## <a name="syntax"></a>语法

```cpp
#pragma vtordisp([push,] n)
#pragma vtordisp(pop)
#pragma vtordisp()
#pragma vtordisp([push,] {on | off})
```

### <a name="parameters"></a>参数

*push*<br/>
内部编译器堆栈上推送当前 vtordisp 设置并将新 vtordisp 设置设置为*n*。  如果*n*未指定，则不会更改当前 vtordisp 设置。

*pop*<br/>
从内部编译器堆栈中移除顶部的记录并将 vtordisp 设置还原为已移除的值。

*n*<br/>
为 vtordisp 设置指定新值。 可能的值为 0、 1 或 2，对应于`/vd0`， `/vd1`，和`/vd2`编译器选项。 有关详细信息，请参阅[/vd （禁用构造置换）](../build/reference/vd-disable-construction-displacements.md)。

*on*<br/>
等效于 `#pragma vtordisp(1)`。

*off*<br/>
等效于 `#pragma vtordisp(0)`。

## <a name="remarks"></a>备注

**Vtordisp**杂注是仅适用于使用虚拟基的代码。 如果派生的类重写它从虚拟基类继承的虚函数，如果构造函数或派生类的析构函数调用该函数使用指向虚拟基类的指针时，编译器可能会引入其他隐藏的**vtordisp**为带虚拟基的类的字段。

**Vtordisp**杂注影响它后面的类的布局。 `/vd0`， `/vd1`，和`/vd2`选项指定为整个模块相同的行为。 指定 0 或*off*取消显示隐藏**vtordisp**成员。 关闭**vtordisp**指向的对象上是否存在函数类的构造函数和析构函数调用虚拟不可能仅**这**指针。

指定 1 或*上*，默认情况下，启用隐藏**vtordisp**它们是必需的成员。

指定 2 启用隐藏**vtordisp**具有虚函数的所有虚拟基的成员。  `vtordisp(2)` 可能需要确保正确的性能**dynamic_cast**上在部分构造的对象。 有关详细信息，请参阅[编译器警告 （等级 1） C4436](../error-messages/compiler-warnings/compiler-warning-level-1-c4436.md)。

`#pragma vtordisp()`（没有参数）可将 vtordisp 设置还原到其初始设置。

```cpp
#pragma vtordisp(push, 2)
class GetReal : virtual public VBase { ... };
#pragma vtordisp(pop)
```

**结束C++特定**

## <a name="see-also"></a>请参阅

[Pragma 指令和 __Pragma 关键字](../preprocessor/pragma-directives-and-the-pragma-keyword.md)