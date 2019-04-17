---
title: Windows Server 2019의에서 파일 공유 감시 배포
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: 파일 공유 목격자 클러스터 쿼럼 응답 파일 공유를 사용할 수 있도록 합니다. 이 항목에서는 파일 공유 목격자 및 파일 공유 감시로 라우터에 연결 된 USB 드라이브를 사용 하 여 포함 하 여 새 기능을 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 1888142f96208800a0417c9caeea89e8a0472e88
ms.sourcegitcommit: d622f7af181ed0063d716b30278d41887a57db19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "9150893"
---
# 파일 공유 감시 배포

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 공유 감시 장애 조치 클러스터의 클러스터 쿼럼에서 응답으로 사용 하는 SMB 공유입니다. 이 항목에서는 파일 공유 감시로 라우터에 연결 된 USB 드라이브를 사용 하는 등, Windows Server 2019의 새로운 기능 및 기술 개요를 제공 합니다.

파일 공유 목격자는 다음과 같은 경우에 유용 합니다.  

- 클러스터의 모든 서버는 신뢰할 수 있는 인터넷에 연결 되어 있으므로 클라우드 감시를 사용할 수 없습니다.
- 디스크 감시를 사용 하 여 공유 드라이브에 앞서 없기 때문에 디스크 감시를 사용할 수 없습니다. 저장소 공간 다이렉트 클러스터, SQL Server 항상에서 가용성 그룹 (AG), Exchange 데이터베이스 가용성 그룹 (DAG), 수 등.  이러한 유형의 클러스터 none 공유 디스크를 사용 합니다.

## 파일 공유 감시 요구 사항

도메인에 가입 된 Windows server에서 파일 공유 감시 호스팅하거나 클러스터를 실행 하는 모든 장치, Windows Server 2019 호스트 SMB 2 또는 이후 파일을 공유할 수 있습니다.

|파일 서버 유형                 | 지원 되는 클러스터 |
|---------------------------------|--------------------|
|모든 장치는 w/2 SMB 파일 공유 | WindowsServer 2019|
|도메인에 가입 된 Windows Server     | Windows Server 2008 이상|

클러스터에서 Windows Server 2019를 실행 중인 경우 요구 사항은 다음과 같습니다.

- *SMB 2 또는 이후 프로토콜을 사용 하는 모든 장치에서*SMB 파일 공유 포함 합니다.
    - 네트워크 연결 저장소 (NAS) 장치
    - Windows 컴퓨터가 작업 그룹에 가입
    - 라우터를 로컬로 연결 된 USB 저장소
- 클러스터를 인증 하기 위해 장치에 로컬 계정
- 파일 공유를 사용 하 여 클러스터를 인증 하기 위한 Active Directory를 대신 사용 하는, 클러스터 이름 개체 (CNO)는 공유에 대 한 쓰기 권한이 있어야 하 고 서버 클러스터와 동일한 Active Directory 포리스트에 있어야 합니다.
- 파일 공유에 최소 5MB의 여유 공간

클러스터를 실행 중인 경우 Windows Server 2016 또는 이전 버전을 요구 사항은 다음과 같습니다.

- *클러스터와 동일한 Active Directory 포리스트에 가입 된 Windows server에* SMB 파일 공유
- 클러스터 이름 개체 (CNO) 공유에 대 한 쓰기 권한이 있어야 합니다.
- 파일 공유에 최소 5MB의 여유 공간

기타 참고 사항:
- 도메인에 가입 된 Windows 서버 이외의 장치에서 호스트 되는 파일 공유 감시를 사용 하려면 현재 사용 해야 합니다 **Set-clusterquorum-자격 증명** PowerShell cmdlet이이 항목의 뒷부분에 설명 된 대로 감시를 설정 해야 합니다.
- 고가용성을 위해 별도 장애 조치 클러스터에서 파일 공유 감시를 사용할 수 있습니다.
- 여러 개의 클러스터에서 파일 공유 사용
- (분산 파일 시스템) 공유 또는 복제 된 저장소의 사용은 장애 조치 클러스터링의 모든 버전에는 지원 되지 않습니다.  이러한 클러스터링 된 서버 서로 독립적으로 실행 중이 고 데이터가 손실 될 수 있는 분할 브레인 상황이 발생할 수 있습니다.

## USB 장치를 사용 하 여 파일 공유 감시 라우터에 만들기

[Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)년 [DataOn 저장소](http://www.dataonstorage.com/) 키오스크 영역에는 저장소 공간 다이렉트 클러스터 보여 주었습니다.  이 클러스터 USB 포트를 사용 하 여 다음과 같은 파일 공유 감시로 [NetGear](https://www.netgear.com) Nighthawk X4S WiFi 라우터에 연결 되었습니다.

![NetGear 감시](media\File-Share-Witness\FSW1.png)

이 특정 라우터에서 USB 장치를 사용 하 여 파일 공유 감시를 만드는 단계는 다음과 같습니다.  방향 제공 하는 단계에서 다른 라우터 및 NAS 어플라이언스 다릅니다 아니며 공급 업체를 사용 하 여 수행 해야 합니다.


1. 전원에 연결 된 USB 장치를 사용 하 여 라우터에 로그인 합니다.

   ![NetGear 인터페이스](media\File-Share-Witness\FSW2.png)

2. 옵션 목록에서 공유를 만들 수 있는 ReadySHARE를 선택 합니다.

   ![NetGear ReadySHARE](media\File-Share-Witness\FSW3.png)

3. 파일 공유 감시에 대 한 기본 공유는 필요한 전부입니다.  편집 버튼을 선택 하면 USB 장치에서 공유를 만들 수 있는 대화 상자 팝업 됩니다.

   ![NetGear 공유 인터페이스](media\File-Share-Witness\FSW4.png)

4. "적용" 단추를 선택한 후 공유 생성 되 고 목록에서 볼 수 있습니다.

   ![NetGear 공유](media\File-Share-Witness\FSW5.png)

5. 공유를 만든 후 클러스터에 대 한 파일 공유 감시를 만드는 PowerShell을 사용 하 여 작업 수행 됩니다.

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   이 장치에 로컬 계정을 입력 하는 대화 상자를 표시 합니다.

USB 기능, NAS 장치 또는 다른 Windows 디바이스와 다른 라우터에 이러한 동일한 유사한 단계를 수행할 수 있습니다.
