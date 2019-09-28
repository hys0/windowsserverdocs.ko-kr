---
title: 볼륨 섀도 복사본 서비스
ms.date: 01/30/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 19e07504dad49c5e23cc49630015529e2a746aa7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394452"
---
# <a name="volume-shadow-copy-service"></a>볼륨 섀도 복사본 서비스

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008, Windows 10, Windows 8.1, Windows 8, Windows 7

중요 한 비즈니스 데이터를 백업 하 고 복원 하는 작업은 다음과 같은 문제로 인해 매우 복잡할 수 있습니다.

  - 데이터를 생성 하는 응용 프로그램이 여전히 실행 되는 동안에는 일반적으로 데이터를 백업 해야 합니다. 즉, 일부 데이터 파일이 열려 있거나 일관성이 없는 상태일 수 있습니다.  
      
  - 데이터 집합이 클 경우에는 한 번에 모두 백업 하기가 어려울 수 있습니다.  
      

백업 및 복원 작업을 올바르게 수행 하려면 백업 응용 프로그램, 백업 중인 lob (기간 업무) 응용 프로그램, 저장소 관리 하드웨어 및 소프트웨어를 모두 조정 해야 합니다. Windows Server® 2003에 도입 된 볼륨 섀도 복사본 서비스 (VSS)를 사용 하면 이러한 구성 요소 간의 대화를 통해 더욱 원활 하 게 작업할 수 있습니다. 모든 구성 요소가 VSS를 지 원하는 경우 응용 프로그램을 오프 라인으로 전환 하지 않고도 응용 프로그램 데이터를 백업 하는 데 사용할 수 있습니다.

VSS는 백업할 데이터의 일관성 있는 섀도 복사본 (스냅숏 또는 지정 시간 복사본이 라고도 함)을 만드는 데 필요한 작업을 조정 합니다. 섀도 복사본은 있는 그대로 사용 하거나 다음과 같은 시나리오에서 사용할 수 있습니다.

  - 다른 하드 디스크 드라이브, 테이프 또는 기타 이동식 미디어에 데이터를 보관 하는 등 응용 프로그램 데이터 및 시스템 상태 정보를 백업 하려고 합니다.  
      
  - 데이터 마이닝입니다.  
      
  - 디스크-디스크 백업을 수행 하 고 있습니다.  
      
  - 데이터를 원래 LUN으로 복원 하거나 실패 한 원래 LUN을 대체 하는 완전히 새로운 LUN으로 복원 하 여 데이터 손실 로부터 빠른 복구가 필요 합니다.  
      

VSS를 사용 하는 Windows 기능 및 응용 프로그램은 다음과 같습니다.

  - [Windows Server 백업](http://go.microsoft.com/fwlink/?linkid=180891) (http://go.microsoft.com/fwlink/?LinkId=180891)  
      
  - [공유 폴더의 섀도 복사본](http://go.microsoft.com/fwlink/?linkid=142874) (http://go.microsoft.com/fwlink/?LinkId=142874)  
      
  - [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=180892) (http://go.microsoft.com/fwlink/?LinkId=180892)  
      
  - [시스템 복원](http://go.microsoft.com/fwlink/?linkid=180893) (http://go.microsoft.com/fwlink/?LinkId=180893)  
      

## <a name="how-volume-shadow-copy-service-works"></a>볼륨 섀도 복사본 서비스 작동 방법

전체 VSS 솔루션에는 다음과 같은 기본 파트가 모두 필요 합니다.

   다른 구성 요소가 서로 통신 하 고 함께 작업할 수 있도록 하는 Windows 운영 체제의 VSS 서비스 부분입니다.

**VSS 요청자**   는 섀도 복사본 (또는 가져오기 또는 삭제와 같은 기타 상위 수준 작업)의 실제 생성을 요청 하는 소프트웨어입니다. 일반적으로이 응용 프로그램은 백업 응용 프로그램입니다. Windows Server 백업 유틸리티와 System Center Data Protection Manager 응용 프로그램은 VSS 요청자입니다. 비 Microsoft® VSS 요청자는 Windows에서 실행 되는 거의 모든 백업 소프트웨어를 포함 합니다.

**VSS 기록기**   구성 요소를 통해 일관 된 데이터 집합이 백업 되도록 보장 합니다. 이는 일반적으로 SQL Server® 또는 Exchange Server와 같은 lob (기간 업무) 응용 프로그램의 일부로 제공 됩니다. 레지스트리와 같은 다양 한 Windows 구성 요소에 대 한 VSS 기록기는 Windows 운영 체제에 포함 되어 있습니다. 타사 VSS 기록기는 백업 중 데이터 일관성을 보장 해야 하는 다양 한 Windows 응용 프로그램에 포함 되어 있습니다.

**VSS 공급자**   섀도 복사본을 만들고 유지 관리 하는 구성 요소입니다. 이는 소프트웨어 또는 하드웨어에서 발생할 수 있습니다. Windows 운영 체제에는 쓰기 복사를 사용 하는 VSS 공급자가 포함 되어 있습니다. SAN (저장 영역 네트워크)을 사용 하는 경우 SAN 용 VSS 하드웨어 공급자를 설치 하는 것이 중요 합니다 (제공 된 경우). 하드웨어 공급자는 호스트 운영 체제에서 섀도 복사본을 만들고 유지 관리 하는 작업을 오프 로드 합니다.

다음 다이어그램에서는 VSS 서비스가 요청자, 기록기 및 공급자와의 좌표계를 사용 하 여 볼륨의 섀도 복사본을 만드는 방법을 보여 줍니다.

![](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**그림 1**   볼륨 섀도 복사본 서비스 아키텍처 다이어그램

### <a name="how-a-shadow-copy-is-created"></a>섀도 복사본을 만드는 방법

이 섹션에서는 섀도 복사본을 만들기 위해 수행 해야 하는 단계를 나열 하 여 요청자, 기록기 및 공급자의 다양 한 역할을 컨텍스트에 넣습니다. 다음 다이어그램에서는 볼륨 섀도 복사본 서비스 요청자, 기록기 및 공급자의 전반적인 조정을 제어 하는 방법을 보여 줍니다.

![](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**그림 2** 섀도 복사본 생성 프로세스

섀도 복사본을 만들려면 요청자, writer 및 provider에서 다음 작업을 수행 합니다.

1.  요청자는 볼륨 섀도 복사본 서비스에 게 작성기를 열거 하 고, 기록기 메타 데이터를 수집 하 고, 섀도 복사본 만들기를 준비 하도록 요청 합니다.  
      
2.  각 작성자는 백업 해야 하는 구성 요소 및 데이터 저장소에 대 한 XML 설명을 만들고 볼륨 섀도 복사본 서비스 제공 합니다. 또한 작성기는 모든 구성 요소에 사용 되는 restore 메서드를 정의 합니다. 볼륨 섀도 복사본 서비스 요청자에 게 작성자의 설명을 제공 하 여 백업할 구성 요소를 선택 합니다.  
      
3.  볼륨 섀도 복사본 서비스은 모든 작성자에 게 섀도 복사본 만들기에 대 한 데이터를 준비 하도록 알립니다.  
      
4.  각 작성기는 모든 열린 트랜잭션 완료, 트랜잭션 로그 롤링 및 캐시 플러시와 같이 적절 한 데이터를 준비 합니다. 데이터를 섀도 복사할 준비가 되 면 작성자가 볼륨 섀도 복사본 서비스에 게 알립니다.  
      
5.  볼륨 섀도 복사본 서비스는 볼륨이 나 볼륨의 섀도 복사본을 만드는 데 필요한 몇 초 동안 응용 프로그램 쓰기 i/o 요청 (읽기 i/o 요청)을 일시적으로 중지 하도록 작성자에 게 지시 합니다. 응용 프로그램 고정은 60 초 보다 더 오래 걸릴 수 없습니다. 볼륨 섀도 복사본 서비스 파일 시스템 버퍼를 플러시한 다음 파일 시스템을 고정 합니다. 그러면 파일 시스템 메타 데이터가 올바르게 기록 되 고 섀도 복사 될 데이터는 일관 된 순서로 기록 됩니다.  
      
6.  볼륨 섀도 복사본 서비스는 공급자에 섀도 복사본을 만들도록 지시 합니다. 섀도 복사본 만들기 기간은 10 초 이하로 지속 되며,이 기간 동안 파일 시스템에 대 한 모든 쓰기 i/o 요청은 고정 된 상태를 유지 합니다.  
      
7.  볼륨 섀도 복사본 서비스 파일 시스템 쓰기 i/o 요청을 해제 합니다.  
      
8.  VSS는 기록기에 응용 프로그램 쓰기 i/o 요청을 재개 하도록 지시 합니다. 이 시점에서 응용 프로그램은 섀도 복사 되는 디스크에 데이터 쓰기를 다시 시작할 수 있습니다.  
      

> [!NOTE]
> 작성자가 60 초 보다 오랫동안 고정 상태를 유지 하거나 공급자가 섀도 복사본을 커밋하는 데 10 초 보다 오래 걸리는 경우 섀도 복사본 만들기를 중단할 수 있습니다. 
<br>

9. 요청자는 프로세스를 다시 시도 하거나 (1 단계로 돌아가기) 나중에 다시 시도 하도록 관리자에 게 알릴 수 있습니다.  
      
10. 섀도 복사본이 성공적으로 만들어지면 볼륨 섀도 복사본 서비스은 요청자에 게 섀도 복사본에 대 한 위치 정보를 반환 합니다. 일부 경우에는 VSS 및 하나 이상의 응용 프로그램이 섀도 복사본을 완료 하기 전에 섀도 복사본의 콘텐츠를 변경할 수 있도록 섀도 복사본을 읽기-쓰기 볼륨으로 일시적으로 사용할 수 있습니다. VSS와 응용 프로그램에서 변경 내용을 적용 한 후 섀도 복사본은 읽기 전용으로 설정 됩니다. 이 단계를 자동 복구 라고 하며, 섀도 복사본을 만들기 전에 완료 되지 않은 섀도 복사본 볼륨의 파일 시스템 또는 응용 프로그램 트랜잭션을 실행 취소 하는 데 사용 됩니다.  
      

### <a name="how-the-provider-creates-a-shadow-copy"></a>공급자가 섀도 복사본을 만드는 방법

하드웨어 또는 소프트웨어 섀도 복사본 공급자는 다음 방법 중 하나를 사용 하 여 섀도 복사본을 만듭니다.

**전체 복사**   이 메서드는 지정 된 시점에 원래 볼륨의 전체 복사본 ("전체 복사본" 또는 "복제")을 만듭니다. 이 복사본은 읽기 전용입니다.

**쓰기 복사-** 이메서드는원래볼륨을복사하지않습니다   . 대신 지정 된 시점 이후에 볼륨에 적용 된 모든 변경 내용 (쓰기 i/o 요청)을 복사 하 여 차등 복사를 수행 합니다.

**리디렉션-쓰기**   이 메서드는 원래 볼륨을 복사 하지 않으며 지정 된 시점 이후 원래 볼륨을 변경 하지 않습니다. 대신, 다른 볼륨으로 모든 변경 내용을 리디렉션하여 차등 복사를 수행 합니다.

## <a name="complete-copy"></a>전체 복사

일반적으로 전체 복사본은 다음과 같이 "분할 미러"를 만들어 만듭니다.

1.  원래 볼륨 및 섀도 복사본 볼륨은 미러 볼륨 세트입니다.  
      
2.  섀도 복사본 볼륨이 원래 볼륨과 분리 되어 있습니다. 이렇게 하면 미러 연결이 끊어집니다.  
      

미러 연결을 끊은 후에는 원래 볼륨 및 섀도 복사본 볼륨은 독립적입니다. 원본 볼륨은 모든 변경 내용 (쓰기 i/o 요청)을 계속 수락 하는 반면 섀도 복사본 볼륨은 중단 시 원래 데이터의 정확한 읽기 전용 복사본으로 유지 됩니다.

### <a name="copy-on-write-method"></a>쓰기 시 복사 방법

쓰기-쓰기 메서드에서 원래 볼륨에 대 한 변경 내용이 발생 하는 경우 (쓰기 i/o 요청이 완료 되기 전에) 수정할 각 블록을 읽고 볼륨의 섀도 복사본 저장 영역 ("diff 영역"이 라고도 함)에 기록 합니다. 섀도 복사본 저장소 영역은 동일한 볼륨 또는 다른 볼륨에 있을 수 있습니다. 이렇게 하면 변경 내용이 덮어쓰기 전에 원래 볼륨의 데이터 블록 복사본이 유지 됩니다.


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
<td><p>원본 데이터: 1 2 3 4 5</p></td>
<td><p>복사 안 함:-</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>캐시에서 변경 된 데이터: 3 ~ 3 '</p></td>
<td><p>섀도 복사본 생성 (차이점만): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>원래 데이터를 덮어썼습니다. 1 2 3 ' 4 5</p></td>
<td><p>섀도 복사본에 저장 된 차이점 및 인덱스: 3</p></td>
</tr>
</tbody>
</table>

**표 1**   섀도 복사본을 만드는 쓰기 복사 방법

쓰기 시 복사 방법은 변경 된 데이터만 복사 하기 때문에 섀도 복사본을 만드는 빠른 방법입니다. Diff 영역의 복사 된 블록을 원래 볼륨의 변경 된 데이터와 결합 하 여 변경 내용이 적용 되기 전에 볼륨을 해당 상태로 복원할 수 있습니다. 많은 변경 내용이 있는 경우 쓰기-쓰기 방법이 비용이 많이 들 수 있습니다.

### <a name="redirect-on-write-method"></a>쓰기 리디렉션 방법

리디렉션-쓰기 메서드에서 원래 볼륨이 변경 (쓰기 i/o 요청)을 받을 때마다 원래 볼륨에 변경 내용이 적용 되지 않습니다. 대신 다른 볼륨의 섀도 복사본 저장 영역에 변경 내용이 기록 됩니다.


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
<td><p>원본 데이터: 1 2 3 4 5</p></td>
<td><p>복사 안 함:-</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>캐시에서 변경 된 데이터: 3 ~ 3 '</p></td>
<td><p>섀도 복사본 생성 (차이점만): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>변경 되지 않은 원본 데이터: 1 2 3 4 5</p></td>
<td><p>섀도 복사본에 저장 된 차이점 및 인덱스: 3</p></td>
</tr>
</tbody>
</table>

**표 2**   섀도 복사본을 만들기 위한 쓰기 리디렉션 방법

쓰기-쓰기 방법과 마찬가지로 리디렉션 쓰기 방법은 데이터에 대 한 변경 내용만 복사 하기 때문에 섀도 복사본을 만드는 빠른 방법입니다. Diff 영역의 복사 된 블록을 원래 볼륨의 변경 되지 않은 데이터와 결합 하 여 데이터의 완전 한 최신 복사본을 만들 수 있습니다. 많은 읽기 i/o 요청이 있는 경우 쓰기 리디렉션 메서드는 비용이 많이 들 수 있습니다.

## <a name="shadow-copy-providers"></a>섀도 복사본 공급자

섀도 복사본 공급자에는 하드웨어 기반 공급자와 소프트웨어 기반 공급자의 두 가지 유형이 있습니다. Windows 운영 체제에 기본 제공 되는 소프트웨어 공급자 인 시스템 공급자도 있습니다.

### <a name="hardware-based-providers"></a>하드웨어 기반 공급자

하드웨어 기반 섀도 복사본 공급자는 하드웨어 저장소 어댑터나 컨트롤러와 함께 작업 하 여 볼륨 섀도 복사본 서비스와 하드웨어 수준 간의 인터페이스 역할을 합니다. 섀도 복사본을 만들고 유지 관리 하는 작업은 저장소 배열에 의해 수행 됩니다.

하드웨어 공급자는 항상 전체 LUN의 섀도 복사본을 가져오지만 볼륨 섀도 복사본 서비스은 요청 된 볼륨의 섀도 복사본만 표시 합니다.

하드웨어 기반 섀도 복사본 공급자는 지정 시간을 정의 하 고, 데이터 동기화를 허용 하 고, 섀도 복사본을 관리 하 고, 백업 응용 프로그램에 공통 인터페이스를 제공 하는 볼륨 섀도 복사본 서비스 기능을 사용 합니다. 그러나 볼륨 섀도 복사본 서비스는 하드웨어 기반 공급자가 섀도 복사본을 생성 하 고 유지 관리 하는 기본 메커니즘을 지정 하지 않습니다.

### <a name="software-based-providers"></a>소프트웨어 기반 공급자

소프트웨어 기반 섀도 복사본 공급자는 일반적으로 파일 시스템과 볼륨 관리자 소프트웨어 간의 소프트웨어 계층에서 읽기 및 쓰기 i/o 요청을 가로채서 처리 합니다.

이러한 공급자는 사용자 모드 DLL 구성 요소 및 하나 이상의 커널 모드 장치 드라이버 (일반적으로 저장소 필터 드라이버)로 구현 됩니다. 하드웨어 기반 공급자와 달리 소프트웨어 기반 공급자는 하드웨어 수준이 아닌 소프트웨어 수준에서 섀도 복사본을 만듭니다.

소프트웨어 기반 섀도 복사본 공급자는 섀도 복사본을 만들 때까지 볼륨 상태를 다시 만드는 데 사용할 수 있는 데이터 집합에 액세스 하 여 볼륨의 "지정 시간" 보기를 유지 해야 합니다. 예를 들어 시스템 공급자의 쓰기 복사 기술이 있습니다. 그러나 볼륨 섀도 복사본 서비스는 소프트웨어 기반 공급자가 섀도 복사본을 만들고 유지 관리 하는 데 사용 하는 기술을 제한 하지 않습니다.

소프트웨어 공급자는 하드웨어 기반 공급자 보다 더 광범위 한 저장소 플랫폼에 적용 될 수 있으며 기본 디스크 또는 논리 볼륨에서 동일 하 게 작동 해야 합니다. 논리적 볼륨은 두 개 이상의 디스크에서 사용 가능한 공간을 결합 하 여 만든 볼륨입니다. 하드웨어 섀도 복사본과 달리 소프트웨어 공급자는 운영 체제 리소스를 사용 하 여 섀도 복사본을 유지 관리 합니다.

기본 디스크에 대 한 자세한 내용은 [기본 디스크 및 볼륨 이란?](http://go.microsoft.com/fwlink/?linkid=180894) 을 참조 하세요. (http://go.microsoft.com/fwlink/?LinkId=180894) TechNet

### <a name="system-provider"></a>시스템 공급자

시스템 공급자 인 섀도 복사본 공급자 하나가 Windows 운영 체제에 제공 됩니다. Windows에서 기본 공급자를 제공 하지만 다른 공급 업체는 저장소 하드웨어 및 소프트웨어 응용 프로그램에 최적화 된 구현을 제공할 수 있습니다.

섀도 복사본에 포함 된 볼륨의 "지정 시간" 보기를 유지 관리 하기 위해 시스템 공급자는 쓰기-쓰기 기술을 사용 합니다. 섀도 복사본을 만든 후 수정 된 볼륨의 블록 복사본은 섀도 복사본 저장 영역에 저장 됩니다.

시스템 공급자는 프로덕션 볼륨을 노출할 수 있으며,이를 정상적으로 작성 하 고 읽을 수 있습니다. 섀도 복사본이 필요할 때 프로덕션 볼륨의 데이터에 대 한 차이점을 논리적으로 적용 하 여 전체 섀도 복사본을 노출 합니다.

시스템 공급자의 경우 섀도 복사본 저장 영역이 NTFS 볼륨에 있어야 합니다. 섀도 복사 되는 볼륨은 NTFS 볼륨이 될 필요는 없지만 시스템에 탑재 된 하나 이상의 볼륨이 NTFS 볼륨 이어야 합니다.

시스템 공급자를 구성 하는 구성 요소 파일은 swprv 및 volsnap입니다.

### <a name="in-box-vss-writers"></a>기본으로 VSS 기록기

Windows 운영 체제에는 다양 한 Windows 기능에 필요한 데이터의 열거를 담당 하는 VSS 기록기 집합이 포함 되어 있습니다.

이러한 작성자에 대 한 자세한 내용은 다음 Microsoft 웹 사이트를 참조 하십시오.

  - [기본으로 VSS 기록기](http://go.microsoft.com/fwlink/?linkid=180895) (http://go.microsoft.com/fwlink/?LinkId=180895)  
      
  - [Windows Server 2008 및 Windows Vista s p 1에 대 한 새로운 기본 Windows VSS 기록기](http://go.microsoft.com/fwlink/?linkid=180896) (http://go.microsoft.com/fwlink/?LinkId=180896)  
      
  - [Windows Server 2008 R2 및 windows 7 용 새 기본 WINDOWS VSS 기록기](http://go.microsoft.com/fwlink/?linkid=180897) (http://go.microsoft.com/fwlink/?LinkId=180897)  
      

## <a name="how-shadow-copies-are-used"></a>섀도 복사본을 사용 하는 방법

응용 프로그램 데이터 및 시스템 상태 정보를 백업 하는 것 외에도 다음을 포함 하 여 여러 가지 용도로 섀도 복사본을 사용할 수 있습니다.

  - Lun 복원 (LUN 다시 동기화 및 LUN 스와핑)  
      
  - 개별 파일 복원 (공유 폴더용 섀도 복사본)  
      
  - 전송 가능한 섀도 복사본을 사용 하 여 데이터 마이닝  
      

### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>Lun 복원 (LUN 다시 동기화 및 LUN 스와핑)

Windows Server 2008 R2 및 Windows 7에서 VSS 요청자는 LUN 다시 동기화 (또는 "LUN 다시 동기화") 라는 하드웨어 섀도 복사본 공급자 기능을 사용할 수 있습니다. 이는 응용 프로그램 관리자가 섀도 복사본에서 원래 LUN 또는 새 LUN으로 데이터를 복원할 수 있도록 하는 빠른 복구 체계입니다.

섀도 복사본은 전체 클론 또는 차등 섀도 복사본 일 수 있습니다. 두 경우 모두 다시 동기화 작업이 끝나면 대상 LUN은 섀도 복사본 LUN과 동일한 콘텐츠를 갖게 됩니다. 다시 동기화 작업 중에 배열은 섀도 복사본에서 대상 LUN으로 블록 수준 복사를 수행 합니다.


> [!NOTE]
> 섀도 복사본은 전송 가능한 하드웨어 섀도 복사본 이어야 합니다. 
<br>


대부분의 배열을 사용 하면 다시 동기화 작업이 시작 된 후 프로덕션 i/o 작업을 즉시 다시 시작할 수 있습니다. 다시 동기화 작업이 진행 중인 동안에는 읽기 요청이 섀도 복사본 LUN으로 리디렉션되고 대상 LUN에 요청을 씁니다. 이렇게 하면 배열이 매우 큰 데이터 집합을 복구 하 고 몇 초 내에 정상적인 작업을 다시 시작할 수 있습니다.

Lun 다시 동기화는 LUN 스와핑과 다릅니다. LUN 교환은 Windows Server 2003 s p 1부터 VSS에서 지 원하는 빠른 복구 시나리오입니다. LUN 교환에서 섀도 복사본을 가져온 다음 읽기-쓰기 볼륨으로 변환 합니다. 변환은 취소할 수 없는 작업이 며 그 후에 VSS Api를 사용 하 여 볼륨 및 기본 LUN을 제어할 수 없습니다. 다음 목록에서는 lun 다시 동기화를 LUN 스와핑과 비교 하는 방법을 설명 합니다.

  - LUN 다시 동기화에서 섀도 복사본은 변경 되지 않으므로 여러 번 사용할 수 있습니다. LUN 스와핑에서 섀도 복사본은 복구에 한 번만 사용할 수 있습니다. 가장 안전에 민감한 관리자의 경우이는 중요 합니다. LUN 다시 동기화를 사용 하는 경우 처음에 문제가 발생 하는 경우 요청자는 전체 복원 작업을 다시 시도할 수 있습니다.  
      
  - LUN 교체의 끝에서 섀도 복사본 LUN은 프로덕션 i/o 요청에 사용 됩니다. 이러한 이유로 복구 작업 후에는 성능이 영향을 받지 않도록 섀도 복사본 LUN은 원래 프로덕션 LUN과 동일한 저장소 품질을 사용 해야 합니다. LUN 다시 동기화를 대신 사용 하는 경우 하드웨어 공급자는 프로덕션 품질 저장소 보다 비용이 적게 드는 저장소에서 섀도 복사본을 유지할 수 있습니다.  
      
  - 대상 lun을 사용할 수 없고 다시 만들어야 하는 경우 LUN 스와핑은 대상 LUN이 필요 하지 않기 때문에 더 경제적 일 수 있습니다.  
      


> [!WARNING]
> 나열 된 모든 작업은 LUN 수준 작업입니다. LUN 다시 동기화를 사용 하 여 특정 볼륨을 복구 하려고 하면 해당 LUN을 공유 하는 다른 모든 볼륨을 되돌리지 않습니다. 
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>개별 파일 복원 (공유 폴더용 섀도 복사본)

공유 폴더용 섀도 복사본은 볼륨 섀도 복사본 서비스를 사용 하 여 파일 서버와 같은 공유 네트워크 리소스에 있는 파일의 지정 시간 복사본을 제공 합니다. 공유 폴더용 섀도 복사본를 통해 사용자는 네트워크에 저장 된 삭제 된 파일 또는 변경 된 파일을 신속 하 게 복구할 수 있습니다. 이러한 작업은 관리자의 도움 없이도 수행할 수 있으므로 생산성을 높이고 관리 비용을 줄일 수 공유 폴더용 섀도 복사본.

[공유 폴더용 섀도 복사본](http://go.microsoft.com/fwlink/?linkid=180898)에 대한 자세한 내용은 http://go.microsoft.com/fwlink/?LinkId=180898) TechNet의 공유 폴더용 섀도 복사본(영문)를 참조하세요.

### <a name="data-mining-by-using-transportable-shadow-copies"></a>전송 가능한 섀도 복사본을 사용 하 여 데이터 마이닝

볼륨 섀도 복사본 서비스와 함께 사용 하도록 디자인 된 하드웨어 공급자를 사용 하 여 동일한 하위 시스템 (예: SAN) 내의 서버로 가져올 수 있는 전송 가능한 섀도 복사본을 만들 수 있습니다. 이러한 섀도 복사본을 사용 하 여 데이터 마이닝을 위한 읽기 전용 데이터로 프로덕션 또는 테스트 설치를 초기값으로 지정할 수 있습니다.

볼륨 섀도 복사본 서비스와 함께 사용 하도록 디자인 된 하드웨어 공급자를 사용 하 여 볼륨 섀도 복사본 서비스 및 저장소 배열을 사용 하는 경우 한 서버에 원본 데이터 볼륨의 섀도 복사본을 만든 다음 섀도 복사본을 다른 서버로 가져올 수 있습니다.  또는 같은 서버로 다시 이동 합니다. 이 프로세스는 데이터 크기에 관계 없이 몇 분 이내에 수행 됩니다. 전송 프로세스는 전송 가능한 섀도 복사본을 지 원하는 섀도 복사본 요청자 (저장소 관리 응용 프로그램)를 사용 하는 일련의 단계를 통해 수행 됩니다.

## <a name="to-transport-a-shadow-copy"></a>섀도 복사본을 전송 하려면

1.  서버에 있는 원본 데이터의 전송 가능한 섀도 복사본을 만듭니다.

2.  SAN에 연결 된 서버에 섀도 복사본을 가져옵니다 (다른 서버 또는 동일한 서버로 가져올 수 있음).

3.  이제 데이터를 사용할 준비가 되었습니다.

![](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**그림 3**   두 서버 간 섀도 복사본 만들기 및 전송


> [!NOTE]
> Windows server 2003에 생성 된 전송 가능한 섀도 복사본을 Windows server 2008 또는 Windows Server 2008 r 2를 실행 하는 서버로 가져올 수 없습니다. Windows server 2008 또는 windows server 2008 r 2에서 만든 전송 가능한 섀도 복사본을 Windows Server 2003를 실행 하는 서버로 가져올 수 없습니다. 그러나 windows server 2008에 생성 된 섀도 복사본은 Windows Server 2008 r 2를 실행 하는 서버로 가져올 수 있으며 그 반대의 경우도 마찬가지입니다. 
<br>


섀도 복사본은 읽기 전용이기 때문에 섀도 복사본을 읽기/쓰기 LUN으로 변환 하려는 경우에는 볼륨 섀도 복사본 서비스 외에도 가상 디스크 서비스 기반 저장소 관리 응용 프로그램 (일부 요청자 포함)을 사용할 수 있습니다. 이 응용 프로그램을 사용 하 여 볼륨 섀도 복사본 서비스 관리에서 섀도 복사본을 제거 하 고 읽기/쓰기 LUN으로 변환할 수 있습니다.

볼륨 섀도 복사본 서비스 전송은 Windows Server 2003 Enterprise Edition, Windows Server 2003 Datacenter Edition, Windows Server 2008 또는 Windows Server 2008 r 2를 실행 하는 컴퓨터에서 고급 솔루션입니다. 저장소 배열에 하드웨어 공급자가 있는 경우에만 작동 합니다. 섀도 복사본 전송은 테이프 백업, 데이터 마이닝 및 테스트를 비롯 한 다양 한 용도로 사용할 수 있습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

이 FAQ는 시스템 관리자 용 VSS (볼륨 섀도 복사본 서비스)에 대 한 질문에 답변 합니다. VSS 응용 프로그램 프로그래밍 인터페이스에 대한 자세한 내용은 Windows 개발자 센터 라이브러리에서 [볼륨 섀도 복사본 서비스](http://go.microsoft.com/fwlink/?linkid=180899) (http://go.microsoft.com/fwlink/?LinkId=180899) 영문)을 참조하세요.

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>볼륨 섀도 복사본 서비스 도입 된 경우 사용할 수 있는 Windows 운영 체제 버전은 무엇 인가요?

VSS는 Windows XP에서 도입 되었습니다. Windows XP, Windows Server 2003, Windows Vista®, Windows Server 2008, Windows 7 및 Windows Server 2008 r 2에서 사용할 수 있습니다.

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>섀도 복사본과 백업 간의 차이점은 무엇 인가요?

하드 디스크 드라이브 백업의 경우 섀도 복사본은 백업 이기도 합니다. 복원에 대 한 섀도 복사본에서 데이터를 복사 하거나 섀도 복사본을 사용 하 여 빠른 복구 시나리오를 수행할 수 있습니다 (예: LUN 다시 동기화 또는 LUN 교환).

데이터를 섀도 복사본에서 테이프나 기타 이동식 미디어로 복사할 때 미디어에 저장 된 콘텐츠는 백업을 구성 합니다. 데이터를 복사한 후에는 섀도 복사본 자체를 삭제할 수 있습니다.

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>볼륨 섀도 복사본 서비스에서 지 원하는 가장 큰 크기의 볼륨은 무엇 인가요?

볼륨 섀도 복사본 서비스은 최대 64 TB의 볼륨 크기를 지원 합니다.

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Windows Server 2008에 대 한 백업을 수행 했습니다. Windows Server 2008 r 2에서 복원할 수 있나요?

사용한 백업 소프트웨어에 따라 달라 집니다. 대부분의 백업 프로그램은 데이터에 대해이 시나리오를 지원 하지만 시스템 상태 백업에 대해서는 지원 하지 않습니다.

이러한 Windows 버전 중 하나에 생성 된 섀도 복사본은 다른 버전에서 사용할 수 있습니다.

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Windows Server 2003에 대 한 백업을 수행 했습니다. Windows Server 2008에서 복원할 수 있나요?

사용한 백업 소프트웨어에 따라 달라 집니다. Windows Server 2003에서 섀도 복사본을 만드는 경우 Windows Server 2008에서 사용할 수 없습니다. 또한 Windows Server 2008에서 섀도 복사본을 만드는 경우 Windows Server 2003에서 복원할 수 없습니다.

### <a name="how-can-i-disable-vss"></a>VSS를 사용 하지 않도록 설정 하려면 어떻게 해야 하나요?

Microsoft Management Console을 사용 하 여 볼륨 섀도 복사본 서비스를 사용 하지 않도록 설정할 수 있습니다. 그러나이 작업을 수행 하면 안 됩니다. VSS를 사용 하지 않도록 설정 하면 시스템 복원과 Windows Server 백업 같이이에 따라 사용 하는 모든 소프트웨어에 영향을 줍니다.

자세한 내용은 다음 Microsoft TechNet 웹 사이트를 참조 하십시오.

  - [시스템 복원](http://go.microsoft.com/fwlink/?linkid=157113) (http://go.microsoft.com/fwlink/?LinkID=157113)  
      
  - [Windows Server 백업](http://go.microsoft.com/fwlink/?linkid=180891) (http://go.microsoft.com/fwlink/?LinkID=180891)  
      

### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>공간을 절약 하기 위해 섀도 복사본에서 파일을 제외할 수 있나요?

VSS는 전체 볼륨의 섀도 복사본을 만들도록 설계 되었습니다. 페이징 파일과 같은 임시 파일은 공간을 절약 하기 위해 섀도 복사본에서 자동으로 생략 됩니다.

섀도 복사본에서 특정 파일을 제외 하려면 다음 레지스트리 키를 사용 합니다. **Filesnottosnapshot**.


> [!NOTE]
> <STRONG>Filesnottosnapshot</STRONG> 레지스트리 키는 응용 프로그램 에서만 사용 됩니다. 이를 사용 하려고 시도 하는 사용자에 게는 다음과 같은 제한 사항이 있습니다.
> <br>
> <UL>
> <LI>이전 버전 기능을 사용 하 여 Windows 서버에서 만든 섀도 복사본에서 파일을 삭제할 수 없습니다.<BR><BR>
> <LI>공유 폴더의 섀도 복사본에서 파일을 삭제할 수 없습니다.<BR><BR>
> <LI><a href="https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow)">Diskshadow</a> 유틸리티를 사용 하 여 만든 섀도 복사본에서 파일을 삭제할 수 있지만 <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin)">Vssadmin</a> 유틸리티를 사용 하 여 만든 섀도 복사본에서 파일을 삭제할 수는 없습니다.<BR><BR>
> <LI>파일은 섀도 복사본에서 가장 효율적으로 삭제 됩니다. 즉, 삭제 되지 않을 수 있습니다.<BR><BR></LI></UL>


자세한 내용은 MSDN의 [섀도 복사본에서 파일 제외](http://go.microsoft.com/fwlink/?linkid=180904) (영문 http://go.microsoft.com/fwlink/?LinkId=180904) )를 참조 하세요.

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>Microsoft 이외의 백업 프로그램에서 VSS 오류가 발생 하 여 실패 했습니다. 무엇을 도와드릴까요?

백업 프로그램을 만든 회사 웹 사이트의 제품 지원 섹션을 확인 하십시오. 문제를 해결 하기 위해 다운로드 하 여 설치할 수 있는 제품 업데이트가 있을 수 있습니다. 그렇지 않은 경우 회사의 기술 지원 부서에 문의 하십시오.

시스템 관리자는 다음 Microsoft TechNet Library 웹 사이트의 VSS 문제 해결 정보를 사용 하 여 VSS 관련 문제에 대 한 진단 정보를 수집할 수 있습니다.

자세한 내용은 TechNet의 [볼륨 섀도 복사본 서비스](http://go.microsoft.com/fwlink/?linkid=180905) (영문 http://go.microsoft.com/fwlink/?LinkId=180905) )을 참조 하세요.

### <a name="what-is-the-diff-area"></a>"Diff 영역" 이란?

섀도 복사본 저장소 영역 (또는 "diff 영역")은 시스템 소프트웨어 공급자가 만든 섀도 복사본의 데이터가 저장 되는 위치입니다.

### <a name="where-is-the-diff-area-located"></a>Diff 영역은 어디에 있나요?

차등 영역은 로컬 볼륨에 있을 수 있습니다. 그러나 저장할 공간이 충분 한 NTFS 볼륨에 있어야 합니다.

### <a name="how-is-the-diff-area-location-determined"></a>Diff 영역 위치는 어떻게 결정 되나요?

다음 기준은이 순서 대로 평가 되어 diff 영역 위치를 결정 합니다.

  - 볼륨에 기존 섀도 복사본이 이미 있는 경우 해당 위치가 사용 됩니다.  
      
  - 원래 볼륨과 섀도 복사본 볼륨 위치 간에 미리 구성 된 수동 연결이 있는 경우 해당 위치가 사용 됩니다.  
      
  - 이전 두 조건에서 위치를 제공 하지 않는 경우 섀도 복사본 서비스는 사용 가능한 공간에 따라 위치를 선택 합니다. 섀도 복사 중인 볼륨이 두 개 이상 있는 경우 섀도 복사본 서비스는 사용 가능한 공간 크기에 따라 사용 가능한 스냅숏 위치 목록을 내림차순으로 만듭니다. 제공 된 위치 수는 섀도 복사 되는 볼륨의 수와 같습니다.  
      
  - 섀도 복사 중인 볼륨이 가능한 위치 중 하나 이면 로컬 연결이 생성 됩니다. 그렇지 않으면 사용 가능한 공간이 가장 많은 볼륨과의 연결이 생성 됩니다.  
      

### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>VSS에서 NTFS가 아닌 볼륨의 섀도 복사본을 만들 수 있나요?

예. 그러나 NTFS 볼륨에 대해서만 영구적 섀도 복사본을 만들 수 있습니다. 또한 시스템에 탑재 된 하나 이상의 볼륨이 NTFS 볼륨 이어야 합니다.

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>한 번에 만들 수 있는 최대 섀도 복사본 수는 얼마 인가요?

단일 섀도 복사본 집합에서 섀도 복사 된 볼륨의 최대 수는 64입니다. 이는 섀도 복사본의 수와 같지 않습니다.

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>볼륨에 대해 유지 관리할 수 있는 시스템 공급자가 만든 소프트웨어 섀도 복사본의 최대 수는 얼마 인가요?

각 볼륨에 대 한 소프트웨어 섀도 복사본의 최대 수는 512입니다. 그러나 기본적으로 공유 폴더의 섀도 복사본 기능에서 사용 하는 64 섀도 복사본만 유지 관리할 수 있습니다. 공유 폴더의 섀도 복사본 기능에 대 한 제한을 변경 하려면 다음 레지스트리 키를 사용 합니다. **MaxShadowCopies**.

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>섀도 복사본 저장소 공간에 사용 되는 공간을 제어 하려면 어떻게 해야 하나요?

**Vssadmin resize shadowstorage** 명령을 입력 합니다.

자세한 내용은 [Vssadmin resize shadowstorage](http://go.microsoft.com/fwlink/?linkid=180906) (TechNet)http://go.microsoft.com/fwlink/?LinkId=180906) 를 참조 하세요.

### <a name="what-happens-when-i-run-out-of-space"></a>공간이 부족 하면 어떻게 되나요?

볼륨에 대 한 섀도 복사본이 가장 오래 된 섀도 복사본부터 삭제 됩니다.

## <a name="volume-shadow-copy-service-tools"></a>볼륨 섀도 복사본 서비스 도구

Windows 운영 체제는 VSS를 사용 하기 위한 다음과 같은 도구를 제공 합니다.

  - [DiskShadow](http://go.microsoft.com/fwlink/?linkid=180907) (http://go.microsoft.com/fwlink/?LinkId=180907)  
      
  - [VssAdmin](http://go.microsoft.com/fwlink/?linkid=84008) (http://go.microsoft.com/fwlink/?LinkId=84008)  
      

### <a name="diskshadow"></a>DiskShadow

DiskShadow는 시스템에서 사용할 수 있는 모든 하드웨어 및 소프트웨어 스냅숏을 관리 하는 데 사용할 수 있는 VSS 요청자입니다. DiskShadow에는 다음과 같은 명령이 포함 됩니다.

  - **목록**: VSS 기록기, VSS 공급자 및 섀도 복사본을 나열 합니다.  
      
  - **만들기**: 새 섀도 복사본을 만듭니다.  
      
  - **가져오기**: 전송 가능한 섀도 복사본을 가져옵니다.  
      
  - **노출**: 드라이브 문자로 영구 섀도 복사본을 노출 합니다 (예:).  
      
  - **되돌리기**: 볼륨을 지정 된 섀도 복사본으로 되돌립니다.  
      

이 도구는 IT 전문가를 위한 것 이지만 개발자가 VSS 기록기 또는 VSS 공급자를 테스트 하는 경우에도이 도구를 사용할 수 있습니다.

DiskShadow는 Windows Server 운영 체제 에서만 사용할 수 있습니다. Windows 클라이언트 운영 체제에서는 사용할 수 없습니다.

### <a name="vssadmin"></a>List

VssAdmin는 섀도 복사본에 대 한 정보를 생성, 삭제 및 나열 하는 데 사용 됩니다. 섀도 복사본 저장소 영역의 크기를 조정 하는 데 사용할 수도 있습니다 ("diff area").

VssAdmin에는 다음과 같은 명령이 포함 됩니다.

  - **그림자 만들기**: 새 섀도 복사본을 만듭니다.  
      
  - **그림자 삭제**: 섀도 복사본을 삭제 합니다.  
      
  - **목록 공급자**: 등록 된 모든 VSS 공급자를 나열 합니다.  
      
  - **기록기 나열**: 모든 구독 된 VSS 기록기를 나열 합니다.  
      
  - **shadowstorage 크기 조정**: 섀도 복사본 저장 영역의 최대 크기를 변경 합니다.  
      

VssAdmin는 시스템 소프트웨어 공급자가 만든 섀도 복사본을 관리 하는 데만 사용할 수 있습니다.

VssAdmin는 Windows 클라이언트 및 Windows Server 운영 체제 버전에서 사용할 수 있습니다.

## <a name="volume-shadow-copy-service-registry-keys"></a>레지스트리 키 볼륨 섀도 복사본 서비스

VSS에서 다음 레지스트리 키를 사용할 수 있습니다.

  - **VssAccessControl**  
      
  - **MaxShadowCopies**  
      
  - **MinDiffAreaFileSize**  
      

### <a name="vssaccesscontrol"></a>VssAccessControl

이 키는 섀도 복사본에 대 한 액세스 권한이 있는 사용자를 지정 하는 데 사용 됩니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조 하십시오.

  - [작성자를 위한 보안 고려 사항](http://go.microsoft.com/fwlink/?linkid=157739) (http://go.microsoft.com/fwlink/?LinkId=157739)  
      
  - [요청자를 위한 보안 고려 사항](http://go.microsoft.com/fwlink/?linkid=180908) (http://go.microsoft.com/fwlink/?LinkId=180908)  
      

### <a name="maxshadowcopies"></a>MaxShadowCopies

이 키는 컴퓨터의 각 볼륨에 저장할 수 있는 최대 클라이언트 액세스 가능 섀도 복사본 수를 지정 합니다. 클라이언트에서 액세스할 수 있는 섀도 복사본은 공유 폴더용 섀도 복사본에서 사용 됩니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조 하세요.

[백업 및 복원을 위한 레지스트리 키 아래에](http://go.microsoft.com/fwlink/?linkid=180909) **MaxShadowCopies** (http://go.microsoft.com/fwlink/?LinkId=180909)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

이 키는 섀도 복사본 저장 영역의 최소 초기 크기 (MB)를 지정 합니다.

자세한 내용은 MSDN 웹 사이트에서 다음 항목을 참조 하세요.

[백업 및 복원을 위한 레지스트리 키 아래에](http://go.microsoft.com/fwlink/?linkid=180910) **MinDiffAreaFileSize** (http://go.microsoft.com/fwlink/?LinkId=180910)

`##`# ' 지원 되는 운영 체제 버전

다음 표에서는 VSS 기능에 대해 지원 되는 최소 운영 체제 버전을 보여 줍니다.


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
<td><p><strong>Filesnottosnapshot</strong> 레지스트리 키</p></td>
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
<td><p>하드웨어 섀도 복사본의 여러 가져오기</p>
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
<td>섀도 복사본을 두 번 이상 가져올 수 있는 기능입니다. 한 번에 하나의 가져오기 작업만 수행할 수 있습니다.
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
<td><p>전송 가능한 자동 복구 된 섀도 복사본</p></td>
<td><p>지원되는 버전 없음</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>동시 백업 세션 (최대 64)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>백업에 대 한 단일 복원 세션 동시</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003 SP2</p></td>
</tr>
<tr class="even">
<td><p>백업을 사용 하는 동시에 최대 8 개의 복원 세션</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>참조

[Windows 개발자 센터의 볼륨 섀도 복사본 서비스](https://docs.microsoft.com/windows/desktop/vss/volume-shadow-copy-service-overview)