---
title: 데스크톱 환경 포함 서버 설치
description: '데스크톱 환경 포함 서버 설치를 얻어서 설치하는 방법 설명 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 01/18/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b38b8a0-4dfc-4130-be00-fc58bba99595
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: eb2e5be2ed19fe7cd64f6c6bd64ca9afafd93bff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812314"
---
# <a name="install-server-with-desktop-experience"></a>데스크톱 환경 포함 서버 설치
> 적용 대상: Windows Server 2016
  

설치 마법사를 사용하여 Windows Server 2016을 설치하면 **Windows Server 2016**과 **Windows Server(데스크톱 환경 포함 서버)** 중에 선택할 수 있습니다. 데스크톱 환경 포함 서버 옵션은 데스크톱 환경 기능이 설치된 Windows Server 2012 R2에서 제공되는 전체 설치 옵션에 해당하는 Windows Server 2016의 옵션입니다. 설치 마법사에서 항목을 선택하지 않으면 **Windows Server 2016**이 설치됩니다. 이는 **Server Core** 설치 옵션입니다.

데스크톱 환경 포함 서버 옵션은 Windows Server 2012 R2에 별도 설치해야 하는 클라이언트 환경 기능을 포함하여 표준 사용자 인터페이스 및 모든 도구가 설치됩니다. 서버 역할과 기능은 서버 관리자 또는 다른 메서드를 통해 설치됩니다. Server Core 옵션에 비해 디스크에 더 많은 공간이 필요하고 서비스 요구 사항이 높기 때문에 데스크톱 환경 포함 서버 옵션에 포함된 추가 사용자 인터페이스 요소와 그래픽 관리 도구가 특별히 필요한 경우가 아니라면 Server Core 설치 옵션을 선택하는 것이 좋습니다. 추가 요소가 없어도 작업이 가능할 것 같으면 [Server Core 설치](Getting-Started-with-Server-Core.md)를 참조하세요. 더 가벼운 설치 옵션을 원한다면 [Nano 서버 설치](Getting-Started-with-Nano-Server.md)를 참조하세요.

>[!NOTE]
>
>일부 이전 릴리스의 Windows Server와 달리 설치 후 Server Core와 데스크톱 경험 기능이 설치된 서버 간에 변환할 수 없습니다. 데스크톱 경험을 설치하고 나중에 Server Core를 사용하기로 결정하는 경우에는 새로 설치를 수행해야 합니다.

**사용자 인터페이스:** 표준 그래픽 사용자 인터페이스("서버 그래픽 셸"). 서버 그래픽 셸에 새로운 Windows 10 셸이 포함되어 있습니다. 이 옵션을 통해 기본적으로 설치되는 특정 Windows 기능은 User-Interfaces-Infra, Server-GUI-Shell, Server-GUI-Mgmt-Infra, InkAndHandwritingServices, ServerMediaFoundation 및 데스크톱 환경입니다. 이러한 기능은 이 릴리스의 서버 관리자에 표시되어 있지만 제거할 수 없으며 이후 릴리스에서 제공되지 않습니다.

**로컬에서 서버 역할 설치, 구성, 제거** : 서버 관리자 또는 Windows PowerShell 사용

**원격으로 서버 역할 설치, 구성, 제거** : 서버 관리자, 원격 서버, RSAT 또는 Windows PowerShell을 사용하여 실행

**Microsoft Management Console: 설치**

## <a name="installation-scenarios"></a>설치 시나리오

### <a name="evaluation"></a>Evaluation
[Windows Server 평가판](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)에서 Windows Server 180일 라이선스 평가판 사본을 얻을 수 있습니다. **Windows Server 2016 | 64비트 ISO 옵션**을 선택하여 다운로드하세요. 또는 **Windows Server 2016 | 가상 랩**을 방문하셔도 됩니다.

> [!IMPORTANT]  
> 14393.0.161119-1705.RS1_REFRESH 이전의 Windows Server 2016의 릴리스에서는 데스크톱 환경 옵션을 사용하여 설치된 Windows Server 2016의 평가판에서 일반 정품 버전으로의 변환만 수행할 수 있습니다(Server Core 옵션 아님). 버전 14393.0.161119-1705.RS1_REFRESH 및 이후 릴리스부터는 사용한 설치 옵션에 상관없이 평가판을 일반 정품으로 변환할 수 있습니다.


### <a name="clean-installation"></a>새로 설치

미디어로 데스크톱 환경 포함 서버 옵션을 설치하려면 드라이브에 미디어를 삽입하고, 컴퓨터를 다시 시작하고, Setup.exe를 실행합니다. 열리는 마법사에서 **Windows Server(데스크톱 환경 포함 서버)**(Standard 또는 Datacenter)를 선택한 다음 마법사를 완료합니다.

### <a name="upgrade"></a>업그레이드
**업그레이드**는 동일한 하드웨어에서 기존 운영 체제 릴리스를 보다 최근 릴리스로 이동하는 작업입니다.

적절한 Windows Server 제품이 이미 전체 설치된 경우 아래와 같이 적절한 Windows Server 2016 버전의 데스크톱 환경 포함 서버 설치로 업그레이드할 수 있습니다.

> [!IMPORTANT]  
> 이 릴리스에서는 성공적인 업그레이드를 위해 특정 OEM 하드웨어 드라이버가 필요하지 않은 가상 컴퓨터에서 업그레이드가 가장 잘 작동합니다. 그렇지 않으면 마이그레이션을 사용하는 것이 좋습니다.  

- 32비트에서 64비트 아키텍처로의 전체 업그레이드는 지원되지 않습니다. Windows Server 2016의 모든 버전은 64비트 전용입니다.
- 한 언어에서 다른 언어로의 전체 업그레이드는 지원되지 않습니다.
- 서버가 도메인 컨트롤러인 경우 자세한 내용은 [Windows Server 2012 R2 및 Windows Server 2012로 도메인 컨트롤러 업그레이드](https://technet.microsoft.com/library/hh994618.aspx)를 참조하세요.
- Windows Server 2016의 시험판 버전(미리 보기)에서 업그레이드는 지원되지 않습니다. Windows Server 2016에 새로 설치하세요.
- Server Core 설치에서 데스크톱 포함 서버 설치로(또는 그 반대로) 전환하는 업그레이드는 지원되지 않습니다.

왼쪽 열에 현재 버전이 표시되지 않으면 이 릴리스의 Windows Server 2016으로 업그레이드할 수 없습니다.

오른쪽 열에 둘 이상의 버전이 표시되면 동일한 시작 버전에서 **어느** 버전으로든 업그레이드할 수 있습니다.

|이 버전을 실행 중인 경우:|업그레이드 가능한 버전|  
|-------------------|----------|  
|Windows Server 2012 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 작업 그룹|Windows Storage Server 2016 작업 그룹|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 작업 그룹|

볼륨 라이선스 버전, 평가판 버전 및 기타 버전 간에 라이선스를 변환하는 경우처럼 Windows Server 2016으로 전환하는 여러 추가 옵션에 대한 자세한 내용은 [업그레이드 옵션](Supported-Upgrade-Paths.md)을 참조하세요.

### <a name="migration"></a>마이그레이션
**마이그레이션**이란 다양한 하드웨어 또는 가상 컴퓨터 집합에 새로 설치한 다음 이전 서버의 워크로드를 새 서버로 전송하여 기존 운영 체제에서 Windows Server 2016으로 이동하는 것을 의미합니다. 설치한 서버 역할에 따라 크게 달라질 수 있는 마이그레이션은 [Windows Server 설치, 업그레이드 및 마이그레이션](https://technet.microsoft.com/windowsserver/dn458795)에 자세히 설명되어 있습니다.

마이그레이션 기능은 다양한 서버 역할에 따라 다릅니다. 다음 그리드는 특히 Windows Server 2016으로 전환하기 위한 서버 역할 업그레이드 및 마이그레이션 옵션을 설명합니다. 개별 역할 마이그레이션 가이드는 [Windows Server에서 역할 및 기능 마이그레이션](https://technet.microsoft.com/windowsserver/jj554790.aspx)을 참조하세요. 설치 및 업그레이드에 대한 자세한 내용은 [Windows Server 설치, 업그레이드 및 마이그레이션](https://technet.microsoft.com/windowsserver/dn458795)을 참조하세요.

|서버 역할|Windows Server 2012 R2에서 업그레이드 가능 여부|Windows Server 2012에서 업그레이드 가능 여부|마이그레이션 지원 여부|가동 중지 시간 없이 마이그레이션을 완료할 수 있는지 여부|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory 인증서 서비스| 예|    예|    예|    아니오|
|Active Directory 도메인 서비스|  예|    예|    예|    예|
|AD FS(Active Directory Federation Services)|  아니요| 아니요| 예|    아니요(새 노드를 팜에 추가해야 함)|
|Active Directory LDS(Lightweight Directory Services)|   예|    예|    예|    예|
|Active Directory Rights Management Services|   예|    예|    예|    아니요|
|장애 조치(failover) 클러스터|예, 노드 일시 중지-드레이닝, 제거, Windows Server 2016으로 업그레이드 및 원본 클러스터 다시 연결을 포함하는 [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) 프로세스 사용. 예, 서버가 업그레이드를 위해 클러스터에 의해 제거된 후 다른 클러스터에 추가되는 경우.|서버가 클러스터에 속하지 않는 동안은 아님. 예, 서버가 업그레이드를 위해 클러스터에 의해 제거된 후 다른 클러스터에 추가되는 경우.  |예|아니요, Windows Server 2012 장애 조치(failover) 클러스터인 경우. 예, Hyper-V VM 포함 Windows Server 2012 R2 장애 조치 클러스터 또는 스케일 아웃 파일 서버 역할을 실행하는 Windows Server 2012 R2 장애 조치 클러스터인 경우. [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)를 참조하세요.|
|파일 및 저장소 서비스| 예|    예|    하위 기능에 따라 다름|  아니요|
|인쇄 및 팩스 서비스|    아니오| 아니오| 예(Printbrm.exe)| 아니요|
|원격 데스크톱 서비스|   예, 모든 하위 역할, 혼합 모드 팜은 지원되지 않음|   예, 모든 하위 역할, 혼합 모드 팜은 지원되지 않음|   예|    아니오|
|웹 서버(IIS)|  예|    예|    예|    아니오|
|Windows Server 필수 패키지 환경|  예|    해당 없음 – 새 기능|  예|    아니요|
|Windows Server Update Services|    예|    예|    예|    아니요|
|클라우드 폴더|  예|    예|    예|    예, [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)를 사용할 경우 WS 2012 R2 클러스터에서|

> [!IMPORTANT]  
> 설치가 완료되고 필요한 모든 서버 역할과 기능을 설치하는 즉시, Windows 업데이트 또는 기타 업데이트 방법을 사용하여 Windows Server 2016에 제공되는 업데이트를 확인하고 설치합니다.

---------------------------------------
다른 설치 옵션이 필요한 경우 또는 설치를 완료했고 특정 워크로드를 배포할 준비가 완료된 경우 [Windows Server 2016 기본 페이지로 돌아갈 수 있습니다](Windows-Server-2016.md).