---
title: diskraid
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20aef1e5-7641-47cf-b4eb-cda117f65b6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2dfda058a7ca266adedbacf8860137c5d1782c7
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867075"
---
# <a name="diskraid"></a>diskraid



DiskRAID는 독립 (또는 저렴 한) 디스크 (RAID) 저장소 하위 시스템의 중복 배열을 구성 하 고 관리 하는 데 사용할 수 있는 명령줄 도구입니다.

RAID는 내결함성이 있는 디스크 시스템을 표준화 하 고 분류 하는 데 사용 되는 방법입니다. RAID 수준은 다양 한 성능, 안정성 및 비용을 혼합 하 여 제공 합니다. RAID는 일반적으로 서버에서 사용 됩니다. 일부 서버는 다음과 같은 세 가지 RAID 수준을 제공 합니다. 수준 0 (스트라이핑), 수준 1 (미러링) 및 수준 5 (패리티를 사용 하는 스트라이핑).

하드웨어 RAID 하위 시스템은 LUN (논리 단위 번호)을 사용 하 여 물리적으로 주소 지정 가능한 저장소 단위를 서로 구분 합니다. LUN 개체에는 하나 이상의 플렉스가 있어야 하 고 추가 플렉스 수는 제한이 없습니다. 각 플렉스는 LUN 개체의 데이터 복사본을 포함 합니다. 플렉스를 LUN 개체에 추가 하 고 제거할 수 있습니다.

대부분의 DiskRAID 명령은 특정 HBA (호스트 버스 어댑터) 포트, 초기자 어댑터, 초기자 포털, 공급자, 하위 시스템, 컨트롤러, 포트, 드라이브, LUN, 대상 포털, 대상 또는 대상 포털 그룹에 대해 작동 합니다. SELECT 명령을 사용 하 여 개체를 선택 합니다. 선택한 개체에 포커스가 있는 것으로 간주 됩니다. 포커스는 동일한 하위 시스템 내에서 여러 개의 Lun을 만드는 것과 같은 일반적인 구성 작업을 단순화 합니다.

> [!NOTE]
> DiskRAID 명령줄 도구는 VDS (가상 디스크 서비스)를 지 원하는 저장소 하위 시스템 에서만 작동 합니다.

## <a name="diskraid-commands"></a>DiskRAID 명령

명령 구문을 보려면 명령을 클릭 합니다.
-   [add](#BKMK_1)
-   [연결](#BKMK_2)
-   [automagic](#BKMK_3)
-   [break](#BKMK_4)
-   [chap](#BKMK_5)
-   [create](#BKMK_6)
-   [delete](#BKMK_7)
-   [세부 정보](#BKMK_8)
-   [분리할](#BKMK_9)
-   [exit](#BKMK_10)
-   [extend](#BKMK_11)
-   [flushcache](#BKMK_12)
-   [help](#BKMK_13)
-   [importtarget](#BKMK_14)
-   [initiator](#BKMK_15)
-   [invalidatecache](#BKMK_16)
-   [lbpolicy](#BKMK_18)
-   [list](#BKMK_19)
-   [login](#BKMK_20)
-   [logout](#BKMK_21)
-   [기간이](#BKMK_22)
-   [name](#BKMK_23)
-   [라인인](#BKMK_24)
-   [온라인](#BKMK_25)
-   [recover](#BKMK_26)
-   [다시 열거](#BKMK_27)
-   [refresh](#BKMK_28)
-   [rem](#BKMK_29)
-   [remove](#BKMK_30)
-   [replace](#BKMK_31)
-   [reset](#BKMK_32)
-   [선택](#BKMK_33)
-   [setflag](#BKMK_34)
-   [축소](#BKMK_shrink)
-   [상태의](#BKMK_35)
-   [해제할](#BKMK_36)

### <a name="BKMK_1"></a>추가

현재 선택한 LUN에 기존 LUN을 추가 하거나 현재 선택 된 iSCSI 대상 포털 그룹에 iSCSI 대상 포털을 추가 합니다.

#### <a name="syntax"></a>구문

```
add plex lun=n [noerr]
add tpgroup tportal=n [noerr]
```

#### <a name="parameters"></a>매개 변수

**플렉스 lun**=*n*

현재 선택한 LUN에 플렉스로 추가할 LUN 번호를 지정 합니다.

> [!CAUTION]
> 플렉스로 추가 되는 LUN의 모든 데이터가 삭제 됩니다.

**tpgroup 포털 새로 =** <em>n</em>

현재 선택 된 iSCSI 대상 포털 그룹에 추가할 iSCSI 대상 포털 번호를 지정 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

### <a name="BKMK_2"></a>연결

현재 선택한 LUN에 대해 지정 된 컨트롤러 포트 목록을 활성으로 설정 합니다 (다른 컨트롤러 포트는 비활성 상태임). 또는 지정 된 컨트롤러 포트를 현재 선택한 LUN의 기존 활성 컨트롤러 포트 목록에 추가 하거나 연결 합니다. 현재 선택한 LUN에 대해 지정 된 iSCSI 대상입니다.

#### <a name="syntax"></a>구문

```
associate controllers [add] <n>[,<n> [,…]]
associate ports [add] <n-m>[,<n-m>[,…]]
associate targets [add] <n>[,<n> [,…]]
```

#### <a name="parameters"></a>매개 변수

**컨트롤러용**

VDS 1.0 공급자에만 사용 됩니다. 현재 선택한 LUN에 연결 된 컨트롤러 목록을 추가 하거나 대체 합니다.

**포트**

VDS 1.1 공급자에만 사용 됩니다. 현재 선택한 LUN에 연결 된 컨트롤러 포트의 목록을 추가 하거나 대체 합니다.

**대상**

VDS 1.1 공급자에만 사용 됩니다. 현재 선택한 LUN에 연결 된 iSCSI 대상 목록을 추가 하거나 대체 합니다.

**add**

VDS 1.0 공급자의 경우 지정 된 컨트롤러를 LUN과 연결 된 컨트롤러의 기존 목록에 추가 합니다. 이 매개 변수를 지정 하지 않으면 컨트롤러 목록이이 LUN과 연결 된 기존 컨트롤러 목록을 대체 합니다.

VDS 1.1 공급자의 경우에서 LUN과 연결 된 컨트롤러 포트의 기존 목록에 지정 된 컨트롤러 포트를 추가 합니다. 이 매개 변수를 지정 하지 않으면 컨트롤러 포트 목록이이 LUN과 연결 된 컨트롤러 포트의 기존 목록을 대체 합니다.
```
<n>[,<n> [, ...]]
```
**Controller** 또는 **targets** 매개 변수와 함께 사용할 경우. 활성 또는 연결로 설정할 컨트롤러 또는 iSCSI 대상의 번호를 지정 합니다.
```
<n-m>[,<n-m>[,…]]
```
**Ports** 매개 변수와 함께 사용 합니다. 컨트롤러 번호 (*n*) 및 포트 번호 (*m*) 쌍을 사용 하 여 활성으로 설정할 컨트롤러 포트를 지정 합니다.

#### <a name="example"></a>예제

다음 예제에서는 VDS 1.1 공급자를 사용 하는 LUN에 포트를 연결 하 고 추가 하는 방법을 보여 줍니다.
```
DISKRAID> SEL LUN 5
LUN 5 is now the selected LUN.

DISKRAID> ASSOCIATE PORTS 0-0,0-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1)

DISKRAID> ASSOCIATE PORTS ADD 1-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1, Ctlr 1 Port 1)
```

### <a name="BKMK_3"></a>automagic

LUN을 구성 하는 방법에 대 한 힌트를 공급자에 게 제공 하는 플래그를 설정 하거나 해제 합니다. 매개 변수 없이 사용 **automagic** 작업은 플래그 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
automagic {set | clear | apply} all <flag=value> [<flag=value> [...]]
```

#### <a name="parameters"></a>매개 변수

**set**

지정 된 플래그를 지정 된 값으로 설정 합니다.

**clear**

지정된 플래그를 지웁니다. **All** 키워드는 모든 automagic 플래그를 지웁니다.

**적용할**

선택한 LUN에 현재 플래그를 적용 합니다.

\<플래그 >

플래그는 3 자 머리글자어로 식별 됩니다.

|플래그|설명|
|----|-----------|
|FCR|빠른 크래시 복구 필요|
|FTL|내결함성|
|MSR|주로 읽기|
|MXD|최대 드라이브|
|MXS|최대 크기가 필요 합니다.|
|ORA|최적의 읽기 맞춤|
|ORS|최적의 읽기 크기|
|OSR|순차 읽기 최적화|
|OSW|순차 쓰기 최적화|
|OWA|최적 쓰기 맞춤|
|O|최적 쓰기 크기|
|RBP|다시 빌드 우선 순위|
|RBV|Read Back Verify 사용|
|RMP|다시 매핑 사용|
|STS|스트라이프 크기|
|WTC|쓰기 가능한 캐싱 사용|
|안 K|분리|

### <a name="BKMK_4"></a>끊어야

현재 선택한 LUN에서 플렉스를 제거 합니다. 플렉스 및 포함 된 데이터는 보존 되지 않으며 드라이브 익스텐트가 회수할 수 있습니다.

#### <a name="syntax"></a>구문

```
break plex=<plex_number> [noerr]
```

#### <a name="parameters"></a>매개 변수

**플렉스로**

제거할 플렉스의 수를 지정 합니다. 이 플렉스 및 포함 된 데이터는 보존 되지 않으며,이 플렉스에서 사용 하는 리소스가 회수 됩니다. LUN에 포함 된 데이터는 일관성이 보장 되지 않습니다. 이 플렉스를 유지 하려면 볼륨 섀도 복사본 서비스 (VSS)를 사용 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

#### <a name="remarks"></a>설명

> [!NOTE]
> **Break** 명령을 사용 하기 전에 먼저 미러된 LUN을 선택 해야 합니다.

> [!CAUTION]
> 플렉스의 모든 데이터가 삭제 됩니다.

> [!CAUTION]
> 원래 LUN에 포함 된 모든 데이터는 일관성이 보장 되지 않습니다.

### <a name="BKMK_5"></a>chap

ISCSI 초기자와 iSCSI 대상이 서로 통신할 수 있도록 CHAP (Challenge 핸드셰이크 인증 프로토콜) 공유 암호를 설정 합니다.

#### <a name="syntax"></a>구문

```
chap initiator set secret=[<secret>] [target=<target>]
chap initiator remember secret=[<secret>] target=<target>
chap target set secret=[<secret>] [initiator=<initiatorname>]
chap target remember secret=[<secret>] initiator=<initiatorname>
```

#### <a name="parameters"></a>매개 변수

**개시자 집합**

초기자가 대상을 인증할 때 상호 CHAP 인증에 사용 되는 로컬 iSCSI 초기자 서비스의 공유 암호를 설정 합니다.

**개시자**

초기자 서비스에서 CHAP 인증 중 대상에 대해 자신을 인증 하기 위해 암호를 사용할 수 있도록 iSCSI 대상의 CHAP 암호를 로컬 iSCSI 초기자 서비스에 전달 합니다.

**대상 집합**

대상이 초기자를 인증할 때 CHAP 인증에 사용 되는 현재 선택 된 iSCSI 대상의 공유 암호를 설정 합니다.

**대상 명심**

는 상호 CHAP 인증 중에 초기자에 인증 하기 위해 대상이 암호를 사용할 수 있도록 iSCSI 초기자의 CHAP 암호를 현재 포커스 내 iSCSI 대상에 전달 합니다.

**기밀**

사용할 비밀을 지정 합니다. 비어 있는 경우 비밀이 지워집니다.

**target**

현재 선택 된 하위 시스템에서 암호와 연결할 대상을 지정 합니다. 개시자에 대 한 암호를 설정 하 고 종료 하는 경우 선택 사항입니다 .이는 이미 연결 된 암호가 없는 모든 대상에 대해 비밀이 사용 됨을 나타냅니다.

**initiatorname**

암호와 연결할 초기자 iSCSI 이름을 지정 합니다. 이 옵션은 대상에서 비밀을 설정 하 고 종료 하는 경우에는 해당 비밀이 아직 연결 되지 않은 모든 초기자에 대해 사용 됨을 나타냅니다.

### <a name="BKMK_6"></a>만드십시오

현재 선택한 하위 시스템에 새 LUN 또는 iSCSI 대상을 만들거나 현재 선택한 대상에 대상 포털 그룹을 만듭니다. **DiskRAID list** 명령을 사용 하 여 실제 바인딩을 볼 수 있습니다.

#### <a name="syntax"></a>구문

```
create lun simple [size=<n>] [drives=<n>] [noerr]
create lun stripe [size=<n>] [drives=<n, n> [,...]]  [stripesize=<n>] [noerr]
create lun raid [size=<n>] [drives=<n, n> [,...]] [stripesize=<n>] [noerr]
create lun mirror [size=<n>] [drives=<n, n> [,...]] [stripesize=<n>] [noerr]
create lun automagic size=<n> [noerr]
create target name=<name> [iscsiname=<iscsiname>] [noerr]
create tpgroup [noerr]
```

#### <a name="parameter"></a>매개 변수

**간단한**

단순 LUN을 만듭니다.

**스트라이프가**

스트라이프 LUN을 만듭니다.

**RAID**

패리티를 사용 하 여 스트라이프 LUN을 만듭니다.

**mirror**

미러된 LUN을 만듭니다.

**automagic**

현재 적용 되는 *automagic* 힌트를 사용 하 여 LUN을 만듭니다. 자세한 내용은 **automagic** 하위 명령을 참조 하세요.

**크기가**=

총 LUN 크기 (mb)를 지정 합니다. **Size =** 매개 변수가 지정 되지 않은 경우 생성 된 LUN은 지정 된 모든 드라이브에서 허용 하는 최대 크기입니다.

일반적으로 공급자는 최소한 요청 된 크기 만큼 큰 LUN을 만들지만, 공급자는 경우에 따라 다음으로 가장 큰 크기까지 반올림 해야 할 수 있습니다. 예를 들어 크기가. 99 GB로 지정 되 고 공급자가 GB 디스크 익스텐트만 할당할 수 있는 경우 결과 LUN은 1gb가 됩니다.

다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.
-   바이트의 **B** 입니다.
-   **Kb** 에 대 한 KB.
-   메가바이트 ( **mb** )
-   기가바이트의 경우 **gb**
-   테라바이트의 경우 **TB** 입니다.
-   페타바이트의 경우 **PB** 입니다.

**개**=

LUN을 만드는 데 사용할 드라이브의 *drive_number* 를 지정 합니다. **Size =** 매개 변수가 지정 되지 않은 경우 생성 된 LUN은 지정 된 모든 드라이브에서 허용 되는 최대 크기입니다. **Size =** 매개 변수가 지정 된 경우 공급자는 지정 된 드라이브 목록에서 드라이브를 선택 하 여 LUN을 만듭니다. 공급자는 가능 하면 지정 된 순서로 드라이브를 사용 하려고 합니다.

**stripesize**=

*스트라이프* 또는 *RAID* LUN의 크기 (mb)를 지정 합니다. LUN을 만든 후에는 stripesize를 변경할 수 없습니다.

다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.
-   바이트의 **B** 입니다.
-   **Kb** 에 대 한 KB.
-   메가바이트 ( **mb** )
-   기가바이트의 경우 **gb**
-   테라바이트의 경우 **TB** 입니다.
-   페타바이트의 경우 **PB** 입니다.

**target**

현재 선택 된 하위 시스템에 새 iSCSI 대상을 만듭니다.

**name**

대상에 대 한 친숙 한 이름을 제공 합니다.

**iscsiname**

대상에 대 한 iSCSI 이름을 제공 하며, 공급자가 이름을 생성 하도록 생략할 수 있습니다.

**tpgroup**

현재 선택한 대상에 새 iSCSI 대상 포털 그룹을 만듭니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

#### <a name="remarks"></a>설명

-   **Size**= 또는 **drives**= 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다.
-   LUN의 스트라이프 크기는 만든 후에는 변경할 수 없습니다.

### <a name="BKMK_7"></a>제거

현재 선택한 LUN, iscsi 대상 (iSCSI 대상에 연결 된 Lun이 없는 한) 또는 iSCSI 대상 포털 그룹을 삭제 합니다.

#### <a name="syntax"></a>구문

```
delete lun [uninstall] [noerr]
delete target [noerr]
delete tpgroup [noerr]
```

#### <a name="parameters"></a>매개 변수

**lun**

현재 선택한 LUN 및 모든 데이터를 삭제 합니다.

**제거할지**

Lun을 삭제 하기 전에 LUN과 연결 된 로컬 시스템의 디스크를 정리 하도록 지정 합니다.

**target**

대상에 연결 된 Lun이 없는 경우 현재 선택 된 iSCSI 대상을 삭제 합니다.

**tpgroup**

현재 선택 된 iSCSI 대상 포털 그룹을 삭제 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

### <a name="BKMK_8"></a>세부 정보

지정 된 형식의 현재 선택 된 개체에 대 한 자세한 정보를 표시 합니다.

#### <a name="syntax"></a>구문

```
Detail {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup} [verbose]
```

#### <a name="parameters"></a>매개 변수

**hbaport**

현재 선택 된 HBA (호스트 버스 어댑터) 포트에 대 한 자세한 정보를 나열 합니다.

**iadapter**

현재 선택 된 iSCSI 초기자 어댑터에 대 한 자세한 정보를 나열 합니다.

**iportal**

현재 선택한 iSCSI 초기자 포털에 대 한 자세한 정보를 나열 합니다.

**provider**

현재 선택 된 공급자에 대 한 자세한 정보를 나열 합니다.

**subsystem**

현재 선택 된 하위 시스템에 대 한 자세한 정보를 나열 합니다.

**controller**

현재 선택한 컨트롤러에 대 한 자세한 정보를 나열 합니다.

**port**

현재 선택한 컨트롤러 포트에 대 한 자세한 정보를 나열 합니다.

**drive**

현재 선택 된 드라이브에 대 한 자세한 정보를 나열 하는 Lun을 포함 합니다.

**lun**

영향을 주는 드라이브를 포함 하 여 현재 선택한 LUN에 대 한 자세한 정보를 나열 합니다. LUN이 파이버 채널 또는 iSCSI 하위 시스템의 일부 인지 여부에 따라 출력이 약간 달라 집니다. 마스크 되지 않은 호스트 목록에 별표가 있는 경우 LUN이 모든 호스트에 마스크 해제 됩니다.

**포털 새로**

현재 선택 된 iSCSI 대상 포털에 대 한 자세한 정보를 나열 합니다.

**target**

현재 선택 된 iSCSI 대상에 대 한 자세한 정보를 나열 합니다.

**tpgroup**

현재 선택 된 iSCSI 대상 포털 그룹에 대 한 자세한 정보를 나열 합니다.

**구문**

LUN 매개 변수만 사용 합니다. 플렉스를 포함 하 여 추가 정보를 나열 합니다.

### <a name="BKMK_9"></a>분리할

현재 선택한 LUN (다른 컨트롤러 포트는 영향을 받지 않음)에 대해 지정 된 컨트롤러 포트 목록을 비활성으로 설정 하거나 현재 선택한 LUN에 대해 지정 된 iSCSI 대상 목록을 분리 합니다.

#### <a name="syntax"></a>구문

```
dissociate controllers <n> [,<n> [,...]]
dissociate ports <n-m>[,<n-m>[,…]]
dissociate targets <n> [,<n> [,…]]
```

#### <a name="parameter"></a>매개 변수

**컨트롤러용**

VDS 1.0 공급자에만 사용 됩니다. 현재 선택한 LUN과 연결 된 컨트롤러 목록에서 컨트롤러를 제거 합니다.

**포트**

VDS 1.1 공급자에만 사용 됩니다. 현재 선택한 LUN과 연결 된 컨트롤러 포트 목록에서 컨트롤러 포트를 제거 합니다.

**대상**

VDS 1.1 공급자에만 사용 됩니다. 현재 선택한 LUN과 연결 된 iSCSI 대상 목록에서 대상을 제거 합니다.
```
<n> [,<n> [,…]]
```
**Controller** 또는 **targets** 매개 변수와 함께 사용할 경우. 비활성 또는 분리로 설정할 컨트롤러 또는 iSCSI 대상의 번호를 지정 합니다.
```
<n-m>[,<n-m>[,…]]
```
**Ports** 매개 변수와 함께 사용 합니다. 컨트롤러 번호 (*n*) 및 포트 번호 (*m*) 쌍을 사용 하 여 비활성으로 설정할 컨트롤러 포트를 지정 합니다.

#### <a name="example"></a>예제

```
DISKRAID> SEL LUN 5
LUN 5 is now the selected LUN.

DISKRAID> ASSOCIATE PORTS 0-0,0-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1)

DISKRAID> ASSOCIATE PORTS ADD 1-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1, Ctlr 1 Port 1)

DISKRAID> DISSOCIATE PORTS 0-0,1-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 1)
```

### <a name="BKMK_10"></a>끝낸

DiskRAID를 종료 합니다.

#### <a name="syntax"></a>구문

```
exit
```

### <a name="BKMK_11"></a>넘으면

LUN의 끝에 섹터를 추가 하 여 현재 선택한 LUN을 확장 합니다. 일부 공급자는 Lun 확장을 지원 하지 않습니다. 는 LUN에 포함 된 볼륨 또는 파일 시스템을 확장 하지 않습니다. LUN을 확장 한 후에는 **DiskPart 확장** 명령을 사용 하 여 연결 된 디스크에 연결 된 디스크 구조를 확장 해야 합니다.

#### <a name="syntax"></a>구문

```
extend lun [size=<LUN_size>] [drives=<drive_number>, [<drive_number>, ...]] [noerr]
```

#### <a name="parameters"></a>매개 변수

**크기 =**

LUN을 확장할 크기 (mb)를 지정 합니다. **Size =** 매개 변수가 지정 되지 않은 경우 LUN은 지정 된 모든 드라이브에서 허용 하는 최대 크기 만큼 확장 됩니다. **Size =** 매개 변수가 지정 된 경우 공급자는 **drives =** 매개 변수로 지정 된 목록에서 드라이브를 선택 하 여 LUN을 만듭니다.

다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.
-   바이트의 **B** 입니다.
-   **Kb** 에 대 한 KB.
-   메가바이트 ( **mb** )
-   기가바이트의 경우 **gb**
-   테라바이트 용 **TB**
-   페타바이트의 경우 **PB**

**드라이브 =**

LUN을 \<만들 때 사용할 드라이브의 drive_number >를 지정 합니다. **Size =** 매개 변수가 지정 되지 않은 경우 생성 된 LUN은 지정 된 모든 드라이브에서 허용 되는 최대 크기입니다. 공급자는 가능 하면 지정 된 순서로 드라이브를 사용 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

#### <a name="remarks"></a>설명

*Size* 또는 \<drive > 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다.

### <a name="BKMK_12"></a>flushcache

현재 선택 된 컨트롤러에 대 한 캐시를 지웁니다.

#### <a name="syntax"></a>구문

```
flushcache controller
```

### <a name="BKMK_13"></a>도움말

모든 DiskRAID 명령 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
help
```

### <a name="BKMK_14"></a>importtarget

현재 선택 된 하위 시스템에 대해 설정 된 현재 VSS (볼륨 섀도 복사본 서비스) 가져오기 대상을 검색 하거나 설정 합니다.

#### <a name="syntax"></a>구문

```
importtarget subsystem [set target]
```

#### <a name="parameter"></a>매개 변수

**대상 설정**

지정 하면 현재 선택 된 대상을 현재 선택 된 하위 시스템에 대 한 VSS 가져오기 대상으로 설정 합니다. 지정 하지 않으면 명령은 현재 선택 된 하위 시스템에 대해 설정 된 현재 VSS 가져오기 대상을 검색 합니다.

### <a name="BKMK_15"></a>초기자

로컬 iSCSI 초기자에 대 한 정보를 검색 합니다.

#### <a name="syntax"></a>구문

```
initiator
```

### <a name="BKMK_16"></a>invalidatecache

현재 선택한 컨트롤러의 캐시를 무효화 합니다.

#### <a name="syntax"></a>구문

```
invalidatecache controller
```

### <a name="BKMK_18"></a>lbpolicy

현재 선택한 LUN에 대 한 부하 분산 정책을 설정 합니다.

#### <a name="syntax"></a>구문

```
lbpolicy set lun type=<type> [paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]]
lbpolicy set lun paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]
```

#### <a name="parameters"></a>매개 변수

**type**

부하 분산 정책을 지정 합니다. 형식을 지정 하지 않은 경우에는 **path** 매개 변수를 지정 해야 합니다. 형식은 다음 중 하나일 수 있습니다.

**장애 조치**: 는 다른 경로를 백업 경로로 사용 하는 기본 경로 하나를 사용 합니다.

**라운드 로빈**: 는 각 경로를 순차적으로 시도 하는 라운드 로빈 방식으로 모든 경로를 사용 합니다.

**SUBSETROUNDROBIN**: 라운드 로빈 방식으로 모든 기본 경로를 사용 합니다. 백업 경로는 모든 기본 경로가 실패 하는 경우에만 사용 됩니다.

**DYNLQD**: 활성 요청 수가 가장 적은 경로를 사용 합니다.

**가중치**: 가중치가 가장 낮은 경로를 사용 합니다 (각 경로에 가중치를 할당 해야 함).

**LEASTBLOCKS**: 는 블록이 가장 적은 경로를 사용 합니다.

**VENDORSPECIFIC**: 공급 업체별 정책을 사용 합니다.

**경로로**

경로가 **기본** 경로 인지 아니면 특정 \<가중치를 >를 지정 합니다. 지정 되지 않은 경로는 모두 백업으로 암시적으로 설정 됩니다. 나열 된 경로는 현재 선택한 LUN의 경로 중 하나 여야 합니다.

### <a name="BKMK_19"></a>은

지정 된 형식의 개체 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
List {hbaports | iadapters | iportals | providers | subsystems | controllers | ports | drives | LUNs | tportals | targets | tpgroups}
```

#### <a name="parameters"></a>매개 변수

**hbaports**

VDS에 알려진 모든 HBA 포트에 대 한 요약 정보를 나열 합니다. 현재 선택한 HBA 포트는 별표 (*)로 표시 됩니다.

**iadapters**

VDS에 알려진 모든 iSCSI 초기자 어댑터에 대 한 요약 정보를 나열 합니다. 현재 선택 된 초기자 어댑터는 별표 (*)로 표시 됩니다.

**iportals**

현재 선택 된 초기자 어댑터의 모든 iSCSI 초기자 포털에 대 한 요약 정보를 나열 합니다. 현재 선택 된 초기자 포털은 별표 (*)로 표시 됩니다.

**providers**

VDS에 알려진 각 공급자에 대 한 요약 정보를 나열 합니다. 현재 선택 된 공급자는 별표 (*)로 표시 됩니다.

**시스템과**

시스템의 각 하위 시스템에 대 한 요약 정보를 나열 합니다. 현재 선택 된 하위 시스템은 별표 (*)로 표시 됩니다.

**컨트롤러용**

현재 선택 된 하위 시스템의 각 컨트롤러에 대 한 요약 정보를 나열 합니다. 현재 선택한 컨트롤러는 별표 (*)로 표시 됩니다.

**포트**

현재 선택한 컨트롤러의 각 컨트롤러 포트에 대 한 요약 정보를 나열 합니다. 현재 선택한 포트는 별표 (*)로 표시 됩니다.

**개**

현재 선택 된 하위 시스템의 각 드라이브에 대 한 요약 정보를 나열 합니다. 현재 선택한 드라이브는 별표 (*)로 표시 됩니다.

**lun**

현재 선택 된 하위 시스템의 각 LUN에 대 한 요약 정보를 나열 합니다. 현재 선택한 LUN은 별표 (*)로 표시 됩니다.

**tportals**

현재 선택 된 하위 시스템의 모든 iSCSI 대상 포털에 대 한 요약 정보를 나열 합니다. 현재 선택한 대상 포털은 별표 (*)로 표시 됩니다.

**대상**

현재 선택 된 하위 시스템의 모든 iSCSI 대상에 대 한 요약 정보를 나열 합니다. 현재 선택 된 대상은 별표 (*)로 표시 됩니다.

**tpgroups**

현재 선택한 대상의 모든 iSCSI 대상 포털 그룹에 대 한 요약 정보를 나열 합니다. 현재 선택 된 포털 그룹은 별표 (*)로 표시 됩니다.

### <a name="BKMK_20"></a>로그인

지정 된 iSCSI 초기자 어댑터를 현재 선택한 iSCSI 대상에 기록 합니다.

#### <a name="syntax"></a>구문

```
login target iadapter=<iadapter> [type={manual | persistent | boot}] [chap={none | oneway | mutual}] [iportal=<iportal>] [tportal=<tportal>] [<flag> [<flag> […]]]
```

#### <a name="parameters"></a>매개 변수

**type**

수행할 로그인 유형 ( **수동**, **영구**또는 **부팅**)을 지정 합니다. 지정 하지 않으면 수동 로그인이 수행 됩니다.

**수동** -수동으로 로그인 합니다.

**영구** -컴퓨터를 다시 시작 하면 자동으로 동일한 로그인을 사용 합니다.

**boot** -(이 옵션은 향후 개발을 위한 것 이며 현재 사용 되지 않습니다<em>.</em>)

**chap**

사용할 CHAP 인증의 유형 ( **none**, **oneway** chap 또는 **상호** CHAP)을 지정 합니다. 지정 되지 않은 경우 인증을 사용 하지 않습니다.

**포털 새로**

현재 선택 된 하위 시스템에서 로그인에 사용할 선택적 대상 포털을 지정 합니다.

**iportal**

지정 된 초기자 어댑터에서 로그인에 사용할 선택적인 초기자 포털을 지정 합니다.

\<플래그 >

3 자 머리글자어로 식별 됩니다.

**IP**: IPsec 필요

**EMP**: 다중 경로 사용

**EHD**: 헤더 다이제스트 사용

**EDD**: 데이터 다이제스트 사용

### <a name="BKMK_21"></a>잠금

지정 된 iSCSI 초기자 어댑터를 현재 선택 된 iSCSI 대상에서 로그 아웃 합니다.

#### <a name="syntax"></a>구문

```
logout target iadapter= <iadapter>
```

#### <a name="parameters"></a>매개 변수

**iadapter**

로그 아웃을 위한 로그인 세션이 있는 시작자 어댑터를 지정 합니다.

### <a name="BKMK_22"></a>기간이

지정 된 형식의 현재 선택 된 개체에 대 한 유지 관리 작업을 수행 합니다.

#### <a name="syntax"></a>구문

```
maintenance <object operation> [count=<iteration>]
```

#### <a name="parameters"></a>매개 변수

\<개체 >

작업을 수행할 개체 유형을 지정 합니다. *개체* 유형은 **하위 시스템**, **컨트롤러**, **포트, 드라이브** 또는 **LUN**이 될 수 있습니다.

\<작업 >

수행할 유지 관리 작업을 지정 합니다. *작업* 유형은 **spinup**, **spindown**, **blink**, **경고음** 또는 **ping**일 수 있습니다. *작업* 을 지정 해야 합니다.

**개수 =**

*작업*을 반복할 횟수를 지정 합니다. 일반적으로이는 **깜박임**, **경고음**또는 **ping**과 함께 사용 됩니다.

### <a name="BKMK_23"></a>이름의

현재 선택 된 하위 시스템, LUN 또는 iSCSI 대상의 이름을 지정 된 이름으로 설정 합니다.

#### <a name="syntax"></a>구문

```
name {subsystem | lun | target} [<name>]
```

#### <a name="parameter"></a>매개 변수

\<name>

하위 시스템, LUN 또는 대상의 이름을 지정 합니다. 이름은 64 자 미만 이어야 합니다. 이름을 제공 하지 않으면 기존 이름 (있는 경우)이 삭제 됩니다.

### <a name="BKMK_24"></a>라인인

지정 된 형식의 현재 선택 된 개체의 상태를 **오프 라인**으로 설정 합니다.

#### <a name="syntax"></a>구문

```
offline <object>
```

#### <a name="parameter"></a>매개 변수

\<개체 >

이 작업을 수행할 개체의 유형을 지정 합니다. \<개체 >

type은 **subsystem**, **controller**, **drive**, **LUN**또는 **포털 새로**일 수 있습니다.

### <a name="BKMK_25"></a>온라인

지정 된 형식의 선택한 개체 상태를 **온라인**으로 설정 합니다. 개체가 **hbaport**인 경우는 현재 선택한 HBA 포트의 경로 상태를 **온라인**으로 변경 합니다.

#### <a name="syntax"></a>구문

```
online <object> 
```

#### <a name="parameter"></a>매개 변수

\<개체 >

이 작업을 수행할 개체의 유형을 지정 합니다. \<개체 >

type은 **hbaport**, **subsystem**, **controller**, **drive**, **LUN**또는 **포털 새로**수 있습니다.

### <a name="BKMK_26"></a>확보

다시 동기화 또는 핫 절약와 같은 필요한 작업을 수행 하 여 현재 선택 된 내결함성 LUN을 복구 합니다. 예를 들어 복구로 인해 핫 스패어가 오류가 발생 한 디스크 또는 다른 디스크 익스텐트 재할당을 포함 하는 RAID 집합에 바인딩될 수 있습니다.

#### <a name="syntax"></a>구문

```
recover <lun>
```

### <a name="BKMK_27"></a>다시 열거

지정 된 형식의 개체를 다시 열거 합니다. LUN 확장 명령을 사용 하는 경우 reenumerate 명령을 사용 하기 전에 refresh 명령을 사용 하 여 디스크 크기를 업데이트 해야 합니다.

#### <a name="syntax"></a>구문

```
reenumerate {subsystems | drives}
```

#### <a name="parameters"></a>매개 변수

**시스템과**

공급자를 쿼리하여 현재 선택 된 공급자에 추가 된 새 하위 시스템을 검색 합니다.

**개**

내부 i/o 버스를 쿼리하여 현재 선택 된 하위 시스템에 추가 된 새 드라이브를 검색 합니다.

### <a name="BKMK_28"></a>고치십시오

현재 선택 된 공급자에 대 한 내부 데이터를 새로 고칩니다.

#### <a name="syntax"></a>구문

```
refresh provider
```

### <a name="BKMK_29"></a>남은

스크립트를 설명 하는 데 사용 됩니다.

#### <a name="syntax"></a>구문

```
Rem <comment>
```

### <a name="BKMK_30"></a>삭제

현재 선택한 대상 포털 그룹에서 지정 된 iSCSI 대상 포털을 제거 합니다.

#### <a name="syntax"></a>구문

```
remove tpgroup tportal=<tportal> [noerr]
```

#### <a name="parameter"></a>매개 변수

**tpgroup 포털 새로 =** \<포털 새로 >

제거할 iSCSI 대상 포털을 지정 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

### <a name="BKMK_31"></a>바꾸십시오

지정 된 드라이브를 현재 선택한 드라이브로 바꿉니다.

#### <a name="syntax"></a>구문

```
replace drive=<drive_number>
```

#### <a name="parameter"></a>매개 변수

**드라이브 =**

교체할 드라이브 \<의 drive_number >를 지정 합니다.

#### <a name="remarks"></a>설명

-   지정한 드라이브가 현재 선택 된 드라이브가 아닐 수 있습니다.

### <a name="BKMK_32"></a>다시 설정

현재 선택한 컨트롤러 또는 포트를 다시 설정 합니다.

#### <a name="syntax"></a>구문

```
Reset {controller | port}
```

#### <a name="parameters"></a>매개 변수

**controller**

컨트롤러를 다시 설정 합니다.

**port**

포트를 다시 설정 합니다.

### <a name="BKMK_33"></a>

현재 선택한 개체를 표시 하거나 변경 합니다.

#### <a name="syntax"></a>구문

```
Select {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup } [<n>]
```

#### <a name="parameters"></a>매개 변수

**object**

선택할 개체의 유형을 지정 합니다. 개체 > 유형은 공급자, 하위 시스템, 컨트롤러, 드라이브 또는 LUN이 될 수 있습니다. \<

**hbaport** [\<n >]

지정 된 로컬 HBA 포트에 포커스를 설정 합니다. HBA 포트가 지정 되지 않은 경우이 명령은 현재 선택 된 HBA 포트 (있는 경우)를 표시 합니다. 잘못 된 HBA 포트 인덱스를 지정 하면 포커스 없는 HBA 포트가 생성 되지 않습니다. HBA 포트를 선택 하면 선택 된 초기자 어댑터와 개시자 포털이 모두 선택 취소 됩니다.

**iadapter** [\<n >]

지정 된 로컬 iSCSI 초기자 어댑터에 포커스를 설정 합니다. 초기자 어댑터를 지정 하지 않으면 명령은 현재 선택 된 초기자 어댑터 (있는 경우)를 표시 합니다. 잘못 된 초기자 어댑터 인덱스를 지정 하면 포커스를 가진 초기자 어댑터가 생성 되지 않습니다. 개시자 어댑터를 선택 하면 선택한 HBA 포트와 초기자 포털이 모두 선택 취소 됩니다.

**iportal** [\<n >]

선택한 iSCSI 초기자 어댑터 내에서 지정 된 로컬 iSCSI 초기자 포털에 포커스를 설정 합니다. 초기자 포털을 지정 하지 않으면 명령은 현재 선택 된 초기자 포털 (있는 경우)을 표시 합니다. 잘못 된 초기자 포털 인덱스를 지정 하면 선택한 초기자 포털이 생성 되지 않습니다.

**공급자** [\<n >]

지정 된 공급자에 포커스를 설정 합니다. 공급자를 지정 하지 않으면 명령은 현재 선택 된 공급자 (있는 경우)를 표시 합니다. 잘못 된 공급자 인덱스를 지정 하면 포커스 없는 공급자가 발생 하지 않습니다.

**하위 시스템** [\<n >]

지정 된 하위 시스템에 포커스를 설정 합니다. 하위 시스템을 지정 하지 않으면 명령은 포커스가 있는 하위 시스템을 표시 합니다 (있는 경우). 잘못 된 하위 시스템 인덱스를 지정 하면 포커스에 없는 하위 시스템도 발생 하지 않습니다. 하위 시스템을 선택 하면 연결 된 공급자가 암시적으로 선택 됩니다.

**컨트롤러** [\<n >]

현재 선택 된 하위 시스템 내의 지정 된 컨트롤러에 포커스를 설정 합니다. 컨트롤러를 지정 하지 않으면 명령은 현재 선택한 컨트롤러 (있는 경우)를 표시 합니다. 잘못 된 컨트롤러 인덱스를 지정 하면 포커스가 없는 컨트롤러가 생성 되지 않습니다. 컨트롤러를 선택 하면 선택한 컨트롤러 포트, 드라이브, Lun, 대상 포털, 대상 및 대상 포털 그룹을 선택 취소 합니다.

**포트** [\<n >]

현재 선택한 컨트롤러 내의 지정 된 컨트롤러 포트에 포커스를 설정 합니다. 포트를 지정 하지 않으면 명령은 현재 선택 된 포트 (있는 경우)를 표시 합니다. 잘못 된 포트 인덱스를 지정 하면 선택한 포트가 생성 되지 않습니다.

**드라이브** [\<n >]

현재 선택한 하위 시스템 내의 지정 된 드라이브 또는 실제 스핀 들에 포커스를 설정 합니다. 드라이브가 지정 되지 않은 경우이 명령은 현재 선택 된 드라이브 (있는 경우)를 표시 합니다. 잘못 된 드라이브 인덱스를 지정 하면 포커스가 없는 드라이브가 생성 되지 않습니다. 드라이브를 선택 하면 선택한 컨트롤러, 컨트롤러 포트, Lun, 대상 포털, 대상 및 대상 포털 그룹의 선택이 취소 됩니다.

**lun** [\<n >]

현재 선택 된 하위 시스템 내의 지정 된 LUN에 포커스를 설정 합니다. LUN을 지정 하지 않으면 명령은 현재 선택한 LUN (있는 경우)을 표시 합니다. 잘못 된 LUN 인덱스를 지정 하면 선택한 LUN이 생성 되지 않습니다. LUN을 선택 하면 선택한 컨트롤러, 컨트롤러 포트, 드라이브, 대상 포털, 대상 및 대상 포털 그룹의 선택이 취소 됩니다.

**포털 새로** [\<n >]

현재 선택한 하위 시스템 내의 지정 된 iSCSI 대상 포털에 포커스를 설정 합니다. 대상 포털을 지정 하지 않으면 명령은 현재 선택한 대상 포털 (있는 경우)을 표시 합니다. 잘못 된 대상 포털 인덱스를 지정 하면 선택한 대상 포털이 생성 되지 않습니다. 대상 포털을 선택 하면 컨트롤러, 컨트롤러 포트, 드라이브, Lun, 대상 및 대상 포털 그룹의 선택이 취소 됩니다.

**대상** [\<n >]

현재 선택 된 하위 시스템 내의 지정 된 iSCSI 대상에 포커스를 설정 합니다. 대상이 지정 되지 않은 경우이 명령은 현재 선택 된 대상 (있는 경우)을 표시 합니다. 잘못 된 대상 인덱스를 지정 하면 대상이 선택 되지 않습니다. 대상을 선택 하면 컨트롤러, 컨트롤러 포트, 드라이브, Lun, 대상 포털 및 대상 포털 그룹의 선택이 취소 됩니다.

**tpgroup** [\<n >]

현재 선택 된 iSCSI 대상 내의 지정 된 iSCSI 대상 포털 그룹에 포커스를 설정 합니다. 대상 포털 그룹을 지정 하지 않으면 명령은 현재 선택한 대상 포털 그룹 (있는 경우)을 표시 합니다. 잘못 된 대상 포털 그룹 인덱스를 지정 하면 포커스가 없는 대상 포털 그룹이 생성 됩니다.

[\<n >]

선택할 > \<개체 번호를 지정 합니다. <object number> 지정 된가 잘못 된 경우 지정 된 형식의 개체에 대 한 모든 기존 선택 항목이 지워집니다. 을 지정 <object number> 하지 않으면 현재 개체가 표시 됩니다.

### <a name="BKMK_34"></a>setflag

현재 선택 된 드라이브를 핫 스패어로 설정 합니다.

#### <a name="syntax"></a>구문

```
setflag drive hotspare={true | false}
```

#### <a name="parameters"></a>매개 변수

**true**

핫 스패어로 현재 선택 된 드라이브를 선택 합니다.

**false**

핫 스패어로 현재 선택 된 드라이브를 선택 취소 합니다.

#### <a name="remarks"></a>설명

핫 스페어는 일반적인 LUN 바인딩 작업에 사용할 수 없습니다. 오류 처리 전용으로 예약 되어 있습니다. 드라이브가 현재 어떤 기존 LUN에도 바인딩되지 않아야 합니다.

### <a name="BKMK_shrink"></a>축소할

선택한 LUN의 크기를 줄입니다.

#### <a name="syntax"></a>구문

```
shrink lun size=<n> [noerr]
```

#### <a name="parameters"></a>매개 변수

**크기 =**

에서 LUN의 크기를 줄이기 위해 원하는 공간 크기 (mb)를 지정 합니다. 다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 인식할 수 있는 접미사 (B, KB, MB, GB, TB 및 PB) 중 하나를 사용 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 하도록 지정 합니다. 이는 스크립트 모드에서 유용 합니다.

### <a name="BKMK_35"></a>상태의

현재 선택 된 HBA (호스트 버스 어댑터) 포트의 경로 상태를 대기 중으로 변경 합니다.

#### <a name="syntax"></a>구문

```
standby hbaport
```

#### <a name="parameters"></a>매개 변수

**hbaport**

현재 선택 된 HBA (호스트 버스 어댑터) 포트의 경로 상태를 대기 중으로 변경 합니다.

### <a name="BKMK_36"></a>해제할

지정 된 호스트에서 현재 선택한 Lun에 액세스할 수 있도록 설정 합니다.

#### <a name="syntax"></a>구문

```
unmask LUN {all | none | [add] wwn=<hexadecimal_number> [;<hexadecimal_number> [;…]] | [add] initiator=<initiator>[;<initiator>[;…]]} [uninstall]
```

#### <a name="parameters"></a>매개 변수

**all**

모든 호스트에서 LUN에 액세스할 수 있도록 지정 합니다. 그러나 iSCSI 하위 시스템에서 모든 대상에 대 한 LUN의 마스크를 해제할 수는 없습니다.

> [!IMPORTANT]
> 마스크 모두 해제 명령을 실행 하기 전에 대상의 로그를 해제 해야 합니다.

**none**

모든 호스트에서 LUN에 액세스할 수 없도록 지정 합니다.

> [!IMPORTANT]
> 마스크 해제 LUN 없음 명령을 실행 하기 전에 대상의 로그를 해제 해야 합니다.

**add**

지정 된 호스트를이 LUN에 액세스할 수 있는 호스트의 기존 목록에 추가 하도록 지정 합니다. 이 매개 변수를 지정 하지 않으면 제공 된 호스트 목록이이 LUN에 액세스할 수 있는 기존 호스트 목록을 대체 합니다.

**WWN =**

LUN 또는 호스트에 액세스할 수 있어야 하는 wwpn (wide name)을 나타내는 16 진수 목록을 지정 합니다. 파이버 채널 하위 시스템의 특정 호스트 집합에 마스크/마스크 해제 하려면 관심 있는 호스트 컴퓨터의 포트에 대해 세미콜론으로 구분 된 WWN 목록을 입력 하면 됩니다.

**시작자 =**

현재 선택한 LUN에 액세스할 수 있어야 하는 iSCSI 초기자 목록을 지정 합니다. ISCSI 하위 시스템의 특정 호스트 집합에 마스크/마스크 해제 하려면 관심 있는 호스트 컴퓨터에서 초기자에 대 한 iSCSI 초기자 이름 목록을 세미콜론으로 구분 하 여 입력 하면 됩니다.

**제거할지**

지정 하는 경우 LUN이 마스킹 되기 전에 로컬 시스템에서 LUN과 연결 된 디스크를 제거 합니다.

## <a name="scripting-diskraid"></a>DiskRAID 스크립팅

DiskRAID는 연결 된 VDS 하드웨어 공급자를 사용 하 여 Windows Server 2008 또는 Windows Server 2003를 실행 하는 모든 컴퓨터에서 스크립팅할 수 있습니다. DiskRAID 스크립트를 호출 하려면 명령 프롬프트에서 다음을 입력 합니다.
```
diskraid /s <script.txt>
```
기본적으로 DiskRAID는 명령 처리를 중지 하 고 스크립트에 문제가 있는 경우 오류 코드를 반환 합니다. 스크립트를 계속 실행 하 고 오류를 무시 하려면 명령에 NOERR 매개 변수를 포함 합니다. 이는 단일 스크립트를 사용 하 여 총 Lun 수에 관계 없이 하위 시스템의 모든 Lun을 삭제 하는 것과 같은 유용한 방법을 허용 합니다. 모든 명령이 NOERR 매개 변수를 지 원하는 것은 아닙니다. NOERR 매개 변수를 포함 했는지 여부에 관계 없이 오류는 항상 명령 구문 오류에서 반환 됩니다.

### <a name="diskraid-error-codes"></a>DiskRAID 오류 코드

|오류 코드|오류 설명|
|----------|-----------------|
|0|오류가 발생 하지 않았습니다. 전체 스크립트가 오류 없이 실행 되었습니다.|
|1|치명적인 예외가 발생 했습니다.|
|2|DiskRAID 명령줄에 지정 된 인수가 잘못 되었습니다.|
|3|DiskRAID에서 지정 된 스크립트나 출력 파일을 열 수 없습니다.|
|4|서비스 DiskRAID 중 하나에서 오류를 반환 했습니다.|
|5|명령 구문 오류가 발생 했습니다. 개체가 잘못 선택 되었거나이 명령과 함께 사용 하기에 적합 하지 않아 스크립트가 실패 했습니다.|

## <a name="example-interactively-view-status-of-subsystem"></a>예: 대화형으로 하위 시스템의 상태 보기

컴퓨터에서 하위 시스템 0의 상태를 확인 하려면 명령줄에 다음을 입력 합니다.
```
diskraid
```
Enter 키를 누릅니다. 다음이 표시 됩니다.
```
Microsoft Diskraid version 5.2.xxxx
Copyright (©) 2003 Microsoft Corporation
On computer: COMPUTER_NAME
```
하위 시스템 0을 선택 하려면 DiskRAID 프롬프트에 다음을 입력 합니다.
```
select subsystem 0
```
Enter 키를 누릅니다. 다음과 유사한 출력이 표시 됩니다.
```
Subsystem 0 is now the selected subsystem.

DISKRAID> list drives

  Drive ###  Status      Health          Size      Free    Bus  Slot  Flags
  ---------  ----------  ------------  --------  --------  ---  ----  -----
  Drive 0    Online      Healthy         107 GB    107 GB    0     1
  Drive 1    Offline     Healthy          29 GB     29 GB    1     0
  Drive 2    Online      Healthy         107 GB    107 GB    0     2
  Drive 3    Not Ready   Healthy          19 GB     19 GB    1     1
```
DiskRAID를 종료 하려면 DiskRAID 프롬프트에 다음을 입력 합니다.
```
exit
```