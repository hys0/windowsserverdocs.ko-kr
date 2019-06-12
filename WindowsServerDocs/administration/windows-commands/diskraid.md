---
title: diskraid
description: '에 대 한 Windows 명령을 항목 * * *- '
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
ms.openlocfilehash: 7ebd65fb56114bff9e6ae4b6a76376561c686dfa
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439560"
---
# <a name="diskraid"></a>diskraid



DiskRAID는 구성 하 고 독립적인 (또는 저렴 한) 디스크 (RAID) 저장소 하위 시스템의 중복 배열을 관리할 수 있는 명령줄 도구입니다.

RAID는 표준화 하 고 내결함성이 있는 디스크 시스템을 분류 하는 데 사용 하는 메서드입니다. RAID 수준 성능, 안정성 및 비용의 다양 한 조합 하 여 제공 합니다. RAID은 서버에서 주로 사용 됩니다. 일부 서버 RAID 수준 중 3 개를 제공합니다. 수준 0 (스트라이핑), 수준 (미러링), 1 및 수준 5 (패리티가 있는 스트라이프).

하드웨어 RAID 하위 시스템 논리 단위 번호 (LUN)를 사용 하 여 다른 물리적으로 주소 지정 가능 저장소 단위를 구분 합니다. LUN 개체를 하나 이상의 복합 있고 임의 개수의 추가 플렉스를 가질 수 있습니다. 각 복합 LUN 개체에 있는 데이터의 복사본을 포함 합니다. 플렉스를 추가 하 고 LUN 개체에서 제거할 수 있습니다.

대부분의 DiskRAID 명령을 특정 호스트 버스 어댑터 (HBA) 포트, 초기자 어댑터, 초기자 포털, 공급자, 하위 시스템, 컨트롤러, 포트, 드라이브, LUN, 대상 포털, 대상 또는 대상 포털 그룹에서 작동합니다. 선택 명령을 사용 하 여 개체를 선택 합니다. 포커스가 있는 선택된 된 개체 라고 합니다. 포커스 같은 하위 시스템 내에서 여러 Lun 만들기와 같은 일반적인 구성 태스크를 간소화 합니다.

> [!NOTE]
> DiskRAID 명령줄 도구 가상 디스크 서비스 (VDS)를 지 원하는 저장소 하위 시스템 에서만 작동 합니다.

## <a name="diskraid-commands"></a>DiskRAID 명령

명령 구문을 보려면에서 명령을 클릭 합니다.
-   [add](#BKMK_1)
-   [associate](#BKMK_2)
-   [automagic](#BKMK_3)
-   [break](#BKMK_4)
-   [chap](#BKMK_5)
-   [create](#BKMK_6)
-   [delete](#BKMK_7)
-   [detail](#BKMK_8)
-   [dissociate](#BKMK_9)
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
-   [maintenance](#BKMK_22)
-   [name](#BKMK_23)
-   [offline](#BKMK_24)
-   [online](#BKMK_25)
-   [recover](#BKMK_26)
-   [reenumerate](#BKMK_27)
-   [refresh](#BKMK_28)
-   [rem](#BKMK_29)
-   [remove](#BKMK_30)
-   [replace](#BKMK_31)
-   [reset](#BKMK_32)
-   [select](#BKMK_33)
-   [setflag](#BKMK_34)
-   [shrink](#BKMK_shrink)
-   [standby](#BKMK_35)
-   [unmask](#BKMK_36)

### <a name="BKMK_1"></a>add

현재 선택 된 LUN에 기존 LUN을 추가 하거나 현재 선택 된 iSCSI 대상 포털 그룹에는 iSCSI 대상 포털을 추가 합니다.

#### <a name="syntax"></a>구문

```
add plex lun=n [noerr]
add tpgroup tportal=n [noerr]
```

#### <a name="parameters"></a>매개 변수

**복합 lun**=*n*

현재 선택한 LUN 플렉스를 추가 하는 LUN 번호를 지정 합니다.

> [!CAUTION]
> 플렉스로 추가 되 고 LUN에 있는 모든 데이터가 삭제 됩니다.

**tpgroup tportal=** <em>n</em>

현재 선택 된 iSCSI 대상 포털 그룹에 추가 하려면 iSCSI 대상 포털 번호를 지정 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시할지를 지정 합니다. 스크립트 모드에서 유용합니다.

### <a name="BKMK_2"></a>associate

포트를 설정 합니다 컨트롤러의 지정된 된 목록으로 활성 (포트 비활성 내용이 다른 컨트롤러), 현재 선택 된 LUN에 대 한 현재 선택 된 LUN에 대 한 기존 활성 컨트롤러 포트 목록에 지정 된 컨트롤러 포트를 추가 또는 연결 된 현재 선택 된 LUN에 대해 지정 된 iSCSI 대상입니다.

#### <a name="syntax"></a>구문

```
associate controllers [add] <n>[,<n> [,…]]
associate ports [add] <n-m>[,<n-m>[,…]]
associate targets [add] <n>[,<n> [,…]]
```

#### <a name="parameters"></a>매개 변수

**controllers**

VDS 1.0 공급자만 사용 합니다. 에 추가 하거나 현재 선택 된 LUN에 연관 된 컨트롤러 목록을 대체 합니다.

**ports**

VDS 1.1 공급자만 사용 합니다. 에 추가 하거나 현재 선택 된 LUN에 연관 된 컨트롤러 포트 목록을 대체 합니다.

**targets**

VDS 1.1 공급자만 사용 합니다. 에 추가 하거나 현재 선택 된 LUN과 연결 된 iSCSI 대상 목록을 대체 합니다.

**add**

VDS 1.0 공급자에 대 한 LUN과 사용 하 여 연결 된 컨트롤러의 기존 목록에 지정 된 컨트롤러를 추가 합니다. 이 매개 변수를 지정 하지 않으면이 LUN과 사용 하 여 연결 된 컨트롤러의 기존 목록 컨트롤러 목록을 대체 합니다.

VDS 1.1 공급자에 대 한 LUN과 사용 하 여 연결 된 컨트롤러 포트의 기존 목록에 지정 된 컨트롤러 포트를 추가 합니다. 이 매개 변수를 지정 하지 않으면이 LUN과 사용 하 여 연결 된 컨트롤러 포트의 기존 목록 컨트롤러 포트 목록을 대체 합니다.
```
<n>[,<n> [, ...]]
```
사용 된 **컨트롤러** 또는 **대상** 매개 변수입니다. 활성 또는 연결로 설정 하는 iSCSI 대상 컨트롤러의 번호를 지정 합니다.
```
<n-m>[,<n-m>[,…]]
```
사용 된 **포트** 매개 변수입니다. 설정할 컨트롤러 번호를 사용 하 여 활성 컨트롤러 포트를 지정 합니다 (*n*) 및 포트 번호 (*m*) 쌍입니다.

#### <a name="example"></a>예제

다음 예제에서는 연결 포트 VDS 1.1 공급자를 사용 하는 LUN에 추가 하는 방법을 보여 줍니다.
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

설정 하거나 LUN을 구성 하는 방법에 대 한 공급자에 힌트를 제공 하는 플래그를 지웁니다. 매개 변수 없이 사용 합니다 **오토 매직** 작업 플래그의 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
automagic {set | clear | apply} all <flag=value> [<flag=value> [...]]
```

#### <a name="parameters"></a>매개 변수

**set**

지정된 된 값으로 지정된 된 플래그를 설정합니다.

**clear**

지정된 된 플래그를 지웁니다. 합니다 **모든** 키워드 모든 오토 매직 플래그를 지웁니다.

**apply**

선택한 LUN에 현재 플래그를 적용합니다.

\<flag>

플래그는 3 자 약어도 식별 됩니다.

|Flag|설명|
|----|-----------|
|FCR|빠른 크래시 복구가 필요|
|FTL|내결함성|
|MSR|대부분 읽기|
|MXD|최대 드라이브|
|MXS|예상 최대 크기|
|ORA|최적의 읽기 맞춤|
|ORS|최적의 읽기 크기|
|OSR|순차 읽기에 대 한 최적화|
|OSW|순차적 쓰기 최적화|
|OWA|최적의 쓰기 맞춤|
|O|최적의 쓰기 크기|
|RBP|우선 순위를 다시 작성|
|RBV|읽기를 다시 확인 사용|
|RMP|사용 하도록 설정 하는 매핑 변경|
|STS|스트라이프 크기|
|WTC|Write-through 캐싱을 사용 하도록 설정|
|YNK|이동식|

### <a name="BKMK_4"></a>break

현재 선택한 LUN에서 플렉스를 제거합니다. 플렉스 및 포함 된 데이터를 유지 하지 되 고 드라이브 범위를 확보할 수 있습니다.

#### <a name="syntax"></a>구문

```
break plex=<plex_number> [noerr]
```

#### <a name="parameters"></a>매개 변수

**plex**

제거할 복합 횟수를 지정 합니다. 플렉스 및 포함 된 데이터를 보존 되지 않습니다 하 고 사용 하는이 복합 리소스를 회수 됩니다. LUN에 포함 된 데이터는 일관 되도록 보장 되지 않습니다. 이 복합 유지 하려는 경우 볼륨 섀도 복사본 서비스 (VSS)를 사용 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시할지를 지정 합니다. 스크립트 모드에서 유용합니다.

#### <a name="remarks"></a>설명

> [!NOTE]
> 미러된 LUN을 사용 하기 전에 먼저 선택 해야 합니다 **중단** 명령입니다.

> [!CAUTION]
> 플렉스의 모든 데이터가 삭제 됩니다.

> [!CAUTION]
> 원본 LUN에 포함 된 모든 데이터가 일관 되도록 보장 되지 않습니다.

### <a name="BKMK_5"></a>chap

ISCSI 초기자와 iSCSI 대상 서로 통신할 수 있도록 핸드셰이크 인증 프로토콜 (CHAP (Challenge) 공유 비밀 설정 합니다.

#### <a name="syntax"></a>구문

```
chap initiator set secret=[<secret>] [target=<target>]
chap initiator remember secret=[<secret>] target=<target>
chap target set secret=[<secret>] [initiator=<initiatorname>]
chap target remember secret=[<secret>] initiator=<initiatorname>
```

#### <a name="parameters"></a>매개 변수

**초기자 설정**

초기자가 대상 하는 경우 상호 CHAP 인증에 사용 되는 로컬 iSCSI 초기자 서비스에서 공유 암호를 설정 합니다.

**초기자 기억**

시작자 서비스 CHAP 인증 하는 동안 대상에 자체 인증을 위해 암호를 사용할 수 있도록 로컬 iSCSI 초기자 서비스는 iSCSI 대상의 CHAP 암호를 전달 합니다.

**대상 집합**

대상이 초기자를 인증 하는 경우 CHAP 인증을 위해 사용 되는 현재 선택 된 iSCSI 대상 공유 암호를 설정 합니다.

**대상 기억**

대상 상호 CHAP 인증 중 시작자에 게 자체 인증 하기 위해 암호를 사용할 수 있도록 현재 포커스 내 iSCSI 대상에는 iSCSI 초기자 CHAP 암호를 전달 합니다.

**secret**

사용 하 여 암호를 지정 합니다. 비어 있는 경우 암호는 지워집니다.

**target**

암호를 사용 하 여 연결 하려면 현재 선택한 하위 시스템에는 대상을 지정 합니다. 초기자에서 암호를 설정 하는 경우이 선택 사항이 며 연결된 암호를 이미 있지 않은 모든 대상에 대 한 암호를 사용 함을 나타냅니다을 제외.

**initiatorname**

암호를 사용 하 여 연결 하는 초기자 iSCSI 이름을 지정 합니다. 대상에서 암호를 설정 하는 경우이 선택 사항이 며 연결된 암호를 이미 있지 않은 모든 초기자에 대 한 암호를 사용 함을 나타냅니다을 제외 합니다.

### <a name="BKMK_6"></a>create

현재 선택한 하위 시스템에서 새 LUN 또는 iSCSI 대상을 만들거나 현재 선택한 대상에 대상 포털 그룹을 만듭니다. 사용 하 여 실제 바인딩이 볼 수 있습니다 합니다 **DiskRAID 목록** 명령입니다.

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

**simple**

간단한 LUN을 만듭니다.

**stripe**

스트라이프 LUN을 만듭니다.

**RAID**

패리티가 있는 스트라이프 LUN을 만듭니다.

**mirror**

미러된 LUN을 만듭니다.

**automagic**

사용 하 여 LUN을 만듭니다는 *오토 매직* 현재에서 힌트입니다. 참조 된 **오토 매직** 자세한 하위 명령.

**size**=

총 LUN 크기를 메가바이트 단위로 지정합니다. 경우는 **크기 =** 매개 변수를 지정 하지 않으면 생성 LUN 가능한 최대 크기 지정 된 모든 드라이브에서 허용 됩니다.

공급자를 일반적으로 LUN을 적어도 요청된 된 크기 만큼 크지 만들지만 공급자 경우도 다음 최대 크기에 맞게 반올림 해야 할 수 있습니다. 예를 들어.99 GB 및 공급자 수 GB 디스크 익스텐트 할당만으로 크기 지정 된 경우 결과 LUN 1GB는 것입니다.

다른 단위를 사용 하 여 크기를 지정 하려면 크기 직후 다음 인식 된 접미사 중 하나를 사용 합니다.
-   **B** 바이트에 대 한 합니다.
-   **KB** 킬로바이트에 대 한 합니다.
-   **MB** 메가바이트에 대 한 합니다.
-   **GB** 기가바이트에 대 한 합니다.
-   **TB** 테라바이트에 대 한 합니다.
-   **PB** 페타바이트에 대 한 합니다.

**drives**=

지정 된 *drive_number* 드라이브의 LUN을 만드는 데 있습니다. 경우는 **크기 =** 매개 변수를 지정 하지 않으면 생성 LUN은 지정 된 모든 드라이브에서 허용 가능한 최대 크기입니다. 경우는 **크기 =** 공급자 드라이브를 LUN을 만들려면 지정 된 드라이브 목록에서 선택, 매개 변수를 지정 합니다. 공급자는 가능한 경우 지정한 순서에 따라 드라이브를 사용 하려고 합니다.

**stripesize**=

크기를 메가바이트 단위로 지정 된 *스트라이프* 하거나 *RAID* LUN. stripesize LUN이 만들어지면 변경할 수 없습니다.

다른 단위를 사용 하 여 크기를 지정 하려면 크기 직후 다음 인식 된 접미사 중 하나를 사용 합니다.
-   **B** 바이트에 대 한 합니다.
-   **KB** 킬로바이트에 대 한 합니다.
-   **MB** 메가바이트에 대 한 합니다.
-   **GB** 기가바이트에 대 한 합니다.
-   **TB** 테라바이트에 대 한 합니다.
-   **PB** 페타바이트에 대 한 합니다.

**target**

현재 선택한 하위 시스템에 새 iSCSI 대상을 만듭니다.

**name**

대상에 대 한 친숙 한 이름을 제공합니다.

**iscsiname**

이름을 생성 하는 제공 된 iSCSI 대상에 대 한 이름을 지정 하 고 공급자를 생략할 수 있습니다.

**tpgroup**

현재 선택한 대상에 새 iSCSI 대상 포털 그룹을 만듭니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시할지를 지정 합니다. 스크립트 모드에서 유용합니다.

#### <a name="remarks"></a>설명

-   중 하나는 **크기**= 또는 **드라이브**= 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다 수 있습니다.
-   만든 후 LUN에 대 한 스트라이프 크기를 변경할 수 없습니다.

### <a name="BKMK_7"></a>delete

현재 선택 된 LUN, iSCSI 대상 (한 가지 iSCSI 대상과 사용 하 여 연결 하지 Lun) 또는 iSCSI 대상 포털 그룹을 삭제 합니다.

#### <a name="syntax"></a>구문

```
delete lun [uninstall] [noerr]
delete target [noerr]
delete tpgroup [noerr]
```

#### <a name="parameters"></a>매개 변수

**lun**

현재 선택한 LUN 및 모든 데이터가 삭제 됩니다.

**uninstall**

LUN을 삭제 하기 전에 연결 LUN과 로컬 시스템에 디스크를 정리할 수를 지정 합니다.

**target**

현재 선택 된 iSCSI 대상 Lun이 없습니다 대상에 연결 된 경우 삭제 합니다.

**tpgroup**

현재 선택 된 iSCSI 대상 포털 그룹을 삭제합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시할지를 지정 합니다. 스크립트 모드에서 유용합니다.

### <a name="BKMK_8"></a>detail

지정 된 형식의 현재 선택한 개체에 대 한 자세한 정보를 표시 합니다.

#### <a name="syntax"></a>구문

```
Detail {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup} [verbose]
```

#### <a name="parameters"></a>매개 변수

**hbaport**

현재 선택 된 호스트 버스 어댑터 (HBA) 포트에 대 한 자세한 정보를 나열 합니다.

**iadapter**

현재 선택 된 iSCSI 초기자 어댑터에 대 한 자세한 정보를 나열 합니다.

**iportal**

현재 선택 된 iSCSI 초기자 포털에 대 한 자세한 정보를 나열 합니다.

**provider**

현재 선택한 공급자에 대 한 자세한 정보를 나열 합니다.

**subsystem**

현재 선택한 하위 시스템에 대 한 자세한 정보를 나열 합니다.

**controller**

현재 선택 된 컨트롤러에 대 한 자세한 정보를 나열 합니다.

**port**

현재 선택 된 컨트롤러 포트에 대 한 자세한 정보를 나열 합니다.

**drive**

이동 Lun을 포함 하 여 현재 선택 된 드라이브에 대 한 자세한 정보를 나열 합니다.

**lun**

목록 세부 정보는 영향을 주는 포함 하 여 현재 선택 된 LUN 구동 합니다. 출력은 LUN의 파이버 채널 또는 iSCSI 하위 시스템의 일부 인지 여부에 따라 약간 다릅니다. 마스크 해제 된 호스트 목록 별표만 들어 있으면이 LUN 모든 호스트에 마스크 되지 않음을 의미 합니다.

**tportal**

현재 선택 된 iSCSI 대상 포털에 대 한 자세한 정보를 나열 합니다.

**target**

현재 선택 된 iSCSI 대상에 대 한 자세한 정보를 나열 합니다.

**tpgroup**

현재 선택 된 iSCSI 대상 포털 그룹에 대 한 자세한 정보를 나열 합니다.

**verbose**

LUN 매개 변수로 사용할 수 있습니다. 해당 플렉스를 포함 한 추가 정보를 나열 합니다.

### <a name="BKMK_9"></a>dissociate

(포트 받지 않으며 다른 컨트롤러), 현재 선택 된 LUN에 대 한 비활성으로 지정 된 컨트롤러 포트 목록을 집합 또는 현재 선택 된 LUN에 대해 지정된 된 iSCSI 대상 목록을 분리 합니다.

#### <a name="syntax"></a>구문

```
dissociate controllers <n> [,<n> [,...]]
dissociate ports <n-m>[,<n-m>[,…]]
dissociate targets <n> [,<n> [,…]]
```

#### <a name="parameter"></a>매개 변수

**controllers**

VDS 1.0 공급자만 사용 합니다. 현재 선택 된 LUN에 연관 된 컨트롤러 목록에서 컨트롤러를 제거 합니다.

**ports**

VDS 1.1 공급자만 사용 합니다. 현재 선택 된 LUN에 연관 된 컨트롤러 포트 목록에서 컨트롤러 포트를 제거 합니다.

**targets**

VDS 1.1 공급자만 사용 합니다. 현재 선택 된 LUN과 연결 된 iSCSI 대상의 목록에서 대상을 제거 합니다.
```
<n> [,<n> [,…]]
```
사용 된 **컨트롤러** 또는 **대상** 매개 변수입니다. 컨트롤러 또는 비활성으로 설정 하거나 분리 하려면 iSCSI 대상의 번호를 지정 합니다.
```
<n-m>[,<n-m>[,…]]
```
사용 된 **포트** 매개 변수입니다. 컨트롤러 번호를 사용 하 여 비활성으로 설정 하려면 컨트롤러 포트를 지정 합니다 (*n*) 및 포트 번호 (*m*) 쌍입니다.

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

### <a name="BKMK_10"></a>exit

DiskRAID를 종료합니다.

#### <a name="syntax"></a>구문

```
exit
```

### <a name="BKMK_11"></a>extend

섹터 LUN의 끝에 추가 하 여 현재 선택한 LUN을 확장 합니다. 일부 공급자는 Lun 확장을 지원 합니다. 모든 볼륨 또는 LUN에 포함 된 파일 시스템 확장 되지 않습니다. LUN을 확장 한 후 연결 된 디스크에 구조를 사용 하 여 확장 해야 합니다 **DiskPart 확장** 명령입니다.

#### <a name="syntax"></a>구문

```
extend lun [size=<LUN_size>] [drives=<drive_number>, [<drive_number>, ...]] [noerr]
```

#### <a name="parameters"></a>매개 변수

**size=**

LUN을 확장 하는 메가바이트 단위로 크기를 지정 합니다. 경우는 **크기 =** 매개 변수를 지정 하지 않으면 지정 된 모든 드라이브에서 허용 가능한 최대 크기에 따라 LUN 확장 됩니다. 경우는 **크기 =** 매개 변수가 지정 된, 공급자에서 지정 된 목록에서 드라이브를 선택 합니다 **드라이브 =** LUN을 만들려면 매개 변수.

다른 단위를 사용 하 여 크기를 지정 하려면 크기 직후 다음 인식 된 접미사 중 하나를 사용 합니다.
-   **B** 바이트에 대 한 합니다.
-   **KB** 킬로바이트에 대 한 합니다.
-   **MB** 메가바이트에 대 한 합니다.
-   **GB** 기가바이트에 대 한 합니다.
-   **TB** 테라바이트에 대 한
-   **PB** 페타바이트에 대 한

**drives=**

지정 된 \<drive_number > 드라이브의 LUN을 만들 때 사용 하도록 합니다. 경우는 **크기 =** 매개 변수를 지정 하지 않으면 생성 LUN은 지정 된 모든 드라이브에서 허용 가능한 최대 크기입니다. 가능한 경우 지정한 순서에 따라 드라이브를 사용 하는 공급자입니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 해야 함을 지정 합니다. 스크립트 모드에서 유용합니다.

#### <a name="remarks"></a>설명

중 하나는 *크기* 또는 \<드라이브 > 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다 수 있습니다.

### <a name="BKMK_12"></a>flushcache

현재 선택 된 컨트롤러에서 캐시를 지웁니다.

#### <a name="syntax"></a>구문

```
flushcache controller
```

### <a name="BKMK_13"></a>help

모든 DiskRAID 명령 목록을 표시합니다.

#### <a name="syntax"></a>구문

```
help
```

### <a name="BKMK_14"></a>importtarget

검색 하거나 현재 선택한 하위 시스템에 대해 설정 된 현재 볼륨 섀도 복사본 서비스 (VSS) 가져오기 대상을 설정 합니다.

#### <a name="syntax"></a>구문

```
importtarget subsystem [set target]
```

#### <a name="parameter"></a>매개 변수

**집합 대상**

지정 하면 현재 선택한 하위 시스템에 대 한 VSS 가져오기 대상에 현재 선택한 대상을 설정 합니다. 지정 하지 않으면이 명령은 현재 선택한 하위 시스템에 대해 설정 된 현재 VSS 가져오기 대상을 검색 합니다.

### <a name="BKMK_15"></a>initiator

로컬 iSCSI 초기자에 대 한 정보를 검색합니다.

#### <a name="syntax"></a>구문

```
initiator
```

### <a name="BKMK_16"></a>invalidatecache

현재 선택 된 컨트롤러에서 캐시를 무효화합니다.

#### <a name="syntax"></a>구문

```
invalidatecache controller
```

### <a name="BKMK_18"></a>lbpolicy

현재 선택 된 LUN에 부하 분산 정책을 설정합니다.

#### <a name="syntax"></a>구문

```
lbpolicy set lun type=<type> [paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]]
lbpolicy set lun paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]
```

#### <a name="parameters"></a>매개 변수

**type**

부하 분산 정책을 지정합니다. 형식을 지정 하지 않으면 해당 **경로** 매개 변수를 지정 해야 합니다. 형식에는 다음 중 하나일 수 있습니다.

**장애 조치**: 백업 경로 되 고 다른 경로 사용 하 여 하나의 기본 경로 사용 합니다.

**ROUNDROBIN**: 각 경로 순차적으로 시도 하는 라운드 로빈 방식으로 모든 경로 사용 합니다.

**SUBSETROUNDROBIN**: 모든 기본 경로 사용 하 여 라운드 로빈 방식으로; 백업 경로 모든 주 경로가 실패할 경우에 사용 됩니다.

**DYNLQD**: 가장을 사용 하 여 경로 사용 하 여 활성 요청 수입니다.

**가중치**: (각 경로 할당 해야 가중치) 최소 가중치를 사용 하 여 경로 사용 합니다.

**LEASTBLOCKS**: 최소 블록을 사용 하 여 경로 사용 합니다.

**VENDORSPECIFIC**: 공급 업체 특정 정책을 사용합니다.

**paths**

경로 인지 여부를 지정 **주** 되었거나 특정 \<가중치 >. 지정 되지 않은 모든 경로 백업으로 암시적으로 설정 됩니다. 나열 된 모든 경로 현재 선택 된 LUN의 경로 중 하나 여야 합니다.

### <a name="BKMK_19"></a>list

지정 된 형식의 개체 목록을 표시합니다.

#### <a name="syntax"></a>구문

```
List {hbaports | iadapters | iportals | providers | subsystems | controllers | ports | drives | LUNs | tportals | targets | tpgroups}
```

#### <a name="parameters"></a>매개 변수

**hbaports**

VDS에 알려진 모든 HBA 포트에 대 한 요약 정보를 나열 합니다. 현재 선택 된 HBA 포트에 별표 (*)가 표시 됩니다.

**iadapters**

VDS에 알려진 모든 iSCSI 초기자 어댑터에 대 한 요약 정보를 나열 합니다. 현재 선택 된 초기자 어댑터에 별표 (*)가 표시 됩니다.

**iportals**

현재 선택 된 초기자 어댑터의 모든 iSCSI 초기자 포털에 대 한 요약 정보를 나열합니다. 현재 선택 된 초기자 포털에 별표 (*)가 표시 됩니다.

**providers**

VDS에 각 공급자에 대 한 요약 정보를 나열 합니다. 현재 선택한 공급자에 별표 (*)가 표시 됩니다.

**subsystems**

시스템의 각 하위 시스템에 대 한 요약 정보를 나열합니다. 현재 선택한 하위 시스템에 별표 (*)가 표시 됩니다.

**controllers**

현재 선택한 하위 시스템에서 각 컨트롤러에 대 한 요약 정보를 나열 합니다. 현재 선택한 컨트롤러에 별표 (*)가 표시 됩니다.

**ports**

현재 선택한 컨트롤러의 각 컨트롤러 포트에 대 한 요약 정보를 나열합니다. 현재 선택된 된 포트에 별표 (*)가 표시 됩니다.

**drives**

현재 선택한 하위 시스템의 각 드라이브에 대 한 요약 정보를 나열 합니다. 현재 선택된 된 드라이브에 별표 (*)가 표시 됩니다.

**luns**

현재 선택한 하위 시스템에서 각 LUN에 대 한 요약 정보를 나열합니다. 현재 선택 된 LUN에 별표 (*)가 표시 됩니다.

**tportals**

현재 선택한 하위 시스템의 모든 iSCSI 대상 포털에 대 한 요약 정보를 나열합니다. 현재 선택한 대상 포털에 별표 (*)가 표시 됩니다.

**targets**

현재 선택한 하위 시스템의 모든 iSCSI 대상에 대 한 요약 정보를 나열합니다. 현재 선택한 대상에 별표 (*)가 표시 됩니다.

**tpgroups**

현재 선택한 대상의 모든 iSCSI 대상 포털 그룹에 대 한 요약 정보를 나열합니다. 현재 선택한 포털 그룹에 별표 (*)가 표시 됩니다.

### <a name="BKMK_20"></a>login

현재 선택 된 iSCSI 대상에 지정 된 iSCSI 초기자 어댑터를 기록합니다.

#### <a name="syntax"></a>구문

```
login target iadapter=<iadapter> [type={manual | persistent | boot}] [chap={none | oneway | mutual}] [iportal=<iportal>] [tportal=<tportal>] [<flag> [<flag> […]]]
```

#### <a name="parameters"></a>매개 변수

**type**

수행 하는 로그인의 유형을 지정 합니다. **수동**를 **영구**, 또는 **부팅**합니다. 지정 하지 않으면 수동 로그인이 수행 됩니다.

**수동** -로그인 수동으로.

**영구** -자동으로 컴퓨터를 다시 시작할 때 동일한 로그인을 사용 합니다.

**부트** -(이 옵션은 향후 개발을 위한 이며 현재 사용 되지 않습니다<em>.</em>)

**chap**

사용할 CHAP 인증의 유형을 지정: **none**를 **oneway** CHAP 또는 **상호** CHAP; 인증 안 함 지정 되지 않은 경우 사용 됩니다.

**tportal**

로그인에 사용할 현재 선택한 하위 시스템에는 선택적 대상 포털을 지정 합니다.

**iportal**

로그인에 사용할 지정 된 초기자 어댑터의 선택적 초기자 포털을 지정 합니다.

\<flag>

세 글자 약어를 구분 합니다.

**IPS**: IPsec이 필요

**EMP**: 다중 경로 사용

**EHD**: 헤더 요약을 사용 하도록 설정

**EDD**: 데이터 요약을 사용 하도록 설정

### <a name="BKMK_21"></a>logout

현재 선택 된 iSCSI 대상에서 지정한 iSCSI 초기자 어댑터를 기록합니다.

#### <a name="syntax"></a>구문

```
logout target iadapter= <iadapter>
```

#### <a name="parameters"></a>매개 변수

**iadapter**

로그 아웃 하도록 로그인 세션과 초기자 어댑터를 지정합니다.

### <a name="BKMK_22"></a>maintenance

지정 된 형식의 현재 선택한 개체에서 유지 관리 작업을 수행합니다.

#### <a name="syntax"></a>구문

```
maintenance <object operation> [count=<iteration>]
```

#### <a name="parameters"></a>매개 변수

\<object>

작업을 수행 하는 개체의 형식을 지정 합니다. *개체* 형식 수를 **하위 시스템**를 **컨트롤러**, **포트, 드라이브** 또는 **LUN**합니다.

\<operation>

유지 관리 작업 수행을 지정 합니다. *작업* 형식이 될 수 있습니다 **spinup**를 **spindown**를 **깜박임**를 **경고음** 또는 **ping** . *작업* 지정 해야 합니다.

**count=**

반복 횟수를 지정 합니다 *작업*합니다. 일반적으로 사용 되어 **깜박임**를 **경고음**, 또는 **ping**합니다.

### <a name="BKMK_23"></a>name

현재 선택한 하위 시스템, LUN 또는 iSCSI 대상의 이름이 지정된 된 이름으로 설정합니다.

#### <a name="syntax"></a>구문

```
name {subsystem | lun | target} [<name>]
```

#### <a name="parameter"></a>매개 변수

\<name>

하위 시스템, LUN 또는 대상에 대 한 이름을 지정합니다. 이름 길이 보다 작거나 64 자 여야 합니다. 이름을 제공 하지 않으면, 기존 이름이 있는 경우 삭제 됩니다.

### <a name="BKMK_24"></a>offline

지정 된 형식의 현재 선택한 개체의 상태를 설정 **오프 라인**합니다.

#### <a name="syntax"></a>구문

```
offline <object>
```

#### <a name="parameter"></a>매개 변수

\<object>

이 작업을 수행 하는 개체의 형식을 지정 합니다. \<개체 >

형식은 될 수 있습니다 **하위 시스템**를 **컨트롤러**를 **드라이브**를 **LUN**, 또는 **포털**합니다.

### <a name="BKMK_25"></a>online

지정 된 형식의 선택한 개체의 상태를 설정 **온라인**합니다. 개체가 있으면 **hbaport**를 현재 선택된 된 HBA 포트에 경로의 상태를 변경 **온라인**합니다.

#### <a name="syntax"></a>구문

```
online <object> 
```

#### <a name="parameter"></a>매개 변수

\<object>

이 작업을 수행 하는 개체의 형식을 지정 합니다. \<개체 >

형식이 될 수 있습니다 **hbaport**를 **하위 시스템**를 **컨트롤러**를 **드라이브**를 **LUN**, 또는  **포털**합니다.

### <a name="BKMK_26"></a>recover

현재 선택한 내결함성 LUN을 복구 하려면 다시 동기화 또는 핫 프로세스인 등 필요한 작업을 수행 합니다. 예를 들어, 복구를 핫 스패어 바인딩할 않을 실패 한 디스크 또는 다른 디스크 범위 재할당 RAID 집합입니다.

#### <a name="syntax"></a>구문

```
recover <lun>
```

### <a name="BKMK_27"></a>reenumerate

지정 된 형식의 개체를 reenumerates입니다. LUN 명령 확장을 사용 하는 경우 다시 나열 명령을 사용 하기 전에 디스크 크기를 업데이트 하려면 새로 고침 명령을 사용 해야 합니다.

#### <a name="syntax"></a>구문

```
reenumerate {subsystems | drives}
```

#### <a name="parameters"></a>매개 변수

**subsystems**

현재 선택한 공급자에 추가 된 새 하위 키를 검색할 공급자를 쿼리 합니다.

**drives**

현재 선택한 하위 시스템에 추가 된 모든 새 드라이브를 검색할 내부 I/O 버스를 쿼리 합니다.

### <a name="BKMK_28"></a>refresh

현재 선택 된 공급자에 대 한 내부 데이터를 새로 고칩니다.

#### <a name="syntax"></a>구문

```
refresh provider
```

### <a name="BKMK_29"></a>rem

스크립트를 설명 하는 데 사용 합니다.

#### <a name="syntax"></a>구문

```
Rem <comment>
```

### <a name="BKMK_30"></a>remove

현재 선택한 대상 포털 그룹에서 지정 된 iSCSI 대상 포털을 제거합니다.

#### <a name="syntax"></a>구문

```
remove tpgroup tportal=<tportal> [noerr]
```

#### <a name="parameter"></a>매개 변수

**tpgroup tportal=** \<tportal>

제거할 iSCSI 대상 포털을 지정 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시 해야 함을 지정 합니다. 스크립트 모드에서 유용합니다.

### <a name="BKMK_31"></a>replace

현재 선택된 된 드라이브를 사용 하 여 지정된 된 드라이브를 대체합니다.

#### <a name="syntax"></a>구문

```
replace drive=<drive_number>
```

#### <a name="parameter"></a>매개 변수

**drive=**

지정 된 \<drive_number > 교체 드라이브에 대 한 합니다.

#### <a name="remarks"></a>설명

-   지정된 된 드라이브에 현재 선택된 된 드라이브를 사용할 수 없습니다.

### <a name="BKMK_32"></a>reset

현재 선택한 컨트롤러 또는 포트를 다시 설정합니다.

#### <a name="syntax"></a>구문

```
Reset {controller | port}
```

#### <a name="parameters"></a>매개 변수

**controller**

컨트롤러를 다시 설정합니다.

**port**

포트를 다시 설정합니다.

### <a name="BKMK_33"></a>select

표시 하거나 현재 선택한 개체를 변경 합니다.

#### <a name="syntax"></a>구문

```
Select {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup } [<n>]
```

#### <a name="parameters"></a>매개 변수

**object**

선택할 개체의 형식을 지정 합니다. 합니다 \<개체 > 형식이 될 수 있습니다 **공급자**, **하위 시스템**를 **컨트롤러**를 **드라이브**, 또는 **LUN**.

**hbaport** [\<n>]

지정된 된 로컬 HBA 포트에 포커스를 설정 합니다. 없는 HBA 포트를 지정 하는 경우 (해당 되는 경우) 명령은 현재 선택 된 HBA 포트를 표시 합니다. 잘못 된 HBA 포트 인덱스를 지정 하는 없습니다 포커스 내에서 HBA 포트에 발생 합니다. 모든 선택한 초기자 어댑터 및 초기자 포털 HBA 포트를 선택 하면 선택 취소 합니다.

**iadapter** [\<n>]

지정 된 로컬 iSCSI 초기자 어댑터에 포커스를 설정합니다. 초기자 어댑터가 지정 된 경우 (해당 되는 경우) 명령은 현재 선택 된 초기자 어댑터를 표시 합니다. 잘못 된 초기자 어댑터 인덱스 지정 포커스 초기자 어댑터가 없습니다 발생 합니다. 모든 선택된 된 HBA 포트 및 초기자 포털 초기자 어댑터를 선택 하면 선택 취소 합니다.

**iportal** [\<n>]

선택한 iSCSI 초기자 어댑터 내에서 지정 된 로컬 iSCSI 초기자 포털에 포커스를 설정합니다. 초기자 포털 없음이 지정 된 경우 (해당 되는 경우) 명령은 현재 선택 된 초기자 포털을 표시 합니다. 잘못 된 초기자 포털 인덱스를 지정 하는 없는 선택한 초기자 포털에서 발생 합니다.

**provider** [\<n>]

지정된 된 공급자에 포커스를 설정합니다. 없는 공급자를 지정 하는 경우 (해당 되는 경우) 명령은 현재 선택 된 공급자를 표시 합니다. 포커스 내 공급자가 없습니다 발생 잘못 된 공급자 인덱스를 지정 합니다.

**subsystem** [\<n>]

지정 된 하위 시스템에 포커스를 설정합니다. 하위 시스템이 지정 된 경우 (해당 되는 경우) 명령 포커스가 있는 하위 시스템을 표시 합니다. 포커스 내 하위 시스템이 잘못 된 하위 시스템 인덱스를 지정 하 하면 됩니다. 하위 시스템을 암시적으로 선택 하면 연결된 공급자를 선택 합니다.

**controller** [\<n>]

현재 선택한 하위 시스템 내에서 지정 된 컨트롤러 포커스를 설정합니다. 컨트롤러 없음이 지정 된 경우 (해당 되는 경우) 명령은 현재 선택 된 컨트롤러를 표시 합니다. 잘못 된 컨트롤러 인덱스 지정 포커스 컨트롤러 없음 발생 합니다. 컨트롤러를 선택 하면 선택한 컨트롤러 포트, 드라이브, Lun, 대상 포털, 대상 및 대상 포털 그룹을 선택 취소 합니다.

**port** [\<n>]

현재 선택한 컨트롤러 내에서 지정 된 컨트롤러 포트에 포커스를 설정합니다. 지정 된 포트가 없는 경우 (해당 되는 경우) 명령은 현재 선택된 된 포트를 표시 합니다. 잘못 된 포트 인덱스를 지정 하는 없는 선택한 포트에서 발생 합니다.

**drive** [\<n>]

지정한 드라이브 또는 현재 선택 된 하위 시스템 내에서 실제 스핀 들에 포커스를 설정합니다. 드라이브를 지정 하는 경우 (해당 되는 경우) 명령은 현재 선택된 된 드라이브를 표시 합니다. 잘못 된 드라이브 인덱스를 지정 하는 포커스 드라이브에서 발생 합니다. 드라이브를 선택 하면 선택한 컨트롤러, 컨트롤러 포트, Lun, 대상 포털, 대상 및 대상 포털 그룹을 선택 취소 합니다.

**lun** [\<n>]

현재 선택한 하위 시스템 내에서 지정 된 LUN에 포커스를 설정 합니다. 없는 LUN을 지정 하는 경우 명령 (있는 경우) 현재 선택 된 LUN을 표시 합니다. 잘못 된 LUN 인덱스를 지정 하는 선택한 없는 LUN에 발생 합니다. LUN을 선택 하면 선택한 컨트롤러, 컨트롤러 포트, 드라이브, 대상 포털, 대상 및 대상 포털 그룹을 선택 취소 합니다.

**tportal** [\<n>]

현재 선택한 하위 시스템 내에서 지정 된 iSCSI 대상 포털에 포커스를 설정합니다. 대상 포털 없음이 지정 된 경우 명령 (있는 경우) 현재 선택한 대상 포털을 표시 합니다. 잘못 된 대상 포털 인덱스를 지정 하는 없는 선택한 대상 포털에서 발생 합니다. 대상 포털을 선택 하면 모든 컨트롤러, 컨트롤러 포트, 드라이브, Lun, 대상 및 대상 포털 그룹을 선택 취소 합니다.

**target** [\<n>]

현재 선택한 하위 시스템 내에서 지정 된 iSCSI 대상에 포커스를 설정합니다. 대상이 지정 된 경우 (해당 되는 경우) 명령은 현재 선택 된 대상을 표시 합니다. 잘못 된 대상 인덱스를 지정 합니다. 선택한 대상이 없습니다. 발생 합니다. 대상 선택 컨트롤러, 컨트롤러 포트, 드라이브, Lun, 대상 포털 및 대상 포털 그룹을 선택 취소 합니다.

**tpgroup** [\<n>]

지정 된 iSCSI 대상 포털 내의 그룹은 현재 선택 된 iSCSI 대상에 포커스를 설정 합니다. 대상 포털 그룹 없음이 지정 된 경우 명령은 현재 선택 된 대상 포털 그룹 (있는 경우)를 표시 합니다. 포커스 내 대상 포털 그룹 없음 결과 잘못 된 대상 포털 그룹 인덱스를 지정 하 합니다.

[\<n>]

지정는 \<수 개체 >를 선택 합니다. 경우는 <object number> 지정 유효 하지 않은 기존 선택 영역에 지정 된 형식의 개체에 대 한 선택이 취소 됩니다. 없으면 <object number> 지정, 현재 개체가 표시 됩니다.

### <a name="BKMK_34"></a>setflag

현재 선택된 된 드라이브를 핫 스패어로 설정합니다.

#### <a name="syntax"></a>구문

```
setflag drive hotspare={true | false}
```

#### <a name="parameters"></a>매개 변수

**true**

핫 스패어로 현재 선택된 된 드라이브를 선택합니다.

**false**

핫 스패어로 현재 선택된 된 드라이브를 선택 취소 합니다.

#### <a name="remarks"></a>설명

일반 LUN 바인딩 작업에 대 한 핫 스패어를 사용할 수 없습니다. 오류만 처리 되도록 지정 되어 있습니다. 모든 기존 LUN에 드라이브를 현재 바인딩할 수 있어야 합니다.

### <a name="BKMK_shrink"></a>shrink

선택한 LUN의 크기를 줄입니다.

#### <a name="syntax"></a>구문

```
shrink lun size=<n> [noerr]
```

#### <a name="parameters"></a>매개 변수

**size=**

원하는 양의 공간 (mb) LUN의 크기를 줄이기 위해으로 지정 합니다. 다른 단위를 사용 하 여 크기를 지정 하려면 크기 직후 인식된 접미사 (B, KB, MB, GB, TB 및 PB) 중 하나를 사용 합니다.

**noerr**

이 작업을 수행 하는 동안 발생 하는 모든 오류를 무시할지를 지정 합니다. 스크립트 모드에서 유용합니다.

### <a name="BKMK_35"></a>standby

현재 선택 된 호스트 버스 어댑터 (HBA) 포트 대기 경로의 상태를 변경합니다.

#### <a name="syntax"></a>구문

```
standby hbaport
```

#### <a name="parameters"></a>매개 변수

**hbaport**

현재 선택 된 호스트 버스 어댑터 (HBA) 포트 대기 경로의 상태를 변경합니다.

### <a name="BKMK_36"></a>unmask

지정된 된 호스트에서 액세스할 수 있는 현재 선택 된 Lun을 만듭니다.

#### <a name="syntax"></a>구문

```
unmask LUN {all | none | [add] wwn=<hexadecimal_number> [;<hexadecimal_number> [;…]] | [add] initiator=<initiator>[;<initiator>[;…]]} [uninstall]
```

#### <a name="parameters"></a>매개 변수

**all**

LUN 수 있도록 모든 호스트에서 액세스할 수를 지정 합니다. 그러나 iSCSI 하위 시스템의 모든 대상 LUN를 마스크 해제할 수 없습니다.

> [!IMPORTANT]
> 모든 마스크 해제 명령을 실행 하기 전에 대상의 로그 아웃을 해야 합니다.

**없음**

LUN은 임의의 호스트에 액세스할 수 없습니다 지정 합니다.

> [!IMPORTANT]
> UNMASK LUN NONE 명령을 실행 하기 전에 대상의 로그 아웃을 해야 합니다.

**add**

지정 된 호스트를이 LUN에서 액세스할 수 있는 호스트의 기존 목록에 추가 되어야 함을 지정 합니다. 이 매개 변수를 지정 하지 않으면이 LUN에서 액세스할 수 있는 호스트의 기존 목록을 제공 하는 호스트의 목록이 바뀝니다.

**WWN=**

16 진수 숫자는 LUN을 호스트 해야 액세스할 수는 전 세계 이름을 나타내는 목록을 지정 합니다. 마스크/마스크 해제할 호스트 파이버 채널 하위 시스템의 특정 집합을 관심 호스트 컴퓨터에서 세미콜론으로 구분 된 목록을 WWN의 포트를 입력할 수 있습니다.

**initiator=**

ISCSI 초기자는 현재 선택한 LUN은 내게 필요한 옵션의 목록을 지정 합니다. 마스크/마스크 해제할 iSCSI 하위 시스템에서 호스트의 특정 집합을 관심 있는 호스트 컴퓨터에서 초기자에 대 한 iSCSI 초기자 이름의 세미콜론으로 구분 된 목록을 입력할 수 있습니다.

**uninstall**

를 지정 하는 경우에 LUN 마스킹 전에 로컬 시스템에서 LUN과 연결 된 디스크를 제거 합니다.

## <a name="scripting-diskraid"></a>DiskRAID 스크립팅

DiskRAID 연결된 VDS 하드웨어 공급자를 사용 하 여 Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 스크립팅할 수 있습니다. 명령 프롬프트에서 입력 DiskRAID 스크립트를 호출 합니다.
```
diskraid /s <script.txt>
```
기본적으로 DiskRAID 명령 처리를 중지 하 고 스크립트에 문제가 없는 경우에 오류 코드를 반환 합니다. 계속 하려면 스크립트를 실행 하 고 오류를 무시 명령에 디스크 매개 변수를 포함 합니다. 단일 스크립트를 사용 하 여 Lun의 총 수에 관계 없이 하위 시스템의 모든 Lun을 삭제 하려면 이러한 유용한 사례를 허용 합니다. 모든 명령은 디스크 크기를 지원합니다. 오류는 디스크 크기를 포함 하는 여부에 관계 없이 명령 구문 오류 발생 시 항상 반환 됩니다.

### <a name="diskraid-error-codes"></a>DiskRAID 오류 코드

|오류 코드|오류 설명|
|----------|-----------------|
|0|오류가 발생 했습니다. 전체 스크립트가 오류 없이 실행 합니다.|
|1|치명적인 예외가 발생 했습니다.|
|2|DiskRAID 명령줄에 지정 된 인수가 잘못 되었습니다.|
|3|DiskRAID 지정한 스크립트 또는 출력 파일을 열 수 없습니다.|
|4|사용 하 여 DiskRAID 서비스 중 하나는 오류를 반환 합니다.|
|5|명령 구문 오류가 발생 했습니다. 스크립트에 개체를 잘못 선택 않거나 해당 명령 사용 하 여 사용 하기에 적합 하지 않아서 실패 했습니다.|

## <a name="example-interactively-view-status-of-subsystem"></a>예: 대화형으로 하위 시스템의 상태를 보려면

컴퓨터에 0 하위 시스템의 상태를 확인 하려는 경우 명령줄에서 다음을 입력 합니다.
```
diskraid
```
Enter 키를 누릅니다. 다음 표시 됩니다.
```
Microsoft Diskraid version 5.2.xxxx
Copyright (©) 2003 Microsoft Corporation
On computer: COMPUTER_NAME
```
하위 시스템 0을 선택 하려면 DiskRAID 프롬프트에서 다음을 입력:
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
DiskRAID를 종료 하려면 DiskRAID 프롬프트에서 다음을 입력 합니다.
```
exit
```