---
title: TN038:MFC OLE IUnknown 实现
ms.date: 06/28/2018
helpviewer_keywords:
- aggregation macros [MFC]
- COM interfaces, base interface
- IUnknown interface
- END_INTERFACE_MAP macro [MFC]
- TN038
- BEGIN_INTERFACE_PART macro [MFC]
- DECLARE_INTERFACE_MAP macro [MFC]
- BEGIN_INTERFACE_MAP macro [MFC]
- OLE [MFC], implementing IUnknown interface
- METHOD_PROLOGUE macro [MFC]
- STDMETHOD macro [MFC]
- END_INTERFACE_PART macro [MFC]
- INTERFACE_PART macro
ms.assetid: 19d946ba-beaf-4881-85c6-0b598d7f6f11
ms.openlocfilehash: a366d200c272570b4806a8642f287a7ef69b430e
ms.sourcegitcommit: 934cb53fa4cb59fea611bfeb9db110d8d6f7d165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65611309"
---
# <a name="tn038-mfcole-iunknown-implementation"></a>TN038:MFC/OLE IUnknown 实现

> [!NOTE]
> 以下技术说明在首次包括在联机文档中后未更新。 因此，某些过程和主题可能已过时或不正确。 要获得最新信息，建议你在联机文档索引中搜索热点话题。

OLE 2 的核心是“OLE 组件对象模型”，又称为 COM。 COM 定义协同对象如何互相通信的标准。 这包括“对象”外观的详细信息，其中包括方法如何在对象上分派。 COM 还定义了一个基类，所有兼容 COM 的类都由此派生。 此基类是[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)。 尽管[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口被称为C++类，COM 不是特定于任何一种语言，它可以在 C、 PASCAL 或任何其他可以支持的 COM 对象二进制布局的语言中实现。

OLE 将所有类派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)作为"接口。 这是一个重要的区别，因为"接口"例如[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)携带没有实现。 它只定义对象借由通信的协议，而不定义这些实现可以完成的具体事项。 这对于允许最大灵活性的系统而言是合理的。 MFC 的作用是实现 MFC/C++ 程序的默认行为。

若要了解 MFC 的实现[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)必须先了解此接口是什么。 简化的版本[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)定义如下：

```cpp
class IUnknown
{
public:
    virtual HRESULT QueryInterface(REFIID iid, void** ppvObj) = 0;
    virtual ULONG AddRef() = 0;
    virtual ULONG Release() = 0;
};
```

> [!NOTE]
> 此例中省略了某些必要的调用约定详细信息，例如 `__stdcall`。

[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)并[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)成员函数控制对象的内存管理。 COM 使用引用计数方案跟踪对象。 从来不会像在 C++ 中一样直接引用对象。 相反，始终通过指针引用 COM 对象。 若要在所有者用完时释放对象使用它，该对象的[释放](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)调用成员 (而不是使用 delete 运算符，如就执行此操作的传统的C++对象)。 引用计数机制允许管理单个对象的多个引用。 实现[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)并[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)维护引用计数对象 — 其引用计数达到零时才会删除该对象。

[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)并[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)从实现的角度而言相当简单明了。 此处为普通实现：

```cpp
ULONG CMyObj::AddRef()
{
    return ++m_dwRef;
}

ULONG CMyObj::Release()
{
    if (--m_dwRef == 0)
    {
        delete this;
        return 0;
    }
    return m_dwRef;
}
```

[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))成员函数是一些更有趣。 不是非常有趣的事情有一个对象，其唯一的成员函数是[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)和[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)— 很高兴告诉对象来完成更多的事情，比[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)提供了。 这就是[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))非常有用。 它允许你在同一对象上获取不同的“接口”。 这些接口通常派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)并通过添加新的成员函数添加附加功能。 COM 接口从不在接口中声明成员变量，并且所有成员函数都声明为纯虚。 例如，应用于对象的

```cpp
class IPrintInterface : public IUnknown
{
public:
    virtual void PrintObject() = 0;
};
```

若要获取 IPrintInterface，如果只有[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)，调用[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))使用`IID`的`IPrintInterface`。 `IID` 是唯一标识接口的 128 位数字。 你或 OLE 定义的每个接口都具有 `IID`。 如果*pUnk*指向的指针[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)对象，若要从中检索 IPrintInterface 的代码可能是：

```cpp
IPrintInterface* pPrint = NULL;
if (pUnk->QueryInterface(IID_IPrintInterface, (void**)&pPrint) == NOERROR)
{
    pPrint->PrintObject();
    pPrint->Release();
    // release pointer obtained via QueryInterface
}
```

这种方法似乎相当容易，但您将如何实现同时支持 IPrintInterface 的对象和[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口在这种情况下它很简单，因为 IPrintInterface 直接派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown) — 通过实现 IPrintInterface， [IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)则会自动支持。 例如：

```cpp
class CPrintObj : public CPrintInterface
{
    virtual HRESULT QueryInterface(REFIID iid, void** ppvObj);
    virtual ULONG AddRef();
    virtual ULONG Release();
    virtual void PrintObject();
};
```

实现[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)并[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)将完全相同实现更高版本。 `CPrintObj::QueryInterface` 将如下所示：

```cpp
HRESULT CPrintObj::QueryInterface(REFIID iid, void FAR* FAR* ppvObj)
{
    if (iid == IID_IUnknown || iid == IID_IPrintInterface)
    {
        *ppvObj = this;
        AddRef();
        return NOERROR;
    }
    return E_NOINTERFACE;
}
```

可以看到，如果接口标识符 (IID) 得到识别，指针会返回到对象；否则会出现错误。 另请注意，成功[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))导致隐式[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)。 当然，你还必须实现 CEditObj::Print。 这是简单的因为 IPrintInterface 直接派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 但是，如果你想要支持两个不同的接口，派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)，请考虑以下：

```cpp
class IEditInterface : public IUnkown
{
public:
    virtual void EditObject() = 0;
};
```

尽管有许多不同的方法用于实现同时支持 IEditInterface 和 IPrintInterface 的类，包括使用 C++ 多重继承，但本说明将集中讨论如何使用嵌套类实现此功能。

```cpp
class CEditPrintObj
{
public:
    CEditPrintObj();

    HRESULT QueryInterface(REFIID iid, void**);
    ULONG AddRef();
    ULONG Release();
    DWORD m_dwRef;

    class CPrintObj : public IPrintInterface
    {
    public:
        CEditPrintObj* m_pParent;
        virtual HRESULT QueryInterface(REFIID iid, void** ppvObj);
        virtual ULONG AddRef();
        virtual ULONG Release();
    } m_printObj;

    class CEditObj : public IEditInterface
    {
    public:
        CEditPrintObj* m_pParent;
        virtual ULONG QueryInterface(REFIID iid, void** ppvObj);
        virtual ULONG AddRef();
        virtual ULONG Release();
    } m_editObj;
};
```

以下内容包括整个实现：

```cpp
CEditPrintObj::CEditPrintObj()
{
    m_editObj.m_pParent = this;
    m_printObj.m_pParent = this;
}

ULONG CEditPrintObj::AddRef()
{
    return ++m_dwRef;
}

CEditPrintObj::Release()
{
    if (--m_dwRef == 0)
    {
        delete this;
        return 0;
    }
    return m_dwRef;
}

HRESULT CEditPrintObj::QueryInterface(REFIID iid, void** ppvObj)
{
    if (iid == IID_IUnknown || iid == IID_IPrintInterface)
    {
        *ppvObj = &m_printObj;
        AddRef();
        return NOERROR;
    }
    else if (iid == IID_IEditInterface)
    {
        *ppvObj = &m_editObj;
        AddRef();
        return NOERROR;
    }
    return E_NOINTERFACE;
}

ULONG CEditPrintObj::CEditObj::AddRef()
{
    return m_pParent->AddRef();
}

ULONG CEditPrintObj::CEditObj::Release()
{
    return m_pParent->Release();
}

HRESULT CEditPrintObj::CEditObj::QueryInterface(REFIID iid, void** ppvObj)
{
    return m_pParent->QueryInterface(iid, ppvObj);
}

ULONG CEditPrintObj::CPrintObj::AddRef()
{
    return m_pParent->AddRef();
}

ULONG CEditPrintObj::CPrintObj::Release()
{
    return m_pParent->Release();
}

HRESULT CEditPrintObj::CPrintObj::QueryInterface(REFIID iid, void** ppvObj)
{
    return m_pParent->QueryInterface(iid, ppvObj);
}
```

请注意，大部分[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)实现放置在 CEditPrintObj 类而不会复制 ceditprintobj:: Ceditobj 和 ceditprintobj:: Cprintobj 中的代码。 这样可以减少代码量并避免 Bug。 此处的关键点在于从 IUnknown 接口可以调用[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))以检索任何接口可能支持该对象，并从每个接口就可以执行相同操作。 这意味着，所有[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))从每个接口可用的函数必须具有行为完全相同的方式。 为了让这些嵌入对象调用“外部对象”中的实现，使用了后向指针 (m_pParent)。 m_pParent 指针在 CEditPrintObj 构造函数计算期间初始化。 然后还会实现 CEditPrintObj::CPrintObj::PrintObject 和 CEditPrintObj::CEditObj::EditObject。 添加了相当多的代码来添加编辑对象的能力这一功能。 幸运的是，接口只有一个成员函数的情况相当罕见（尽管确实存在），并且在这种情况下，通常会将 EditObject 和 PrintObject 合并到单个接口中。

对于如此简单的方案而言，解释和代码都相当多。 MFC/OLE 类提供更简单的替代方案。 MFC 实现使用的技术与使用消息映射包装 Windows 消息的方法类似。 此功能称为*接口映射*和下一节中讨论。

## <a name="mfc-interface-maps"></a>MFC 接口映射

MFC/OLE 包括一个与 MFC 的“消息映射”和“分派映射”在概念和执行上类似的“接口映射”实现。 MFC 的接口映射的核心功能如下所示：

- 标准实现[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)，内置`CCmdTarget`类。

- 维护的引用计数，修改[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)和[版本](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)

- 数据驱动实现[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))

此外，接口映射支持以下高级功能：

- 支持创建可聚合 COM 对象

- 支持在 COM 对象实现期间使用聚合对象

- 实现可钩进且可扩展

有关聚合的详细信息，请参阅[聚合](/windows/desktop/com/aggregation)主题。

MFC 的接口映射支持来源于 `CCmdTarget` 类。 `CCmdTarget` "*具有一个*"引用计数以及所有与关联的成员函数[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)实现 (例如位于引用计数`CCmdTarget`)。 要创建支持 OLE COM 的类，请从 `CCmdTarget` 派生类并使用各种宏以及 `CCmdTarget` 的成员函数实现所需接口。 MFC 的实现使用嵌套类定义每个接口实现，与上面的示例非常类似。 借助 IUnknown 标准实现和数个可以消除一些重复代码的宏，此操作变得更轻松。

## <a name="interface-map-basics"></a>接口映射基本知识

### <a name="to-implement-a-class-using-mfcs-interface-maps"></a>使用 MFC 的接口映射实现类

1. 从 `CCmdTarget` 直接或间接派生类。

2. 使用派生类定义中的 `DECLARE_INTERFACE_MAP` 函数。

3. 对于每个你想要支持的接口，使用类定义中的 BEGIN_INTERFACE_PART 和 END_INTERFACE_PART 宏。

4. 在实现文件中，使用 BEGIN_INTERFACE_MAP 和 END_INTERFACE_MAP 宏来定义类的接口映射。

5. 对于支持每个 IID，使用 INTERFACE_PART 宏之间 BEGIN_INTERFACE_MAP 和 END_INTERFACE_MAP 宏，以将该 IID 映射到特定于您的类"部分"。

6. 实现表示所支持接口的每个嵌套类。

7. METHOD_PROLOGUE 宏用于访问父代、 `CCmdTarget`-派生的对象。

8. [AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)，[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)，和[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))可以委派给`CCmdTarget`这些函数的实现 (`ExternalAddRef`， `ExternalRelease`，和`ExternalQueryInterface`)。

以上 CPrintEditObj 示例可按下列方式实现：

```cpp
class CPrintEditObj : public CCmdTarget
{
public:
    // member data and member functions for CPrintEditObj go here

// Interface Maps
protected:
    DECLARE_INTERFACE_MAP()

    BEGIN_INTERFACE_PART(EditObj, IEditInterface)
        STDMETHOD_(void, EditObject)();
    END_INTERFACE_PART(EditObj)

    BEGIN_INTERFACE_PART(PrintObj, IPrintInterface)
        STDMETHOD_(void, PrintObject)();
    END_INTERFACE_PART(PrintObj)
};
```

以上声明创建派生自 `CCmdTarget` 的类。 DECLARE_INTERFACE_MAP 宏告知框架，此类将具有自定义接口映射。 此外，BEGIN_INTERFACE_PART 和 END_INTERFACE_PART 宏定义嵌套的类，在这种情况下使用名称为 CEditObj 和 CPrintObj （X 仅用于区分嵌套的类从其开始使用"C"和接口的类的全局类"I"开头）。 创建了这些类的两个嵌套成员，分别为 m_CEditObj 和 m_CPrintObj。 宏自动声明[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)，[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)，并[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))函数中; 因此仅声明函数特定于此接口：EditObject 和 PrintObject (使用 STDMETHOD 使用 OLE 宏，以便 **_stdcall**和虚拟关键字提供了以适合目标平台)。

实现此类的接口映射：

```cpp
BEGIN_INTERFACE_MAP(CPrintEditObj, CCmdTarget)
    INTERFACE_PART(CPrintEditObj, IID_IPrintInterface, PrintObj)
    INTERFACE_PART(CPrintEditObj, IID_IEditInterface, EditObj)
END_INTERFACE_MAP()
```

这将分别连接 IID_IPrintInterface IID 和 m_CPrintObj 以及 IID_IEditInterface 和 m_CEditObj。 `CCmdTarget`的实现[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_)) (`CCmdTarget::ExternalQueryInterface`) 使用此映射返回指向 m_CPrintObj 和 m_CEditObj 请求时。 无需包括 `IID_IUnknown` 的条目；请求 `IID_IUnknown` 时，框架将使用映射中的第一个接口（在此例中为 m_CPrintObj）。

尽管 BEGIN_INTERFACE_PART 宏自动声明[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)，[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)并[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))为你的函数，您仍需要实现它们：

```cpp
ULONG FAR EXPORT CEditPrintObj::XEditObj::AddRef()
{
    METHOD_PROLOGUE(CEditPrintObj, EditObj)
    return pThis->ExternalAddRef();
}

ULONG FAR EXPORT CEditPrintObj::XEditObj::Release()
{
    METHOD_PROLOGUE(CEditPrintObj, EditObj)
    return pThis->ExternalRelease();
}

HRESULT FAR EXPORT CEditPrintObj::XEditObj::QueryInterface(
    REFIID iid,
    void FAR* FAR* ppvObj)
{
    METHOD_PROLOGUE(CEditPrintObj, EditObj)
    return (HRESULT)pThis->ExternalQueryInterface(&iid, ppvObj);
}

void FAR EXPORT CEditPrintObj::XEditObj::EditObject()
{
    METHOD_PROLOGUE(CEditPrintObj, EditObj)
    // code to "Edit" the object, whatever that means...
}
```

CEditPrintObj::CPrintObj 的实现将与上面对 CEditPrintObj::CEditObj 的定义类似。 尽管可以创建能够用于自动生成这些函数的宏（在 MFC/OLE 开发的早期阶段是这种情况），但在宏生成多行代码时，设置断点会变得困难。 因此，会手动展开此代码。

通过使用消息映射的框架实现，有许多事项不再需要完成：

- 实现 QueryInterface

- 实现 AddRef 和 Release

- 在两个接口上声明其中一个内置方法

此外，框架在内部使用消息映射。 这让你可以从框架类进行派生，例如 `COleServerDoc`，它已支持某些接口并向框架提供的接口提供替换项或添加项。 框架完全支持从基类继承接口映射，因此你可进行此操作。 这是基类的为什么 BEGIN_INTERFACE_MAP 采用其第二个参数的名称的原因。

> [!NOTE]
> 通常不可能仅通过从 MFC 版本继承 OLE 接口的嵌入专用化来重用 MFC 的 OLE 接口内置实现的实现。 这是不可能因为 METHOD_PROLOGUE 宏来访问该文件包含使用`CCmdTarget`-派生的对象意味着*固定偏移量*从嵌入的对象的`CCmdTarget`-派生的对象。 举例来说，这意味着你无法在 `COleClientItem::XAdviseSink` 中从 MFC 的实现派生嵌入 XMyAdviseSink，因为 XAdviseSink 依赖于对 `COleClientItem` 对象顶部进行特定偏移。

> [!NOTE]
> 但是，你可以为所有你想要其具有 MFC 默认行为的函数委托到 MFC 实现。 这在 `COleFrameHook` 类（它为许多函数委托到 m_xOleInPlaceUIWindow）中的 `IOleInPlaceFrame` (XOleInPlaceFrame) 的 MFC 实现中完成。 选择这种设计是为了减少实现多个接口的对象的运行时大小；它可以避免使用后向指针（例如上一节中使用 m_pParent 的方式）。

### <a name="aggregation-and-interface-maps"></a>聚合和接口映射

除支持独立 COM 对象外，MFC 还支持聚合。 聚合本身是太复杂的主题，介绍;请参阅[聚合](/windows/desktop/com/aggregation)聚合的详细信息的主题。 本说明将简单介绍对内置到框架和接口映射中的聚合的支持。

有两种方法可以使用聚合：（1） 使用支持聚合，COM 对象和 （2） 实现可由另一个聚合的对象。 这些功能可称为“使用聚合对象”和“使对象可聚合”。 MFC 两者都支持。

### <a name="using-an-aggregate-object"></a>使用聚合对象

要使用聚合对象，需要有某种方法能将聚合连接到 QueryInterface 机制中。 换言之，聚合对象必须表现得像是你的对象的本机部分一样。 那么，如何会除了 INTERFACE_PART 宏，MFC 的接口映射机制中的此绑定的嵌套的对象映射到 IID，还可以声明聚合对象作为的一部分在`CCmdTarget`派生的类。 若要执行此操作，请使用 INTERFACE_AGGREGATE 宏。 这允许您指定的成员变量 (它必须是一个指向[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)或派生类)，这是集成到接口映射机制。 如果指针不为 NULL`CCmdTarget::ExternalQueryInterface`是调用，框架将自动调用聚合对象[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))成员函数，如果`IID`请求不是一个本机`IID`s支持的`CCmdTarget`对象本身。

#### <a name="to-use-the-interfaceaggregate-macro"></a>使用 INTERFACE_AGGREGATE 宏

1. 声明将包含指向聚合对象的指针的成员变量 (`IUnknown*`)。

2. 在您按名称引用成员变量的接口映射中包含 INTERFACE_AGGREGATE 宏。

3. 在某些情况下（通常在 `CCmdTarget::OnCreateAggregates` 期间），请将成员变量初始化为除 NULL 之外的值。

例如：

```cpp
class CAggrExample : public CCmdTarget
{
public:
    CAggrExample();

protected:
    LPUNKNOWN m_lpAggrInner;
    virtual BOOL OnCreateAggregates();

    DECLARE_INTERFACE_MAP()
    // "native" interface part macros may be used here
};

CAggrExample::CAggrExample()
{
    m_lpAggrInner = NULL;
}

BOOL CAggrExample::OnCreateAggregates()
{
    // wire up aggregate with correct controlling unknown
    m_lpAggrInner = CoCreateInstance(CLSID_Example,
        GetControllingUnknown(), CLSCTX_INPROC_SERVER,
        IID_IUnknown, (LPVOID*)&m_lpAggrInner);

    if (m_lpAggrInner == NULL)
        return FALSE;
    // optionally, create other aggregate objects here
    return TRUE;
}

BEGIN_INTERFACE_MAP(CAggrExample, CCmdTarget)
    // native "INTERFACE_PART" entries go here
    INTERFACE_AGGREGATE(CAggrExample, m_lpAggrInner)
END_INTERFACE_MAP()
```

m_lpAggrInner 变量在构造函数中初始化为 NULL。 该框架将忽略 NULL 成员变量中的默认实现[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))。 `OnCreateAggregates` 是实际创建聚合对象的适合位置。 如果要在 `COleObjectFactory` 的 MFC 实现外部创建对象，那么必须显式调用它。 讨论聚合对象的创建时，在 `CCmdTarget::OnCreateAggregates` 中创建聚合以及使用 `CCmdTarget::GetControllingUnknown` 的原因就会变得很明显。

此技术可为你的对象提供聚合对象支持的所有接口及其本机接口。 如果只需要聚合支持的一部分接口，可以替代 `CCmdTarget::GetInterfaceHook`。 这使您非常低级的 hookability，类似于[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))。 你通常会想要拥有聚合支持的所有接口。

### <a name="making-an-object-implementation-aggregatable"></a>使对象实现可聚合

对象可聚合，实现[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)，[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)，并[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))必须委托到"控制未知"。 换而言之，它是对象的一部分，它必须委托[AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)，[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)，并[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))到不同的对象，也派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)。 此“控制未知”在创建对象时就会提供给对象，即提供给 `COleObjectFactory` 的实现。 将其实现需要花费一小笔开销，并且在某些情况下并不必要，因此 MFC 使其成为可选项。 要使对象可聚合，请从该对象的构造函数调用 `CCmdTarget::EnableAggregation`。

如果对象还使用聚合，则必须确保将正确的“控制未知”传递给聚合对象。 通常这[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)创建聚合时，将指针传递给对象。 例如，pUnkOuter 参数对于使用 `CoCreateInstance` 创建的对象而言是“控制未知”。 正确的“控制未知”指针可通过调用 `CCmdTarget::GetControllingUnknown` 进行检索。 但是，从该函数返回的值在构造函数计算期间无效。 因此，建议只在 `CCmdTarget::OnCreateAggregates` 替代中创建自己的聚合，该替代中 `GetControllingUnknown` 的返回值是可靠的，即使聚合是从 `COleObjectFactory` 实现创建的。

添加或释放人工引用计数时，对象操作正确的引用计数十分重要。 为确保这一点，请始终调用 `ExternalAddRef` 和 `ExternalRelease`，而不要调用 `InternalRelease` 和 `InternalAddRef`。 很少在支持聚合的类上调用 `InternalRelease` 或 `InternalAddRef`。

## <a name="reference-material"></a>参考资料

OLE 的高级用法（例如定义自己的接口或替代框架对 OLE 接口的实现）需要使用基础接口映射机制。

本节讨论用于实现这些高级功能的每个宏和 API。

### <a name="ccmdtargetenableaggregation--function-description"></a>CCmdTarget::EnableAggregation － 函数说明

```cpp
void EnableAggregation();
```

#### <a name="remarks"></a>备注

如果希望对该类型的对象支持 OLE 聚合，请在派生类的构造函数中调用此函数。 这将准备可聚合对象需要的特殊 IUnknown 实现。

### <a name="ccmdtargetexternalqueryinterface--function-description"></a>CCmdTarget::ExternalQueryInterface － 函数说明

```cpp
DWORD ExternalQueryInterface(
    const void FAR* lpIID,
    LPVOIDFAR* ppvObj
);
```

#### <a name="parameters"></a>参数

*lpIID*<br/>
指向 IID 的较远指针（QueryInterface 的第一个自变量）

*ppvObj*<br/>
指向 IUnknown* 的指针（QueryInterface 的第二个参数）

#### <a name="remarks"></a>备注

在 IUnknown 实现中为你的类实现的每个接口调用此函数。 此函数基于对象的接口映射提供 QueryInterface 的标准数据驱动实现。 需要将返回值转换为 HRESULT。 如果对象进行了聚合，则此函数将调用“控制 IUnknown”，而不会使用本地接口映射。

### <a name="ccmdtargetexternaladdref--function-description"></a>CCmdTarget::ExternalAddRef － 函数说明

```cpp
DWORD ExternalAddRef();
```

#### <a name="remarks"></a>备注

在 IUnknown::AddRef 实现中为你的类实现的每个接口调用此函数。 返回值是 CCmdTarget 对象的新引用计数。 如果对象进行了聚合，则此函数将调用“控制 IUnknown”，而不会操作本地引用计数。

### <a name="ccmdtargetexternalrelease--function-description"></a>CCmdTarget::ExternalRelease － 函数说明

```cpp
DWORD ExternalRelease();
```

#### <a name="remarks"></a>备注

在 IUnknown::Release 实现中为你的类实现的每个接口调用此函数。 返回值指示对象的新引用计数。 如果对象进行了聚合，则此函数将调用“控制 IUnknown”，而不会操作本地引用计数。

### <a name="declareinterfacemap--macro-description"></a>DECLARE_INTERFACE_MAP － 宏说明

```cpp
DECLARE_INTERFACE_MAP
```

#### <a name="remarks"></a>备注

在从 `CCmdTarget` 派生并且将拥有接口映射的任何类中使用此宏。 在很大程度使用 DECLARE_MESSAGE_MAP 方式相同。 此宏调用应放置在类定义中（通常在标头 (.H) 文件中）。 DECLARE_INTERFACE_MAP 具有的类必须实现文件中定义的接口映射 (。CPP) 使用 BEGIN_INTERFACE_MAP 和 END_INTERFACE_MAP 宏。

### <a name="begininterfacepart-and-endinterfacepart--macro-descriptions"></a>BEGIN_INTERFACE_PART 和 END_INTERFACE_PART － 宏说明

```cpp
BEGIN_INTERFACE_PART(localClass, iface);
END_INTERFACE_PART(localClass)
```

#### <a name="parameters"></a>参数

*localClass*<br/>
实现接口的类的名称

*iface*<br/>
此类实现的接口的名称

#### <a name="remarks"></a>备注

对于每个类将实现的接口，需要具有 BEGIN_INTERFACE_PART 和 END_INTERFACE_PART 对。 这些宏定义从你定义的 OLE 接口派生的本地类以及该类的嵌入成员变量。 [AddRef](/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)，[发行](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)，并[QueryInterface](/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))自动声明的成员。 必须包括属于要实现的接口的其他成员函数的声明 （这些声明放 BEGIN_INTERFACE_PART 和 END_INTERFACE_PART 宏之间）。

*Iface*自变量是你想要实现，例如 OLE 接口`IAdviseSink`，或`IPersistStorage`（或你自己的自定义接口）。

*LocalClass*参数是将定义的本地类的名称。 名称前面会自动追加一个“X”。 此命名约定用于避免与同名的全局类发生冲突。 此外，嵌入成员相同的名称*localClass*命名但其前缀为 m_x。

例如：

```cpp
BEGIN_INTERFACE_PART(MyAdviseSink, IAdviseSink)
    STDMETHOD_(void, OnDataChange)(LPFORMATETC, LPSTGMEDIUM);
    STDMETHOD_(void, OnViewChange)(DWORD, LONG);
    STDMETHOD_(void, OnRename)(LPMONIKER);
    STDMETHOD_(void, OnSave)();
    STDMETHOD_(void, OnClose)();
END_INTERFACE_PART(MyAdviseSink)
```

将定义从 IAdviseSink 派生的名为 XMyAdviseSink 的本地类和在该类中声明的名为 m_xMyAdviseSink 的成员。注意：

> [!NOTE]
> 开头的行`STDMETHOD`_ 实质上是复制从 OLE2。H 和略有修改。 从 OLE2.H 复制它们能减少难以解决的错误。

### <a name="begininterfacemap-and-endinterfacemap--macro-descriptions"></a>BEGIN_INTERFACE_MAP 和 END_INTERFACE_MAP － 宏说明

```cpp
BEGIN_INTERFACE_MAP(theClass, baseClass)
END_INTERFACE_MAP
```

#### <a name="parameters"></a>参数

*theClass*<br/>
要在其中定义接口映射的类

*baseClass*<br/>
从其类*类*派生。

#### <a name="remarks"></a>备注

BEGIN_INTERFACE_MAP 和 END_INTERFACE_MAP 宏用于实现文件中实际定义接口映射。 对于每个实现的接口是一个或多个 INTERFACE_PART 宏调用。 对于每个类使用的聚合，没有一个 INTERFACE_AGGREGATE 宏调用。

### <a name="interfacepart--macro-description"></a>INTERFACE_PART － 宏说明

```cpp
INTERFACE_PART(theClass, iid, localClass)
```

#### <a name="parameters"></a>参数

*theClass*<br/>
包含接口映射的类的名称。

*iid*<br/>
要映射到嵌入类的 `IID`。

*localClass*<br/>
本地类的名称（去掉“X”）。

#### <a name="remarks"></a>备注

对于每个对象支持的接口 BEGIN_INTERFACE_MAP 宏和 END_INTERFACE_MAP 宏之间使用此宏。 它允许您将 IID 映射到指示的类的成员*类*并*localClass*。 M_x 将添加到*localClass*自动。 请注意，多个 `IID` 可以与单个成员关联。 当你仅实现一个“派生程度最高”的接口并希望同时提供所有中间接口时，这非常有用。 `IOleInPlaceFrameWindow` 接口就是一个很好的示例。 其层次结构如下所示：

```Hierarchy
IUnknown
    IOleWindow
        IOleUIWindow
            IOleInPlaceFrameWindow
```

如果对象实现`IOleInPlaceFrameWindow`，客户端可能`QueryInterface`上任意一个接口： `IOleUIWindow`， `IOleWindow`，或[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)，除"派生程度最高"接口`IOleInPlaceFrameWindow`（即实际上是实现）。 若要处理这种情况可以使用多个 INTERFACE_PART 宏将映射到每个基接口`IOleInPlaceFrameWindow`接口：

在类定义文件中：

```cpp
BEGIN_INTERFACE_PART(CMyFrameWindow, IOleInPlaceFrameWindow)
```

在类实现文件中：

```cpp
BEGIN_INTERFACE_MAP(CMyWnd, CFrameWnd)
    INTERFACE_PART(CMyWnd, IID_IOleWindow, MyFrameWindow)
    INTERFACE_PART(CMyWnd, IID_IOleUIWindow, MyFrameWindow)
    INTERFACE_PART(CMyWnd, IID_IOleInPlaceFrameWindow, MyFrameWindow)
END_INTERFACE_MAP
```

该框架负责 IUnknown，因为它始终是必需的。

### <a name="interfacepart--macro-description"></a>INTERFACE_PART － 宏说明

```cpp
INTERFACE_AGGREGATE(theClass, theAggr)
```

#### <a name="parameters"></a>参数

*theClass*<br/>
包含接口映射的类的名称，

*theAggr*<br/>
要聚合的成员变量的名称。

#### <a name="remarks"></a>备注

此宏用于告知框架，类正在使用聚合对象。 它必须显示 BEGIN_INTERFACE_PART 和 END_INTERFACE_PART 宏之间。 聚合对象是单独的对象，派生自[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)。 通过使用聚合和 INTERFACE_AGGREGATE 宏，可以使聚合支持似乎由该对象直接支持的所有接口。 *TheAggr*参数是只需从派生类的成员变量的名称[IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown) （直接或间接）。 所有 INTERFACE_AGGREGATE 宏必须都遵循 INTERFACE_PART 宏放置到接口映射中时。

## <a name="see-also"></a>请参阅

[按编号列出的技术说明](../mfc/technical-notes-by-number.md)<br/>
[按类别列出的技术说明](../mfc/technical-notes-by-category.md)
