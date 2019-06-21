---
Title: 볼륨 섀도 복사본 서비스
ms.date: 01/30/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 0a4af25723c6d1e796cd3255875c15faf21fb8be
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284381"
---
# <a name="volume-shadow-copy-service"></a>볼륨 섀도 복사본 서비스

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008, Windows 10, Windows 8.1, Windows 8, Windows 7

백업 및 복원 하는 중요 한 비즈니스 데이터는 다음 문제로 인해 매우 복잡할 수 있습니다.

  - 데이터는 일반적으로 데이터를 생성 하는 응용 프로그램이 실행 되는 동안 백업 해야 합니다. 즉, 데이터 파일 중 일부가 열려 있을 하거나 일관성 없는 상태로 될 수 있습니다.  
      
  - 데이터 집합이 큰 경우에 모두 한 번에 백업 하려면 어려울 수 있습니다.  
      

백업 응용 프로그램는 백업 되는 기간 업무 응용 프로그램 및 저장소 관리 하드웨어 및 소프트웨어 간의 긴밀 한 협력을 해야 올바르게 백업 및 복원 작업을 수행 합니다. 복사 서비스 VSS (볼륨 섀도), Windows Server® 2003에 도입 된, 보다 효과적으로 일할 수 있도록 하려면 이러한 구성 요소 간의 대화를 지원 합니다. 모든 구성 요소가 VSS를 지원 하는 경우에 응용 프로그램을 오프 라인으로 전환 하지 않고 응용 프로그램 데이터를 백업 하려면 사용할 수 있습니다.

VSS 백업 되는 데이터의 일관 된 섀도 복사본 (스냅숏 또는 지정 시간 복사본 라고도 함)를 만드는 데 필요한 작업을 조정 합니다. 섀도 복사본으로 사용할 수 있습니다-인 또는 다음과 같은 시나리오에서 사용할 수 있습니다.

  - 응용 프로그램 데이터 및 시스템 상태 정보를 다른 하드 디스크 드라이브, 테이프 또는 다른 이동식 미디어로 데이터 보관을 포함 하 여 백업 하려고 합니다.  
      
  - 데이터 마이닝 있습니다.  
      
  - 디스크-디스크 백업을 수행 하려고 합니다.  
      
  - 실패 한 원본 LUN을 대체 하는 완전히 새로운 LUN 또는 원래 LUN에 데이터를 복원 하 여 데이터 손실 로부터 빠른 복구를 해야 합니다.  
      

Windows 기능 및 VSS를 사용 하는 응용 프로그램에는 다음과 같습니다.

  - [Windows Server Backup](http://go.microsoft.com/fwlink/?linkid=180891) (http://go.microsoft.com/fwlink/?LinkId=180891)  
      
  - [공유 폴더의 섀도 복사본](http://go.microsoft.com/fwlink/?linkid=142874) (http://go.microsoft.com/fwlink/?LinkId=142874)  
      
  - [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=180892) (http://go.microsoft.com/fwlink/?LinkId=180892)  
      
  - [시스템 복원](http://go.microsoft.com/fwlink/?linkid=180893) (http://go.microsoft.com/fwlink/?LinkId=180893)  
      

## <a name="how-volume-shadow-copy-service-works"></a>볼륨 섀도 복사본 서비스의 작동 원리

완전 한 VSS 솔루션에 다음 기본 부분이 모두 필요합니다.

**VSS 서비스**   다른 구성 요소를 보장 하는 Windows 운영 체제의 일부로 서로 올바르게 통신할 수와 함께 사용 합니다.

**VSS 요청자**   섀도 복사본 (또는 가져오기 또는 삭제와 같은 기타 상위 수준 작업)의 실제 생성을 요청 하는 소프트웨어입니다. 일반적으로이 백업 응용 프로그램입니다. Windows Server 백업 유틸리티 및 System Center Data Protection Manager 응용 프로그램 VSS 요청자는입니다. Microsoft 이외의® VSS 요청자는 Windows에서 실행 되는 거의 모든 백업 소프트웨어를 포함 합니다.

**VSS 기록기**   백업할 일관 된 데이터 집합이 있는 것을 보장 하는 구성 요소입니다. 일반적으로 SQL Server® 또는 Exchange Server와 같은 기간 업무 응용 프로그램의 일부로 제공 됩니다. 레지스트리와 같은 다양 한 Windows 구성 요소에 대 한 VSS 기록기는 Windows 운영 체제 포함 됩니다. 비-Microsoft VSS 기록기 등록 백업 중 데이터 일관성을 보장 해야 하는 Windows에 대 한 많은 응용 프로그램에 포함 됩니다.

**VSS 공급자**   만들어 섀도 복사본을 유지 하는 구성 요소입니다. 하드웨어 또는 소프트웨어에서 발생할 수 있습니다. Windows 운영 체제는 기록 중 복사를 사용 하는 VSS 공급자를 포함 합니다. 저장 영역 네트워크 (SAN)를 사용 하는 경우 제공 되는 경우 SAN에 대 한 VSS 하드웨어 공급자를 설치 하는 중요 한 됩니다. 하드웨어 공급자를 만들고 호스트 운영 체제에서 섀도 복사본을 유지 관리 작업을 오프 로드 합니다.

다음 다이어그램에서는 VSS는 볼륨의 섀도 복사본을 만들려면 요청자, 기록기 및 공급자를 사용 하 여 좌표를 서비스 하는 방법을 보여 줍니다.

![](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**그림 1**   볼륨 섀도 복사본 서비스의 아키텍처 다이어그램

### <a name="how-a-shadow-copy-is-created"></a>섀도 복사본을 만드는 방법을

이 섹션에서는 섀도 복사본을 만들 하기 위해 수행 해야 하는 단계를 나열 하 여 컨텍스트에 요청자, 저자, 그리고 공급자의 다양 한 역할을 넣습니다. 다음 다이어그램은 볼륨 섀도 복사본 서비스 요청자, 저자, 그리고 공급자의 전체 조정을 제어 하는 방법을 보여 줍니다.

![](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**그림 2** 섀도 복사본 생성 프로세스

요청자, 기록기 및 공급자는 섀도 복사본을 만들려면 다음 작업을 수행 합니다.

1.  요청자는 기록기를 열거, 기록기 메타 데이터를 수집 하 고, 섀도 복사본 만들기를 준비 하는 볼륨 섀도 복사본 서비스를 요청 합니다.  
      
2.  각 작성기를 백업 해야 하는 구성 요소 및 데이터 저장소에 대 한 XML 설명을 만들고 볼륨 섀도 복사본 서비스를 제공 합니다. 작성기에는 또한 모든 구성 요소에 사용 되는 복원 메서드를 정의 합니다. 볼륨 섀도 복사본 서비스는 백업 되는 구성 요소를 선택 하는 요청자에 게는 기록기의 설명 합니다.  
      
3.  볼륨 섀도 복사본 서비스는 섀도 복사본에 대 한 데이터를 준비 하려면 모든 기록기를 알립니다.  
      
4.  각 작성기는 적절 하 게 데이터를 준비, 모두 완료와 같은 트랜잭션, 트랜잭션 로그를 롤링 및 캐시 플러시를 엽니다. 데이터 섀도 복사 되도록 준비 되 면 볼륨 섀도 복사본 서비스 기록기에 알립니다.  
      
5.  볼륨 섀도 복사본 서비스 기록기 응용 프로그램 쓰기 I/O 요청 (읽기 I/O 요청은 여전히 가능)를 일시적으로 중지 지시 된 볼륨 또는 볼륨의 섀도 복사본을 만드는 데 필요한 몇 초입니다. 응용 프로그램 중지 60 초 보다 오래 걸리기 허용 되지 않습니다. Volume Shadow Copy Service 파일 시스템 버퍼를 플러시하고 파일 시스템 메타 데이터를 올바르게 기록 되 고 섀도 복사 되도록 데이터에서 일관적인 순서로 기록 됩니다 있는지을 보장 하는 파일 시스템을 중지 합니다.  
      
6.  볼륨 섀도 복사본 서비스 섀도 복사본 공급자에 알려 줍니다. 섀도 복사본 생성 기간 동안 모든 쓰기 파일 시스템에 I/O 요청이 고정 된 상태로 유지 10 초 이하의 지속 됩니다.  
      
7.  볼륨 섀도 복사본 서비스는 파일 시스템 쓰기 I/O 요청을 해제합니다.  
      
8.  VSS 기록기 응용 프로그램 쓰기 I/O 요청을 재개 하도록 지시 합니다. 이 시점에서 응용 프로그램은 섀도 복사 되는 디스크에 데이터 쓰기를 다시 시작 하려면 무료입니다.  
      

> [!NOTE]
> 섀도 복사본을 만드는 기록기 공급자 섀도 복사본을 커밋 하도록 10 초 보다 더 오래 걸릴 경우 60 초 보다 오랫동안 고정 상태로 유지 되 면 중단 될 수 있습니다. 
<br>

9. 요청자에 게 (1 단계로 다시 이동) 하는 프로세스를 다시 시도할 수 있습니다 하거나 나중에 다시 시도 관리자에 게 알립니다.  
      
10. 섀도 복사본을 정상적으로 작성 하는 경우 볼륨 섀도 복사본 서비스 요청자에 게 섀도 복사본 위치 정보를 반환 합니다. 일부 경우에 섀도 복사본을 일시적으로 사용할 수 있습니다 읽기-쓰기 볼륨으로는 VSS 및 하나 이상의 응용 프로그램이 섀도 복사본이 완료 되기 전에 섀도 복사본의 콘텐츠를 변경할 수 있도록 합니다. VSS 및 응용 프로그램 변경 작업을 후 읽기 전용 섀도 복사본이 만들어집니다. 이 단계는 자동 복구 라고 하 고 트랜잭션 실행을 취소 모든 응용 프로그램 또는 파일 시스템 섀도 복사본 볼륨의 섀도 복사본이 만들어지기 전에 완료 되지 않은 데 사용 됩니다.  
      

### <a name="how-the-provider-creates-a-shadow-copy"></a>공급자가 섀도 복사본을 만드는 방법

하드웨어 또는 소프트웨어 섀도 복사본 공급자가 섀도 복사본을 만들기 위한 다음 방법 중 하나를 사용 합니다.

**복사 완료**   이 메서드 시간에서 지정 된 시점 원래 볼륨 ("전체 복사본" 또는 "복제" 라고 함) 전체 복사본을 만듭니다. 이 복사본은 읽기 전용입니다.

**쓰기 시 복사**   이 메서드는 원본 볼륨을 복사 하지 않습니다. 대신, 시간에 지정 된 후 볼륨에 적용 된 모든 변경 내용 (완료 된 쓰기 I/O 요청 수)를 복사 하 여 차등 복사본을 만듭니다.

**쓰기 시 리디렉션**   이 메서드는 원래 볼륨을 복사 하지 않습니다 하 고 해당 변경 하지 않습니다 모든 원본 볼륨에 지정 된 후 시간에서입니다. 대신, 모든 변경 내용을 다른 볼륨으로 리디렉션하여 차등 복사본을 만듭니다.

## <a name="complete-copy"></a>완전 한 복사본

전체 복사본을 다음과 같이 "분할 미러" 하 여 일반적으로 만들어집니다.

1.  원본 볼륨 및 섀도 복사본 볼륨은 미러 볼륨 집합입니다.  
      
2.  원래 볼륨에서 섀도 복사본 볼륨이 분리 됩니다. 이 미러의 연결을 끊습니다.  
      

미러 서버 연결이 중단 되 면 원래 볼륨 및 섀도 복사본 볼륨은 독립적입니다. 원본 볼륨 섀도 복사본 하는 동안 모든 변경 사항 (쓰기 I/O 요청)을 허용 하도록 계속 볼륨 중단 시 원래 데이터의 읽기 전용 복사본을 정확 하 게 유지 합니다.

### <a name="copy-on-write-method"></a>쓰기 시 복사 메서드

쓰기 시 복사 방법에서는 원본 볼륨에 대 한 변경 발생 하면 (쓰기 전에 I/O 요청이 완료 될)를 수정할 각 블록 읽고 볼륨의 섀도 복사본 저장소 영역 (해당 "차등 영역"이 라고도 함)에 기록 합니다. 섀도 복사본 저장 영역의 동일한 볼륨 또는 다른 볼륨에 있을 수 있습니다. 이 변경 내용을 덮어씁니다 전에 원본 볼륨에 있는 데이터 블록의 복사본을 유지 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Time</th>
<th>원본 데이터 (상태 및 데이터)</th>
<th>섀도 복사본 (상태 및 데이터)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>원래 데이터: 1 2 3 4 5</p></td>
<td><p>복사본이:-</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>데이터 캐시에서 변경: 3에 3 '</p></td>
<td><p>섀도 복사본 생성 (차이점에만 해당): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>원래 데이터를 덮어씁니다. 1 2 3’ 4 5</p></td>
<td><p>차이점 및 섀도 복사본에 저장 된 인덱스의 경우: 3</p></td>
</tr>
</tbody>
</table>

**표 1**   섀도 복사본을 만드는 쓰기 시 복사 메서드

쓰기 시 복사 메서드 섀도 복사본을 만들기 위한 빠른 방법 이므로 변경 된 데이터만 복사 합니다. 변경 전의 상태로 볼륨을 복원 하려면 원래 볼륨에서 변경 된 데이터를 사용 하 여 차등 영역에서 복사한 요소를 결합할 수 있습니다. 많은 변경 내용이 기록 중 복사 메서드 비용이 많이 드는 될 수 있습니다.

### <a name="redirect-on-write-method"></a>쓰기 시 리디렉션 메서드

쓰기 시 리디렉션 메서드를 원래 볼륨에서 변경 (쓰기 I/O 요청)을 받을 때마다 원본 볼륨에 변경 내용이 적용 되지 않습니다. 대신, 변경 내용은 다른 볼륨의 섀도 복사본 저장소 영역에 기록 됩니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Time</th>
<th>원본 데이터 (상태 및 데이터)</th>
<th>섀도 복사본 (상태 및 데이터)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>원래 데이터: 1 2 3 4 5</p></td>
<td><p>복사본이:-</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>데이터 캐시에서 변경: 3에 3 '</p></td>
<td><p>섀도 복사본 생성 (차이점에만 해당): 3’</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>원래 데이터를 변경 되지 않음: 1 2 3 4 5</p></td>
<td><p>차이점 및 섀도 복사본에 저장 된 인덱스의 경우: 3’</p></td>
</tr>
</tbody>
</table>

**표 2**   섀도 복사본을 만드는 쓰기 리디렉션 메서드

쓰기 시 복사 메서드처럼 쓰기 리디렉션 메서드는 데이터 변경 내용만 복사 하므로 섀도 복사본을 만들기 위한 빠른 메서드입니다. 차등 영역에서 복사한 요소는 데이터의 완전 한 최신 사본을 만들 원본 볼륨의 변경 되지 않은 데이터와 결합할 수 있습니다. 읽기 I/O 요청이 많은 경우에 쓰기 리디렉션 메서드 비용이 많이 드는 될 수 있습니다.

## <a name="shadow-copy-providers"></a>섀도 복사본 공급자

섀도 복사본 공급자의 두 가지가: 하드웨어 기반의 공급자 및 공급자 소프트웨어를 기반으로 합니다. Windows 운영 체제 기본 제공 되는 소프트웨어 공급 업체는 시스템 공급자 이기도 합니다.

### <a name="hardware-based-providers"></a>하드웨어 기반의 공급자

볼륨 섀도 복사본 서비스 및 저장소 어댑터 하드웨어 또는 컨트롤러를 함께에서 사용 하 여 하드웨어 수준 간의 인터페이스로 하드웨어 기반 섀도 복사본 공급자 작업. 저장소 배열에서 만들고 섀도 복사본을 유지 관리 작업 수행 됩니다.

항상 하드웨어 공급자는 전체 LUN의 섀도 복사본을 걸리지만 Volume Shadow Copy Service에만 요청 된 볼륨을 볼륨의 섀도 복사본을 노출 합니다.

하드웨어 기반 섀도 복사본 공급자는 볼륨 섀도 복사본 서비스 사용 시점을에서 정의 하는 기능 데이터 동기화를 허용 섀도 복사본을 관리 하 고 백업 응용 프로그램을 사용 하 여 공통 인터페이스를 제공 합니다. 그러나 볼륨 섀도 복사본 서비스는 하드웨어 기반 공급자를 생성 하 고 섀도 복사본을 유지 관리의 기본 메커니즘을 지정 하지 않습니다.

### <a name="software-based-providers"></a>공급자 소프트웨어를 기반으로

소프트웨어를 기반으로 하는 섀도 복사본 공급자 일반적으로 가로채 거 나 프로세스 읽기 및 쓰기 I/O 요청이 파일 시스템 및 볼륨 관리자 소프트웨어 간의 소프트웨어 계층입니다.

이러한 공급자는 사용자 모드 DLL 구성 요소 및 하나 이상의 커널 모드 장치 드라이버를 저장소 필터 드라이버는 일반적으로 구현 됩니다. 하드웨어 기반 공급자와 달리 공급자 소프트웨어를 기반으로 하드웨어 수준이 아닌 소프트웨어 수준에서 섀도 복사본을 만듭니다.

소프트웨어를 기반으로 하는 섀도 복사본 공급자 섀도 복사본 생성 시간 전에 볼륨 상태를 다시 만드는 데 사용할 수 있는 데이터 집합을 통해 볼륨의 "-시점" 뷰를 유지 해야 합니다. 예로 시스템 공급자의 쓰기 시 복사 기술입니다. 그러나 볼륨 섀도 복사본 서비스는 소프트웨어 기반 공급자를 사용 하 여 만들고 섀도 복사본을 유지 하는 기술에 제한이 배치 합니다.

소프트웨어 공급 업체는 하드웨어 기반 공급자 보다 더 광범위 한 저장소 플랫폼에 적용 됩니다 하 고 기본 디스크 또는 논리 볼륨을 사용 하 여 원활 하 게 작동 해야 합니다. (논리 볼륨은 둘 이상의 디스크에서 사용 가능한 공간을 결합 하 여 만든 볼륨입니다.) 하드웨어 섀도 복사본을 달리 소프트웨어 공급자는 섀도 복사본을 유지 하기 위해 운영 체제 리소스를 사용 합니다.

기본 디스크에 대 한 자세한 내용은 참조 하세요. [기본 디스크와 볼륨 이란?](http://go.microsoft.com/fwlink/?linkid=180894) (http://go.microsoft.com/fwlink/?LinkId=180894) TechNet에 있습니다.

### <a name="system-provider"></a>시스템 공급자

한 섀도 복사본 공급자를 시스템 공급자는 Windows 운영 체제에서 제공 됩니다. Windows에서 기본 공급자가 제공 되지만 다른 공급 업체는 저장소 하드웨어 및 소프트웨어 응용 프로그램에 최적화 된 구현을 제공 합니다.

볼륨 섀도 복사본에 포함 된 "-시점" 보기를 유지 하려면 시스템 공급자는 쓰기 시 복사 기술을 사용 합니다. 볼륨 섀도 복사본 만들기를 시작한 후 수정 된 블록의 복사본을 섀도 복사본 저장소 영역에 저장 됩니다.

시스템 공급자에 기록 하 고 일반적으로에서 읽을 수 있는 프로덕션 볼륨을 노출할 수 있습니다. 섀도 복사본이 필요한 전체 섀도 복사본을 노출 하려면 프로덕션 볼륨에 논리적으로 데이터에 대 한 차이점 적용 합니다.

시스템 공급자에 대 한 섀도 복사본 저장 영역의 NTFS 볼륨에 있어야 합니다. 볼륨 섀도 복사본을 NTFS 볼륨을 사용할 필요가 없습니다 있지만 시스템에 탑재 된 볼륨을 하나 이상에 NTFS 볼륨 이어야 합니다.

시스템 공급자를 구성 하는 구성 요소 파일은 swprv.dll 및 volsnap.sys입니다.

### <a name="in-box-vss-writers"></a>상자에서 VSS 기록기

Windows 운영 체제에는 다양 한 Windows 기능에 필요한 데이터를 열거 하는 일을 담당 하는 VSS 작성자 집합이 포함 됩니다.

이러한 기록기에 대 한 자세한 내용은 다음 Microsoft 웹 사이트를 참조 하세요.

  - [상자에서 VSS 기록기](http://go.microsoft.com/fwlink/?linkid=180895) (http://go.microsoft.com/fwlink/?LinkId=180895)  
      
  - [Windows Server 2008 및 Windows Vista SP1에 대 한 새 기본 VSS 기록기](http://go.microsoft.com/fwlink/?linkid=180896) (http://go.microsoft.com/fwlink/?LinkId=180896)  
      
  - [Windows Server 2008 R2 및 Windows 7에 대 한 새 기본 VSS 기록기](http://go.microsoft.com/fwlink/?linkid=180897) (http://go.microsoft.com/fwlink/?LinkId=180897)  
      

## <a name="how-shadow-copies-are-used"></a>섀도 복사본을 사용 하는 방법

응용 프로그램 데이터 및 시스템 상태 정보를 백업 하는 것 외에도 섀도 복사본에서는 다음과 같은 다양 한 데이터를 사용할 수 있습니다.

  - Lun (LUN 다시 동기화 하 고 LUN)를 복원합니다.  
      
  - 개별 파일 복원 (공유 폴더의 섀도 복사본)  
      
  - 전송 가능한 섀도 복사본을 사용 하 여 데이터 마이닝  
      

### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>Lun (LUN 다시 동기화 하 고 LUN)를 복원합니다.

Windows Server 2008 R2 및 Windows 7에서 VSS 요청자 LUN 동기화 (또는 "LUN 동기화") 이라는 하드웨어 섀도 복사본 공급자 기능을 사용할 수 있습니다. 응용 프로그램 관리자가 새 LUN 또는 원래 LUN에 섀도 복사본에서 데이터를 복원할 수 있는 빠른 복구 구성표입니다.

섀도 복사본을 복제본을 전체 또는 차등 섀도 복사본 수 있습니다. 두 경우 모두 다시 동기화 작업의 끝에서 대상 LUN 내용이 동일한 LUN 섀도 복사본을 갖습니다. 다시 동기화 작업 중 배열 섀도 복사본에서 블록 수준 복사 대상 LUN로 수행합니다.


> [!NOTE]
> 섀도 복사본을 전송 가능한 하드웨어 섀도 복사본 이어야 합니다. 
<br>


대부분의 배열과 동기화 작업 시작 된 후에 곧 다시 시작 하려면 프로덕션 I/O 작업을 허용 합니다. 동기화 작업을 진행 하는 동안 요청 섀도 복사본이 LUN 리디렉션됩니다 읽고 쓸 요청 대상 LUN. 따라서 매우 큰 데이터 집합을 복구 하 고 몇 초 안에 정상적인 작업을 다시 시작 하는 배열입니다.

LUN 다시 동기화는 LUN 교환에서 다릅니다. LUN 교환에는 Windows Server 2003 SP1 이후 VSS 지원 되는 빠른 복구 시나리오입니다. LUN 교환에서 섀도 복사본을 가져오고 읽기-쓰기 볼륨으로 변환 됩니다. 변환 되는 작업을 취소할 수 및 볼륨 및 기본 LUN을 제어할 수 없습니다 VSS Api를 사용 하 여 그 후 합니다. 다음 목록에서는 LUN 교환 된 LUN 다시 동기화 비교 하는 방법을 설명 합니다.

  - LUN 다시 동기화에서 섀도 복사본이 변경 되지 않습니다, 여러 번 사용할 수 있습니다. LUN 교환 섀도 복사본을 사용할 수 한 번만 복구 합니다. 가장 보안에 민감한 관리자에 게이 반드시합니다. LUN 다시 동기화를 사용 하면 오류가 발생 한 경우 처음 요청자에 게 전체 복원 작업을 재시도할 수입니다.  
      
  - LUN 교환 끝 섀도 복사본이 LUN 프로덕션 I/O 요청에 사용 됩니다. 이러한 이유로 섀도 복사본이 LUN는 성능은 복구 작업 후 받지 않습니다 되도록 원래 프로덕션 LUN으로 동일한 품질의 저장소를 사용 해야 합니다. LUN 다시 동기화를 사용 하는 경우 하드웨어 공급자를 프로덕션 수준 저장소 보다 저렴 하 게 연결 된 저장소에 있는 섀도 복사본을 유지할 수 있습니다.  
      
  - 대상 LUN을 사용할 수 없으면을 만들어야 하는 경우 LUN 교환 때문일 수 있습니다 더 경제적 대상 LUN 필요 하지 않습니다.  
      


> [!WARNING]
> 모든 나열 된 작업은 LUN 수준 작업입니다. LUN 다시 동기화를 사용 하 여 특정 볼륨을 복구 하려는 경우 LUN을 공유 하는 다른 모든 볼륨을 되돌리려면 하려는 모르게 합니다. 
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>개별 파일 복원 (공유 폴더의 섀도 복사본)

공유 폴더의 섀도 복사본 파일 서버 등 공유 네트워크 리소스에 있는 파일의 지정 시간 복사본을 제공 하는 볼륨 섀도 복사본 서비스를 사용 합니다. 공유 폴더의 섀도 복사본을 사용 하 여 사용자 네트워크에 저장 된 파일을 삭제 또는 변경 된를 신속 하 게 복구할 수 있습니다. 관리자의 도움 없이 변경할 수 있습니다, 때문에 공유 폴더의 섀도 복사본 생산성을 향상 하 고 관리 비용을 줄일 수 있습니다.

공유 폴더의 섀도 복사본에 대 한 자세한 내용은 참조 [공유 폴더의 섀도 복사본](http://go.microsoft.com/fwlink/?linkid=180898) (http://go.microsoft.com/fwlink/?LinkId=180898) TechNet에 있습니다.

### <a name="data-mining-by-using-transportable-shadow-copies"></a>전송 가능한 섀도 복사본을 사용 하 여 데이터 마이닝

볼륨 섀도 복사본 서비스를 사용 하 여 사용 하도록 설계 된 하드웨어 공급자를 사용 하 여 동일한 하위 시스템 (예: SAN) 내에서 서버로 가져올 수 있는 전송 가능한 섀도 복사본을 만들 수 있습니다. 이 섀도 복사본은 프로덕션 시드 또는 데이터 마이닝에 대 한 읽기 전용 데이터를 사용 하 여 설치를 테스트에 사용할 수 있습니다.

볼륨 섀도 복사본 서비스와 저장소 배열 Volume Shadow Copy Service 사용을 위해 설계 된 하드웨어 공급자를 사용 하 여 하나 이상의 서버에서 원본 데이터 볼륨의 섀도 복사본을 만들고 다음 다른 서버로 섀도 복사본을 가져올 수 있기  (또는 동일한 서버로 백)입니다. 이 프로세스는 데이터의 크기에 관계 없이 몇 분 후에 수행 됩니다. 전송 프로세스는 일련의 전송 가능한 섀도 복사본을 지 원하는 섀도 복사본 요청자 (저장소 관리 응용 프로그램)를 사용 하는 단계를 통해 수행 됩니다.

## <a name="to-transport-a-shadow-copy"></a>섀도 복사본을 전송 하려면

1.  서버에서 원본 데이터의 전송 가능한 섀도 복사본을 만듭니다.

2.  SAN에 연결 된 서버에 섀도 복사본을 가져옵니다 (동일한 서버나 다른 서버에 가져올 수 있음).

3.  데이터를 사용할 준비가 되었습니다.

![](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**그림 3**   두 서버 간에 전송 하 고 섀도 복사본 만들기


> [!NOTE]
> Windows Server 2008을 실행 하는 서버 또는 Windows Server 2008 R2에 Windows Server 2003에서 생성 되는 전송 가능한 섀도 복사본을 가져올 수 없습니다. Windows Server 2003을 실행 하는 서버에 Windows Server 2008 또는 Windows Server 2008 R2에서 만들어진 전송 가능한 섀도 복사본을 가져올 수 없습니다. 그러나 Windows Server 2008 R2 또는 그 반대로 이전을 실행 하는 서버는 Windows Server 2008에서 만들어진 섀도 복사본을 가져올 수 있습니다. 
<br>


섀도 복사본은 읽기 전용이기 때문에 섀도 복사본을 읽기/쓰기 LUN 변환 하려는 경우에 가상 디스크 서비스 기반 저장소 관리 응용 프로그램 (일부 요청자 포함) 볼륨 섀도 복사본 서비스 외에도 사용할 수 있습니다. 이 응용 프로그램을 사용 하 여 섀도 복사본 볼륨 섀도 복사본 서비스 관리에서 제거 수 있으며 읽기/쓰기 LUN으로 변환할 수 있습니다.

볼륨 섀도 복사본 서비스 전송에는 Windows Server 2003 Enterprise Edition, Windows Server 2003 Datacenter Edition, Windows Server 2008 또는 Windows Server 2008 R2를 실행 하는 컴퓨터에서 고급 솔루션입니다. 저장소 배열에 하드웨어 공급자가 하는 경우에 작동 합니다. 섀도 복사 전송에서는 데이터 마이닝, 테스트 및 테이프 백업을 포함 한 다양 한 사용할 수 있습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

이 FAQ는 볼륨 섀도 복사 서비스 (VSS)에 대 한 시스템 관리자에 대 한 질문을 답변합니다. VSS 응용 프로그램 프로그래밍 인터페이스에 대 한 정보를 참조 하세요 [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/?linkid=180899) (http://go.microsoft.com/fwlink/?LinkId=180899) Windows 개발자 센터 라이브러리에서.

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>볼륨 섀도 복사본 서비스 도입 하는 경우 Windows 운영 체제 버전에서 사용 가능한가?

VSS는 Windows XP에 도입 되었습니다. Windows XP, Windows Server 2003, Windows Vista®, Windows Server 2008, Windows 7 및 Windows Server 2008 R2에서 제공 됩니다.

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>섀도 복사본 및 백업 간의 차이 무엇입니까?

하드 디스크 드라이브 백업 섀도 복사본 생성 경우도 백업 합니다. 복원에 대 한 섀도 복사본을 외부 데이터를 복사할 수 있습니다 또는 빠른 복구 시나리오에 대 한 섀도 복사본을 사용할 수 있습니다-예를 들어 LUN 다시 동기화 하거나 LUN 교환 합니다.

데이터는 섀도 복사본에서 테이프나 다른 이동식 미디어에 복사 하는 경우 미디어에 저장 되는 콘텐츠의 백업을 구성 합니다. 데이터에서 복사 된 후에 자체 섀도 복사본을 삭제할 수 있습니다.

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>볼륨 섀도 복사본 서비스를 지 원하는 최대 크기 볼륨은 어떻게 되나요?

볼륨 섀도 복사본 서비스는 최대 64TB의 볼륨 크기를 지원합니다.

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Windows Server 2008에서 백업을 만들었습니다. 복원할 수 해당 Windows Server 2008 R2에서?

사용 하는 백업 소프트웨어에 따라 다릅니다. 시스템 상태 백업이 아니라 데이터에 대 한 대부분의 백업 프로그램에서이 시나리오를 지원 합니다.

다른 Windows의 이러한 버전 중 하나에서 만들어진 섀도 복사본을 사용할 수 있습니다.

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Windows Server 2003에서 백업을 만들었습니다. 복원할 수 해당 Windows Server 2008에서?

사용 하는 백업 소프트웨어에 따라 다릅니다. Windows Server 2003에서 섀도 복사본을 만드는 경우 Windows Server 2008에서 사용할 수 없습니다. 또한 Windows Server 2008에서 섀도 복사본을 만드는 경우 Windows Server 2003에서 복원할 수 없습니다.

### <a name="how-can-i-disable-vss"></a>VSS을 비활성화 하려면 어떻게 해야 하나요?

Microsoft Management Console을 사용 하 여 볼륨 섀도 복사본 서비스를 사용 하지 않도록 설정 하는 것이 가능 합니다. 그러나이 수행 하지 해야 합니다. 부정적인 VSS를 사용 하지 않으면 시스템 복원 Windows Server Backup 등, 종속 된 모든 소프트웨어를 사용에 영향을 줍니다.

자세한 내용은 다음 Microsoft TechNet 웹 사이트를 참조 하세요.

  - [시스템 복원](http://go.microsoft.com/fwlink/?linkid=157113) (http://go.microsoft.com/fwlink/?LinkID=157113)  
      
  - [Windows Server Backup](http://go.microsoft.com/fwlink/?linkid=180891) (http://go.microsoft.com/fwlink/?LinkID=180891)  
      

### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>공간 절약을 위해 섀도 복사본에서 파일 제외

VSS는 전체 볼륨의 섀도 복사본을 만들도록 설계 되었습니다. 페이징 파일과 같은 임시 파일을 공간 절약을 위해 섀도 복사본에서 자동으로 생략 됩니다.

섀도 복사본에서 특정 파일을 제외 하려면 다음 레지스트리 키를 사용 합니다. **FilesNotToSnapshot**.


> [!NOTE]
> 합니다 <STRONG>FilesNotToSnapshot</STRONG> 레지스트리 키만 응용 프로그램에서 사용할 것입니다. 사용 하려고 하는 사용자는 다음과 같은 제한 사항이 발생 합니다.
> <br>
> <UL>
> <LI>이전 버전 기능을 사용 하 여 Windows 서버에 만들어진 섀도 복사본에서 파일을 삭제할 수 없습니다 것입니다.<BR><BR>
> <LI>공유 폴더의 섀도 복사본에서 파일을 삭제할 수 없습니다 것입니다.<BR><BR>
> <LI>사용 하 여 생성 된 섀도 복사본에서 파일을 삭제할 수 있습니다 합니다 <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow)">Diskshadow</a> 유틸리티를 하지만 사용 하 여 생성 된 섀도 복사본에서 파일을 삭제할 수 없습니다는 <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin)">Vssadmin</a> 유틸리티입니다.<BR><BR>
> <LI>최상의 노력을 기준으로 섀도 복사본에서 파일이 삭제 됩니다. 이 삭제 되지 않습니다 보장 되는 것을 의미 합니다.<BR><BR></LI></UL>


자세한 내용은 [섀도 복사본에서 파일 제외](http://go.microsoft.com/fwlink/?linkid=180904) (http://go.microsoft.com/fwlink/?LinkId=180904) MSDN에서.

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>타사 백업 프로그램 VSS 오류로 인해 실패 합니다. 무엇을 도와드릴까요?

백업 프로그램을 만든 회사의 웹 사이트의 제품 지원 섹션을 확인 합니다. 다운로드 및 설치 문제를 해결할 수 있는 제품 업데이트가 있을 수 있습니다. 그렇지 않은 경우 회사의 제품 지원 부서에 문의 하세요.

시스템 관리자 VSS와 관련 된 문제에 대 한 진단 정보를 수집한 다음 Microsoft TechNet 라이브러리 웹 사이트에서 VSS 문제 해결 정보를 사용할 수 있습니다.

자세한 내용은 [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/?linkid=180905) (http://go.microsoft.com/fwlink/?LinkId=180905) TechNet에 있습니다.

### <a name="what-is-the-diff-area"></a>"차등 영역" 이란?

섀도 복사본 저장소 영역 (또는 "차등 영역") 시스템 소프트웨어 공급자에서 만들어진 섀도 복사본에 대 한 데이터가 저장 된 위치입니다.

### <a name="where-is-the-diff-area-located"></a>차등 영역 어디에 있나요?

차등 영역 모든 로컬 볼륨에 있을 수 있습니다. 그러나 저장에 충분 한 공간이 있는 NTFS 볼륨에 배치 해야 합니다.

### <a name="how-is-the-diff-area-location-determined"></a>결정 되는 diff 영역 위치는 어떻게?

다음 조건은 diff 영역 위치를 확인 하려면이 순서 대로 평가 됩니다.

  - 볼륨 섀도 복사본을 기존 이미 있으면 해당 위치가 사용 됩니다.  
      
  - 원본 볼륨 및 섀도 복사본 볼륨 위치 간의 수동 연결을 미리 구성 된 경우 해당 위치가 사용 됩니다.  
      
  - 이전 두 조건을 위치를 제공 하지 않으면 경우 섀도 복사본 서비스는 사용 가능한 공간을 기반으로 하는 위치를 선택 합니다. 둘 이상의 볼륨 섀도 복사 되는, 섀도 복사본 서비스 목록을 내림차순에서 사용 가능한 공간의 크기를 기준으로 가능한 스냅숏 위치를 만듭니다. 제공 된 위치 수가 섀도 복사본 볼륨의 수와 같습니다.  
      
  - 섀도 복사본 볼륨을 사용 하면 가능한 위치 중 하나인 경우 로컬 연결을 생성 됩니다. 그렇지 않으면 가장 사용 가능한 공간이 볼륨와 연결 하 여 만들어집니다.  
      

### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>VSS는 NTFS가 아닌 볼륨의 섀도 복사본을 만들 수 있습니까?

예 그러나 NTFS 볼륨에 대해서만 영구 섀도 복사본을 만들 수 있습니다. 또한 시스템에 탑재 된 볼륨을 하나 이상에 NTFS 볼륨 이어야 합니다.

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>최대 한 번 만들면 섀도 복사본 이란?

단일 섀도 복사본 집합에 있는 섀도 복사본 볼륨의 최대 수는 64입니다. Note이 아닌지 섀도 복사본의 수와 동일 합니다.

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>새로운 소프트웨어 섀도 복사본의 최대가 만들어집니다 시스템 공급자가 볼륨에 대해 유지할 수 있나요?

최대 수는 512 각 볼륨에 대 한 소프트웨어 섀도 복사본입니다. 그러나 기본적으로 64 개의 섀도 복사본 공유 폴더의 섀도 복사본 기능에 의해 사용 되는 유지할 수 있습니다. 공유 폴더의 섀도 복사본 기능에 대 한 제한을 변경 하려면 다음 레지스트리 키를 사용 합니다. **MaxShadowCopies**.

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>섀도 복사본 저장소 공간에 사용 되는 공간을 제어 하는 방법을

형식 합니다 **vssadmin 조정 shadowstorage** 명령입니다.

자세한 내용은 [Vssadmin 조정 shadowstorage](http://go.microsoft.com/fwlink/?linkid=180906) (http://go.microsoft.com/fwlink/?LinkId=180906) TechNet의 합니다.

### <a name="what-happens-when-i-run-out-of-space"></a>공간이 부족할 경우 어떻게 되나요?

섀도 복사본 볼륨에 대 한 오래 된 섀도 복사본이 삭제 됩니다.

## <a name="volume-shadow-copy-service-tools"></a>볼륨 섀도 복사본 서비스 도구

Windows 운영 체제는 VSS를 사용 하 여 작업에 대 한 다음과 같은 도구를 제공 합니다.

  - [DiskShadow](http://go.microsoft.com/fwlink/?linkid=180907) (http://go.microsoft.com/fwlink/?LinkId=180907)  
      
  - [VssAdmin](http://go.microsoft.com/fwlink/?linkid=84008) (http://go.microsoft.com/fwlink/?LinkId=84008)  
      

### <a name="diskshadow"></a>DiskShadow

DiskShadow는 모든 하드웨어 및 소프트웨어 스냅숏을 관리 하는 시스템에 수 있는 하는 데 사용할 수 있는 VSS 요청자입니다. DiskShadow에는 다음과 같은 명령이 포함 됩니다.

  - **list**: VSS 기록기를 VSS 공급자 및 섀도 복사본을 나열합니다.  
      
  - **create**: 새 섀도 복사본을 만듭니다.  
      
  - **import**: 전송 가능한 섀도 복사본을 가져옵니다.  
      
  - **expose**: 예를 들어 드라이브 문자) (으로 영구 섀도 복사본을 노출  
      
  - **revert**: 지정된 된 섀도 복사본으로 볼륨을 되돌립니다.  
      

이 도구는 IT 전문가가 사용 하 여 위한 것 이지만 개발자도 유용할 것은 VSS 기록기 또는 VSS 공급자를 테스트 하는 경우.

DiskShadow는 Windows Server 운영 체제 에서만 사용할 수 있습니다. Windows 클라이언트 운영 체제에서 사용할 수 있는 것입니다.

### <a name="vssadmin"></a>VssAdmin

VssAdmin 만들기, 삭제 및 섀도 복사본에 대 한 정보를 나열 됩니다. 섀도 복사본 저장소 영역 ("차등 영역")의 크기를 조정 하려면 데도 수 있습니다.

VssAdmin에 다음과 같은 명령이 포함 됩니다.

  - **그림자 만드는**: 새 섀도 복사본을 만듭니다.  
      
  - **그림자를 삭제 합니다**: 섀도 복사본을 삭제  
      
  - **공급자 목록**: 등록 된 모든 VSS 공급자를 나열합니다.  
      
  - **작성기 목록**: 모든 VSS 기록기 등록  
      
  - **shadowstorage 조정**: 섀도 복사본 저장 영역의의 최대 크기를 변경합니다.  
      

VssAdmin 관리 시스템 소프트웨어 공급자에서 만들어진 섀도 복사본에만 사용할 수 있습니다.

VssAdmin은 Windows 클라이언트 및 Windows Server 운영 체제 버전에서 제공 됩니다.

## <a name="volume-shadow-copy-service-registry-keys"></a>볼륨 섀도 복사본 서비스 레지스트리 키

다음 레지스트리 키가 VSS 사용 하 여 사용할 수 있습니다.

  - **VssAccessControl**  
      
  - **MaxShadowCopies**  
      
  - **MinDiffAreaFileSize**  
      

### <a name="vssaccesscontrol"></a>VssAccessControl

섀도 복사본에 액세스할 수 있는 사용자 지정 하려면이 키를 사용 합니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조 하세요.

  - [작성기에 대 한 보안 고려 사항](http://go.microsoft.com/fwlink/?linkid=157739) (http://go.microsoft.com/fwlink/?LinkId=157739)  
      
  - [요청자에 대 한 보안 고려 사항](http://go.microsoft.com/fwlink/?linkid=180908) (http://go.microsoft.com/fwlink/?LinkId=180908)  
      

### <a name="maxshadowcopies"></a>MaxShadowCopies

이 키는 컴퓨터의 각 볼륨에 저장할 수 있는 클라이언트에서 액세스할 수 있는 섀도 복사본의 최대 수를 지정 합니다. 클라이언트에서 액세스할 수 있는 섀도 복사본 공유 폴더의 섀도 복사본에서 사용 됩니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조 합니다.

**MaxShadowCopies** 아래에서 [레지스트리 키 백업 및 복원에 대 한](http://go.microsoft.com/fwlink/?linkid=180909) (http://go.microsoft.com/fwlink/?LinkId=180909)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

이 키의 섀도 복사본 저장소 영역 (mb)에서의 최소 초기 크기를 지정합니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조 합니다.

**MinDiffAreaFileSize** 아래에서 [레지스트리 키 백업 및 복원에 대 한](http://go.microsoft.com/fwlink/?linkid=180910) (http://go.microsoft.com/fwlink/?LinkId=180910)

`##`#' 지원 되는 운영 체제 버전

다음 표에서 VSS 기능에 대 한 최소 지원 되는 운영 체제 버전을 나열합니다.


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
<td><p>LUN 교체를 사용 하 여 빠른 복구</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2003 SP1</p></td>
</tr>
<tr class="odd">
<td><p>여러는 하드웨어 섀도 복사본 가져오기</p>
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
<td>이 섀도 복사본을 두 번 이상 가져올 수 있습니다. 한 번에 하나의 가져오기 작업을 수행할 수 있습니다.
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
<td><p>공유 폴더의 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>전송 가능한 자동 복구 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>동시 백업 세션 (최대 64)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>동시 백업을 사용 하 여 단일 복원 세션</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003 sp2</p></td>
</tr>
<tr class="even">
<td><p>동시 백업을 사용 하 여 최대 8 개의 복원 세션</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>참조

[Windows 개발자 센터에서 볼륨 섀도 복사본 서비스](https://docs.microsoft.com/windows/desktop/vss/volume-shadow-copy-service-overview)