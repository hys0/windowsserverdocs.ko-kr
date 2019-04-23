---
title: Server Core 앱 호환성 FOD(Feature on Demand)
description: 필요에 따라 Windows Server 기능을 설치 하는 방법
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: b8211ace56aa6565295a15adce26a8dfbc98e1e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866114"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>Server Core 앱 호환성 FOD(Feature on Demand)

> Windows Server 2019 및 Windows Server 버전 1809에 적용 됩니다.

**필요에 따라 Server Core 앱 호환성 기능** 은 Windows Server 2019 Server Core 설치 또는 Windows Server 버전 1809, 언제 든 지 추가할 수 있는 선택적 기능 패키지입니다.

기능에서 FOD (주문형)에 대 한 자세한 내용은 참조 하세요. [주문형 기능](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)합니다.


## <a name="why-install-the-app-compatibility-fod"></a>앱 호환성 FOD 설치 하는 이유? 

응용 프로그램 호환성, Server Core에 대 한 주문형 기능을 추가 하지 않고 이진 파일 및 데스크톱 환경 포함 Windows Server에서 패키지의 하위 집합을 포함 하 여 Windows Server Core 설치 옵션의 응용 프로그램 호환성을 크게 개선 합니다 Windows Server Desktop Experience 그래픽 환경입니다. 이 선택적 패키지를 별도 ISO 또는 Windows Update에서 사용할 수 있지만 Windows Server Core 설치와 이미지에만 추가할 수 있습니다.

앱 호환성 FOD 제공 두 기본 값은:

1.  이미 시장에 또는 이미 조직에서 개발 되어 배포는 서버 응용 프로그램에 대 한 Server Core의 호환성을 증가 합니다.

2.  OS 구성 요소 및 향상 된 응용 프로그램 호환성 문제 해결 및 디버깅 시나리오 예에 사용 되는 소프트웨어 도구를 제공 하는 데 유용 합니다.

Server Core 앱 호환성 FOD 부분을 포함 하는 대로 사용할 수 있는 운영 체제 구성 요소:

-   Microsoft Management Console (mmc.exe)

-   이벤트 뷰어 (Eventvwr.msc)

-   성능 모니터 (PerfMon.exe)

-   리소스 모니터 (Resmon.exe)

-   장치 관리자 (Devmgmt.msc)

-   파일 탐색기 (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   디스크 관리 (Diskmgmt.msc)

-   장애 조치 클러스터 관리자 (CluAdmin.msc)

    -   먼저 Windows Server를 클러스터링 하는 장애 조치 기능이 필요합니다.

        -   Powershell Cmdlet을 사용 하 여 추가 하 고, `Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools`

        -   장애 조치 클러스터 관리자를 실행 하려면 입력 **cluadmin** 명령 프롬프트에서.

## <a name="installing-the-app-compatibility-fod"></a>응용 프로그램 호환성 FOD 설치

 >[!IMPORTANT] 
   >앱 호환성 FOD Server Core에만 설치할 수 있습니다. Server Core 앱 호환성 FOD 데스크톱 환경 포함 Windows Server의 Windows Server 설치에 추가 하지 마십시오.

### <a name="to-add-the-server-core-app-compatibility-feature-on-demand-fod-to-a-running-instance-of-server-core"></a>Server Core의 실행 인스턴스를 필요 시 (해당 FOD)에서 Server Core 응용 프로그램 호환성 기능을 추가 하려면

 >[!NOTE] 
   > 이 절차에서는 배포 이미지 서비스 및 관리 (DISM.exe) 명령줄 도구를 사용 합니다. DISM 명령에 대 한 자세한 내용은 참조 하세요. [DISM 기능 패키지 서비스 명령줄 옵션](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-capabilities-package-servicing-command-line-options)합니다.

>[!NOTE] 
   > Windows Server 2019 Server Core 설치 또는 Windows Server 버전 1809, 설치는 동일한 FOD 선택적 패키지 ISO를 사용할 수 있습니다.

>[!NOTE] 
   > 컴퓨터 또는 Server Core를 실행 하는 가상 머신을 Windows Update에 연결할 경우 1 ~ 7 아래 단계를 건너뛸 수 있습니다. 하지만 8 단계에서 DISM 명령의 /Source 및 /LimitAccess 남겨 두어야 합니다.

1. 서버 FOD 선택적 패키지 ISO를 다운로드 하 여 ISO 로컬 네트워크의 공유 폴더에 복사.

 - 볼륨 라이선스가 있는 경우에 OS ISO 이미지 파일을 가져온 위치 하 고 같은 포털에서 서버 FOD ISO 이미지 파일을 다운로드할 수 있습니다. [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)합니다.
 - Server FOD ISO 이미지 파일에서 제공 됩니다. 합니다 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 또는 합니다 [Visual Studio 포털](https://visualstudio.microsoft.com) 구독자에 대 한 합니다.


2. 및에 해당 FOD 추가 하려는 로컬 네트워크에 연결 된 Server Core 컴퓨터에서 관리자 권한으로 로그인 합니다.

3. 사용 하 여 **사용 하 여 net**, 또는 해당 FOD ISO의 위치에 연결할 다른 방법입니다.

4. 선택한 로컬 폴더에는 해당 FOD ISO를 복사 합니다.

5. 입력 하 여 PowerShell 시작 **powershell.exe** 명령 프롬프트에서.

6. 다음 명령을 사용 하 여 해당 FoD ISO를 탑재 합니다.

        Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

7. 형식 **종료** PowerShell을 종료 합니다.

8.  다음 명령을 실행합니다.

        DISM /Online /Add-Capability /CapabilityName:"ServerCore.AppCompatibility~~~~0.0.1.0" /Source:drive_letter_of_mounted_ISO: /LimitAccess

9.  진행률 표시줄이 완료 되 면 운영 체제를 다시 시작 합니다.

### <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>필요에 따라 (Server Core 앱 호환성 FOD 추가) 후 Server Core에 Internet Explorer 11을 추가 하려면

 >[!NOTE]  
   > Server Core 앱 호환성 FOD Internet Explorer 11을 추가 하기 위해 필요 하지만 Internet Explorer 11 Server Core 앱 호환성 FOD 추가 하지 않아도 됩니다.

1.  이미 추가 앱 호환성 FOD 있는 Server Core 컴퓨터에 ISO 로컬로 복사 Server FOD 선택적 패키지 관리자 권한으로 로그인 합니다.

2.  입력 하 여 PowerShell 시작 **powershell.exe** 명령 프롬프트에서.

3.  다음 명령을 사용 하 여 해당 FoD ISO를 탑재 합니다.

         Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

4.  형식 **종료** PowerShell을 종료 합니다.


5.  다음 명령을 실행합니다.

        Dism /online /add-package:drive_letter_of_mounted_iso:"Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

6.  진행률 표시줄이 완료 되 면 운영 체제를 다시 시작 합니다.

 
#### <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>릴리스 정보 및 Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지에 대 한 제안

- **중요:** 나 문제, 고려 사항, 설치 및 Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지의 사용을 진행 하기 전에 지침에 대 한 Windows Server 2019 릴리스 정보를 참조 하세요.
 
 >[!NOTE] 
   > 누적 업데이트를 설치 하려면 Windows Update를 사용 하 여 앱 호환성 FOD를 추가할 때 Server Core의 콘솔 환경을 사용 하 여 깜박임 발생 하는 것이 가능 합니다.  2018 년 12 월을 사용 하 여이 문제를 해결 하는 업데이트 합니다.  자세한 정보 및 해결 단계를 참조 하세요. [4481610 기술 자료 문서: Windows Server 2019 Server Core에서 Server Core 앱 호환성 FOD를 설치한 후 화면이 깜박인다](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)합니다.

- 앱 호환성 FOD 및 서버를 재부팅을 설치한 후 콘솔 창 프레임 색상 명령을 다른 파란색 음영으로 변경 됩니다.

- 또한 Internet Explorer 11 선택적 패키지를 설치, 두 번 클릭 하 여 로컬로.htm 파일을 저장 하려는 경우 지원 되지 않습니다. 그러나 수 있습니다 **마우스 오른쪽 단추로 클릭** 선택한 **IE를 사용 하 여 엽니다**, 또는 Internet Explorer에서 직접 열 수 있습니다 **파일** -> **열기**. 

- 향상을 위해 앱 호환성 FOD를 사용 하 여 Server Core의 응용 프로그램 호환성, IIS 관리 콘솔에 Server Core에 선택적 구성 요소로 추가 되었습니다.  그러나 먼저 IIS 관리 콘솔을 사용 하는 앱 호환성 FOD를 추가 하는 데 반드시 필요한 것입니다. IIS 관리 콘솔 앱 호환성 FOD 추가 하 여 Server Core에 사용할 수만 있는 Microsoft Management Console (mmc.exe)에 의존 합니다.  Powershell을 사용 하 여 [ **Install-windowsfeature** ](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) IIS 관리 콘솔을 추가 합니다.

- 으로 일반 지침을 서버에 앱 설치 핵심 (유무와 관계 없이 이러한 선택적 패키지) 해당 하는 경우 지점 자동 설치 옵션 및 지침을 사용 하는 데 필요한 경우가 있습니다. 
    
 - 예를 들어 SQL Server 2016 및 SQL Server 2017에 대 한 SQL Server Management Studio Server Core에 설치할 수 있습니다 및 앱 호환성 FOD 존재 하는 경우에 완벽 하 게 작동 합니다.  하세요 [명령 프롬프트에서 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)합니다.
 - SQL Server Management Studio 원하지 않는 경우 다음이 아닌 경우 Server Core 앱 호환성 FOD를 설치 하는 데 필요한  하세요 [Server Core에 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)합니다.

