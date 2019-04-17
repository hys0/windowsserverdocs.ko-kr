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
ms.sourcegitcommit: dbb4738fdac3b7911952ff11f1eaed9649d6567a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "9149903"
---
# Server Core 앱 호환성 FOD(Feature on Demand)

> Windows Server 2019 및 Windows Server, 버전 1809에 적용 됩니다.

**Server Core 앱 호환성 Feature on Demand는** Windows Server 2019 Server Core 설치 또는 Windows Server, 버전 1809, 언제 든 지 추가할 수 있는 선택적 기능 패키지입니다.

On Demand (FOD) 기능에 대 한 자세한 내용은 [주문형 기능을](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)참조 하세요.


## 앱 호환성 FOD를 설치 하는 이유 

앱 호환성, Server Core에 대 한 주문형 기능 추가 하지 않고 이진 파일 및 데스크톱 환경 포함 Windows Server에서 패키지의 하위 집합을 포함 하 여 Windows Server Core 설치 옵션의 응용 프로그램 호환성을 크게 향상 합니다 Windows Server 데스크톱 환경 그래픽 환경입니다. 이 선택적 패키지를 Windows 업데이트 또는 별도 ISO에서 사용할 수 있지만 Windows Server Core 설치와 이미지에 추가할 수 있습니다.

앱 호환성 FOD 제공 두 가지 기본 값은.

1.  Server Core의 지역/국가에 이미 있는 또는 이미 조직에서 개발 되어 배포 하는 서버 응용 프로그램에 대 한 호환성을 높입니다.

2.  OS 구성 요소 및 소프트웨어 도구의 예 문제 해결 및 디버깅 시나리오에 사용 되는 향상 된 응용 프로그램 호환성을 제공 하는 데 도움이 됩니다.

Server Core 앱 호환성 FOD의 일환으로 사용할 수 있는 운영 체제 구성 요소:

-   Microsoft Management Console (mmc.exe)

-   이벤트 뷰어 (Eventvwr.msc)

-   성능 모니터 (PerfMon.exe)

-   리소스 모니터 (Resmon.exe)

-   장치 관리자 (Devmgmt.msc)

-   파일 탐색기 (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   디스크 관리 (Diskmgmt.msc)

-   장애 조치 클러스터 관리자 (CluAdmin.msc)

    -   먼저 장애 조치 클러스터링 Windows Server 기능 추가 해야합니다.

        -   Powershell Cmdlet을 사용 하 여를 추가 하려면 `Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools`

        -   장애 조치 클러스터 관리자를 실행 하려면 **cluadmin** 명령 프롬프트를 입력 합니다.

## 앱 호환성 FOD 설치

 >[!IMPORTANT] 
   >앱 호환성 FOD Server Core에만 설치할 수 있습니다. Server Core 앱 호환성 FOD 데스크톱 환경 포함 Windows Server의 Windows Server 설치에 추가 하지 마세요.

### Server Core의 실행 중인 인스턴스를 demand (FOD)에서 Server Core 앱 호환성 기능을 추가 하려면

 >[!NOTE] 
   > 이 절차는 배포 이미지 서비스 및 관리 (DISM.exe) 명령줄 도구를 사용합니다. DISM 명령에 대 한 자세한 내용은 [DISM 기능 패키지 서비스 명령줄 옵션](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-capabilities-package-servicing-command-line-options)을 참조 하세요.

>[!NOTE] 
   > Windows Server 2019 Server Core 설치 또는 Windows Server, 버전 1809, 설치에 대 한 동일한 FOD 선택적 패키지 ISO를 사용할 수 있습니다.

>[!NOTE] 
   > 컴퓨터 또는 Server Core를 실행 하는 가상 컴퓨터를 Windows 업데이트에 연결할 경우 아래 1-7 단계를 건너뛸 수 있습니다. 하지만 8 단계에서 DISM 명령에서 명령을 및 /LimitAccess 되도록 하십시오.

1. 서버 FOD 선택적 패키지 ISO를 다운로드 하 고 ISO 로컬 네트워크에서 공유 폴더에 복사 합니다.

 - 볼륨 라이선스를가지고 있는 경우 OS ISO 이미지 파일을 획득 하는 동일한 포털에서 서버 FOD ISO 이미지 파일을 다운로드할 수 있습니다: [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
 - 서버 FOD ISO 이미지 파일 구독자는 [Visual Studio 포털](https://visualstudio.microsoft.com) 또는 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 에서 사용할 수도 있습니다.


2. Server Core 및 FOD를 추가 하려면 로컬 네트워크에 연결 되어 있는 컴퓨터에서 관리자 권한으로 로그인 합니다.

3. **순 사용**또는 다른 방법을 사용 하 여 FOD ISO의 위치에 연결 합니다.

4. FOD ISO 사용자가 선택한 로컬 폴더에 복사 합니다.

5. 명령 프롬프트에서 **powershell.exe** 입력 하 여 PowerShell을 시작 합니다.

6. 다음 명령을 사용 하 여 FoD ISO를 탑재 합니다.

        Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

7. PowerShell을 종료 하려면 **종료** 를 입력 합니다.

8.  다음 명령을 실행합니다.

        DISM /Online /Add-Capability /CapabilityName:"ServerCore.AppCompatibility~~~~0.0.1.0" /Source:drive_letter_of_mounted_ISO: /LimitAccess

9.  진행률 표시줄이 완료 되 면 운영 체제를 다시 시작 합니다.

### 필요에 따라 (Server Core 앱 호환성 FOD 추가) 후 Internet Explorer 11 Server Core에 추가 하려면

 >[!NOTE]  
   > Server Core 앱 호환성 FOD Internet Explorer 11을 추가 하기 위해 필요 하지만 Internet Explorer 11 Server Core 앱 호환성 FOD 추가할 필요 하지 않습니다.

1.  Server Core 컴퓨터에 이미 추가 앱 호환성 FOD 및 ISO 로컬로 복사 서버 FOD 선택적 패키지에서 관리자 권한으로 로그인 합니다.

2.  명령 프롬프트에서 **powershell.exe** 입력 하 여 PowerShell을 시작 합니다.

3.  다음 명령을 사용 하 여 FoD ISO를 탑재 합니다.

         Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

4.  PowerShell을 종료 하려면 **종료** 를 입력 합니다.


5.  다음 명령을 실행합니다.

        Dism /online /add-package:drive_letter_of_mounted_iso:"Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

6.  진행률 표시줄이 완료 되 면 운영 체제를 다시 시작 합니다.

 
#### 릴리스 정보 및 Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지에 대 한 제안

- **중요:** 문제, 고려 사항, 또는 Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지의 설치 및 사용을 진행 하기 전에 지침에 대 한 Windows Server 2019 릴리스 정보를 참조 하십시오.
 
 >[!NOTE] 
   > 것이 누적 업데이트를 설치 하려면 Windows 업데이트를 사용한 후 앱 호환성 FOD를 추가 하는 경우 Server Core 콘솔 경험이 깜박임 발생할 수 있습니다.  업데이트 2018 년 12 월을 사용 하 여이 문제를 해결 합니다.  자세한 정보 및 확인 단계에 대 한 참조 [기술 자료 문서 4481610: 화면 깜박임 Server Core 앱 호환성 FOD에서 Windows Server 2019 Server Core 설치](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core).

- 앱 호환성 FOD 및 서버를 다시 부팅의 설치 후 명령 콘솔 창 프레임 색 파란색의 다른 음영으로 변경 됩니다.

- 또한 Internet Explorer 11 선택적 패키지를 설치, 로컬로 열을 두 번 클릭 하면.htm 파일을 저장 하도록 선택 하면 지원 되지 않습니다. **하지만 마우스 오른쪽 단추로 클릭** 수 및 **IE를 사용 하 여 열기**를 선택 하거나 Internet Explorer **파일**에서 직접 열 수 있습니다 -> **를 엽니다**. 

- 앱 호환성 FOD의 Server Core 앱 호환성을 강화 하는 IIS 관리 콘솔에 Server Core에 선택적 구성 요소로 추가 되었습니다.  하지만 앱 호환성 FOD IIS 관리 콘솔을 사용 하려면 먼저 추가 하는 데 반드시 필요한 것입니다. IIS 관리 콘솔은만 Server Core 앱 호환성 FOD의 Microsoft Management Console (mmc.exe)에 의존 합니다.  Powershell [**WindowsFeature 설치를**](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) 사용 하 여 IIS 관리 콘솔을 추가 합니다.

- 때 서버에서 설치 앱 코어 (있거나 없는 이러한 선택적 패키지)이 가이드의 일반적인 지점은 자동 설치 옵션 및 지침을 사용 하는 데 필요한 경우가 있습니다. 
    
 - 예를 들어 SQL Server 2016 및 SQL Server 2017 SQL Server Management Studio Server Core에 설치할 수 있으며 앱 호환성 FOD가 있는 경우이 제대로 작동 합니다.  [명령 프롬프트에서 SQL Server를 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)를 참조 합니다.
 - SQL Server Management Studio 원하지 않는 경우 다음 필요 없는 Server Core 앱 호환성 FOD 설치 합니다.  [Server Core에서 SQL Server를 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)를 참조 합니다.

