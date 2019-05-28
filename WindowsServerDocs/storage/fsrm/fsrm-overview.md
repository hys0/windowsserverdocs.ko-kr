---
title: FSRM(파일 서버 리소스 관리자) 개요
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 5/14/2018
description: FSRM (파일 서버 리소스 관리자)는 Windows Server 파일 서버에 데이터를 관리 및 분류할 수 있는 도구입니다.
ms.openlocfilehash: 8488c7418ac03be53db7164678fad353bc7c637d
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476133"
---
# <a name="file-server-resource-manager-fsrm-overview"></a>FSRM(파일 서버 리소스 관리자) 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (반기 채널) 

FSRM(파일 서버 리소스 관리자)는 파일 서버에 저장된 데이터를 관리 및 분류하는 데 사용할 수 있는 Windows Server의 역할 서비스입니다. 자동으로 파일을 분류, 이러한 분류에 따라 작업 수행, 폴더에 할당량을 설정 및 저장소 사용량을 모니터링 하는 보고서를 만들 파일 서버 리소스 관리자를 사용할 수 있습니다.

이기도 작은 지점을 뿐만 [변경 저널을 사용 하지 않도록 설정 하는 기능을 추가](#whats-new) Windows Server, 버전 1803에서에서.

## <a name="features"></a>기능

파일 서버 리소스 관리자에는 다음과 같은 기능이 포함되어 있습니다.

-   [할당량 관리](quota-management.md) 볼륨이 나 폴더에 허용 되는 공간을 제한할 수 있으며 볼륨에 만들어진 새 폴더에 자동으로 적용 합니다. 또한 새 볼륨이나 폴더에 적용 가능한 할당량 템플릿을 정의할 수도 있습니다.  
-   [파일 분류 인프라](classification-management.md) 데이터를 보다 효과적으로 관리할 수 있도록 분류 프로세스를 자동화 함으로써 데이터에 대 한 정보를 제공 합니다. 이 분류를 기준으로 파일을 분류하고 정책을 적용할 수 있습니다. 예제 정책으로는 파일 액세스, 파일 암호화 및 파일 만료를 제한하는 동적 액세스 제어가 있습니다. 파일 분류 규칙을 사용하여 자동으로 또는 선택한 파일이나 폴더의 속성을 수정하여 수동으로 파일을 분류할 수 있습니다.
-   [파일 관리 작업](file-management-tasks.md) 분류에 따라 파일에 조건부 정책이 나 동작을 적용할 수 있습니다. 파일 관리 작업의 조건으로는 파일 위치, 분류 속성, 파일을 만든 날짜, 파일을 마지막으로 수정한 날짜 또는 파일에 마지막으로 액세스한 시간 등이 있습니다. 파일 관리 작업에서 수행할 수 있는 동작으로는 파일 만료, 암호화 또는 사용자 지정 명령 실행 등이 있습니다.
-   [파일 차단 관리](file-screening-management.md) 파일 형식을 제어 하는 데 도움이 됩니다. 해당 사용자는 파일 서버에 저장할 수 있습니다. 공유 파일에 저장 가능한 확장명을 제한할 수 있습니다. 예를 들면 확장명이 MP3인 파일을 파일 서버의 개인 공유 폴더에 저장하지 못하도록 하는 파일 차단을 만들 수 있습니다.
-   [저장소 보고서](storage-reports-management.md) 디스크 사용 추세와 데이터를 분류 하는 방법을 쉽게 식별할 수 있도록 합니다. 선택한 사용자 그룹의 권한이 없는 파일을 저장하려는 시도를 모니터링할 수도 있습니다.  
  
파일 서버 리소스 관리자를 사용 하 여 포함 된 기능 구성 및 파일 서버 리소스 관리자 앱을 사용 하거나 Windows PowerShell을 사용 하 여 관리할 수 있습니다.
  
> [!IMPORTANT]
>  파일 서버 리소스 관리자는 NTFS 파일 시스템으로 포맷된 볼륨만 지원합니다. 복원 파일 시스템은 지원되지 않습니다.  
  
## <a name="practical-applications"></a>유용한 팁  
 파일 서버 리소스 관리자를 위한 몇 가지 유용한 팁이 아래 나와 있습니다.  
  
-   파일 분류 인프라를 동적 Access Control 시나리오와 함께 사용하여 파일 서버에서 파일을 분류하는 방식에 따라 파일 및 폴더 액세스 권한을 부여하는 정책을 만듭니다.  
  
-   주민 등록 번호가 10개 이상 포함된 파일을 개인 식별 가능한 정보가 담긴 파일로 태그를 지정하는 파일 분류 규칙을 만듭니다.  
  
-   지난 10년간 수정되지 않은 파일을 만료합니다.  
  
-   각 사용자의 홈 디렉터리에 200MB의 할당량을 만든 다음 180MB가 사용되면 할당량을 수정합니다.  
  
-   개인 공유 폴더에 음악 파일을 저장하도록 허용하지 않습니다.  
  
-   매주 일요일 자정에 지난 이틀간 가장 많이 사용된 파일의 목록을 생성하는 보고서가 실행되도록 예약합니다. 이렇게 하면 주말의 저장소 작업을 파악하여 서버 가동 중지 시간을 적절하게 계획할 수 있습니다.  

## <a name="whats-new"></a>새로운 기능-FSRM 변경 저널을 만들지 못하게 방지

Windows Server, 버전 1803에서부터 서비스가 시작 될 때 볼륨에 변경 저널 (USN 저널 라고도 함)를 만들기에서 파일 서버 리소스 관리자 서비스를 이제 방지할 수 있습니다. 이 약간의 각 볼륨에서 공간을 절약할 수 있지만 실시간 파일 분류 사용 하지 않도록 설정 됩니다.

오래 된 새 기능에 대 한 참조 [What's New 파일 서버 리소스 관리자에서](https://technet.microsoft.com/library/dn383587.aspx)합니다.

파일 서버 리소스 관리자에서 서비스를 시작할 때 변경 저널을 일부 또는 모든 볼륨 만들기를 방지 하려면 다음 단계를 사용 합니다. 

1. SRMSVC 서비스를 중지 합니다. 예를 들어, 관리자 권한으로 PowerShell 세션을 열려면 enter `Stop-Service SrmSvc`합니다.
2. Fsutil 명령을 사용 하 여 공간을 절약 하려는 볼륨에 대 한 USN 저널을 삭제 합니다. 

      ```
      fsutil usn deletejournal /d <VolumeName>
      ```
    예: `fsutil usn deletejournal /d c:`

3. 예를 들어, 입력 하 여 레지스트리 편집기를 엽니다 `regedit` 동일한 PowerShell 세션에서.
4. 다음 키로 이동 합니다. **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SrmSvc\Settings**
5. 필요에 따라 건너뛰기 변경 저널 생성 전체 서버의 특정 볼륨 에서만 사용 하지 않도록 설정 하려는 경우에이 단계를 건너 뛰 세요.
    1. 마우스 오른쪽 단추로 클릭 합니다 **설정을** 키를 선택 합니다 **새로 만들기** > **DWORD (32 비트) 값**합니다. 
    1. 값의 이름을 `SkipUSNCreationForSystem`입니다.
    1. 값을 설정 합니다 **1** (에서 16 진수).
6. 필요에 따라 특정 볼륨에 대 한 변경 저널 만들기를 건너뛸:
    1. 사용 하 여 건너 뛰 려 볼륨 경로 가져오기는 `fsutil volume list` 명령 또는 다음 PowerShell 명령을:
        ```PowerShell
        Get-Volume | Format-Table DriveLetter,FileSystemLabel,Path
        ```
       출력 예는 다음과 같습니다.

       ```
        DriveLetter FileSystemLabel Path
        ----------- --------------- ----
                    System Reserved \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        C                           \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
       ```
    2. 다시 레지스트리 편집기에서 마우스 오른쪽 단추로 클릭 합니다 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SrmSvc\Settings** 키를 선택 합니다 **새로 만들기** > **다중 문자열 값**합니다.
    3. 값의 이름을 `SkipUSNCreationForVolumes`입니다.
    4. 각 볼륨의 수 만들기를 건너뛸 변경 저널에 별도 줄에 각 경로 배치 하면 경로 입력 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

        ```
        \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
        ```

        > [!NOTE] 
        > 레지스트리 편집기를 확인할 수 있습니다 빈 문자열을 제거 하는 무시 해도 안전이 경고를 표시 합니다. *데이터 형식 reg_multi_sz와의 빈 문자열을 포함할 수 없습니다. 레지스트리 편집기 찾은 빈 문자열을 제거 합니다.*

7. SRMSVC 서비스를 시작 합니다. 예를 들어 PowerShell 세션에서 입력 `Start-Service SrmSvc`합니다.



## <a name="see-also"></a>참조

- [동적 액세스 제어](https://technet.microsoft.com/library/dn408191(v=ws.11).aspx) 