---
title: Diskraid
description: 독립 (또는 저렴 한) 디스크 (RAID) 저장소 하위 시스템의 중복 배열을 구성 하 고 관리할 수 있는 Diskraid 명령줄 도구에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20aef1e5-7641-47cf-b4eb-cda117f65b6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0745c708878fa9da6571666b5702b4408976164
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924766"
---
# <a name="diskraid"></a>Diskraid

**Diskraid** 는 독립 (또는 저렴 한) 디스크 (RAID) 저장소 하위 시스템의 중복 배열을 구성 하 고 관리 하는 데 사용할 수 있는 명령줄 도구입니다.

RAID는 일반적으로 내결함성 디스크 시스템을 표준화 하 고 범주화 하기 위해 서버에서 사용 됩니다. RAID 수준은 다양 한 성능, 안정성 및 비용을 혼합 하 여 제공 합니다. 일부 서버는 수준 0 (스트라이핑), 수준 1 (미러링) 및 수준 5 (패리티를 사용 하는 스트라이핑)의 세 가지 RAID 수준을 제공 합니다.

하드웨어 RAID 하위 시스템은 LUN (논리 단위 번호)을 사용 하 여 물리적으로 주소 지정 가능한 저장소 단위를 서로 구분 합니다. LUN 개체에는 하나 이상의 플렉스가 있어야 하 고 추가 플렉스 수는 제한이 없습니다. 각 플렉스는 LUN 개체의 데이터 복사본을 포함 합니다. 플렉스를 LUN 개체에 추가 하 고 제거할 수 있습니다.

대부분의 Diskraid 명령은 특정 HBA (호스트 버스 어댑터) 포트, 초기자 어댑터, 초기자 포털, 공급자, 하위 시스템, 컨트롤러, 포트, 드라이브, LUN, 대상 포털, 대상 또는 대상 포털 그룹에 대해 작동 합니다. **Select** 명령을 사용 하 여 개체를 선택 합니다. 선택한 개체에 포커스가 있는 것으로 간주 됩니다. 포커스는 동일한 하위 시스템 내에서 여러 개의 Lun을 만드는 것과 같은 일반적인 구성 작업을 단순화 합니다.

> [!NOTE]
> Diskraid 명령줄 도구는 VDS (가상 디스크 서비스)를 지 원하는 저장소 하위 시스템 에서만 작동 합니다.

## <a name="diskraid-commands"></a>Diskraid 명령

다음 명령은 Diskraid 도구 내에서 사용할 수 있습니다.

### <a name="add"></a>add

현재 선택한 LUN에 기존 LUN을 추가 하거나 현재 선택 된 iSCSI 대상 포털 그룹에 iSCSI 대상 포털을 추가 합니다.

#### <a name="syntax"></a>구문

```
add plex lun=n [noerr]
add tpgroup tportal=n [noerr]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 플렉스 lun =`<n>` | 현재 선택한 LUN에 플렉스로 추가할 LUN 번호를 지정 합니다. 주의: 플렉스로 추가 되는 LUN의 모든 데이터가 삭제 됩니다. |
| tpgroup 포털 새로 =`<n>` | 현재 선택 된 iSCSI 대상 포털 그룹에 추가할 iSCSI 대상 포털 번호를 지정 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="associate"></a>연결

현재 선택한 LUN의 지정 된 컨트롤러 포트 목록을 활성으로 설정 합니다 (다른 컨트롤러 포트는 비활성 상태임). 또는 현재 선택한 lun의 기존 활성 컨트롤러 포트 목록에 지정 된 컨트롤러 포트를 추가 하거나 현재 선택한 LUN에 대해 지정 된 iSCSI 대상을 연결 합니다.

#### <a name="syntax"></a>구문

```
associate controllers [add] <n>[,<n> [,…]]
associate ports [add] <n-m>[,<n-m>[,…]]
associate targets [add] <n>[,<n> [,…]]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| Controller | 현재 선택한 LUN에 연결 된 컨트롤러 목록을 추가 하거나 대체 합니다. VDS 1.0 공급자와만 사용 합니다. |
| ports | 현재 선택한 LUN에 연결 된 컨트롤러 포트의 목록을 추가 하거나 대체 합니다. VDS 1.1 공급자와만 사용 합니다. |
| 대상 | 현재 선택한 LUN에 연결 된 iSCSI 대상 목록을 추가 하거나 대체 합니다. VDS 1.1 공급자와만 사용 합니다. |
| add | **VDS 1.0 공급자를 사용 하는 경우:** 지정 된 컨트롤러를 LUN과 연결 된 컨트롤러의 기존 목록에 추가 합니다. 이 매개 변수를 지정 하지 않으면 컨트롤러 목록이이 LUN과 연결 된 기존 컨트롤러 목록을 대체 합니다.<p>**VDS 1.1 공급자를 사용 하는 경우:** 지정 된 컨트롤러 포트를 LUN과 연결 된 컨트롤러 포트의 기존 목록에 추가 합니다. 이 매개 변수를 지정 하지 않으면 컨트롤러 포트 목록이이 LUN과 연결 된 컨트롤러 포트의 기존 목록을 대체 합니다. |
| `<n>[,<n> [, ...]]` | **Controller** 또는 **targets** 매개 변수와 함께 사용 합니다. 활성 또는 연결로 설정할 컨트롤러 또는 iSCSI 대상의 번호를 지정 합니다. |
| `<n-m>[,<n-m>[,…]]` | **Ports** 매개 변수와 함께 사용 합니다. 컨트롤러 번호 (*n*) 및 포트 번호 (*m*) 쌍을 사용 하 여 활성으로 설정할 컨트롤러 포트를 지정 합니다. |

#### <a name="example"></a>예제

VDS 1.1 공급자를 사용 하는 LUN에 포트를 연결 하 고 추가 하려면:

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

### <a name="automagic"></a>automagic

LUN을 구성 하는 방법에 대 한 힌트를 공급자에 게 제공 하는 플래그를 설정 하거나 해제 합니다. 매개 변수 없이 사용 **automagic** 작업은 플래그 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
automagic {set | clear | apply} all <flag=value> [<flag=value> [...]]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| set | 지정 된 플래그를 지정 된 값으로 설정 합니다. |
| 지우기 | 지정된 플래그를 지웁니다. **All** 키워드는 모든 automagic 플래그를 지웁니다. |
| apply | 선택한 LUN에 현재 플래그를 적용 합니다. |
| `<flag>` | 플래그는 다음을 포함 하 여 3 자 약어로 식별 됩니다.<ul><li>**Fcr** -빠른 크래시 복구 필요</li><li>**Ftl** -내결함성</li><li>**MSR** -대부분 읽기</li><li>**Mxd** -최대 드라이브</li><li>**Mxs** -최대 크기가 필요 합니다.</li><li>**ORA** -최적 읽기 맞춤</li><li>**ORS** -최적 읽기 크기</li><li>**OSR** -순차 읽기 최적화</li><li>**Osw** -순차적 쓰기를 위한 최적화</li><li> **OWA** -최적의 쓰기 맞춤</li><li>**O** -최적 쓰기 크기</li><li>**Rbp** -다시 빌드 우선 순위</li><li>**RBV** -다시 읽기 확인 사용</li><li>**Rmp** -다시 매핑 사용</li><li>**STS** -스트립 크기</li><li>**Wtc** -쓰기-쓰기 캐싱 사용</li><li>안 **k** -이동식</li></ul> |

### <a name="break"></a>break

현재 선택한 LUN에서 플렉스를 제거 합니다. 플렉스 및 포함 된 데이터는 보존 되지 않으며 드라이브 익스텐트가 회수할 수 있습니다.

> [!CAUTION]
> 이 명령을 사용 하기 전에 먼저 미러된 LUN을 선택 해야 합니다. 플렉스의 모든 데이터가 삭제 됩니다. 원래 LUN에 포함 된 모든 데이터는 일관성이 보장 되지 않습니다.

#### <a name="syntax"></a>구문

```
break plex=<plex_number> [noerr]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 플렉스로 | 제거할 플렉스의 수를 지정 합니다. 이 플렉스 및 포함 된 데이터는 보존 되지 않으며,이 플렉스에서 사용 하는 리소스가 회수 됩니다. LUN에 포함 된 데이터는 일관성이 보장 되지 않습니다. 이 플렉스를 유지 하려면 볼륨 섀도 복사본 서비스 (VSS)를 사용 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="chap"></a>chap

ISCSI 초기자와 iSCSI 대상이 서로 통신할 수 있도록 CHAP (Challenge 핸드셰이크 인증 프로토콜) 공유 암호를 설정 합니다.

#### <a name="syntax"></a>구문

```
chap initiator set secret=[<secret>] [target=<target>]
chap initiator remember secret=[<secret>] target=<target>
chap target set secret=[<secret>] [initiator=<initiatorname>]
chap target remember secret=[<secret>] initiator=<initiatorname>
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 개시자 집합 | 초기자가 대상을 인증할 때 상호 CHAP 인증에 사용 되는 로컬 iSCSI 초기자 서비스의 공유 암호를 설정 합니다. |
| 개시자 | 초기자 서비스에서 CHAP 인증 중 대상에 대해 자신을 인증 하기 위해 암호를 사용할 수 있도록 iSCSI 대상의 CHAP 암호를 로컬 iSCSI 초기자 서비스에 전달 합니다. |
| 대상 집합 | 대상이 초기자를 인증할 때 CHAP 인증에 사용 되는 현재 선택 된 iSCSI 대상의 공유 암호를 설정 합니다. |
| 대상 명심 | 는 상호 CHAP 인증 중에 초기자에 인증 하기 위해 대상이 암호를 사용할 수 있도록 iSCSI 초기자의 CHAP 암호를 현재 포커스 내 iSCSI 대상에 전달 합니다. |
| secret | 사용할 비밀을 지정 합니다. 비어 있는 경우 비밀이 지워집니다. |
| 대상 | 현재 선택 된 하위 시스템에서 암호와 연결할 대상을 지정 합니다. 개시자에 대 한 암호를 설정 하 고 종료 하는 경우 선택 사항입니다 .이는 이미 연결 된 암호가 없는 모든 대상에 대해 비밀이 사용 됨을 나타냅니다. |
| initiatorname | 암호와 연결할 초기자 iSCSI 이름을 지정 합니다. 이 옵션은 대상에서 비밀을 설정 하 고 종료 하는 경우에는 해당 비밀이 아직 연결 되지 않은 모든 초기자에 대해 사용 됨을 나타냅니다. |

### <a name="create"></a>create

현재 선택한 하위 시스템에 새 LUN 또는 iSCSI 대상을 만들거나 현재 선택한 대상에 대상 포털 그룹을 만듭니다. **Diskraid list** 명령을 사용 하 여 실제 바인딩을 볼 수 있습니다.

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

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| simple | 단순 LUN을 만듭니다. |
| 줄무늬(stripe) | 스트라이프 LUN을 만듭니다. |
| raid | 패리티를 사용 하 여 스트라이프 LUN을 만듭니다. |
| mirror | 미러된 LUN을 만듭니다. |
| automagic | 현재 적용 되는 *automagic* 힌트를 사용 하 여 LUN을 만듭니다. 자세한 내용은이 문서의 **automagic** 하위 명령을 참조 하세요. |
| 크기 = | 총 LUN 크기 (mb)를 지정 합니다. **Size**= 또는 **drives**= 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다. **Size =** 매개 변수가 지정 되지 않은 경우 생성 된 LUN은 지정 된 모든 드라이브에서 허용 하는 최대 크기입니다.<p>일반적으로 공급자는 최소한 요청 된 크기 만큼 큰 LUN을 만들지만, 공급자는 경우에 따라 다음으로 가장 큰 크기까지 반올림 해야 할 수 있습니다. 예를 들어 크기가. 99 GB로 지정 되 고 공급자가 GB 디스크 익스텐트만 할당할 수 있는 경우 결과 LUN은 1gb가 됩니다. 다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.<ul><li>**B** -바이트</li><li>**KB** -킬로바이트</li><li>**Mb-mb**</li><li>**Gb-gb**</li><li>**TB** -테라바이트</li><li>**PB** -페타바이트.</li></ul> |
| 드라이브 = | LUN을 만드는 데 사용할 드라이브의 *drive_number* 지정 합니다. **Size**= 또는 **drives**= 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다. **Size =** 매개 변수가 지정 되지 않은 경우 생성 된 LUN은 지정 된 모든 드라이브에서 허용 되는 최대 크기입니다. **Size =** 매개 변수가 지정 된 경우 공급자는 지정 된 드라이브 목록에서 드라이브를 선택 하 여 LUN을 만듭니다. 공급자는 가능 하면 지정 된 순서로 드라이브를 사용 하려고 합니다. |
| stripesize = | *스트라이프* 또는 *raid* LUN의 크기 (mb)를 지정 합니다. LUN을 만든 후에는 stripesize를 변경할 수 없습니다. 다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.<ul><li>**B** -바이트</li><li>**KB** -킬로바이트</li><li>**Mb-mb**</li><li>**Gb-gb**</li><li>**TB** -테라바이트</li><li>**PB** -페타바이트.</li></ul> |
| 대상 | 현재 선택 된 하위 시스템에 새 iSCSI 대상을 만듭니다. |
| name | 대상에 대 한 친숙 한 이름을 제공 합니다. |
| iscsiname | 대상에 대 한 iSCSI 이름을 제공 하며, 공급자가 이름을 생성 하도록 생략할 수 있습니다. |
| tpgroup | 현재 선택한 대상에 새 iSCSI 대상 포털 그룹을 만듭니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="delete"></a>delete

현재 선택한 LUN, iscsi 대상 (iSCSI 대상에 연결 된 Lun이 없는 한) 또는 iSCSI 대상 포털 그룹을 삭제 합니다.

#### <a name="syntax"></a>구문

```
delete lun [uninstall] [noerr]
delete target [noerr]
delete tpgroup [noerr]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| lun | 현재 선택한 LUN 및 모든 데이터를 삭제 합니다. |
| 제거 | Lun을 삭제 하기 전에 LUN과 연결 된 로컬 시스템의 디스크를 정리 하도록 지정 합니다. |
| 대상 | 대상에 연결 된 Lun이 없는 경우 현재 선택 된 iSCSI 대상을 삭제 합니다. |
| tpgroup | 현재 선택 된 iSCSI 대상 포털 그룹을 삭제 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="detail"></a>세부 정보

지정 된 형식의 현재 선택 된 개체에 대 한 자세한 정보를 표시 합니다.

#### <a name="syntax"></a>구문

```
detail {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup} [verbose]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| hbaport | 현재 선택 된 HBA (호스트 버스 어댑터) 포트에 대 한 자세한 정보를 나열 합니다. |
| iadapter | 현재 선택 된 iSCSI 초기자 어댑터에 대 한 자세한 정보를 나열 합니다. |
| iportal | 현재 선택한 iSCSI 초기자 포털에 대 한 자세한 정보를 나열 합니다. |
| provider | 현재 선택 된 공급자에 대 한 자세한 정보를 나열 합니다. |
| subsystem | 현재 선택 된 하위 시스템에 대 한 자세한 정보를 나열 합니다. |
| Controller | 현재 선택한 컨트롤러에 대 한 자세한 정보를 나열 합니다. |
| 포트 | 현재 선택한 컨트롤러 포트에 대 한 자세한 정보를 나열 합니다. |
| 드라이브 | 현재 선택 된 드라이브에 대 한 자세한 정보를 나열 하는 Lun을 포함 합니다. |
| lun | 영향을 주는 드라이브를 포함 하 여 현재 선택한 LUN에 대 한 자세한 정보를 나열 합니다. LUN이 파이버 채널 또는 iSCSI 하위 시스템의 일부 인지 여부에 따라 출력이 약간 달라 집니다. 마스크 되지 않은 호스트 목록에 별표가 있는 경우 LUN이 모든 호스트에 마스크 해제 됩니다. |
| 포털 새로 | 현재 선택 된 iSCSI 대상 포털에 대 한 자세한 정보를 나열 합니다. |
| 대상 | 현재 선택 된 iSCSI 대상에 대 한 자세한 정보를 나열 합니다. |
| tpgroup | 현재 선택 된 iSCSI 대상 포털 그룹에 대 한 자세한 정보를 나열 합니다. |
| verbose | LUN 매개 변수만 사용 합니다. 플렉스를 포함 하 여 추가 정보를 나열 합니다. |

### <a name="dissociate"></a>분리할

현재 선택한 LUN (다른 컨트롤러 포트는 영향을 받지 않음)에 대해 지정 된 컨트롤러 포트 목록을 비활성으로 설정 하거나 현재 선택한 LUN에 대해 지정 된 iSCSI 대상 목록을 분리 합니다.

#### <a name="syntax"></a>구문

```
dissociate controllers <n> [,<n> [,...]]
dissociate ports <n-m>[,<n-m>[,…]]
dissociate targets <n> [,<n> [,…]]
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| controllers | 현재 선택한 LUN과 연결 된 컨트롤러 목록에서 컨트롤러를 제거 합니다. VDS 1.0 공급자와만 사용 합니다. |
| ports | 현재 선택한 LUN과 연결 된 컨트롤러 포트 목록에서 컨트롤러 포트를 제거 합니다. VDS 1.1 공급자와만 사용 합니다. |
| 대상 | 현재 선택한 LUN과 연결 된 iSCSI 대상 목록에서 대상을 제거 합니다. VDS 1.1 공급자와만 사용 합니다. |
| `<n> [,<n> [,…]]` | **Controller** 또는 **targets** 매개 변수와 함께 사용할 경우. 비활성 또는 분리로 설정할 컨트롤러 또는 iSCSI 대상의 번호를 지정 합니다. |
| `<n-m>[,<n-m>[,…]]` | **Ports** 매개 변수와 함께 사용 합니다. 컨트롤러 번호 (*n*) 및 포트 번호 (*m*) 쌍을 사용 하 여 비활성으로 설정할 컨트롤러 포트를 지정 합니다. |

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

### <a name="exit"></a>exit

Diskraid를 종료 합니다.

#### <a name="syntax"></a>구문

```
exit
```

### <a name="extend"></a>extend

LUN의 끝에 섹터를 추가 하 여 현재 선택한 LUN을 확장 합니다. 일부 공급자는 Lun 확장을 지원 하지 않습니다. 는 LUN에 포함 된 볼륨 또는 파일 시스템을 확장 하지 않습니다. LUN을 확장 한 후에는 **DiskPart 확장** 명령을 사용 하 여 연결 된 디스크에 연결 된 디스크 구조를 확장 해야 합니다.

#### <a name="syntax"></a>구문

```
extend lun [size=<LUN_size>] [drives=<drive_number>, [<drive_number>, ...]] [noerr]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 크기 | LUN을 확장할 크기 (mb)를 지정 합니다. *크기* 또는 `<drive>` 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다. **Size =** 매개 변수가 지정 되지 않은 경우 LUN은 지정 된 모든 드라이브에서 허용 하는 최대 크기 만큼 확장 됩니다. **Size =** 매개 변수가 지정 된 경우 공급자는 **drives =** 매개 변수로 지정 된 목록에서 드라이브를 선택 하 여 LUN을 만듭니다. 다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.<ul><li>**B** -바이트</li><li>**KB** -킬로바이트</li><li>**Mb-mb**</li><li>**Gb-gb**</li><li>**TB** -테라바이트</li><li>**PB** -페타바이트.</li></ul> |
| 드라이브 = | `<drive_number>`LUN을 만들 때 사용할 드라이브의를 지정 합니다. *크기* 또는 `<drive>` 매개 변수를 지정 해야 합니다. 함께 사용할 수도 있습니다. **Size =** 매개 변수가 지정 되지 않은 경우 생성 된 LUN은 지정 된 모든 드라이브에서 허용 되는 최대 크기입니다. 공급자는 가능 하면 지정 된 순서로 드라이브를 사용 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="flushcache"></a>flushcache

현재 선택 된 컨트롤러에 대 한 캐시를 지웁니다.

#### <a name="syntax"></a>구문

```
flushcache controller
```

### <a name="help"></a>도움말

모든 Diskraid 명령 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
help
```

### <a name="importtarget"></a>importtarget

현재 선택 된 하위 시스템에 대해 설정 된 현재 VSS (볼륨 섀도 복사본 서비스) 가져오기 대상을 검색 하거나 설정 합니다.

#### <a name="syntax"></a>구문

```
importtarget subsystem [set target]
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 대상 설정 | 지정 하면 현재 선택 된 대상을 현재 선택 된 하위 시스템에 대 한 VSS 가져오기 대상으로 설정 합니다. 지정 하지 않으면 명령은 현재 선택 된 하위 시스템에 대해 설정 된 현재 VSS 가져오기 대상을 검색 합니다. |

### <a name="initiator"></a>initiator

로컬 iSCSI 초기자에 대 한 정보를 검색 합니다.

#### <a name="syntax"></a>구문

```
initiator
```

### <a name="invalidatecache"></a>invalidatecache

현재 선택한 컨트롤러의 캐시를 무효화 합니다.

#### <a name="syntax"></a>구문

```
invalidatecache controller
```

### <a name="lbpolicy"></a>lbpolicy

현재 선택한 LUN에 대 한 부하 분산 정책을 설정 합니다.

#### <a name="syntax"></a>구문

```
lbpolicy set lun type=<type> [paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]]
lbpolicy set lun paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| type | 부하 분산 정책을 지정 합니다. 형식을 지정 하지 않은 경우에는 **path** 매개 변수를 지정 해야 합니다. Type은 다음 중 하나일 수 있습니다.<ul><li>**장애 조치 (FAILOVER)** -다른 경로를 백업 경로로 사용 하는 기본 경로 하나를 사용 합니다.</li><li>**라운드 로빈** -각 경로를 순차적으로 시도 하는 라운드 로빈 방식으로 모든 경로를 사용 합니다.</li><li>**Subsetroundrobin** -라운드 로빈 방식으로 모든 기본 경로를 사용 합니다. 백업 경로는 모든 기본 경로가 실패 하는 경우에만 사용 됩니다.</li><li>**DYNLQD** -활성 요청 수가 가장 적은 경로를 사용 합니다.<li><li>**가중치가** 적용 됨-가중치가 가장 낮은 경로를 사용 합니다 (각 경로에 가중치를 할당 해야 함).</li><li>**LEASTBLOCKS** -블록이 가장 적은 경로를 사용 합니다.</li><li>**VENDORSPECIFIC** -공급 업체별 정책을 사용 합니다.</li></ul> |
| 경로 | 경로가 **기본** 경로 인지 또는 특정를 포함 하는지 여부를 지정 합니다 `<weight>` . 지정 되지 않은 경로는 모두 백업으로 암시적으로 설정 됩니다. 나열 된 경로는 현재 선택한 LUN의 경로 중 하나 여야 합니다. |

### <a name="list"></a>list

지정 된 형식의 개체 목록을 표시 합니다.

#### <a name="syntax"></a>구문

```
list {hbaports | iadapters | iportals | providers | subsystems | controllers | ports | drives | LUNs | tportals | targets | tpgroups}
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| hbaports | VDS에 알려진 모든 HBA 포트에 대 한 요약 정보를 나열 합니다. 현재 선택한 HBA 포트는 별표 (*)로 표시 됩니다. |
| iadapters | VDS에 알려진 모든 iSCSI 초기자 어댑터에 대 한 요약 정보를 나열 합니다. 현재 선택 된 초기자 어댑터는 별표 (*)로 표시 됩니다. |
| iportals | 현재 선택 된 초기자 어댑터의 모든 iSCSI 초기자 포털에 대 한 요약 정보를 나열 합니다. 현재 선택 된 초기자 포털은 별표 (*)로 표시 됩니다. |
| providers | VDS에 알려진 각 공급자에 대 한 요약 정보를 나열 합니다. 현재 선택 된 공급자는 별표 (*)로 표시 됩니다. |
| 하위 시스템 | 시스템의 각 하위 시스템에 대 한 요약 정보를 나열 합니다. 현재 선택 된 하위 시스템은 별표 (*)로 표시 됩니다. |
| controllers | 현재 선택 된 하위 시스템의 각 컨트롤러에 대 한 요약 정보를 나열 합니다. 현재 선택한 컨트롤러는 별표 (*)로 표시 됩니다. |
| ports | 현재 선택한 컨트롤러의 각 컨트롤러 포트에 대 한 요약 정보를 나열 합니다. 현재 선택한 포트는 별표 (*)로 표시 됩니다. |
| 드라이브 | 현재 선택 된 하위 시스템의 각 드라이브에 대 한 요약 정보를 나열 합니다. 현재 선택한 드라이브는 별표 (*)로 표시 됩니다. |
| lun | 현재 선택 된 하위 시스템의 각 LUN에 대 한 요약 정보를 나열 합니다. 현재 선택한 LUN은 별표 (*)로 표시 됩니다. |
| tportals | 현재 선택 된 하위 시스템의 모든 iSCSI 대상 포털에 대 한 요약 정보를 나열 합니다. 현재 선택한 대상 포털은 별표 (*)로 표시 됩니다. |
| 대상 | 현재 선택 된 하위 시스템의 모든 iSCSI 대상에 대 한 요약 정보를 나열 합니다. 현재 선택 된 대상은 별표 (*)로 표시 됩니다. |
| tpgroups | 현재 선택한 대상의 모든 iSCSI 대상 포털 그룹에 대 한 요약 정보를 나열 합니다. 현재 선택 된 포털 그룹은 별표 (*)로 표시 됩니다. |

### <a name="login"></a>로그인

지정 된 iSCSI 초기자 어댑터를 현재 선택한 iSCSI 대상에 기록 합니다.

#### <a name="syntax"></a>구문

```
login target iadapter=<iadapter> [type={manual | persistent | boot}] [chap={none | oneway | mutual}] [iportal=<iportal>] [tportal=<tportal>] [<flag> [<flag> […]]]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| type | 수행할 로그인 유형을 **manual** 또는 **persistent**로 지정 합니다. 지정 하지 않으면 수동 로그인이 수행 됩니다. |
| 수동 | 수동으로 로그인 합니다. 또한 향후 개발을 위한 **부팅** 옵션을 제공 하며 현재 사용 되지 않습니다. |
| 지속적 | 컴퓨터를 다시 시작 하면 자동으로 동일한 로그인을 사용 합니다. |
| chap | 사용할 CHAP 인증의 유형 ( **none**, **oneway** chap 또는 **상호** CHAP)을 지정 합니다. 지정 되지 않은 경우 인증을 사용 하지 않습니다. |
| 포털 새로 | 현재 선택 된 하위 시스템에서 로그인에 사용할 선택적 대상 포털을 지정 합니다. |
| iportal | 지정 된 초기자 어댑터에서 로그인에 사용할 선택적인 초기자 포털을 지정 합니다. |
| `<flag>` | 3 자 머리글자어로 식별 됩니다.<ul><li>**Ip** -IPsec 필요</li><li>**EMP** -다중 경로 사용</li><li>**Ehd** -헤더 다이제스트 사용</li><li>**EDD** -데이터 다이제스트 사용</li></ul> |

### <a name="logout"></a>logout

지정 된 iSCSI 초기자 어댑터를 현재 선택 된 iSCSI 대상에서 로그 아웃 합니다.

#### <a name="syntax"></a>구문

```
logout target iadapter= <iadapter>
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| iadapter | 로그 아웃을 위한 로그인 세션이 있는 시작자 어댑터를 지정 합니다. |

### <a name="maintenance"></a>유지 관리

지정 된 형식의 현재 선택 된 개체에 대 한 유지 관리 작업을 수행 합니다.

#### <a name="syntax"></a>구문

```
maintenance <object operation> [count=<iteration>]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<object>` | 작업을 수행할 개체 유형을 지정 합니다. *개체* 유형은 **하위 시스템**, **컨트롤러**, **포트, 드라이브** 또는 **LUN**이 될 수 있습니다. |
| `<operation>` | 수행할 유지 관리 작업을 지정 합니다. *작업* 유형은 **spinup**, **spindown**, **blink**, **경고음** 또는 **ping**일 수 있습니다. *작업* 을 지정 해야 합니다. |
| 개수 = | *작업*을 반복할 횟수를 지정 합니다. 일반적으로이는 **깜박임**, **경고음**또는 **ping**과 함께 사용 됩니다. |

### <a name="name"></a>name

현재 선택 된 하위 시스템, LUN 또는 iSCSI 대상의 이름을 지정 된 이름으로 설정 합니다.

#### <a name="syntax"></a>구문

```
name {subsystem | lun | target} [<name>]
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<name>` | 하위 시스템, LUN 또는 대상의 이름을 지정 합니다. 이름은 64 자 미만 이어야 합니다. 이름을 제공 하지 않으면 기존 이름 (있는 경우)이 삭제 됩니다. |

### <a name="offline"></a>오프라인

지정 된 형식의 현재 선택 된 개체의 상태를 **오프 라인**으로 설정 합니다.

#### <a name="syntax"></a>구문

```
offline <object>
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<object>` | 이 작업을 수행할 개체의 유형을 지정 합니다. 형식은 **subsystem**, **controller**, **drive**, **LUN**또는 **포털 새로**일 수 있습니다. |

### <a name="online"></a>온라인

지정 된 형식의 선택한 개체 상태를 **온라인**으로 설정 합니다. 개체가 **hbaport**인 경우는 현재 선택한 HBA 포트의 경로 상태를 **온라인**으로 변경 합니다.

#### <a name="syntax"></a>구문

```
online <object>
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<object>` | 이 작업을 수행할 개체의 유형을 지정 합니다. 유형은 **hbaport**, **subsystem**, **controller**, **drive**, **LUN**또는 **포털 새로**수 있습니다. |

### <a name="recover"></a>recover

다시 동기화 또는 핫 절약와 같은 필요한 작업을 수행 하 여 현재 선택 된 내결함성 LUN을 복구 합니다. 예를 들어 복구로 인해 핫 스패어가 오류가 발생 한 디스크 또는 다른 디스크 익스텐트 재할당을 포함 하는 RAID 집합에 바인딩될 수 있습니다.

#### <a name="syntax"></a>구문

```
recover <lun>
```

### <a name="reenumerate"></a>다시 열거

지정 된 형식의 개체를 다시 열거 합니다. LUN 확장 명령을 사용 하는 경우 reenumerate 명령을 사용 하기 전에 refresh 명령을 사용 하 여 디스크 크기를 업데이트 해야 합니다.

#### <a name="syntax"></a>구문

```
reenumerate {subsystems | drives}
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 하위 시스템 | 공급자를 쿼리하여 현재 선택 된 공급자에 추가 된 새 하위 시스템을 검색 합니다. |
| 드라이브 | 내부 i/o 버스를 쿼리하여 현재 선택 된 하위 시스템에 추가 된 새 드라이브를 검색 합니다. |

### <a name="refresh"></a>refresh

현재 선택 된 공급자에 대 한 내부 데이터를 새로 고칩니다.

#### <a name="syntax"></a>구문

```
refresh provider
```

### <a name="rem"></a>rem

스크립트를 설명 하는 데 사용 됩니다.

#### <a name="syntax"></a>구문

```
Rem <comment>
```

### <a name="remove"></a>remove

현재 선택한 대상 포털 그룹에서 지정 된 iSCSI 대상 포털을 제거 합니다.

#### <a name="syntax"></a>구문

```
remove tpgroup tportal=<tportal> [noerr]
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| tpgroup 포털 새로 =`<tportal>` | 제거할 iSCSI 대상 포털을 지정 합니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="replace"></a>replace

지정 된 드라이브를 현재 선택한 드라이브로 바꿉니다. 지정한 드라이브가 현재 선택 된 드라이브가 아닐 수 있습니다.

#### <a name="syntax"></a>구문

```
replace drive=<drive_number>
```

##### <a name="parameter"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 드라이브 = | 바꿀 드라이브의를 지정 합니다 `<drive_number>` . |

### <a name="reset"></a>reset

현재 선택한 컨트롤러 또는 포트를 다시 설정 합니다.

#### <a name="syntax"></a>구문

```
reset {controller | port}
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| Controller | 컨트롤러를 다시 설정 합니다. |
| 포트 | 포트를 다시 설정 합니다. |

### <a name="select"></a>선택

현재 선택한 개체를 표시 하거나 변경 합니다.

#### <a name="syntax"></a>구문

```
select {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup } [<n>]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 개체 | **공급자**, **하위 시스템**, **컨트롤러**, **드라이브**또는 **LUN**을 포함 하 여 선택할 개체의 유형을 지정 합니다. |
| hbaport`[<n>]` | 지정 된 로컬 HBA 포트에 포커스를 설정 합니다. HBA 포트가 지정 되지 않은 경우이 명령은 현재 선택 된 HBA 포트 (있는 경우)를 표시 합니다. 잘못 된 HBA 포트 인덱스를 지정 하면 포커스 없는 HBA 포트가 생성 되지 않습니다. HBA 포트를 선택 하면 선택 된 초기자 어댑터와 개시자 포털이 모두 선택 취소 됩니다. |
| iadapter`[<n>]` | 지정 된 로컬 iSCSI 초기자 어댑터에 포커스를 설정 합니다. 초기자 어댑터를 지정 하지 않으면 명령은 현재 선택 된 초기자 어댑터 (있는 경우)를 표시 합니다. 잘못 된 초기자 어댑터 인덱스를 지정 하면 포커스를 가진 초기자 어댑터가 생성 되지 않습니다. 개시자 어댑터를 선택 하면 선택한 HBA 포트와 초기자 포털이 모두 선택 취소 됩니다. |
| iportal`[<n>]` | 선택한 iSCSI 초기자 어댑터 내에서 지정 된 로컬 iSCSI 초기자 포털에 포커스를 설정 합니다. 초기자 포털을 지정 하지 않으면 명령은 현재 선택 된 초기자 포털 (있는 경우)을 표시 합니다. 잘못 된 초기자 포털 인덱스를 지정 하면 선택한 초기자 포털이 생성 되지 않습니다. |
| 공급자별`[<n>]` | 지정 된 공급자에 포커스를 설정 합니다. 공급자를 지정 하지 않으면 명령은 현재 선택 된 공급자 (있는 경우)를 표시 합니다. 잘못 된 공급자 인덱스를 지정 하면 포커스 없는 공급자가 발생 하지 않습니다. |
| 하위`[<n>]` | 지정 된 하위 시스템에 포커스를 설정 합니다. 하위 시스템을 지정 하지 않으면 명령은 포커스가 있는 하위 시스템을 표시 합니다 (있는 경우). 잘못 된 하위 시스템 인덱스를 지정 하면 포커스에 없는 하위 시스템도 발생 하지 않습니다. 하위 시스템을 선택 하면 연결 된 공급자가 암시적으로 선택 됩니다. |
| controller`[<n>]` | 현재 선택 된 하위 시스템 내의 지정 된 컨트롤러에 포커스를 설정 합니다. 컨트롤러를 지정 하지 않으면 명령은 현재 선택한 컨트롤러 (있는 경우)를 표시 합니다. 잘못 된 컨트롤러 인덱스를 지정 하면 포커스가 없는 컨트롤러가 생성 되지 않습니다. 컨트롤러를 선택 하면 선택한 컨트롤러 포트, 드라이브, Lun, 대상 포털, 대상 및 대상 포털 그룹을 선택 취소 합니다. |
| 포트인`[<n>]` | 현재 선택한 컨트롤러 내의 지정 된 컨트롤러 포트에 포커스를 설정 합니다. 포트를 지정 하지 않으면 명령은 현재 선택 된 포트 (있는 경우)를 표시 합니다. 잘못 된 포트 인덱스를 지정 하면 선택한 포트가 생성 되지 않습니다. |
| 드라이브나`[<n>]` | 현재 선택한 하위 시스템 내의 지정 된 드라이브 또는 실제 스핀 들에 포커스를 설정 합니다. 드라이브가 지정 되지 않은 경우이 명령은 현재 선택 된 드라이브 (있는 경우)를 표시 합니다. 잘못 된 드라이브 인덱스를 지정 하면 포커스가 없는 드라이브가 생성 되지 않습니다. 드라이브를 선택 하면 선택한 컨트롤러, 컨트롤러 포트, Lun, 대상 포털, 대상 및 대상 포털 그룹의 선택이 취소 됩니다. |
| lun`[<n>]` | 현재 선택 된 하위 시스템 내의 지정 된 LUN에 포커스를 설정 합니다. LUN을 지정 하지 않으면 명령은 현재 선택한 LUN (있는 경우)을 표시 합니다. 잘못 된 LUN 인덱스를 지정 하면 선택한 LUN이 생성 되지 않습니다. LUN을 선택 하면 선택한 컨트롤러, 컨트롤러 포트, 드라이브, 대상 포털, 대상 및 대상 포털 그룹의 선택이 취소 됩니다. |
| 포털 새로`[<n>]` | 현재 선택한 하위 시스템 내의 지정 된 iSCSI 대상 포털에 포커스를 설정 합니다. 대상 포털을 지정 하지 않으면 명령은 현재 선택한 대상 포털 (있는 경우)을 표시 합니다. 잘못 된 대상 포털 인덱스를 지정 하면 선택한 대상 포털이 생성 되지 않습니다. 대상 포털을 선택 하면 컨트롤러, 컨트롤러 포트, 드라이브, Lun, 대상 및 대상 포털 그룹의 선택이 취소 됩니다. |
| 대상을`[<n>]` | 현재 선택 된 하위 시스템 내의 지정 된 iSCSI 대상에 포커스를 설정 합니다. 대상이 지정 되지 않은 경우이 명령은 현재 선택 된 대상 (있는 경우)을 표시 합니다. 잘못 된 대상 인덱스를 지정 하면 대상이 선택 되지 않습니다. 대상을 선택 하면 컨트롤러, 컨트롤러 포트, 드라이브, Lun, 대상 포털 및 대상 포털 그룹의 선택이 취소 됩니다. |
| tpgroup`[<n>]` | 현재 선택 된 iSCSI 대상 내의 지정 된 iSCSI 대상 포털 그룹에 포커스를 설정 합니다. 대상 포털 그룹을 지정 하지 않으면 명령은 현재 선택한 대상 포털 그룹 (있는 경우)을 표시 합니다. 잘못 된 대상 포털 그룹 인덱스를 지정 하면 포커스가 없는 대상 포털 그룹이 생성 됩니다. |
|`[<n>]` | `<object number>`선택할를 지정 합니다. 지정 된 `<object number>` 가 잘못 된 경우 지정 된 형식의 개체에 대 한 모든 기존 선택 항목이 지워집니다. 을 지정 하지 않으면 `<object number>` 현재 개체가 표시 됩니다.

### <a name="setflag"></a>setflag

현재 선택 된 드라이브를 핫 스패어로 설정 합니다. 핫 스페어는 일반적인 LUN 바인딩 작업에 사용할 수 없습니다. 오류 처리 전용으로 예약 되어 있습니다. 드라이브가 현재 어떤 기존 LUN에도 바인딩되지 않아야 합니다.

#### <a name="syntax"></a>구문

```
setflag drive hotspare={true | false}
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| true | 핫 스패어로 현재 선택 된 드라이브를 선택 합니다. |
| false | 핫 스패어로 현재 선택 된 드라이브를 선택 취소 합니다. |

### <a name="shrink"></a>축소

선택한 LUN의 크기를 줄입니다.

#### <a name="syntax"></a>구문

```
shrink lun size=<n> [noerr]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 크기 | 에서 LUN의 크기를 줄이기 위해 원하는 공간 크기 (mb)를 지정 합니다. 다른 단위를 사용 하 여 크기를 지정 하려면 크기 바로 뒤에 다음과 같은 인식 된 접미사 중 하나를 사용 합니다.<ul><li>**B** -바이트</li><li>**KB** -킬로바이트</li><li>**Mb-mb**</li><li>**Gb-gb**</li><li>**TB** -테라바이트</li><li>**PB** -페타바이트. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 Diskraid는 오류가 발생 하지 않은 것 처럼 명령을 계속 처리 합니다. |

### <a name="standby"></a>대기

현재 선택 된 HBA (호스트 버스 어댑터) 포트의 경로 상태를 대기 중으로 변경 합니다.

#### <a name="syntax"></a>구문

```
standby hbaport
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| hbaport | 현재 선택 된 HBA (호스트 버스 어댑터) 포트의 경로 상태를 대기 중으로 변경 합니다. |

### <a name="unmask"></a>해제할

지정 된 호스트에서 현재 선택한 Lun에 액세스할 수 있도록 설정 합니다.

#### <a name="syntax"></a>구문

```
unmask lun {all | none | [add] wwn=<hexadecimal_number> [;<hexadecimal_number> [;…]] | [add] initiator=<initiator>[;<initiator>[;…]]} [uninstall]
```

##### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 모두 | 모든 호스트에서 LUN에 액세스할 수 있도록 지정 합니다. 그러나 iSCSI 하위 시스템에서 모든 대상에 대 한 LUN의 마스크를 해제할 수는 없습니다.<P>명령을 실행 하기 전에 대상의 로그를 로그 아웃 해야 합니다 `unmask lun all` . |
| 없음 | 모든 호스트에서 LUN에 액세스할 수 없도록 지정 합니다.<P>명령을 실행 하기 전에 대상의 로그를 로그 아웃 해야 합니다 `unmask lun none` . |
| add | 지정 된 호스트를이 LUN에 액세스할 수 있는 호스트의 기존 목록에 추가 하도록 지정 합니다. 이 매개 변수를 지정 하지 않으면 제공 된 호스트 목록이이 LUN에 액세스할 수 있는 기존 호스트 목록을 대체 합니다. |
| wwn = | LUN 또는 호스트에 액세스할 수 있어야 하는 wwpn (wide name)을 나타내는 16 진수 목록을 지정 합니다. 파이버 채널 하위 시스템의 특정 호스트 집합에 마스크/마스크 해제 하려면 관심 있는 호스트 컴퓨터의 포트에 대해 세미콜론으로 구분 된 WWN 목록을 입력 하면 됩니다. |
| 시작자 = | 현재 선택한 LUN에 액세스할 수 있어야 하는 iSCSI 초기자 목록을 지정 합니다. ISCSI 하위 시스템의 특정 호스트 집합에 마스크/마스크 해제 하려면 관심 있는 호스트 컴퓨터에서 초기자에 대 한 iSCSI 초기자 이름 목록을 세미콜론으로 구분 하 여 입력 하면 됩니다. |
| 제거 | 지정 하는 경우 LUN이 마스킹 되기 전에 로컬 시스템에서 LUN과 연결 된 디스크를 제거 합니다. |

## <a name="scripting-diskraid"></a>Diskraid 스크립팅

지원 되는 Windows Server 버전을 실행 하는 컴퓨터에서 Diskraid를 연결 된 VDS 하드웨어 공급자를 사용 하 여 Diskraid를 스크립팅할 수 있습니다. Diskraid 스크립트를 호출 하려면 명령 프롬프트에서 다음을 입력 합니다.

```
diskraid /s <script.txt>
```

기본적으로 Diskraid는 명령 처리를 중지 하 고 스크립트에 문제가 있는 경우 오류 코드를 반환 합니다. 스크립트를 계속 실행 하 고 오류를 무시 하려면 명령에 **noerr** 매개 변수를 포함 합니다. 이는 단일 스크립트를 사용 하 여 총 Lun 수에 관계 없이 하위 시스템의 모든 Lun을 삭제 하는 것과 같은 유용한 방법을 허용 합니다. 모든 명령이 **noerr** 매개 변수를 지 원하는 것은 아닙니다. **Noerr** 매개 변수를 포함 했는지 여부에 관계 없이 오류는 항상 명령 구문 오류에 반환 됩니다.

## <a name="diskraid-error-codes"></a>Diskraid 오류 코드

| 오류 코드 | 오류 설명 |
| ---------- | ----------------- |
| 0 | 오류가 발생하지 않았습니다. 전체 스크립트가 오류 없이 실행 되었습니다. |
| 1 | 치명적인 예외가 발생 했습니다. |
| 2 | Diskraid 명령줄에 지정 된 인수가 잘못 되었습니다. |
| 3 | Diskraid에서 지정 된 스크립트나 출력 파일을 열 수 없습니다. |
| 4 | 서비스 Diskraid 중 하나에서 오류를 반환 했습니다. |
| 5 | 명령 구문 오류가 발생 했습니다. 개체가 잘못 선택 되었거나이 명령과 함께 사용 하기에 적합 하지 않아 스크립트가 실패 했습니다. |

## <a name="example"></a>예제

컴퓨터에서 하위 시스템 0의 상태를 확인 하려면 다음을 입력 합니다.

```
diskraid
```

ENTER 키를 누르고 다음과 유사한 출력을 표시 합니다.

```
Microsoft Diskraid version 5.2.xxxx
Copyright (©) 2003 Microsoft Corporation
On computer: COMPUTER_NAME
```

하위 시스템 0을 선택 하려면 Diskraid 프롬프트에 다음을 입력 합니다.

```
select subsystem 0
```

ENTER 키를 누르고 다음과 유사한 출력을 표시 합니다.

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

Diskraid를 종료 하려면 Diskraid 프롬프트에 다음을 입력 합니다.

```
exit
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)