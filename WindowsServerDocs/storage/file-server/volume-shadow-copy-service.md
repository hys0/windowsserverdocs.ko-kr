---
title: 볼륨 섀도 복사본 서비스
ms.date: 01/30/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 1ab941e25da7171349bb24762940af3bf886c165
ms.sourcegitcommit: a4b489d0597b6a73c905d3448d5bc332efd6191b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77675364"
---
# <a name="volume-shadow-copy-service"></a>볼륨 섀도 복사본 서비스

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008, Windows 10, Windows 8.1, Windows 8, Windows 7

중요한 비즈니스 데이터의 백업 및 복원은 다음과 같은 문제로 인해 매우 복잡할 수 있습니다.

  - 일반적으로 데이터를 생성하는 애플리케이션이 계속 실행되는 동안 데이터를 백업해야 합니다. 즉, 일부 데이터 파일이 열려 있거나 일관성 없는 상태일 수 있습니다.

  - 데이터 세트가 클 경우 한 번에 모두 백업하기가 어려울 수 있습니다.


백업 및 복원 작업을 올바르게 수행하려면 백업 애플리케이션, 백업 중인 LOB(기간 업무) 애플리케이션, 스토리지 관리 하드웨어 및 소프트웨어 간에 긴밀하게 조정해야 합니다. Windows Server® 2003에 도입된 VSS(볼륨 섀도 복사본 서비스)를 사용하면 이러한 구성 요소 간의 대화를 통해 쉽게 더 효율적으로 작동할 수 있습니다. 모든 구성 요소에서 VSS를 지원하는 경우 애플리케이션을 오프라인으로 전환하지 않고도 애플리케이션 데이터를 백업하는 데 사용할 수 있습니다.

VSS는 백업할 데이터의 일관성 있는 섀도 복사본(스냅샷 또는 특정 시점 복사본이라고도 함)을 만드는 데 필요한 작업을 조정합니다. 섀도 복사본은 있는 그대로 사용하거나 다음과 같은 시나리오에서 사용할 수 있습니다.

  - 다른 하드 디스크 드라이브, 테이프 또는 다른 이동식 미디어에 데이터를 보관하는 것을 포함하여 애플리케이션 데이터 및 시스템 상태 정보를 백업하려고 합니다.

  - 데이터 마이닝입니다.

  - 디스크-디스크 백업을 수행합니다.

  - 데이터를 원본 LUN 또는 실패한 원본 LUN을 대체하는 완전히 새로운 LUN으로 복원하여 데이터 손실을 빠르게 복구해야 합니다.


VSS를 사용하는 Windows 기능 및 애플리케이션은 다음과 같습니다.

  - [Windows Server 백업](https://go.microsoft.com/fwlink/?linkid=180891)(https://go.microsoft.com/fwlink/?LinkId=180891)

  - [공유 폴더의 섀도 복사본](https://go.microsoft.com/fwlink/?linkid=142874)(https://go.microsoft.com/fwlink/?LinkId=142874)

  - [System Center Data Protection Manager](https://go.microsoft.com/fwlink/?linkid=180892)(https://go.microsoft.com/fwlink/?LinkId=180892)

  - [시스템 복원](https://go.microsoft.com/fwlink/?linkid=180893)(https://go.microsoft.com/fwlink/?LinkId=180893)


## <a name="how-volume-shadow-copy-service-works"></a>볼륨 섀도 복사본 서비스의 작동 방식

완전한 VSS 솔루션에 필요한 기본 구성 요소는 다음과 같습니다.

**VSS 서비스**   다른 구성 요소가 서로 올바르게 통신하고 함께 작동할 수 있도록 하는 Windows 운영 체제의 일부입니다.

**VSS 요청자**   섀도 복사본을 실제로 만들도록(또는 섀도 복사본 가져오기 또는 삭제와 같은 다른 고급 작업) 요청하는 소프트웨어입니다. 일반적으로 이는 백업 애플리케이션입니다. Windows Server 백업 유틸리티와 System Center Data Protection Manager 애플리케이션은 VSS 요청자입니다. 비 Microsoft® VSS 요청자에는 Windows에서 실행되는 거의 모든 백업 소프트웨어가 포함되어 있습니다.

**VSS 기록기**   일관성 있는 데이터 세트가 백업되도록 보장하는 구성 요소입니다. 일반적으로 SQL Server® 또는 Exchange Server와 같은 LOB(기간 업무) 애플리케이션의 일부로 제공됩니다. Windows 운영 체제에는 레지스트리와 같은 다양한 Windows 구성 요소에 대한 VSS 기록기가 포함되어 있습니다. 타사 VSS 기록기는 다양한 Windows용 애플리케이션에 포함되어 백업 중에 데이터 일관성을 보장해야 합니다.

**VSS 공급자**   섀도 복사본을 만들고 유지 관리하는 구성 요소입니다. 이 작업은 소프트웨어 또는 하드웨어에서 수행될 수 있습니다. Windows 운영 체제에는 기록 중 복사를 사용하는 VSS 공급자가 포함되어 있습니다. SAN(저장 영역 네트워크)을 사용하는 경우 SAN용 VSS 하드웨어 공급자를 설치해야 합니다. 하드웨어 공급자는 호스트 운영 체제에서 섀도 복사본을 만들고 유지 관리하는 작업을 오프로드합니다.

다음 다이어그램에서는 VSS 서비스에서 요청자, 기록기 및 공급자와 조정하여 볼륨의 섀도 복사본을 만드는 방법을 보여 줍니다.

![](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**그림 1**   볼륨 섀도 복사본 서비스의 아키텍처 다이어그램

### <a name="how-a-shadow-copy-is-created"></a>섀도 복사본을 만드는 방법

이 섹션에서는 섀도 복사본을 만드는 데 필요한 단계를 나열하여 요청자, 기록기 및 공급자의 다양한 역할을 컨텍스트에 배치합니다. 다음 다이어그램에서는 볼륨 섀도 복사본 서비스에서 요청자, 기록기 및 공급자에 대한 전반적인 조정을 제어하는 방법을 보여 줍니다.

![](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**그림 2** 섀도 복사본 만들기 프로세스

섀도 복사본을 만들려면 요청자, 기록기 및 공급자에서 다음 작업을 수행합니다.

1.  요청자에서 볼륨 섀도 복사본 서비스에 기록기를 열거하고, 기록기 메타데이터를 수집하고. 섀도 복사본 만들기를 준비하도록 요청합니다.

2.  각 기록기에서 백업해야 하는 구성 요소 및 데이터 저장소에 대한 XML 설명을 만들고, 이를 볼륨 섀도 복사본 서비스에 제공합니다. 또한 기록기는 모든 구성 요소에 사용되는 복원 방법을 정의합니다. 볼륨 섀도 복사본 서비스에서 백업할 구성 요소를 선택하는 요청자에 기록기의 설명을 제공합니다.

3.  볼륨 섀도 복사본 서비스에서 섀도 복사본을 만들기 위해 데이터를 준비하도록 모든 기록기에 알립니다.

4.  각 기록기에서 모든 열린 트랜잭션을 완료하고, 트랜잭션 로그를 롤링하며, 캐시를 플러시하는 등 데이터를 적절하게 준비합니다. 데이터를 섀도 복사할 준비가 되면 기록기에서 볼륨 섀도 복사본 서비스에 알립니다.

5.  볼륨 섀도 복사본 서비스에서 하나 이상의 볼륨에 대한 섀도 복사본을 만드는 데 필요한 애플리케이션 쓰기 I/O 요청(읽기 I/O 요청도 여전히 가능)을 몇 초 동안 일시적으로 고정하도록 요청자에게 지시합니다. 애플리케이션을 고정하는 데 걸리는 시간은 최대 60초입니다. 볼륨 섀도 복사본 서비스는 파일 시스템 버퍼를 플러시한 다음, 파일 시스템을 고정하여 파일 시스템 메타데이터가 올바르게 기록되고 섀도 복사할 데이터가 일관된 순서로 기록되도록 합니다.

6.  볼륨 섀도 복사본 서비스에서 섀도 복사본을 만들도록 공급자에 지시합니다. 섀도 복사본 만들기 기간은 10초 이하로 지속되며, 이 기간 동안 파일 시스템에 대한 모든 쓰기 I/O 요청이 고정된 상태로 유지됩니다.

7.  볼륨 섀도 복사본 서비스에서 파일 시스템 쓰기 I/O 요청을 해제합니다.

8.  VSS에서 애플리케이션 쓰기 I/O 요청을 해제하도록 기록기에 지시합니다. 이 시점에서 애플리케이션은 섀도 복사되는 디스크에 데이터를 쓰는 작업을 다시 시작할 수 있습니다.


> [!NOTE]
> 기록기를 60초 이상 고정 상태로 유지하거나 공급자에서 섀도 복사본을 커밋하는 데 10초 넘게 걸리는 경우 섀도 복사본 만들기가 중단될 수 있습니다.
<br>

9. 요청자에서 프로세스를 다시 시도하거나(1단계로 돌아가기) 나중에 다시 시도하도록 관리자에게 알릴 수 있습니다.

10. 섀도 복사본이 성공적으로 만들어지면 볼륨 섀도 복사본 서비스에서 섀도 복사본의 위치 정보를 요청자에 반환합니다. 경우에 따라 섀도 복사본을 일시적으로 읽기-쓰기 볼륨으로 사용할 수 있으므로 섀도 복사본이 완료되기 전에 VSS 및 하나 이상의 애플리케이션에서 섀도 복사본의 콘텐츠를 변경할 수 있습니다. VSS와 애플리케이션에서 이러한 변경을 수행하면 섀도 복사본이 읽기 전용으로 설정됩니다. 이 단계를 자동 복구라고 하며, 이는 섀도 복사본을 만들기 전에 완료되지 않은 섀도 복사본 볼륨에서 파일 시스템 또는 애플리케이션 트랜잭션을 실행 취소하는 데 사용됩니다.


### <a name="how-the-provider-creates-a-shadow-copy"></a>공급자에서 섀도 복사본을 만드는 방법

하드웨어 또는 소프트웨어 섀도 복사본 공급자는 다음 방법 중 하나를 사용하여 섀도 복사본을 만듭니다.

**완전한 복사**   이 방법은 원본 볼륨의 완전한 복사본("전체 복사본" 또는 "복제본")을 지정한 특정 시점에 만듭니다. 이 복사본은 읽기 전용입니다.

**기록 중 복사**   이 방법은 원본 볼륨을 복사하지 않습니다. 대신 지정한 특정 시점 이후에 볼륨에 대한 모든 변경 내용(완료된 쓰기 I/O 요청)을 복사하여 차등 복사본을 만듭니다.

**기록 중 리디렉션**   이 방법은 원본 볼륨을 복사하지 않으며, 지정한 특정 시점 이후에 원본 볼륨을 변경하지 않습니다. 대신 모든 변경 내용을 다른 볼륨으로 리디렉션하여 차등 복사본을 만듭니다.

## <a name="complete-copy"></a>완전한 복사

완전한 복사는 일반적으로 다음과 같이 "분할된 미러"를 수행하여 만듭니다.

1. 원본 볼륨과 섀도 복사본 볼륨은 미러된 볼륨 세트입니다.

2. 섀도 복사본 볼륨은 원본 볼륨과 분리되어 있습니다. 이렇게 하면 미러 연결이 끊어집니다.


미러 연결이 끊어지면 원본 볼륨과 섀도 복사본 볼륨이 독립적으로 유지됩니다. 원본 볼륨은 모든 변경 내용(쓰기 I/O 요청)을 계속 받아들이지만, 섀도 복사본 볼륨은 연결이 끊긴 시점의 원본 데이터에 대한 정확한 읽기 전용 복사본으로 유지됩니다.

### <a name="copy-on-write-method"></a>기록 중 복사 방법

기록 중 복사 방법에서 원본 볼륨이 변경되면(단, 쓰기 I/O 요청이 완료되기 전) 수정될 각 블록을 읽은 다음, 볼륨의 섀도 복사본 저장 영역("차등 영역"이라고도 함)에 기록합니다. 섀도 복사본 저장 영역은 동일한 볼륨 또는 다른 볼륨에 있을 수 있습니다. 이렇게 하면 원본 볼륨의 데이터 블록 복사본을 유지한 후에 변경 내용으로 덮어씁니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>시간</th>
<th>원본 데이터(상태 및 데이터)</th>
<th>섀도 복사본(상태 및 데이터)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>원본 데이터: 1 2 3 4 5</p></td>
<td><p>복사 안 함: —</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>캐시에서 데이터가 변경됨: 3에서 3'로</p></td>
<td><p>섀도 복사본 생성(차등만): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>원본 데이터를 덮어씀: 1 2 3' 4 5</p></td>
<td><p>차등 및 인덱스가 섀도 복사본에 저장됨: 3</p></td>
</tr>
</tbody>
</table>

**표 1**   섀도 복사본을 만드는 기록 중 복사 방법

기록 중 복사 방법은 변경된 데이터만 복사하므로 섀도 복사본을 만드는 빠른 방법입니다. 차등 영역의 복사된 블록을 원본 볼륨의 변경된 데이터와 결합하여 변경하기 전에 볼륨을 해당 상태로 복원할 수 있습니다. 변경 내용이 많을 경우 기록 중 복사 방법의 비용이 많이 들 수 있습니다.

### <a name="redirect-on-write-method"></a>기록 중 리디렉션 방법

기록 중 리디렉션 방법에서는 원본 볼륨에서 변경(쓰기 I/O 요청)을 받을 때마다 해당 변경 내용이 원본 볼륨에 적용되지 않습니다. 대신 변경 내용이 다른 볼륨의 섀도 복사본 저장 영역에 쓰여집니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>시간</th>
<th>원본 데이터(상태 및 데이터)</th>
<th>섀도 복사본(상태 및 데이터)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>원본 데이터: 1 2 3 4 5</p></td>
<td><p>복사 안 함: —</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>캐시에서 데이터가 변경됨: 3에서 3'로</p></td>
<td><p>섀도 복사본 생성(차등만): 3'</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>원본 데이터가 변경되지 않음: 1 2 3 4 5</p></td>
<td><p>차등 및 인덱스가 섀도 복사본에 저장됨: 3'</p></td>
</tr>
</tbody>
</table>

**표 2**   섀도 복사본을 만드는 기록 중 리디렉션 방법

기록 중 복사 방법과 마찬가지로, 기록 중 리디렉션 방법은 데이터에 대한 변경 내용만 복사하므로 섀도 복사본을 만드는 빠른 방법입니다. 차등 영역에 복사된 블록을 원본 볼륨의 변경되지 않은 데이터와 결합하여 완전한 최신의 데이터 복사본을 만들 수 있습니다. 읽기 I/O 요청이 많을 경우 기록 중 리디렉션 방법의 비용이 많이 들 수 있습니다.

## <a name="shadow-copy-providers"></a>섀도 복사본 공급자

섀도 복사본 공급자에는 하드웨어 기반 공급자와 소프트웨어 기반 공급자의 두 가지 유형이 있습니다. 또한 Windows 운영 체제에 기본 제공되는 소프트웨어 공급자인 시스템 공급자도 있습니다.

### <a name="hardware-based-providers"></a>하드웨어 기반 공급자

하드웨어 기반 섀도 복사본 공급자는 하드웨어 스토리지 어댑터 또는 컨트롤러와 함께 작동하여 볼륨 섀도 복사본 서비스와 하드웨어 수준 간의 인터페이스 역할을 합니다. 섀도 복사본을 만들고 유지 관리하는 작업은 스토리지 배열로 수행됩니다.

하드웨어 공급자는 항상 전체 LUN의 섀도 복사본을 가져오지만, 볼륨 섀도 복사본 서비스는 요청된 볼륨 하나 이상의 섀도 복사본만 공개합니다.

하드웨어 기반 섀도 복사본 공급자는 특정 시점을 정의하고, 데이터 동기화를 허용하고, 섀도 복사본을 관리하고, 공통 인터페이스를 백업 애플리케이션에 제공하는 볼륨 섀도 복사본 서비스 기능을 사용합니다. 그러나 볼륨 섀도 복사본 서비스는 하드웨어 기반 공급자에서 섀도 복사본을 생성하고 유지 관리하는 기본 메커니즘을 지정하지 않습니다.

### <a name="software-based-providers"></a>소프트웨어 기반 공급자

소프트웨어 기반 섀도 복사본 공급자는 일반적으로 파일 시스템과 볼륨 관리자 소프트웨어 간의 소프트웨어 계층에서 읽기 및 쓰기 I/O 요청을 가로채서 처리합니다.

이러한 공급자는 사용자 모드 DLL 구성 요소 및 하나 이상의 커널 모드 디바이스 드라이버(일반적으로 스토리지 필터 드라이버)로 구현됩니다. 하드웨어 기반 공급자와 달리, 소프트웨어 기반 공급자는 하드웨어 수준이 아니라 소프트웨어 수준에서 섀도 복사본을 만듭니다.

소프트웨어 기반 섀도 복사본 공급자는 섀도 복사본을 만들기 전에 볼륨 상태를 다시 만드는 데 사용할 수 있는 데이터 세트에 액세스하여 볼륨의 "특정 시점" 보기를 유지해야 합니다. 예를 들어 시스템 공급자의 기록 중 복사 기술이 있습니다. 그러나 볼륨 섀도 복사본 서비스는 소프트웨어 기반 공급자에서 섀도 복사본을 만들고 유지 관리하는 데 사용하는 기술을 제한하지 않습니다.

소프트웨어 공급자는 하드웨어 기반 공급자보다 더 광범위한 스토리지 플랫폼에 적용할 수 있으며, 기본 디스크 또는 논리 볼륨과 동일하게 작동해야 합니다. (논리 볼륨은 둘 이상의 디스크에서 사용 가능한 공간을 결합하여 만든 볼륨입니다.) 하드웨어 섀도 복사본과 달리, 소프트웨어 공급자는 운영 체제 리소스를 사용하여 섀도 복사본을 유지 관리합니다.

기본 디스크에 대한 자세한 내용은 TechNet의 [기본 디스크 및 볼륨이란?](https://go.microsoft.com/fwlink/?linkid=180894) (https://go.microsoft.com/fwlink/?LinkId=180894) 을 참조하세요.

### <a name="system-provider"></a>시스템 공급자

섀도 복사본 공급자 중 하나인 시스템 공급자는 Windows 운영 체제에 제공됩니다. Windows에서 기본 공급자를 제공하지만, 다른 공급업체는 스토리지 하드웨어 및 소프트웨어 애플리케이션에 최적화된 구현을 무료로 제공할 수 있습니다.

섀도 복사본에 포함된 볼륨의 "특정 시점" 보기를 유지하기 위해 시스템 공급자는 기록 중 복사 기술을 사용합니다. 섀도 복사본 만들기를 시작한 이후 수정된 볼륨의 블록 복사본은 섀도 복사본 저장 영역에 저장됩니다.

시스템 공급자는 정상적으로 쓰고 읽을 수 있는 프로덕션 볼륨을 공개할 수 있습니다. 섀도 복사본이 필요한 경우 프로덕션 볼륨의 데이터에 대한 차이를 논리적으로 적용하여 전체 섀도 복사본을 공개합니다.

시스템 공급자의 경우 섀도 복사본 저장 영역은 NTFS 볼륨에 있어야 합니다. 섀도 복사할 볼륨은 NTFS 볼륨일 필요는 없지만, 시스템에 탑재된 하나 이상의 볼륨은 NTFS 볼륨이어야 합니다.

시스템 공급자를 구성하는 구성 요소 파일은 swprv.dll 및 volsnap.sys입니다.

### <a name="in-box-vss-writers"></a>기본 제공 VSS 기록기

Windows 운영 체제에는 다양한 Windows 기능에 필요한 데이터를 열거해야 하는 일단의 VSS 기록기가 포함되어 있습니다.

이러한 기록기에 대한 자세한 내용은 다음 Microsoft Docs 웹 페이지를 참조하세요.

- [기본 제공 VSS 기록기](https://docs.microsoft.com/windows/win32/vss/in-box-vss-writers)(https://docs.microsoft.com/windows/win32/vss/in-box-vss-writers)


## <a name="how-shadow-copies-are-used"></a>섀도 복사본을 사용하는 방법

섀도 복사본은 애플리케이션 데이터 및 시스템 상태 정보를 백업하는 것 외에도 다음을 포함한 다양한 용도로 사용할 수 있습니다.

  - LUN 복원(LUN 다시 동기화 및 LUN 교환)

  - 개별 파일 복원(공유 폴더용 섀도 복사본)

  - 전송 가능한 섀도 복사본을 사용하여 데이터 마이닝


### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>LUN 복원(LUN 다시 동기화 및 LUN 교환)

Windows Server 2008 R2 및 Windows 7에서 VSS 요청자는 LUN 다시 동기화(또는 "LUN resync")라는 하드웨어 섀도 복사본 공급자 기능을 사용할 수 있습니다. 이는 애플리케이션 관리자가 데이터를 섀도 복사본에서 원본 LUN 또는 새 LUN으로 복원할 수 있는 빠른 복구 체계입니다.

섀도 복사본은 전체 복제본 또는 차등 섀도 복사본일 수 있습니다. 두 경우 모두 다시 동기화 작업이 완료되면 대상 LUN에서 섀도 복사본 LUN과 동일한 콘텐츠를 갖게 됩니다. 다시 동기화 작업 중에 배열은 블록 수준 복사를 섀도 복사본에서 대상 LUN으로 수행합니다.


> [!NOTE]
> 섀도 복사본은 전송 가능한 하드웨어 섀도 복사본이어야 합니다.
<br>


대부분의 배열에서는 다시 동기화 작업이 시작된 직후에 프로덕션 I/O 작업을 다시 시작할 수 있습니다. 다시 동기화 작업이 진행되는 동안에는 읽기 요청은 섀도 복사본 LUN으로 리디렉션되고, 쓰기 요청은 대상 LUN으로 리디렉션됩니다. 이렇게 하면 배열에서 매우 큰 데이터 세트를 복구하고 몇 초 내에 정상적인 작업을 다시 시작할 수 있습니다.

LUN 다시 동기화는 LUN 교환과 다릅니다. LUN 교환은 Windows Server 2003 SP1 이후 VSS에서 지원한 빠른 복구 시나리오입니다. LUN 교환에서는 섀도 복사본을 가져온 다음, 읽기-쓰기 볼륨으로 변환합니다. 변환은 되돌릴 수 없는 작업이며, 그 이후에는 VSS API를 사용하여 해당 볼륨 및 기본 LUN을 제어할 수 없습니다. 다음 목록에서는 LUN 다시 동기화와 LUN 교환을 비교하는 방법을 설명합니다.

  - LUN 다시 동기화에서 섀도 복사본은 변경되지 않으므로 여러 번 사용할 수 있습니다. LUN 교환에서 섀도 복사본은 복구에 한 번만 사용할 수 있습니다. 이는 안전에 가장 민감한 관리자에게 중요합니다. LUN 다시 동기화를 사용할 때 문제가 처음 발생하는 경우 요청자는 전체 복원 작업을 다시 시도할 수 있습니다.

  - LUN 교환이 완료되면 섀도 복사본 LUN이 프로덕션 I/O 요청에 사용됩니다. 이러한 이유로 복구 작업 후 성능에 영향을 주지 않도록 섀도 복사본 LUN에서 원본 프로덕션 LUN과 동일한 품질의 스토리지를 사용해야 합니다. LUN 다시 동기화를 대신 사용하는 경우 하드웨어 공급자는 프로덕션 품질 스토리지보다 저렴한 스토리지에서 섀도 복사본을 유지할 수 있습니다.

  - 대상 LUN을 사용할 수 없고 다시 만들어야 하는 경우 대상 LUN이 필요하지 않으므로 LUN 교환이 더 경제적일 수 있습니다.


> [!WARNING]
> 나열된 모든 작업은 LUN 수준 작업입니다. LUN 다시 동기화를 사용하여 특정 볼륨을 복구하려는 경우 자신도 모르게 해당 LUN을 공유하는 다른 모든 볼륨도 되돌릴 수 있습니다.
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>개별 파일 복원(공유 폴더용 섀도 복사본)

공유 폴더용 섀도 복사본은 볼륨 섀도 복사본 서비스를 사용하여 파일 서버와 같은 공유 네트워크 리소스에 있는 파일의 특정 시점 복사본을 제공합니다. 공유 폴더용 섀도 복사본을 사용하면 네트워크에 저장된 삭제되거나 변경된 파일을 빠르게 복구할 수 있습니다. 관리자의 지원 없이도 복구할 수 있으므로 공유 폴더용 섀도 복사본은 생산성을 높이고 관리 비용을 절감할 수 있습니다.

[공유 폴더용 섀도 복사본](https://go.microsoft.com/fwlink/?linkid=180898)에 대한 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=180898) TechNet의 공유 폴더용 섀도 복사본(영문)를 참조하세요.

### <a name="data-mining-by-using-transportable-shadow-copies"></a>전송 가능한 섀도 복사본을 사용하여 데이터 마이닝

볼륨 섀도 복사본 서비스에서 사용하도록 설계된 하드웨어 공급자를 사용하면 동일한 하위 시스템(예: SAN) 내의 서버로 가져올 수 있는 전송 가능한 섀도 복사본을 만들 수 있습니다. 이러한 섀도 복사본은 데이터 마이닝을 위한 읽기 전용 데이터로 프로덕션 또는 테스트 설치를 시드하는 데 사용할 수 있습니다.

볼륨 섀도 복사본 서비스 및 볼륨 섀도 복사본 서비스에서 사용하도록 설계된 하드웨어 공급자가 있는 스토리지 배열을 사용하면 한 서버에서 원본 데이터 볼륨의 섀도 복사본을 만든 다음, 해당 섀도 복사본을 다른 서버로(또는 동일한 서버로 다시) 가져올 수 있습니다. 이 프로세스는 데이터 크기에 관계없이 몇 분 이내에 수행됩니다. 전송 프로세스는 전송 가능한 섀도 복사본을 지원하는 섀도 복사본 요청자(스토리지 관리 애플리케이션)를 사용하는 일련의 단계를 통해 수행됩니다.

## <a name="to-transport-a-shadow-copy"></a>섀도 복사본을 전송하려면

1.  서버에서 원본 데이터의 전송 가능한 섀도 복사본을 만듭니다.

2.  섀도 복사본을 SAN에 연결된 서버로 가져옵니다(다른 서버나 동일한 서버로 가져올 수 있음).

3.  이제 데이터를 사용할 준비가 되었습니다.

![](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**그림 3**   섀도 복사본 만들기 및 두 서버 간에 전송


> [!NOTE]
> Windows Server 2003에서 만든 전송 가능한 섀도 복사본은 Windows Server 2008 또는 Windows Server 2008 R2를 실행하는 서버로 가져올 수 없습니다. Windows Server 2008 또는 Windows Server 2008 R2에서 만든 전송 가능한 섀도 복사본은 Windows Server 2003을 실행하는 서버로 가져올 수 없습니다. 그러나 Windows Server 2008에서 만든 섀도 복사본은 Windows Server 2008 R2를 실행하는 서버로 가져올 수 있으며, 그 반대의 경우도 마찬가지입니다.
<br>


섀도 복사본은 읽기 전용이기 때문에 섀도 복사본을 읽기/쓰기 LUN으로 변환하려는 경우 볼륨 섀도 복사본 서비스 외에도 가상 디스크 서비스 기반 스토리지 관리 애플리케이션(일부 요청자 포함)을 사용할 수 있습니다. 이 애플리케이션을 사용하면 볼륨 섀도 복사본 서비스 관리에서 섀도 복사본을 제거하고 이를 읽기/쓰기 LUN으로 변환할 수 있습니다.

볼륨 섀도 복사본 서비스 전송은 Windows Server 2003 Enterprise Edition, Windows Server 2003 Datacenter Edition, Windows Server 2008 또는 Windows Server 2008 R2를 실행하는 컴퓨터의 고급 솔루션입니다. 하드웨어 공급자가 스토리지 배열에 있는 경우에만 작동합니다. 섀도 복사본 전송은 테이프 백업, 데이터 마이닝 및 테스트를 포함한 다양한 용도로 사용할 수 있습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

이 FAQ는 시스템 관리자를 대신하여 VSS(볼륨 섀도 복사본 서비스)에 대한 질문에 답변합니다. VSS 응용 프로그램 프로그래밍 인터페이스에 대한 자세한 내용은 Windows 개발자 센터 라이브러리에서 [볼륨 섀도 복사본 서비스](https://go.microsoft.com/fwlink/?linkid=180899) (https://go.microsoft.com/fwlink/?LinkId=180899) 영문)을 참조하세요.

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>볼륨 섀도 복사본 서비스는 언제 도입되었나요? 사용할 수 있는 Windows 운영 체제 버전은 무엇인가요?

VSS는 Windows XP에서 처음 도입되었습니다. Windows XP, Windows Server 2003, Windows Vista®, Windows Server 2008, Windows 7 및 Windows Server 2008 R2에서 사용할 수 있습니다.

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>섀도 복사본과 백업의 차이점은 무엇인가요?

하드 디스크 드라이브 백업의 경우 생성한 섀도 복사본은 백업이기도 합니다. 복원을 위해 섀도 복사본에서 데이터를 복사할 수 있거나, 섀도 복사본을 사용하여 빠른 복구 시나리오(예: LUN 다시 동기화 또는 LUN 교환)에 사용할 수 있습니다.

데이터를 섀도 복사본에서 테이프 또는 기타 이동식 미디어로 복사할 때 백업이 미디어에 저장된 콘텐츠로 구성됩니다. 섀도 복사본 자체는 데이터를 복사한 후에 삭제할 수 있습니다.

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>볼륨 섀도 복사본 서비스에서 지원하는 가장 큰 크기의 볼륨은 무엇인가요?

볼륨 섀도 복사본 서비스는 최대 64TB의 볼륨 크기를 지원합니다.

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Windows Server 2008에서 백업을 수행했습니다. Windows Server 2008 R2에서 이 백업을 복원할 수 있나요?

사용한 백업 소프트웨어에 따라 달라집니다. 대부분의 백업 프로그램은 데이터에 대해 이 시나리오를 지원하지만 시스템 상태 백업에는 지원하지 않습니다.

이러한 Windows 버전 중 하나에서 만든 섀도 복사본은 다른 버전에서 사용할 수 있습니다.

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Windows Server 2003에서 백업을 수행했습니다. Windows Server 2008에서 이 백업을 복원할 수 있나요?

사용한 백업 소프트웨어에 따라 달라집니다. Windows Server 2003에서 섀도 복사본을 만드는 경우 이 섀도 복사본은 Windows Server 2008에서 사용할 수 없습니다. 또한 Windows Server 2008에서 섀도 복사본을 만드는 경우 섀도 복사본은 Windows Server 2003에서 사용할 수 없습니다.

### <a name="how-can-i-disable-vss"></a>VSS를 사용하지 않도록 설정하려면 어떻게 해야 하나요?

Microsoft Management Console을 사용하여 볼륨 섀도 복사본 서비스를 사용하지 않도록 설정할 수 있습니다. 그러나 이 작업을 수행하면 안 됩니다. VSS를 사용하지 않도록 설정하면 시스템 복원 및 Windows Server 백업과 같이 VSS를 사용하는 소프트웨어에 부정적인 영향을 줍니다.

자세한 내용은 다음 Microsoft TechNet 웹 사이트를 방문하세요.

- [시스템 복원](https://go.microsoft.com/fwlink/?linkid=157113)(https://go.microsoft.com/fwlink/?LinkID=157113)

- [Windows Server 백업](https://go.microsoft.com/fwlink/?linkid=180891)(https://go.microsoft.com/fwlink/?LinkID=180891)


### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>공간을 절약하기 위해 섀도 복사본에서 파일을 제외할 수 있나요?

VSS는 전체 볼륨의 섀도 복사본을 만들도록 설계되었습니다. 페이징 파일과 같은 임시 파일은 공간을 절약하기 위해 섀도 복사본에서 자동으로 생략됩니다.

섀도 복사본에서 특정 파일을 제외하려면 **FilesNotToSnapshot** 레지스트리 키를 사용합니다.


> [!NOTE]
> <STRONG>FilesNotToSnapshot</STRONG> 레지스트리 키는 애플리케이션에서만 사용할 수 있습니다. 이 키를 사용하려는 사용자에게는 다음과 같은 제한 사항이 있습니다.
> <br>
> <UL>
> <LI>이전 버전 기능을 사용하여 Windows Server에서 만든 섀도 복사본에서 파일을 삭제할 수 없습니다.<BR><BR>
> <LI>공유 폴더용 섀도 복사본에서 파일을 삭제할 수 없습니다.<BR><BR>
> <LI><a href="https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow)">Diskshadow</a> 유틸리티를 사용하여 만든 섀도 복사본에서 파일을 삭제할 수 있지만, <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin)">Vssadmin</a> 유틸리티를 사용하여 만든 섀도 복사본에서는 파일을 삭제할 수 없습니다.<BR><BR>
> <LI>파일은 섀도 복사본에서 가장 효율적으로 삭제됩니다. 즉, 삭제되지 않을 수 있습니다.<BR><BR></LI></UL>


자세한 내용은 MSDN의 [섀도 복사본에서 파일 제외](https://go.microsoft.com/fwlink/?linkid=180904)(https://go.microsoft.com/fwlink/?LinkId=180904) 를 참조하세요.

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>VSS 오류로 인해 타사 백업 프로그램이 실패했습니다. 어떻게 해야 하나요?

백업 프로그램을 만든 회사의 웹 사이트에 있는 제품 지원 섹션을 확인하세요. 문제를 해결하기 위해 다운로드하여 설치할 수 있는 제품 업데이트가 있을 수 있습니다. 그렇지 않으면 회사의 제품 지원 부서에 문의하세요.

시스템 관리자는 다음 Microsoft TechNet 라이브러리 웹 사이트의 VSS 문제 해결 정보를 사용하여 VSS 관련 문제에 대한 진단 정보를 수집할 수 있습니다.

자세한 내용은 TechNet의 [볼륨 섀도 복사본 서비스](https://go.microsoft.com/fwlink/?linkid=180905)(https://go.microsoft.com/fwlink/?LinkId=180905) 를 참조하세요.

### <a name="what-is-the-diff-area"></a>"차등 영역"은 무엇인가요?

섀도 복사본 저장 영역(또는 "차등 영역")은 시스템 소프트웨어 공급자에서 만든 섀도 복사본의 데이터가 저장되는 위치입니다.

### <a name="where-is-the-diff-area-located"></a>차등 영역은 어디에 있나요?

차등 영역은 모든 로컬 볼륨에 있을 수 있습니다. 그러나 저장 공간이 충분한 NTFS 볼륨에 있어야 합니다.

### <a name="how-is-the-diff-area-location-determined"></a>차등 영역 위치는 어떻게 결정되나요?

차등 영역 위치를 결정하기 위해 다음 기준이 순서대로 평가됩니다.

  - 기존 섀도 복사본이 볼륨에 이미 있는 경우 해당 위치가 사용됩니다.

  - 원본 볼륨과 섀도 복사본 볼륨의 위치 간에 미리 구성된 수동 연결이 있는 경우 해당 위치가 사용됩니다.

  - 앞의 두 기준에서 위치를 제공하지 않는 경우 섀도 복사본 서비스에서 사용 가능한 공간에 따라 위치를 선택합니다. 둘 이상의 볼륨이 섀도 복사되는 경우 섀도 복사본 서비스에서 사용 가능한 공간의 크기에 따라 가능한 스냅샷 위치 목록을 내림차순으로 만듭니다. 제공되는 위치의 수는 섀도 복사되는 볼륨의 수와 같습니다.

  - 섀도 복사되는 볼륨이 가능한 위치 중 하나인 경우 로컬 연결이 만들어집니다. 그렇지 않으면 사용 가능한 공간이 가장 많은 볼륨과의 연결이 만들어집니다.


### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>VSS에서 NTFS가 아닌 볼륨의 섀도 복사본을 만들 수 있나요?

예. 그러나 영구 섀도 복사본은 NTFS 볼륨에만 만들 수 있습니다. 또한 시스템에 탑재된 하나 이상의 볼륨은 NTFS 볼륨이어야 합니다.

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>한 번에 만들 수 있는 최대 섀도 복사본 수는 얼마인가요?

단일 섀도 복사본 세트에서 섀도 복사되는 최대 볼륨 수는 64개입니다. 이는 섀도 복사본 수와 같지 않습니다.

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>시스템 공급자에서 볼륨에 만들어 유지 관리할 수 있는 소프트웨어 섀도 복사본의 최대 수는 얼마인가요?

각 볼륨의 최대 소프트웨어 섀도 복사본 수는 512개입니다. 그러나 기본적으로 공유 폴더의 섀도 복사본 기능에서 사용하는 64개의 섀도 복사본만 유지 관리할 수 있습니다. 공유 폴더의 섀도 복사본 기능에 대한 제한을 변경하려면 **MaxShadowCopies** 레지스트리 키를 사용합니다.

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>섀도 복사본 저장 공간에 사용되는 공간을 제어하려면 어떻게 해야 하나요?

**vssadmin resize shadowstorage** 명령을 입력합니다.

자세한 내용은 TechNet의 [vssadmin resize shadowstorage](https://go.microsoft.com/fwlink/?linkid=180906)(https://go.microsoft.com/fwlink/?LinkId=180906) 를 참조하세요.

### <a name="what-happens-when-i-run-out-of-space"></a>공간이 부족하면 어떻게 되나요?

볼륨의 섀도 복사본은 가장 오래된 섀도 복사본부터 삭제됩니다.

## <a name="volume-shadow-copy-service-tools"></a>볼륨 섀도 복사본 서비스 도구

Windows 운영 체제에서 VSS 작업을 위해 제공하는 도구는 다음과 같습니다.

  - [DiskShadow](https://go.microsoft.com/fwlink/?linkid=180907)(https://go.microsoft.com/fwlink/?LinkId=180907)

  - [VssAdmin](https://go.microsoft.com/fwlink/?linkid=84008)(https://go.microsoft.com/fwlink/?LinkId=84008)


### <a name="diskshadow"></a>DiskShadow

DiskShadow는 시스템에서 사용할 수 있는 모든 하드웨어 및 소프트웨어 스냅샷을 관리하는 데 사용할 수 있는 VSS 요청자입니다. DiskShadow에 포함된 명령은 다음과 같습니다.

  - **list**: VSS 기록기, VSS 공급자 및 섀도 복사본을 나열합니다.

  - **create**: 새 섀도 복사본을 만듭니다.

  - **import**: 전송 가능한 섀도 복사본을 가져옵니다.

  - **expose**: 영구 섀도 복사본을 공개합니다(예: 드라이브 문자로).

  - **revert**: 볼륨을 지정된 섀도 복사본으로 되돌립니다.


이 도구는 IT 전문가를 위한 것이지만, 개발자가 VSS 기록기 또는 VSS 공급자를 테스트하는 경우에도 유용할 수 있습니다.

DiskShadow는 Windows Server 운영 체제에서만 사용할 수 있으며, Windows 클라이언트 운영 체제에서는 사용할 수 없습니다.

### <a name="vssadmin"></a>VssAdmin

VssAdmin은 섀도 복사본에 대한 정보를 만들고, 삭제하고, 나열하는 데 사용됩니다. 또한 섀도 복사본 저장 영역("차등 영역")의 크기를 조정하는 데에도 사용할 수 있습니다.

VssAdmin에 포함된 명령은 다음과 같습니다.

  - **create shadow**: 새 섀도 복사본을 만듭니다.

  - **delete shadows**: 섀도 복사본을 삭제합니다.

  - **list providers**: 모든 등록된 VSS 공급자를 나열합니다.

  - **list writers**: 모든 구독된 VSS 기록기를 나열합니다.

  - **resize shadowstorage**: 섀도 복사본 저장 영역의 최대 크기를 변경합니다.


VssAdmin은 시스템 소프트웨어 공급자에서 만든 섀도 복사본을 관리하는 데만 사용할 수 있습니다.

VssAdmin은 Windows 클라이언트 및 Windows Server 운영 체제 버전에서 사용할 수 있습니다.

## <a name="volume-shadow-copy-service-registry-keys"></a>볼륨 섀도 복사본 서비스 레지스트리 키

VSS에서 사용할 수 있는 레지스트리 키는 다음과 같습니다.

  - **VssAccessControl**

  - **MaxShadowCopies**

  - **MinDiffAreaFileSize**


### <a name="vssaccesscontrol"></a>VssAccessControl

이 키는 섀도 복사본에 액세스할 수 있는 사용자를 지정하는 데 사용됩니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조하세요.

  - [기록기에 대한 보안 고려 사항](https://go.microsoft.com/fwlink/?linkid=157739)(https://go.microsoft.com/fwlink/?LinkId=157739)

  - [요청자에 대한 보안 고려 사항](https://go.microsoft.com/fwlink/?linkid=180908)(https://go.microsoft.com/fwlink/?LinkId=180908)


### <a name="maxshadowcopies"></a>MaxShadowCopies

이 키는 컴퓨터의 각 볼륨에 저장할 수 있는 클라이언트 액세스 가능 섀도 복사본의 최대 수를 지정합니다. 클라이언트에서 액세스 가능한 섀도 복사본은 공유 폴더용 섀도 복사본에서 사용됩니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조하세요.

**MaxShadowCopies**([백업 및 복원 레지스트리 키](https://go.microsoft.com/fwlink/?linkid=180909)(https://go.microsoft.com/fwlink/?LinkId=180909) 아래)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

이 키는 섀도 복사본 저장 영역의 최소 초기 크기(MB)를 지정합니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조하세요.

**MinDiffAreaFileSize**([백업 및 복원 레지스트리 키](https://go.microsoft.com/fwlink/?linkid=180910)(https://go.microsoft.com/fwlink/?LinkId=180910) 아래)

### <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전

다음 표에는 VSS 기능에 지원되는 최소 운영 체제 버전이 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>VSS 기능</th>
<th>지원되는 최소 클라이언트</th>
<th>지원되는 최소 서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LUN 다시 동기화</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2008 R2</p></td>
</tr>
<tr class="even">
<td><p><strong>FilesNotToSnapshot</strong> 레지스트리 키</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td><p>전송 가능한 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2003 SP1</p></td>
</tr>
<tr class="even">
<td><p>하드웨어 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>이전 버전의 Windows Server</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="even">
<td><p>LUN 교환을 사용한 빠른 복구</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2003 SP1</p></td>
</tr>
<tr class="odd">
<td><p>하드웨어 섀도 복사본 여러 번 가져오기</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="media/volume-shadow-copy-service/Dd560667.note(WS.10).gif" />참고</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>섀도 복사본을 두 번 이상 가져오는 기능입니다. 한 번에 하나의 가져오기 작업만 수행할 수 있습니다.
<p></p></td>
</tr>
</tbody>
</table>
<p></p>
</div></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>공유 폴더용 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>전송 가능한 자동 복구 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>동시 백업 세션 수(최대 64개)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>백업과의 동시 복원 단일 세션</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003 SP2</p></td>
</tr>
<tr class="even">
<td><p>백업과의 동시 복원 최대 8개 세션</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>참고 항목

[Windows 개발자 센터의 볼륨 섀도 복사본 서비스](https://docs.microsoft.com/windows/desktop/vss/volume-shadow-copy-service-overview)
