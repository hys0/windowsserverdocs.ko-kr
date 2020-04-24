---
title: Windows Server 2016에 대한 업그레이드 및 변환 옵션
description: Windows Server 2016에 대해 지원되는 모든 업그레이드 경로를 설명합니다.
ms.prod: windows-server
ms.date: 01/18/2017
ms.technology: server-general
ms.topic: article
ms.assetid: 74aa1da3-7076-4a1f-ad5b-9e17bd46dba2
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 05e891d4170458018577b39bc83e952bf18d420e
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826506"
---
# <a name="upgrade-and-conversion-options-for-windows-server-2016"></a>Windows Server 2016에 대한 업그레이드 및 변환 옵션

>적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 여러 이전 운영 체제에서 Windows Server&reg; 2016으로 업그레이드하는 다양한 방법에 대해 설명합니다.

Windows Server 2016으로 이동하는 프로세스는 작업을 시작하는 운영 체제와 진행 경로에 따라 크게 다를 수 있습니다. 다음 용어를 사용하여 새로운 Windows Server 2016 배포에 포함될 수 있는 다양한 작업 간을 구분할 수 있습니다.

- **설치** 는 기본적으로 하드웨어에 새 운영 체제를 가져온다는 개념을 갖습니다. 특히 **새로 설치** 를 위해서는 이전 운영 체제를 삭제해야 합니다. Windows Server 2016 설치에 대한 자세한 내용은 [Windows Server 2016에 대한 시스템 요구 사항 및 설치 정보](https://technet.microsoft.com/windows-server-docs/get-started/system-requirements--and-installation)를 참조하세요. 다른 버전의 Windows Server 설치에 대한 자세한 내용은 [Windows Server 설치 및 업그레이드](https://technet.microsoft.com//windowsserver/dn527667)를 참조하세요.

- **마이그레이션**은 다른 하드웨어 또는 가상 머신 집합으로 전환하여 기존 운영 체제에서 Windows Server 2016으로 이동하는 것을 의미합니다. 설치한 서버 역할에 따라 크게 달라질 수 있는 마이그레이션은 [Windows Server 설치, 업그레이드 및 마이그레이션](https://technet.microsoft.com/windowsserver/dn458795)에 자세히 설명되어 있습니다.

- **클러스터 OS 롤링 업그레이드**는 관리자가 Hyper-V 또는 스케일 아웃 파일 서버 워크로드를 중지하지 않고 클러스터 노드의 운영 체제를 Windows Server 2012 R2에서 Windows Server 2016으로 업그레이드할 수 있는 Windows Server 2016의 새로운 기능입니다. 이 기능을 사용하면 서비스 수준 계약에 영향을 줄 수 있는 가동 중지 시간을 방지할 수 있습니다. 이 새로운 기능은 [클러스터 운영 체제 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)에 자세히 설명되어 있습니다.

- **라이선스 변환** 일부 운영 체제 릴리스에서는 간단한 명령과 적절한 라이선스 키를 사용하여 단일 단계에서 특정 버전의 릴리스를 동일한 릴리스의 다른 버전으로 변환할 수 있습니다. 이를 라이선스 변환이라고 합니다. 예를 들어 Windows Server 2016 Standard를 실행하는 경우 Windows Server 2016 Datacenter로 변환할 수 있습니다.

- **업그레이드**는 동일한 하드웨어에서 기존 운영 체제 릴리스를 보다 최근 릴리스로 이동하는 작업입니다. (이를 현재 위치 업그레이드라고도 합니다.) 예를 들어 서버에서 Windows Server 2012 또는 Windows Server 2012 R2를 실행하는 경우 Windows Server 2016으로 업그레이드할 수 있습니다. 평가판 운영 체제를 일반 정품 버전으로 업그레이드하거나, 이전 일반 정품 버전을 새 버전으로 업그레이드하거나, 경우에 따라 운영 체제의 볼륨 라이선스 버전을 일반 정품 버전으로 업그레이드할 수 있습니다.

> [!IMPORTANT]  
> 성공적인 업그레이드를 위해 특정 OEM 하드웨어 드라이버가 필요하지 않은 가상 컴퓨터에서 업그레이드가 가장 잘 작동합니다.  

> [!IMPORTANT]  
> 14393.0.161119-1705.RS1_REFRESH 이전의 Windows Server 2016의 릴리스에서는 데스크톱 환경 옵션을 사용하여 설치된 Windows Server 2016의 평가판에서 **일반 정품 버전으로의 변환만 수행**할 수 있습니다(Server Core 옵션 아님). 버전 14393.0.161119-1705.RS1_REFRESH 및 이후 릴리스부터는 사용한 설치 옵션에 상관없이 평가판을 일반 정품으로 변환할 수 있습니다.

> [!IMPORTANT]  
> 서버에서 NIC 팀을 사용하는 경우 업그레이드하기 전에 NIC 팀을 비활성화했다가 업그레이드가 완료된 후 다시 활성화합니다. 자세한 내용은 [NIC 팀 개요](https://technet.microsoft.com/library/hh831648(v=ws.11).aspx)를 참조하세요.

## <a name="upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016"></a>Windows Server 정품 이전 버전을 Windows Server 2016으로 업그레이드

아래 표는 **이미 사용 허가를 받은**, 즉 평가판이 아닌 각 Windows 운영 체제를 Windows Server 2016의 어떤 버전으로 업그레이드할 수 있는지를 간략하게 요약한 것입니다.

지원되는 경로는 다음 일반 지침을 참조하세요.

- 32비트에서 64비트 아키텍처로의 업그레이드는 지원되지 않습니다. Windows Server 2016의 모든 버전은 64비트 전용입니다.
- 한 언어에서 다른 언어로의 업그레이드는 지원되지 않습니다.
- 서버가 도메인 컨트롤러인 경우 자세한 내용은 [Windows Server 2012 R2 및 Windows Server 2012로 도메인 컨트롤러 업그레이드](https://technet.microsoft.com/library/hh994618.aspx)를 참조하세요.
- Windows Server 2016의 시험판 버전(미리 보기)에서 업그레이드는 지원되지 않습니다. Windows Server 2016에 새로 설치하세요.
- Server Core 설치에서 데스크톱 포함 서버 설치로(또는 그 반대로) 전환하는 업그레이드는 지원되지 않습니다.
- 이전 Windows Server 설치에서 Windows Server 평가판으로 업그레이드는 지원되지 않습니다. 평가판 버전은 새로 설치로 설치되어야 합니다.

왼쪽 열에 현재 버전이 표시되지 않으면 이 릴리스의 Windows Server 2016으로 업그레이드할 수 없습니다.

오른쪽 열에 둘 이상의 버전이 표시되면 동일한 시작 버전에서 **어느** 버전으로든 업그레이드할 수 있습니다.

|이 버전을 실행 중인 경우:|업그레이드 가능한 버전|  
|-------------------|----------|  
|Windows Server 2012 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 작업 그룹|Windows Storage Server 2016 작업 그룹|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 작업 그룹|


## <a name="per-server-role-considerations-for-upgrading"></a>업그레이드 시 서버 역할 고려 사항

이전 일반 정품 버전에서 Windows Server 2016으로 업그레이드가 가능한 지원되는 업그레이드 경로에서도 이미 설치된 특정 서버 역할이 업그레이드 후에도 계속 작동할 수 있도록 준비 작업이나 기타 작업이 필요할 수 있습니다. 필요할 수 있는 추가 단계에 대한 자세한 내용은 업그레이드하려는 각 서버 역할에 대한 특정 TechNet 라이브러리 항목을 참조하세요.

## <a name="converting-a-current-evaluation-version-to-a-current-retail-version"></a>현재 평가판을 현재 일반 정품 버전으로 변환

Windows Server 2016 Standard 평가판을 Windows Server 2016 Standard(일반 정품) 또는 Datacenter(일반 정품)로 변환할 수 있습니다. 마찬가지로, Windows Server 2016 Datacenter 평가판을 일반 정품 버전으로 변환할 수 있습니다.

> [!IMPORTANT]  
> 14393.0.161119-1705.RS1_REFRESH 이전의 Windows Server 2016의 릴리스에서는 데스크톱 환경 옵션을 사용하여 설치된 Windows Server 2016의 평가판에서 일반 정품 버전으로의 변환만 수행할 수 있습니다(Server Core 옵션 아님). 버전 14393.0.161119-1705.RS1_REFRESH 및 이후 릴리스부터는 사용한 설치 옵션에 상관없이 평가판을 일반 정품으로 변환할 수 있습니다.

평가판에서 일반 정품으로 변환하기 전에 서버에서 실제로 평가판을 실행 중인지 확인합니다. 다음 방법 중 하나로 확인할 수 있습니다.

- 관리자 권한 명령 프롬프트에서 **slmgr.vbs /dlv**명령을 실행합니다. 평가판의 경우 출력에 EVAL이 포함됩니다.

- 시작 화면에서 **제어판**을 엽니다. **시스템 및 보안**을 연 다음 **시스템**을 엽니다. **시스템** 페이지의 Windows 정품 인증 영역에서 Windows 정품 인증 상태를 확인합니다. Windows 정품 인증 상태에 대한 자세한 내용을 보려면 Windows 정품 인증에서 **세부 정보 보기** 를 클릭합니다.

이미 Windows 정품 인증을 완료한 경우 데스크톱에 남은 평가 기간이 표시됩니다.

서버에서 평가판 대신 일반 정품 버전을 실행하는 경우 이 항목의 이전 일반 정품 버전의 Windows Server를 Windows Server 2016으로 업그레이드 섹션에서 Windows Server 2016으로 업그레이드하는 방법을 확인할 수 있습니다.

**Windows Server 2016 Essentials**의 경우: **slmgr.vbs** 명령에서 일반 정품, 볼륨 라이선스 또는 OEM 키를 입력하여 완전한 정품으로 변환할 수 있습니다.

서버에서 Windows Server 2016 Standard 또는 Windows Server 2016 Datacenter의 평가판을 실행하는 경우 다음과 같은 방법으로 일반 정품으로 전환할 수 있습니다.

1.    서버가 **도메인 컨트롤러**인 경우 일반 정품으로 전환할 수 없습니다. 이 경우 서버에 일반 정품을 실행하는 도메인 컨트롤러를 추가로 설치하고 평가판을 실행하는 도메인 컨트롤러에서 AD DS를 제거해야 합니다. 자세한 내용은 [Windows Server 2012 R2 및 Windows Server 2012로 도메인 컨트롤러 업그레이드](https://technet.microsoft.com/library/hh994618.aspx)를 참조하세요.
2.    사용 조건을 읽습니다.
3.    관리자 권한 명령 프롬프트에서 **DISM /online /Get-CurrentEdition**명령을 사용하여 현재 버전 이름을 확인합니다. 버전 ID(버전 이름의 축약형)를 메모해 둡니다. 그런 다음 버전 ID와 일반 정품 제품 키를 제공하여 **DISM /online /Set-Edition:\<edition ID\> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula**를 실행합니다. 서버가 두 번 다시 시작됩니다.

Windows Server 2016 Standard 평가판의 경우 동일한 명령 및 적절한 제품 키를 사용하여 한 번에 Windows Server 2016 Datacenter 일반 정품으로 전환할 수 있습니다.

> [!TIP] 
> Dism.exe에 대한 자세한 내용은 [DISM 명령줄 옵션](https://go.microsoft.com/fwlink/?LinkId=192466)을 참조하세요.

## <a name="converting-a-current-retail-edition-to-a-different-current-retail-edition"></a>현재 일반 정품 버전을 다른 현재 일반 정품 버전으로 변환

Windows Server 2016을 설치한 후 언제든지 설치 프로그램을 실행하여 설치를 복구(전체 복구라고도 함)하거나, 경우에 따라 다른 버전으로 전환할 수 있습니다.
설치 프로그램을 실행하여 Windows Server 2016 버전에 대한 전체 복구를 수행하면 처음 시작한 버전으로 돌아갑니다.

Windows Server 2016 Standard의 경우 시스템을 다음과 같이 Windows Server 2016 Datacenter로 변환할 수 있습니다. 관리자 권한 명령 프롬프트에서 **DISM /online /Get-CurrentEdition**명령을 사용하여 현재 버전 이름을 확인합니다. Windows Server 2016 Standard의 경우 `ServerStandard`가 됩니다. 명령 **DISM /online /Get-TargetEditions**를 실행하여 업그레이드하려는 버전의 ID를 가져옵니다. 이 버전 ID(버전 이름의 축약형)를 메모해 둡니다. 그런 다음, 대상의 버전 ID와 일반 정품 제품 키를 제공하여 **DISM /online /Set-Edition:\<edition ID\> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula**를 실행합니다. 서버가 두 번 다시 시작됩니다.

## <a name="converting-a-current-retail-version-to-a-current-volume-licensed-version"></a>현재 일반 정품 버전을 현재 볼륨 라이선스 버전으로 변환

Windows Server 2016을 설치한 후 언제든지 일반 정품 버전, 볼륨 라이선스 버전 또는 OEM 버전 간에 자유롭게 변환할 수 있습니다. 이러한 변환에서 버전은 동일하게 유지됩니다. 평가판 버전으로 시작하는 경우 먼저 일반 정품 버전으로 변환한 다음 위의 설명대로 상호 변환할 수 있습니다.

이렇게 하려면 관리자 권한 명령 프롬프트에서 **slmgr /ipk \<key\>** 를 실행합니다.

여기서 \<key\>는 적절한 볼륨 라이선스, 일반 정품 또는 OEM 제품 키입니다.
