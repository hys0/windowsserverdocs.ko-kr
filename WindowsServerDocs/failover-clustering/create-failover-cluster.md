---
title: 장애 조치 클러스터 만들기
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016에 대 한 장애 조치 클러스터를 만드는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f919e69488c4f2272ddd07e535ba4e2248ddf79c
ms.sourcegitcommit: 5cbaca9685720f11d896c4ca167c86e74c032feb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "6068981"
---
# 장애 조치 클러스터 만들기

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

이 항목에는 장애 조치 클러스터 관리자 스냅인 또는 Windows PowerShell을 사용 하 여 장애 조치 클러스터를 만드는 방법을 보여 줍니다. 일반적인 배포에서 Active Directory 도메인 서비스 (AD DS)에 클러스터와 관련된 된 클러스터 된 역할에 대 한 컴퓨터 개체가 만들어지는 설명 합니다. 저장소 공간 다이렉트 클러스터를 배포 하는 경우 대신 [저장소 공간 다이렉트 배포](../storage/storage-spaces/deploy-storage-spaces-direct.md)참조 합니다.

Active Directory 분리 클러스터를 배포할 수 있습니다. 이 배포 방법은 해당 컴퓨터에서 AD DS 개체는 미리 준비를 요청 해야 또는 AD DS의 컴퓨터 개체를 만들 수 있는 권한이 없는 장애 조치 클러스터를 만들 수 있습니다. 이 옵션만 Windows PowerShell을 통해 사용할 수 있으며 특정 시나리오에만 권장 됩니다. 자세한 내용은 [Active Directory-Detached 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))를 참조 하세요.

#### 검사 목록: 장애 조치 클러스터 만들기

|상태|작업|참조|
|:---:|---|---|
|☐|필수 구성 요소를 확인 합니다.|[필수 구성 요소를 확인 합니다.](#verify-the-prerequisites)|
|☐|클러스터 노드를 추가 하려면 모든 서버에서 장애 조치 클러스터링 기능을 설치 합니다.|[장애 조치 클러스터링 기능 설치](#install-the-failover-clustering-feature)|
|☐|구성의 유효성을 검사 하려면 클러스터 유효성 검사 마법사 실행|[구성을 확인합니다](#validate-the-configuration)|
|☐|장애 조치 클러스터를 만들려면 클러스터 만들기 마법사 실행|[장애 조치 클러스터 만들기](#create-the-failover-cluster)|
|☐|호스트 클러스터 작업에 클러스터링 된 역할 만들기|[클러스터 된 역할을 만듭니다.](#create-clustered-roles)|

## 필수 구성 요소를 확인 합니다.

시작 하기 전에 다음 필수 조건을 확인 합니다.

- 모든 서버를 클러스터 노드를 추가 하려면 동일한 버전의 Windows Server를 실행 되 고 있는지 확인 합니다.
- 구성이 지원 되는지 확인 하려면 하드웨어 요구 사항을 검토 합니다. 자세한 내용은 [장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션을](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612869(v%3dws.11))참조 하세요. 저장소 공간 다이렉트 클러스터를 만드는 경우에 [저장소 공간 다이렉트 하드웨어 요구 사항을](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)참조 하세요.
- 클러스터 저장소 클러스터를 만드는 동안를 추가 하려면 모든 서버에서 저장소에 액세스할 수 있는지를 확인 합니다. (또한 추가 클러스터 저장소 클러스터를 만든 후.)
- 클러스터 노드를 추가 하려면 모든 서버 동일한 Active Directory 도메인에 가입 되어 있는지 확인 합니다.
- (선택 사항) 한 OU (조직 단위)를 만들고 클러스터 노드와 OU에 추가 하려는 서버에 대 한 컴퓨터 계정을 이동 합니다. 모범 사례로, 장애 조치 클러스터는 AD DS에 고유한 OU에 배치 하는 것이 좋습니다. 이 그룹 정책 설정 또는 보안 템플릿 설정을 클러스터 노드에 영향을 효과적으로 제어할 수 있습니다. 고유한 OU에 클러스터를 분리 하 여도 방지할 수 클러스터 컴퓨터 개체의 실수로 삭제 합니다.

또한 다음 계정 요구 사항을 확인 합니다.

- 클러스터를 만드는 데 사용할 계정 클러스터 노드를 추가 하려면 모든 서버에서 관리자 권한을 가진 도메인 사용자 인지 확인 합니다.
- 다음 중 하나에 해당 하는지 확인 합니다.
    - 클러스터를 만드는 사용자 OU 또는 클러스터를 구성 하는 서버 있는 컨테이너 **만들기 컴퓨터 개체** 권한이 있습니다.
    - 사용자 **컴퓨터 개체** 권한이 없으면 클러스터에 대 한 클러스터 컴퓨터 개체 사전 준비 하려면 도메인 관리자를 요청 합니다. 자세한 내용은 [Active Directory 도메인 서비스에서 Prestage 클러스터 컴퓨터 개체](prestage-cluster-adds.md)를 참조 하세요.

>[!NOTE]
>Windows Server 2012 r 2에서 Active Directory 분리 클러스터를 만들려는 경우에이 요구 사항은 적용 되지 않습니다. 자세한 내용은 [Active Directory-Detached 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))를 참조 하세요.

## 장애 조치 클러스터링 기능 설치

장애 조치 클러스터 노드를 추가 하려면 모든 서버에서 장애 조치 클러스터링 기능을 설치 해야 합니다.

### 장애 조치 클러스터링 기능 설치

1. 서버 관리자를 시작합니다.
2. **관리** 메뉴에서 **역할 및 기능 추가**선택 합니다.
3. **시작 하기 전에** 페이지에서 **다음**을 선택 합니다.
4. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 선택한 **다음**을 선택 합니다.
5. **대상 서버 선택** 페이지에서이 기능을 설치 하려면 서버를 선택 하 고 **** 을 선택 합니다.
6. **서버 역할 선택** 페이지에서 **다음**을 선택 합니다.
7. **기능 선택** 페이지에서 **장애 조치 클러스터링** 확인란을 선택 합니다.
8. 장애 조치 클러스터 관리 도구를 설치 하려면 **추가 기능**을 선택 하 고 **** 을 선택 합니다.
9. **확인 설치 선택** 페이지에서 **설치**를 선택 합니다.
<br>서버를 다시 시작 장애 조치 클러스터링 기능에 대 한 필요 하지 않습니다.

10. 설치가 완료 되 면 **닫기**를 선택 합니다.
11. 장애 조치 클러스터 노드를 추가 하려면 모든 서버에서이 절차를 반복 합니다.

>[!NOTE]
>장애 조치 클러스터링 기능을 설치한 후에 Windows 업데이트에서 최신 업데이트를 적용 하는 것이 좋습니다. 또한, Windows Server 2012 기반 장애 조치 클러스터에 대 한 [권장 핫픽스 및 업데이트에 대 한 Windows Server 2012 기반 장애 조치 클러스터인 경우](https://support.microsoft.com/help/2784261/recommended-hotfixes-and-updates-for-windows-server-2012-based-failove) Microsoft 지원 문서를 검토 하 고 적용 되는 업데이트를 설치 합니다.

## 구성을 확인합니다

장애 조치 클러스터를 만들기 전에 하드웨어와 하드웨어 설정이 장애 조치 클러스터링과 호환 하는지 확인 하기 위해 구성의 유효성을 검사 하는 것이 좋습니다. Microsoft 구성을 완료 모든 유효성 검사를 통과 하는 경우에 클러스터 솔루션을 지 원하는 테스트 및 클러스터 노드에서 실행 되는 Windows Server 버전에 대 한 모든 하드웨어 인증 되는 경우.

>[!NOTE]
>모든 테스트를 실행 하려면 두 개 이상의 노드가 있어야 합니다. 노드가 하나만 있는 경우이 여러 중요 한 저장소 테스트는 실행 되지 않습니다.

### 클러스터 유효성 검사 테스트를 실행 합니다.

1. 원격 서버 관리 도구에서 설치 된 장애 조치 클러스터 관리 도구를 사용 하는 컴퓨터에서 또는 장애 조치 클러스터링 기능을 설치한 서버에서 장애 조치 클러스터 관리자를 시작 합니다. 서버에서 이렇게 하려면 서버 관리자를 시작 하 고 **도구** 메뉴에서 **장애 조치 클러스터 관리자**를 선택 합니다.
2. **장애 조치 클러스터 관리자** 창의 **관리**, **구성의 유효성을 검사**를 선택 합니다.
3. **시작 하기 전에** 페이지에서 **다음**을 선택 합니다.
4. **선택 서버 또는 클러스터** 페이지 **이름 입력** 상자에서 NetBIOS 이름 또는 장애 조치 클러스터 노드를 추가 하려는 서버의 정규화 된 도메인 이름을 입력 하 고 **추가**선택 합니다. 추가 하려는 각 서버에 대해이 단계를 반복 합니다. 이와 동시에 여러 서버를 추가 하려면 이름을 쉼표 또는 세미콜론으로 구분 합니다. 예를 들어 형식 *server1.contoso.com, server2.contoso.com*이름을 입력 합니다. 완료 되 면 **다음**을 선택 합니다.
5. **테스트 옵션** 페이지에서 선택 **(권장) 모든 테스트를 실행**하 고 **** 을 선택 합니다.
6. **확인** 페이지에서 **다음**을 선택 합니다.

    유효성 검사 페이지 테스트 실행의 상태를 표시 합니다.
7. **요약** 페이지에서 다음 중 하나를 수행 합니다.
    
      - 결과 테스트가 성공적으로 완료 및 구성을 클러스터링에 적합 합니다.을 즉시 클러스터를 만들려는 경우, **이제 유효성이 검사 된 노드를 사용 하 여 클러스터 만들기** 확인란 선택 되어 있는지 확인 한 후 **완료**를 선택 합니다. 그런 다음, [장애 조치 클러스터 만들기](#create-the-failover-cluster) 절차의 4 단계를 계속 진행 합니다.
      - 결과 경고 또는 오류가 발생 했음을 나타냅니다, 세부 정보를 보려면 어떤 문제를 해결 해야 결정을 **보고서 보기** 선택 합니다. 특정 유효성 검사 테스트에 대 한 경고 장애 조치 클러스터의이 부분 지원할 수 있지만 권장된 모범 사례를 충족할 수 있음을 인식 합니다.
        
        >[!NOTE]
        >저장소 공간 영구 예약 유효성 검사 테스트에 대 한 경고를 수신 하는 경우에 대 한 자세한 내용은 [Windows 장애 조치 클러스터 유효성 검사 경고 디스크는 저장소 공간에 대 한 영구 예약을 지원 하지 나타냅니다](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) 게시 블로그를 참조 하세요.

하드웨어 유효성 검사 테스트에 대 한 자세한 내용은 [장애 조치 클러스터에 대 한 하드웨어 유효성 검사](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)를 참조 하세요.

## 장애 조치 클러스터 만들기

이 단계를 완료 하려면 사용자 계정으로 로그온 하는이 항목의 [필수 구성 요소를 확인](#verify-the-prerequisites) 섹션에서 설명 하는 요구 사항을 충족 하는지 확인 합니다.

1. 서버 관리자를 시작합니다.
2. **도구** 메뉴에서 **장애 조치 클러스터 관리자**를 선택 합니다.
3. **장애 조치 클러스터 관리자** 창의 **관리** **클러스터 만들기**를 선택 합니다.
    
    클러스터 만들기 마법사가 열립니다.
4. **시작 하기 전에** 페이지에서 **다음**을 선택 합니다.
5. **서버 선택** 페이지 **이름 입력** 상자에 표시 되 면 NetBIOS 이름 또는 장애 조치 클러스터 노드를 추가 하려는 서버의 정규화 된 도메인 이름을 입력 하 고 **추가**선택 합니다. 추가 하려는 각 서버에 대해이 단계를 반복 합니다. 이와 동시에 여러 서버를 추가 하려면 이름을 쉼표 또는 세미콜론으로 구분 합니다. 예를 들어 형식 *server1.contoso.com; server2.contoso.com*이름을 입력 합니다. 완료 되 면 **다음**을 선택 합니다.
    
    >[!NOTE]
    >클러스터 [유효성 검사 구성 절차](#validate-the-configuration)에서 유효성 검사를 실행 한 후 즉시 만들 하기로 선택한 경우 **서버 선택** 페이지를 나타나지 않습니다. 유효성이 검사 된 노드는 다시 입력 하지 않았을 수 있도록 클러스터 만들기 마법사를 자동으로 추가 됩니다.
6. 이전에 유효성 검사를 건너뛰면 **유효성 검사 경고** 페이지가 나타납니다. 클러스터 유효성 검사를 실행 하는 것이 좋습니다. Microsoft에서 모든 유효성 검사 테스트를 통과 하는 클러스터만 지원 됩니다. 유효성 검사 테스트를 실행 하려면 **예**, 선택 하 고 **** 을 선택 합니다. [유효성 검사 구성에](#validate-the-configuration)에서 설명 된 대로 유효성 검사 구성 마법사를 완료 합니다.
7. **클러스터를 관리 하기 위한 액세스 지점** 페이지에서 다음을 수행 합니다.
    
    1. **클러스터 이름** 상자에서 클러스터를 관리 하는 데 사용할 이름을 입력 합니다. 전에 다음 정보를 검토를 수행 합니다.
        
          - 클러스터 생성 하는 동안이 이름은 AD DS에서 클러스터 컴퓨터 개체 ( *클러스터 이름 개체* 또는 *CNO*라고도 함)으로 등록 됩니다. 클러스터에 대 한 NetBIOS 이름을 지정 하는 경우 CNO 클러스터 노드에 대 한 컴퓨터 개체 상주 하는 동일한 위치에 만들어집니다. 이 기본 컴퓨터 컨테이너 또는 OU 수 있습니다.
          - CNO에 대 한 다른 위치를 지정 하려면 OU의 고유 이름 **클러스터 이름** 상자에 입력할 수 있습니다. 예: *CN = ClusterName, OU 클러스터, DC = Contoso, DC = com =* 합니다.
          - 도메인 관리자가 클러스터 노드가 있는 보다 다른 OU에 CNO 미리 준비 하는 경우 도메인 관리자가 제공 하는 고유 이름을 지정 합니다.
    2. 서버에 DHCP를 사용 하도록 구성 된 네트워크 어댑터를 찾을 수 없는 경우 장애 조치 클러스터에 대 한 하나 이상의 고정 IP 주소를 구성 해야 합니다. 클러스터 관리에 사용 하려는 각 네트워크 옆에 있는 확인란을 선택 합니다. 선택한 네트워크 옆 **주소** 필드를 선택 하 고 클러스터를 할당 하고자 하는 IP 주소를 입력 합니다. 이 IP 주소 (또는 주소) 클러스터 이름에서 시스템 DNS (도메인 이름)와 연결 됩니다.
    3. 완료 되 면 **다음**을 선택 합니다.
8. **확인** 페이지에서 설정을 검토 합니다. 기본적으로 **모든 적격 저장소 클러스터에 추가** 확인란이 선택 되어 있습니다. 다음 중 하나를 수행 하려는 경우이 확인란의 선택을 취소 합니다.
    
      - 나중에 저장소를 구성 하려고 합니다.
      - 장애 조치 클러스터 관리자를 통해 또는 장애 조치 클러스터링 Windows PowerShell cmdlet을 통해 클러스터 저장소 공간을 만들고 아직 만들지 않은 저장소 공간에서 파일 및 저장소 서비스 계획 합니다. 자세한 내용은 [클러스터 저장소 공간 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)를 참조 하세요.
9. **다음** 장애 조치 클러스터 만들기를 선택 합니다.
10. **요약** 페이지에서 장애 조치 클러스터 성공적으로 만들어졌는지 확인 합니다. 모든 경고 또는 오류가 없다면 요약 출력을 확인 하거나 전체 보고서를 보려면 **보고서 보기** 선택 합니다. **완료**를 선택 합니다.
11. 클러스터를 만들 것인지 탐색 트리에서 **장애 조치 클러스터 관리자** 에서 클러스터 이름이 나열 되어 있는지 확인 합니다. 클러스터 이름을 확장 하 고 **노드**, **저장소** 또는 **네트워크** 관련된 리소스를 보려면 아래의 항목을 선택할 수 있습니다.
    
    실현 DNS에 성공적으로 복제에 클러스터 이름 시간이 오래 걸릴 수 있습니다. 성공적인 DNS 등록 및 복제 후 서버 관리자에서 **모든 서버** 를 선택 하는 경우 클러스터 이름으로 표시 해야 **관리 효율성** 상태를 **온라인**으로 서버.

클러스터를 만든 후 할 수 있는 것 같은 클러스터 쿼럼 구성을 확인 하 고 선택적으로 클러스터 공유 볼륨 (CSV)를 만듭니다. 자세한 내용은 [에서 저장소 공간 다이렉트 이해 쿼럼](../storage/storage-spaces/understand-quorum.md) 및 [장애 조치 클러스터에서 사용 하 여 클러스터 공유 볼륨](failover-cluster-csvs.md)을 참조 하세요.

## 클러스터 된 역할을 만듭니다.

장애 조치 클러스터를 만든 후에 호스트 클러스터 작업에 클러스터링 된 역할을 만들 수 있습니다.

>[!NOTE]
>클라이언트 액세스 포인트를 필요로 하는 클러스터링 된 역할에 대 한 가상 컴퓨터 개체 (VCO) AD DS에 만들어집니다. 기본적으로 클러스터에 대 한 모든 Vco CNO로 동일한 컨테이너 또는 OU에 생성 됩니다. 클러스터를 만든 후 이동할 수 있습니다 CNO OU를 실현 합니다.

클러스터 된 역할을 만드는 방법은 다음과 같습니다.

1. 서버 관리자를 사용 하거나 Windows PowerShell 역할 또는 각 장애 조치 클러스터 노드에서 클러스터 된 역할에 필요한 기능을 설치 합니다. 예를 들어 클러스터 된 파일 서버를 만들려는 경우 모든 클러스터 노드에서 파일 서버 역할을 설치 합니다.
    
    다음 표에서 고가용성 마법사와 관련 된 서버 역할 또는 필수 조건으로 설치 해야 하는 기능에서 구성할 수 있는 클러스터 된 역할을 보여 줍니다.
    
    <table>
    <thead>
    <tr class="header">
    <th>클러스터 된 역할</th>
    <th>역할 또는 기능 필수 구성 요소</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>DFS Namespace 서버</td>
    <td>DFS 네임 스페이스 (파일 서버 역할의 일부)</td>
    </tr>
    <tr class="even">
    <td>DHCP 서버</td>
    <td>DHCP 서버 역할</td>
    </tr>
    <tr class="odd">
    <td>Distributed Transaction Coordinator DTC)</td>
    <td>없음</td>
    </tr>
    <tr class="even">
    <td>파일 서버</td>
    <td>파일 서버 역할</td>
    </tr>
    <tr class="odd">
    <td>일반 응용 프로그램</td>
    <td>해당 없음</td>
    </tr>
    <tr class="even">
    <td>일반 스크립트</td>
    <td>해당 없음</td>
    </tr>
    <tr class="odd">
    <td>일반 서비스</td>
    <td>해당 없음</td>
    </tr>
    <tr class="even">
    <td>Hyper-v 복제본 브로커</td>
    <td>Hyper-v 역할</td>
    </tr>
    <tr class="odd">
    <td>iSCSI 대상 서버</td>
    <td>iSCSI 대상 서버 (파일 서버 역할의 일부)</td>
    </tr>
    <tr class="even">
    <td>iSNS 서버</td>
    <td>iSNS 서버 서비스 기능</td>
    </tr>
    <tr class="odd">
    <td>메시지 큐</td>
    <td>메시지 큐 서비스 기능</td>
    </tr>
    <tr class="even">
    <td>다른 서버</td>
    <td>없음</td>
    </tr>
    <tr class="odd">
    <td>가상 컴퓨터</td>
    <td>Hyper-v 역할</td>
    </tr>
    <tr class="even">
    <td>WINS 서버</td>
    <td>WINS 서버 기능</td>
    </tr>
    </tbody>
    </table>
2. 장애 조치 클러스터 관리자에서 클러스터 이름을 확장 하 고 **역할**마우스 오른쪽 단추로 클릭 한 다음 **구성 역할**을 선택 합니다.
3. 클러스터 된 역할을 만드는 고가용성 마법사의 단계를 수행 합니다.
4. **역할** 창에서 클러스터 된 역할 생성 되었는지 확인 하려면 역할 **실행**의 상태에 있는지 확인 합니다. 또한 역할 창 소유자 노드를 나타냅니다. 장애 조치를 테스트 하려면 역할을 마우스 오른쪽 단추로 클릭 하 고 **이동**을 가리킨 다음 **노드 선택**를 선택 합니다. **클러스터 된 역할 이동** 대화 상자에서 원하는 클러스터 노드를 선택 하 고 **확인**을 선택 합니다. **소유자 노드** 열에서 소유자 노드를 변경 하는 것을 확인 합니다.

## Windows PowerShell을 사용 하 여 장애 조치 클러스터 만들기

다음 Windows PowerShell cmdlet이이 항목의 이전 절차와 동일한 기능을 수행합니다. 표시 될 수 바꿈 여러 줄에서 서식 제약 조건으로 인해 하는 경우에 한 줄에 각 cmdlet을 입력 합니다.

>[!NOTE]
>Windows Server 2012 r 2에서 Active Directory 분리 클러스터를 만들려면 Windows PowerShell을 사용 해야 합니다. 구문에 대 한 자세한 내용은 [Active Directory-Detached 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))를 참조 하세요.

다음 예제에서는 장애 조치 클러스터링 기능을 설치합니다.

```PowerShell
Install-WindowsFeature –Name Failover-Clustering –IncludeManagementTools
```

다음 예제에서는 *1* 을 *서버 2*라고 하는 컴퓨터에서 모든 클러스터 유효성 검사 테스트를 실행 합니다.

```PowerShell
Test-Cluster –Node Server1, Server2
```

>[!NOTE]
>**테스트 클러스터** cmdlet은 현재 작업 디렉터리에 로그 파일에 결과 출력합니다. 예: < 사용자 이름 > C:\Users\ \AppData\Local\Temp 합니다.

다음 예제에서는 *서버 1* 노드와 *MyCluster* 및 *서버 2*라는는 정적 IP 주소 *192.168.1.12*, 할당 및 장애 조치 클러스터에 적합 한 모든 저장소를 추가 하는 장애 조치 클러스터를 만듭니다.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12
```

다음 예제에서는 이전 예제와 같이 동일한 장애 조치 클러스터 만들지만 장애 조치 클러스터에 적합 한 저장소를 추가 하지 않습니다.

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12 -NoStorage
```

다음 예제에서는 라는 *MyCluster* *Contoso.com*도메인의 OU *클러스터* 에서 클러스터를 만듭니다.

```PowerShell
New-Cluster -Name CN=MyCluster,OU=Cluster,DC=Contoso,DC=com -Node Server1, Server2
```

클러스터링 된 역할을 추가 하는 방법의 예제를 [추가 ClusterFileServerRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clusterfileserverrole?view=win10-ps) 등 [추가 ClusterGenericApplicationRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergenericapplicationrole?view=win10-ps)항목을 참조 하세요.

## 자세한 정보

  - [장애 조치 클러스터링](failover-clustering.md)
  - [Hyper-v 클러스터 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj863389(v%3dws.11)>)
  - [응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831349(v%3dws.11)>)
  - [Active Directory 분리 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))
  - [고가용성을 위한 게스트 클러스터링 사용](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)
  - [클러스터 인식 업데이트](cluster-aware-updating.md)
  - [새 클러스터](https://docs.microsoft.com/powershell/module/failoverclusters/new-cluster?view=win10-ps)
  - [테스트 클러스터](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)
