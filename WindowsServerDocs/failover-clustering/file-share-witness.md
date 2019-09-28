---
title: Windows Server 2019에서 파일 공유 감시 배포
ms.prod: windows-server
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: 파일 공유 미러링 모니터 서버를 사용 하면 파일 공유를 사용 하 여 클러스터 쿼럼에 응답할 수 있습니다. 이 항목에서는 파일 공유 감시로 라우터에 연결 된 USB 드라이브를 사용 하는 것을 포함 하 여 파일 공유 미러링 모니터 서버 및 새 기능에 대해 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 9f0a0c5b48f7c382367e4b1100ff649fe73d3be9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369756"
---
# <a name="deploy-a-file-share-witness"></a>파일 공유 감시 배포

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 공유 감시는 장애 조치 (Failover) 클러스터가 클러스터 쿼럼에서 응답으로 사용 하는 SMB 공유입니다. 이 항목에서는 파일 공유 감시로 라우터에 연결 된 USB 드라이브를 사용 하는 것을 포함 하 여 Windows Server 2019의 새로운 기능 및 기술에 대 한 개요를 제공 합니다.

파일 공유 미러링 모니터 서버는 다음과 같은 경우에 유용 합니다.  

- 클러스터의 일부 서버에서 신뢰할 수 있는 인터넷 연결이 없기 때문에 클라우드 감시를 사용할 수 없습니다.
- 디스크 감시에 사용할 공유 드라이브가 없으므로 디스크 감시를 사용할 수 없습니다. 스토리지 공간 다이렉트 클러스터, SQL Server Always On 가용성 그룹 (AG), Exchange 데이터베이스 가용성 그룹 (DAG) 등이 있습니다.  이러한 유형의 클러스터는 공유 디스크를 사용 하지 않습니다.

## <a name="file-share-witness-requirements"></a>파일 공유 감시 요구 사항

도메인에 가입 된 Windows server에서 파일 공유 감시를 호스팅하거나, 클러스터가 Windows Server 2019를 실행 하는 경우 SMB 2 이상 파일 공유를 호스트할 수 있습니다.

|파일 서버 유형                 | 지원 되는 클러스터 |
|---------------------------------|--------------------|
|SMB 2 파일 공유에 있는 모든 장치 | Windows Server 2019|
|도메인에 가입 된 Windows Server     | Windows Server 2008 이상|

클러스터가 Windows Server 2019를 실행 하는 경우 요구 사항은 다음과 같습니다.

- 다음을 포함 하 여 *smb 2 이상 프로토콜을 사용 하는 모든 장치의*smb 파일 공유
    - NAS (네트워크 연결 저장소) 장치
    - 작업 그룹에 가입 된 Windows 컴퓨터
    - 로컬로 연결 된 USB 저장소가 있는 라우터
- 클러스터를 인증 하는 장치의 로컬 계정
- 대신 파일 공유를 사용 하 여 클러스터를 인증 하는 데 Active Directory를 사용 하는 경우 클러스터 이름 개체 (CNO)에 공유에 대 한 쓰기 권한이 있어야 하 고, 서버가 클러스터와 동일한 Active Directory 포리스트에 있어야 합니다.
- 파일 공유의 사용 가능한 공간이 5mb 이상입니다.

클러스터가 Windows Server 2016 이전 버전을 실행 하는 경우 요구 사항은 다음과 같습니다.

- *클러스터와 동일한 Active Directory 포리스트에 조인 된 Windows 서버의* SMB 파일 공유
- 클러스터 이름 개체 (CNO)에는 공유에 대 한 쓰기 권한이 있어야 합니다.
- 파일 공유의 사용 가능한 공간이 5mb 이상입니다.

기타 참고 사항:
- 도메인에 가입 된 Windows server 이외의 장치에서 호스트 되는 파일 공유 감시를 사용 하려면 현재이 항목의 뒷부분에서 설명 하는 대로 감시를 설정 하는 데 **-ClusterQuorum** 설정 해야 합니다.
- 고가용성을 위해 별도의 장애 조치 (Failover) 클러스터에서 파일 공유 감시를 사용할 수 있습니다.
- 파일 공유는 여러 클러스터에서 사용할 수 있습니다.
- 모든 버전의 장애 조치 (failover) 클러스터링에서는 DFS (분산 파일 시스템) 공유 또는 복제 된 저장소를 사용할 수 없습니다.  이로 인해 클러스터 된 서버가 서로 독립적으로 실행 되 고 데이터가 손실 될 수 있는 분할 된 두뇌 상황이 발생할 수 있습니다.

## <a name="creating-a-file-share-witness-on-a-router-with-a-usb-device"></a>USB 장치를 사용 하 여 라우터에 파일 공유 감시 만들기

[Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)에서 [저장소의 dataon](http://www.dataonstorage.com/) 키오스크 영역에 스토리지 공간 다이렉트 클러스터가 있습니다.  이 클러스터는이와 비슷한 파일 공유 감시로 USB 포트를 사용 하 여 [Netgear](https://www.netgear.com) Nighthawk X4S WiFi 라우터에 연결 되었습니다.

![NetGear 감시](media/File-Share-Witness/FSW1.png)

이 특정 라우터에 USB 장치를 사용 하 여 파일 공유 감시를 만드는 단계는 다음과 같습니다.  다른 라우터와 NAS 어플라이언스에 대 한 단계는 다를 수 있으며 공급 업체에서 제공 하는 지침을 사용 하 여 수행 해야 합니다.


1. 연결 된 USB 장치를 사용 하 여 라우터에 로그인 합니다.

   ![NetGear 인터페이스](media/File-Share-Witness/FSW2.png)

2. 옵션 목록에서 ReadySHARE를 선택 하 여 공유를 만들 수 있는 위치를 선택 합니다.

   ![NetGear ReadySHARE](media/File-Share-Witness/FSW3.png)

3. 파일 공유 감시의 경우 기본 공유만 있으면 됩니다.  편집 단추를 선택 하면 USB 장치에서 공유를 만들 수 있는 대화 상자가 표시 됩니다.

   ![NetGear 공유 인터페이스](media/File-Share-Witness/FSW4.png)

4. 적용 단추를 선택 하면 공유가 만들어지고 목록에서 볼 수 있습니다.

   ![NetGear 공유](media/File-Share-Witness/FSW5.png)

5. 공유를 만든 후에는 클러스터에 대 한 파일 공유 감시 만들기가 PowerShell을 사용 하 여 수행 됩니다.

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   그러면 장치의 로컬 계정을 입력할 수 있는 대화 상자가 표시 됩니다.

이와 동일한 비슷한 단계는 USB 기능, NAS 장치 또는 기타 Windows 장치를 사용 하는 다른 라우터에서 수행할 수 있습니다.
