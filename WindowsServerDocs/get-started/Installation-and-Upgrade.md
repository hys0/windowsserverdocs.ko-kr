---
title: Windows Server 설치 및 업그레이드
description: ''
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 07/12/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f876bd-63ff-4c3a-95d4-a8dd8d0d119c
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: c3b9070fc6cb9227ccfa445e23983d9e91fe5c82
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859194"
---
# <a name="windows-server-installation-and-upgrade"></a>Windows Server 설치 및 업그레이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 및 Windows Server 2008에 대한 연장 지원이 2020년 1월에 종료됩니다. [업그레이드 옵션에 대 한 자세한](#upgrading-from-windows-server-2008-r2-or-windows-server-2008)합니다.

Windows Server 새 버전으로 전환할 시점입니까? 현재 무엇을 실행 중인가에 따라 다양한 옵션이 있습니다.

## <a name="installation"></a>설치
동일한 하드웨어에서 Windows Server 새 버전으로 전환하고자 할 경우 언제나 확실한 방법은 새 운영 체제를 같은 하드웨어에 있는 기존 버전 위에 바로 설치하여 기존 운영 체제를 삭제하는 **새로 설치**입니다. 가장 간단한 방법이지만 먼저 데이터를 백업하고 나중에 응용 프로그램을 재설치할 계획을 세워야 합니다. 시스템 요구 사항 등과 같이 미리 알아야 할 사항들이 몇 가지 있으니 [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418), [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) 등의 세부 사항을 반드시 확인하시기 바랍니다.

Windows Server 2016 Technical Preview 등과 같은 시험판 버전에서 정식 버전(Windows Server 2016)으로 전환하는 경우에는 항상 새로 설치가 필요합니다.

## <a name="migration-recommended-for-windows-server-2016"></a>마이그레이션(Windows Server 2016에 권장)

Windows Server [마이그레이션] 설명서는 Windows Server를 실행하는 원본 컴퓨터로부터 동일 버전 또는 새 버전의 Windows Server를 실행하는 다른 대상 컴퓨터로 역할 또는 기능을 한 번에 하나씩 마이그레이션할 때 도움이 됩니다. 이와 같은 목적일 때 마이그레이션은 동일한 컴퓨터에서 기능을 업그레이드하는 작업이 아니라 하나의 역할 또는 기능과 그 데이터를 다른 컴퓨터로 옮기는 작업으로 정의됩니다. 기존 워크로드와 데이터를 더 최신 버전의 Windows Server로 옮기기 위해 권장되는 방식입니다. 시작하려면 Windows Server 2016의 [server role upgrade and migration matrix(서버 역할 업그레이드 및 마이그레이션 매트릭스)](https://go.microsoft.com/fwlink/?LinkId=828595)를 확인하시기 바랍니다.

## <a name="cluster-os-rolling-upgrade"></a>클러스터 운영 체제 롤링 업그레이드
클러스터 OS 롤링 업그레이드는 관리자가 Hyper-V 또는 스케일 아웃 파일 서버 워크로드를 중지하지 않고 클러스터 노드의 운영 체제를 Windows Server 2012 R2에서 Windows Server 2016으로 업그레이드할 수 있는 Windows Server 2016의 새로운 기능입니다. 이 기능을 사용하면 서비스 수준 계약에 영향을 줄 수 있는 가동 중지 시간을 방지할 수 있습니다. 이 새로운 기능은 [클러스터 운영 체제 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)에 자세히 설명되어 있습니다.

## <a name="license-conversion"></a>라이선스 변환
일부 운영 체제 릴리스에서는 해당 릴리스의 특정 버전을 간단한 명령과 적절한 라이선스 키만으로 동일한 릴리스의 다른 버전으로 한 번에 변환할 수 있습니다. 이를 **라이선스 변환**이라 합니다. 예를 들어 서버가 Windows Server 2016 Standard를 실행하는 경우 Windows Server 2016 Datacenter로 변환할 수 있습니다. 또한 일부 Windows Server 릴리스에서는 동일한 명령과 적절한 키를 이용하여 OEM, 볼륨 라이선스 및 일반 정품 버전 사이에서 자유롭게 변환할 수도 있습니다.

## <a name="upgrade"></a>업그레이드
서버를 완전히 갈아엎지 않고 동일한 하드웨어와 이미 설정해 둔 서버 역할을 모두 유지하고자 할 경우에는 **업그레이드**가 하나의 옵션이며 매우 다양한 방법이 있습니다. 전형적인 업그레이드에서는 설정과 서버 역할, 데이터 등을 그대로 유지하면서 기존 운영 체제를 새 운영 체제로 교체합니다. 예를 들어 서버에서 Windows Server 2012 R2를 실행하는 경우 Windows Server 2016으로 업그레이드할 수 있습니다. 그러나 모든 기존 운영 체제가 모든 새 운영 체제로 업그레이드될 수 있는 것은 아닙니다.
 
>[!NOTE]
>성공적인 업그레이드를 위해 특정 OEM 하드웨어 드라이버가 필요하지 않은 가상 컴퓨터에서 업그레이드가 가장 잘 작동합니다.
 
평가판 운영 체제를 일반 정품 버전으로 업그레이드하거나, 이전 일반 정품 버전을 새 버전으로 업그레이드하거나, 경우에 따라 운영 체제의 볼륨 라이선스 버전을 일반 정품 버전으로 업그레이드할 수 있습니다.

업그레이드를 시작하기 전에, 현재 상태에서 원하는 상태로 전환하는 방법을 이 페이지에 수록된 테이블을 통해 확인하시기 바랍니다.

각 옵션과 함께 설치되는 기능 및 설치 후 사용 가능한 관리 옵션을 포함하여 Windows Server 2016 Technical Preview에서 사용할 수 있는 설치 옵션 간의 차이점에 대한 자세한 내용은 [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkId=828598)을 참조하시기 바랍니다.

>[!NOTE]
>어느 버전의 Windows Server로든 마이그레이션 또는 업그레이드할 때마다 반드시 해당 버전의 [지원 주기 정책](https://support.microsoft.com/lifecycle)과 지원 기간을 검토 및 파악하여 그에 따라 계획을 수립해야 합니다. 관심 있는 특정 Windows Server 릴리스에 대한 [수명 주기 정보](https://support.microsoft.com/lifecycle)를 검색할 수 있습니다.
 
 
## <a name="upgrading-to-windows-server-2016"></a>Windows Server 2016으로 업그레이드
업그레이드 관련 주의 사항과 제한 사항, Windows Server 2016 버전 간 변환, 평가판의 일반 정품 버전으로의 변환 등을 포함한 자세한 내용은 [Supported Upgrade Paths for Windows Server 2016(Windows Server 2016에 대한 업그레이드 및 변환 옵션)](https://go.microsoft.com/fwlink/?LinkId=828602)을 참조하시기 바랍니다.
 
>[!NOTE]
>참고: Server Core 설치에서 데스크톱 포함 서버 설치로(또는 그 반대로) 전환하는 업그레이드는 지원되지 않습니다. 업그레이드 또는 변환하는 기존 운영 체제가 Server Core 설치인 경우 새 운영 체제 역시 Server Core 설치가 될 것입니다.
 
이전 Windows Server 일반 정품 버전으로부터 Windows Server 2016 일반 정품 버전으로 업그레이드할 때 지원되는 경로를 정리한 빠른 참조 표:


|현재 실행 중인 버전:|업그레이드 가능한 버전:|
|--------------------------------|---------------------------------------|
|Windows Server 2012 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Hyper-V Server 2012 R2|Hyper-V Server 2016(클러스터 OS 롤링 업그레이드 기능)|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 작업 그룹|Windows Storage Server 2016 작업 그룹|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 작업 그룹|
 
### <a name="license-conversion"></a>라이선스 변환
Windows Server 2016 Standard 일반 정품 버전을 Windows Server 2016 Datacenter 일반 정품 버전으로 변환할 수 있습니다.

Windows Server 2016 Essentials 일반 정품 버전을 Windows Server 2016 Standard 일반 정품 버전으로 변환할 수 있습니다.

Windows Server 2016 Standard 평가판을 Windows Server 2016 Standard(일반 정품) 또는 Datacenter(일반 정품)로 변환할 수 있습니다.

Windows Server 2016 Datacenter 평가판을 Windows Server 2016 Datacenter 일반 정품 버전으로 변환할 수 있습니다.
 
## <a name="upgrading-to-windows-server-2012-r2"></a>Windows Server 2012 R2로 업그레이드
업그레이드 관련 주의 사항과 제한 사항, Windows Server 2012 R2 버전 간 변환, 평가판의 일반 정품 버전으로의 변환 등을 포함한 자세한 내용은 [Upgrade Options for Windows Server 2012 R2(Windows Server 2012 R2에 대한 업그레이드 옵션)](https://technet.microsoft.com/library/dn303416.aspx)을 참조하시기 바랍니다.

이전 Windows Server 일반 정품 버전으로부터 Windows Server 2012 R2 일반 정품 버전으로 업그레이드할 때 지원되는 경로를 정리한 빠른 참조 표:

|실행 중인 버전|업그레이드 가능한 버전|
|-------------------------|---------------------------|
|Windows Server 2008 R2 Datacenter sp1|Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Enterprise sp1|Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Standard sp1|Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter|
|Windows Web Server 2008 R2 sp1|Windows Server 2012 R2 Standard|
|Windows Server 2012 Datacenter|Windows Server 2012 R2 Datacenter|
|Windows Server 2012 Standard|Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter|
|Hyper-V Server 2012|Hyper-V Server 2012 R2|

### <a name="license-conversion"></a>라이선스 변환
Windows Server 2012 Standard 일반 정품 버전을 Windows Server 2012 Datacenter 일반 정품 버전으로 변환할 수 있습니다.

Windows Server 2012 Essentials 일반 정품 버전을 Windows Server 2012 Standard 일반 정품 버전으로 변환할 수 있습니다.

Windows Server 2012 Standard 평가판을 Windows Server 2012 Standard(일반 정품) 또는 Datacenter(일반 정품)로 변환할 수 있습니다.

## <a name="upgrading-to-windows-server-2012"></a>Windows Server 2012로 업그레이드
업그레이드와 관련된 중요한 주의 사항과 제한 사항, 평가판 버전을 일반 정품 버전으로 변환하는 방법 등에 관한 자세한 내용은 [Evaluation Versions and Upgrade Options for Windows Server 2012(Windows Server 2012의 평가 버전 및 업그레이드 옵션)](https://technet.microsoft.com/library/jj574204.aspx)을 참조하시기 바랍니다.
 
이전 Windows Server 일반 정품 버전으로부터 Windows Server 2012 일반 정품 버전으로 업그레이드할 때 지원되는 경로를 정리한 빠른 참조 표:

|실행 중인 버전|업그레이드 가능한 버전|
|--------------------------|--------------------------|
|Windows Server 2008 Standard SP2 또는 Windows Server 2008 Enterprise SP2|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 Datacenter SP2|Windows Server 2012 Datacenter|
|Windows Web Server 2008|Windows Server 2012 Standard|
|Windows Server 2008 R2 Standard SP1 또는 Windows Server 2008 R2 Enterprise sp1|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 R2 Datacenter sp1|Windows Server 2012 Datacenter|
|Windows Web Server 2008 R2|Windows Server 2012 Standard|

### <a name="license-conversion"></a>라이선스 변환
Windows Server 2012 Standard 일반 정품 버전을 Windows Server 2012 Datacenter 일반 정품 버전으로 변환할 수 있습니다.

Windows Server 2012 Essentials 일반 정품 버전을 Windows Server 2012 Standard 일반 정품 버전으로 변환할 수 있습니다.

Windows Server 2012 Standard 평가판을 Windows Server 2012 Standard(일반 정품) 또는 Datacenter(일반 정품)로 변환할 수 있습니다.

## <a name="upgrading-from-windows-server-2008-r2-or-windows-server-2008"></a>Windows Server 2008 R2 또는 Windows Server 2008에서 업그레이드

에 설명 된 대로 [업그레이드 Windows Server 2008 및 Windows Server 2008 R2](modernize-windows-server-2008.md), Windows Server 2008 R2 또는 Windows Server 2008에 대 한 연장된 지원은 2020 년 1 월의 끝나는 합니다. 지원 되는 버전의 Windows Server를 업그레이드 하거나 이동 하 여 Azure에서 rehost 해야을 보장 하기 위해 지원에 간격이 없어야 [특수 용 Windows Server 2008 R2 Vm](uploading-specialized-WS08-image-to-azure.md)합니다. 체크 아웃 합니다 [Windows Server에 대 한 마이그레이션 가이드](https://go.microsoft.com/fwlink/?linkid=872689) 정보 및 마이그레이션/업그레이드 계획에 대 한 고려 사항에 대 한 합니다.

온-프레미스 서버에 대 한 Windows Server 2008 R2를 Windows Server 2016 이상에서 직접 업그레이드 경로가 없는 있습니다. 대신, Windows Server 2012 R2로 먼저 업그레이드 한 다음 [Windows Server 2016으로 업그레이드](#Upgrading-to-Windows-Server-2016)합니다.

업그레이드를 계획 하는 Windows Server 2012 R2로 업그레이드 하는 중간 단계에 대 한 다음 지침에 주의 해야 합니다.

  - 32 비트에서 64 비트 아키텍처에서의 전체 업그레이드를 수행할 수 없거나 하나 빌드에서 다른 (예를 들어에서 chk로 서) 형식을 수 없습니다.

  - 동일한 언어의 전체 업그레이드만 지원 됩니다. 다른 언어에서 업그레이드할 수 없습니다.

  - Windows Server 2012 R2 서버 GUI (Windows Server에서 "서버 사용 하 여 전체 데스크톱" 라고 함)를 사용 하 여 Windows Server 2008 server core 설치에서 마이그레이션할 수 없습니다. Windows Server 2012 R2에만 전체 데스크톱을 사용 하 여 서버를 업그레이드 된 server core 설치를 전환할 수 있습니다. Windows Server 2016 이상 *하지* server core에서 전체 데스크톱으로 전환 지원, Windows Server 2016으로 업그레이드 하기 전에 해당 스위치 확인 합니다.
  
자세한 내용은 체크 아웃 [평가 버전 및 업그레이드 옵션 Windows Server 2012 용](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574204\(v=ws.11\)), 역할별 업그레이드 세부 정보를 포함 하는 합니다.

