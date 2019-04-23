---
title: Windows Server 2019에서에서 파일 공유 감시를 배포 합니다.
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: 파일 공유 미러링 모니터 서버를 사용 하면 클러스터 쿼럼의 투표를 하려면 파일 공유를 사용할 수 있습니다. 이 항목에서는 파일 공유 미러링 모니터 서버 및 파일 공유 감시로 라우터에 연결 된 USB 드라이브를 사용 하 여 포함 하는 새로운 기능을 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 1888142f96208800a0417c9caeea89e8a0472e88
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831754"
---
# <a name="deploy-a-file-share-witness"></a>파일 공유 미러링 모니터 서버를 배포 합니다.

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 공유 미러링 모니터 서버는 장애 조치 클러스터의 클러스터 쿼럼에서 투표를 사용 하는 SMB 공유 합니다. 이 항목에서는 기술 및 Windows Server 2019, 파일 공유 감시로 라우터에 연결 된 USB 드라이브를 사용 하는 등의 새로운 기능 개요를 제공 합니다.

파일 공유 미러링 모니터 서버는 다음과 같은 상황에서 유용 하 게 합니다.  

- 클러스터의 모든 서버에 신뢰할 수 있는 인터넷 연결 클라우드 감시를 사용할 수 없습니다.
- 디스크 감시에 사용할 모든 공유 드라이브 없기 때문에 디스크 감시를 사용할 수 없습니다. 저장소 공간 다이렉트 클러스터에서 SQL Server 항상에서 가용성 그룹 (AG), Exchange 데이터베이스 가용성 그룹 (DAG), 수 등입니다.  클러스터의 이러한 유형이 아닌 공유 디스크를 사용 합니다.

## <a name="file-share-witness-requirements"></a>파일 공유 미러링 모니터 서버 요구 사항

도메인에 가입 된 Windows 서버에서 파일 공유 감시를 호스팅하거나 경우 클러스터를 실행 하는 모든 장치, Windows Server 2019 호스트는 SMB 2 또는 이후 파일을 공유할 수 있습니다.

|파일 서버 유형                 | 지원 되는 클러스터 |
|---------------------------------|--------------------|
|모든 장치는 w/SMB 2 파일 공유 | Windows Server 2019|
|도메인에 가입 된 Windows Server     | Windows Server 2008 이상|

클러스터에서 Windows Server 2019을 실행 하는 경우 요구 사항은 다음과 같습니다.

- SMB 파일 공유 *SMB 2 또는 이후 프로토콜을 사용 하는 모든 장치에서*등.
    - Network attached storage (NAS) 장치
    - 작업 그룹에 가입 된 Windows 컴퓨터
    - 로컬로 연결 된 USB 저장소를 사용 하 여 라우터
- 클러스터 인증에 대 한 장치에서 로컬 계정
- 파일 공유를 사용 하 여 클러스터를 인증 하는 것에 대 한 Active Directory를 대신 사용 하는, 하는 경우 클러스터 이름 개체 (CNO) 공유에 대 한 쓰기 권한이 있어야 하 고 서버 클러스터와 동일한 Active Directory 포리스트에 있어야 합니다.
- 파일 공유에 최소 5MB의 여유 공간

클러스터를 실행 중인 경우 Windows Server 2016 또는 이전 버전 요구 사항은 다음과 같습니다.

- SMB 파일 공유 *클러스터와 동일한 Active Directory 포리스트에 가입 된 Windows 서버*
- 클러스터 이름 개체 (CNO) 공유에 대 한 쓰기 권한이 있어야 합니다.
- 파일 공유에 최소 5MB의 여유 공간

기타 참고 사항:
- 호스트를 도메인에 가입 된 Windows server 이외의 장치에서 파일 공유 감시를 사용 하려면 현재 사용 해야 합니다 **Set-clusterquorum-자격 증명** 이 항목의 뒷부분에 설명 된 대로 미러링 모니터를 설정 하려면 PowerShell cmdlet.
- 고가용성을 위해 파일 공유 감시를 별도 장애 조치 클러스터에서 사용할 수 있습니다.
- 여러 클러스터에서 파일 공유를 사용할 수 있습니다.
- 장애 조치 클러스터링의 모든 버전을 사용 하 여 공유 파일 시스템 (DFS (분산) 또는 복제 된 저장소의 사용 지원 되지 않습니다.  클러스터형된 서버 서로 독립적으로 실행 중이 고 데이터 손실을 초래할 수 있는 분할 브레인 상황이 발생할 수 있습니다 이러한 합니다.

## <a name="creating-a-file-share-witness-on-a-router-with-a-usb-device"></a>USB 장치를 사용 하 여 라우터의 파일 공유 감시 만들기

언제 [Microsoft Ignite 2018](https://azure.microsoft.com/ignite/), [DataOn 저장소](http://www.dataonstorage.com/) 키오스크 영역에 저장소 공간 다이렉트 클러스터를 했습니다.  이 클러스터에 연결 된를 [NetGear](https://www.netgear.com) Nighthawk X4S WiFi 라우터가 USB 포트를 사용 하 여 파일 공유 감시 다음과 유사 하 게 합니다.

![NetGear 미러링 모니터 서버](media\File-Share-Witness\FSW1.png)

이 특정 라우터에서 USB 장치를 사용 하 여 파일 공유 미러링 모니터 서버를 만드는 단계는 다음과 같습니다.  참고는 다른 라우터 및 NAS 장치에 대 한 단계는 달라 지 며이 공급 업체를 사용 하 여 수행 해야 하는 지침을 제공 합니다.


1. USB 장치 연결을 사용 하 여 라우터에 로그인 합니다.

   ![NetGear 인터페이스](media\File-Share-Witness\FSW2.png)

2. 옵션의 목록에서 공유를 만들 수 있는 상태인 ReadySHARE를 선택 합니다.

   ![NetGear ReadySHARE](media\File-Share-Witness\FSW3.png)

3. 파일 공유 감시를 기본 공유는 필요한 모든 것입니다.  편집 단추를 선택 하는 USB 장치에서 공유를 만들 수 있는 대화 상자가 팝업 됩니다.

   ![NetGear 공유 인터페이스](media\File-Share-Witness\FSW4.png)

4. [적용] 단추를 선택한 후에 공유 생성 되 고 목록에서 볼 수 있습니다.

   ![NetGear 공유](media\File-Share-Witness\FSW5.png)

5. 공유를 만든 후 클러스터에 대 한 파일 공유 감시를 만드는 PowerShell을 사용 하 여 작업 수행 됩니다.

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   그러면 장치에서 로컬 계정을 입력 하는 대화 상자가 표시 됩니다.

USB 기능, NAS 장치 또는 다른 Windows 장치를 사용 하 여 다른 라우터에서 같은 유사한 단계를 수행할 수 있습니다.
