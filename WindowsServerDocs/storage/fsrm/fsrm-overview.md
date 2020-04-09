---
title: FSRM(파일 서버 리소스 관리자) 개요
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 5/14/2018
description: FSRM (파일 서버 리소스 관리자)은 Windows Server 파일 서버에서 데이터를 관리 및 분류 하는 데 사용할 수 있는 도구입니다.
ms.openlocfilehash: 0ed7e5abce9389283a9b9d641f813b5df89a586b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854246"
---
# <a name="file-server-resource-manager-fsrm-overview"></a>FSRM(파일 서버 리소스 관리자) 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (반기 채널), 

FSRM(파일 서버 리소스 관리자)는 파일 서버에 저장된 데이터를 관리 및 분류하는 데 사용할 수 있는 Windows Server의 역할 서비스입니다. 파일 서버 리소스 관리자를 사용 하 여 자동으로 파일을 분류 하 고, 이러한 분류에 따라 작업을 수행 하 고, 폴더의 할당량을 설정 하 고, 보고서를 모니터링 하는 저장소 사용량을

작은 지점 이지만 Windows Server 버전 1803에서 [변경 저널을 사용 하지 않도록 설정 하는 기능도 추가 되었습니다](#whats-new) .

## <a name="features"></a>기능

파일 서버 리소스 관리자에는 다음과 같은 기능이 포함되어 있습니다.

-   [할당량 관리](quota-management.md) 를 사용 하면 볼륨이 나 폴더에 허용 되는 공간을 제한할 수 있으며 볼륨에 생성 된 새 폴더에 자동으로 적용할 수 있습니다. 또한 새 볼륨이나 폴더에 적용 가능한 할당량 템플릿을 정의할 수도 있습니다.  
-   [파일 분류 인프라](classification-management.md) 는 데이터를 보다 효율적으로 관리할 수 있도록 분류 프로세스를 자동화 하 여 데이터에 대 한 통찰력을 제공 합니다. 이 분류를 기준으로 파일을 분류하고 정책을 적용할 수 있습니다. 예제 정책으로는 파일 액세스, 파일 암호화 및 파일 만료를 제한하는 동적 액세스 제어가 있습니다. 파일 분류 규칙을 사용하여 자동으로 또는 선택한 파일이나 폴더의 속성을 수정하여 수동으로 파일을 분류할 수 있습니다.
-   [파일 관리 작업](file-management-tasks.md) 을 사용 하면 분류에 따라 파일에 조건부 정책이 나 동작을 적용할 수 있습니다. 파일 관리 작업의 조건으로는 파일 위치, 분류 속성, 파일을 만든 날짜, 파일을 마지막으로 수정한 날짜 또는 파일에 마지막으로 액세스한 시간 등이 있습니다. 파일 관리 작업에서 수행할 수 있는 동작으로는 파일 만료, 암호화 또는 사용자 지정 명령 실행 등이 있습니다.
-   [파일 차단 관리](file-screening-management.md) 를 사용 하면 사용자가 파일 서버에 저장할 수 있는 파일 형식을 제어할 수 있습니다. 공유 파일에 저장 가능한 확장명을 제한할 수 있습니다. 예를 들면 확장명이 MP3인 파일을 파일 서버의 개인 공유 폴더에 저장하지 못하도록 하는 파일 차단을 만들 수 있습니다.
-   [저장소 보고서](storage-reports-management.md) 를 사용 하 여 디스크 사용 추세와 데이터 분류 방법을 파악할 수 있습니다. 선택한 사용자 그룹의 권한이 없는 파일을 저장하려는 시도를 모니터링할 수도 있습니다.  
  
파일 서버 리소스 관리자에 포함 된 기능은 파일 서버 리소스 관리자 앱을 사용 하거나 Windows PowerShell을 사용 하 여 구성 하 고 관리할 수 있습니다.
  
> [!IMPORTANT]
>  파일 서버 리소스 관리자는 NTFS 파일 시스템으로 포맷된 볼륨만 지원합니다. 복원 파일 시스템은 지원되지 않습니다.  
  
## <a name="practical-applications"></a>유용한 팁  
 파일 서버 리소스 관리자를 위한 몇 가지 유용한 팁이 아래 나와 있습니다.  
  
-   파일 분류 인프라를 동적 Access Control 시나리오와 함께 사용하여 파일 서버에서 파일을 분류하는 방식에 따라 파일 및 폴더 액세스 권한을 부여하는 정책을 만듭니다.  
  
-   주민 등록 번호가 10개 이상 포함된 파일을 개인 식별 가능한 정보가 담긴 파일로 태그를 지정하는 파일 분류 규칙을 만듭니다.  
  
-   지난 10년간 수정되지 않은 파일을 만료합니다.  
  
-   각 사용자의 홈 디렉터리에 대해 200 메가바이트의 할당량을 만들고 180 메가바이트를 사용 하는 경우 알립니다.  
  
-   개인 공유 폴더에 음악 파일을 저장하도록 허용하지 않습니다.  
  
-   매주 일요일 자정에 지난 이틀간 가장 많이 사용된 파일의 목록을 생성하는 보고서가 실행되도록 예약합니다. 이렇게 하면 주말의 스토리지 작업을 파악하여 서버 가동 중지 시간을 적절하게 계획할 수 있습니다.  

## <a name="whats-new---prevent-fsrm-from-creating-change-journals"></a><a name="whats-new"></a>새로운 기능-FSRM이 변경 저널을 만들 수 없도록 설정

Windows Server, 버전 1803부터, 서비스를 시작할 때 파일 서버 리소스 관리자 서비스에서 볼륨에 변경 저널 (USN 저널이 라고도 함)을 만들 수 없도록 할 수 있습니다. 이렇게 하면 각 볼륨에서 약간의 공간을 절약할 수 있지만 실시간 파일 분류는 사용 하지 않도록 설정 됩니다.

이전 버전의 새로운 기능에 대해서는 [파일 서버 리소스 관리자의 새로운](https://technet.microsoft.com/library/dn383587.aspx)기능을 참조 하세요.

서비스가 시작 될 때 파일 서버 리소스 관리자에서 일부 또는 모든 볼륨에 변경 저널을 만들지 않도록 하려면 다음 단계를 사용 합니다. 

1. SRMSVC 서비스를 중지 합니다. 예를 들어 관리자 권한으로 PowerShell 세션을 열고 `Stop-Service SrmSvc`를 입력 합니다.
2. Fsutil 명령을 사용 하 여 공간을 절약 하려는 볼륨의 USN 저널을 삭제 합니다. 

      ```
      fsutil usn deletejournal /d <VolumeName>
      ```
    예를 들면 다음과 같습니다. `fsutil usn deletejournal /d c:`

3. 예를 들어 동일한 PowerShell 세션에 `regedit`를 입력 하 여 레지스트리 편집기를 엽니다.
4. 다음 키로 이동 합니다. **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\srmsvc\settings**
5. 전체 서버에 대 한 변경 저널 만들기를 선택적으로 건너뛰려면 (특정 볼륨에 대해서만 사용 하지 않도록 설정 하려는 경우이 단계를 건너뜁니다.)
    1. **설정** 키를 마우스 오른쪽 단추로 클릭 한 다음 **새로 만들기** > **DWORD (32 비트) 값**을 선택 합니다. 
    1. 값 `SkipUSNCreationForSystem`의 이름을로 합니다.
    1. 값을 **1** (16 진수)로 설정 합니다.
6. 특정 볼륨에 대 한 변경 저널 만들기를 선택적으로 건너뛰려면:
    1. `fsutil volume list` 명령을 사용 하거나 다음 PowerShell 명령을 사용 하 여 건너 뛰 려는 볼륨 경로를 가져옵니다.
        ```PowerShell
        Get-Volume | Format-Table DriveLetter,FileSystemLabel,Path
        ```
       다음은 출력의 예입니다.

       ```
        DriveLetter FileSystemLabel Path
        ----------- --------------- ----
                    System Reserved \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        C                           \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
       ```
    2. 레지스트리 편집기로 돌아가서 **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\srmsvc\settings** 키를 마우스 오른쪽 단추로 클릭 한 다음 **새로 만들기** > **다중 문자열 값**을 선택 합니다.
    3. 값 `SkipUSNCreationForVolumes`의 이름을로 합니다.
    4. 변경 저널 생성을 건너뛰는 각 볼륨의 경로를 입력 하 여 각 경로를 별도의 줄에 배치 합니다. 예를 들면 다음과 같습니다.

        ```
        \\?\Volume{8d3c9e8a-0000-0000-0000-100000000000}\
        \\?\Volume{8d3c9e8a-0000-0000-0000-501f00000000}\
        ```

        > [!NOTE] 
        > 레지스트리 편집기에서 빈 문자열을 제거 하 여 안전 하 게 무시할 수 있다는 경고를 표시 하는 것을 알 수 있습니다. *REG_MULTI_SZ 형식의 데이터에 빈 문자열을 포함할 수 없습니다. 레지스트리 편집기는 발견 되는 빈 문자열을 모두 제거 합니다.*

7. SRMSVC 서비스를 시작 합니다. 예를 들어 PowerShell 세션에서 `Start-Service SrmSvc`를 입력 합니다.



## <a name="see-also"></a>참고 항목

- [동적 Access Control](https://technet.microsoft.com/library/dn408191(v=ws.11).aspx) 