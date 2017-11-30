---
title: "ICorDebugProcess5::EnumerateHeap 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugProcess5.EnumerateHeap
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugProcess5::EnumerateHeap
helpviewer_keywords:
- EnumerateHeap method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeap method [.NET Framework debugging]
ms.assetid: b0192104-6073-4089-a4df-dc29ee033074
topic_type: apiref
caps.latest.revision: "6"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 41cd7d47650cdfe6a3598ba126be489107181a44
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugprocess5enumerateheap-method"></a><span data-ttu-id="b8c3b-102">ICorDebugProcess5::EnumerateHeap 方法</span><span class="sxs-lookup"><span data-stu-id="b8c3b-102">ICorDebugProcess5::EnumerateHeap Method</span></span>
<span data-ttu-id="b8c3b-103">托管堆上获取对象的枚举数。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-103">Gets an enumerator for the objects on the managed heap.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b8c3b-104">语法</span><span class="sxs-lookup"><span data-stu-id="b8c3b-104">Syntax</span></span>  
  
```  
HRESULT EnumerateHeap(  
    [out] ICorDebugHeapEnum **ppObjects  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="b8c3b-105">参数</span><span class="sxs-lookup"><span data-stu-id="b8c3b-105">Parameters</span></span>  
 `ppObject`  
 <span data-ttu-id="b8c3b-106">[out]指向的地址的指针[ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md)接口对象，它驻留在托管堆对象的枚举数。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-106">[out] A pointer to the address of an [ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md) interface object that is an enumerator for the objects that reside on the managed heap.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b8c3b-107">备注</span><span class="sxs-lookup"><span data-stu-id="b8c3b-107">Remarks</span></span>  
 <span data-ttu-id="b8c3b-108">之前调用`ICorDebugProcess5::EnumerateHeap`方法时，应调用[icordebugprocess5:: Getgcheapinformation](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getgcheapinformation-method.md)方法并检查的值的`areGCStructuresValid`字段返回[COR_HEAPINFO](../../../../docs/framework/unmanaged-api/debugging/cor-heapinfo-structure.md)要确保其当前状态中的垃圾回收堆是可枚举对象。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-108">Before calling the `ICorDebugProcess5::EnumerateHeap` method, you should call the [ICorDebugProcess5::GetGCHeapInformation](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getgcheapinformation-method.md) method and examine the value of the `areGCStructuresValid` field of the returned [COR_HEAPINFO](../../../../docs/framework/unmanaged-api/debugging/cor-heapinfo-structure.md) object to ensure that the garbage collection heap in its current state is enumerable.</span></span> <span data-ttu-id="b8c3b-109">此外，`ICorDebugProcess5::EnumerateHeap`返回`E_FAIL`如果，则附加过早的生存期内的过程中，内存之前为分配托管的堆。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-109">In addition, the `ICorDebugProcess5::EnumerateHeap` returns `E_FAIL` if you attach too early in the lifetime of the process, before memory for the managed heap is allocated.</span></span>  
  
 <span data-ttu-id="b8c3b-110">[ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md)接口对象是从使您能够枚举 ICorDebugEnum 接口派生的标准枚举器[COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md)对象。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-110">The [ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md) interface object is a standard enumerator derived from the ICorDebugEnum interface that allows you to enumerate [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) objects.</span></span> <span data-ttu-id="b8c3b-111">此方法填充[ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md)具有集合对象[COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md)提供信息有关的所有对象的实例。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-111">This method populates the [ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md) collection object with [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) instances that provide information about all objects.</span></span> <span data-ttu-id="b8c3b-112">集合还可能包括[COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md)提供有关对象的不按任何根路径信息的实例对象，但未收集垃圾回收器。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-112">The collection may also include [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) instances that provide information about objects that are not rooted by any object but have not yet been collected by the garbage collector.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b8c3b-113">要求</span><span class="sxs-lookup"><span data-stu-id="b8c3b-113">Requirements</span></span>  
 <span data-ttu-id="b8c3b-114">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="b8c3b-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b8c3b-115">**标头：** CorDebug.idl、 CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="b8c3b-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="b8c3b-116">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b8c3b-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b8c3b-117">**.NET framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b8c3b-117">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b8c3b-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b8c3b-118">See Also</span></span>  
 [<span data-ttu-id="b8c3b-119">ICorDebugProcess5 接口</span><span class="sxs-lookup"><span data-stu-id="b8c3b-119">ICorDebugProcess5 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-interface.md)  
 [<span data-ttu-id="b8c3b-120">调试接口</span><span class="sxs-lookup"><span data-stu-id="b8c3b-120">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)