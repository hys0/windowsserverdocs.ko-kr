---
title: "Windows Server 2016 도메인 컨트롤러 업그레이드"
description: "이 문서에서는 Windows Server 2016 Windows Server 2012 r 2에서 업그레이드 하는 방법에 설명"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 187972c2f44a4d7f91b1b3ac1c905529564cfa6d
ms.sourcegitcommit: f748c6c4ce700b0787ffdd1fca620c21c4331fd2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2017
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Windows Server 2016 도메인 컨트롤러 업그레이드

Windows Server 2016 적용 됩니다.

이 항목에서 Windows Server 2016 Active Directory 도메인 서비스에 대 한 배경 정보를 제공 하 고 Windows Server 2012 또는 Windows Server 2012 R2 도메인 컨트롤러 업그레이드 프로세스에 설명 합니다. 

## <a name="pre-requisites"></a>필수
최신 버전의 Windows Server를 실행 하 고 필요에 따라 이전 도메인 컨트롤러 내리기 하는 도메인 컨트롤러를 도메인 업그레이드 하는 권장된 방법은입니다. 이 방법은 기존 도메인 컨트롤러의 운영 체제를 업그레이드 하는 것이 좋습니다. 이 목록은 일반 단계에 따라 Windows Server의 최신 버전을 실행 하는 도메인 컨트롤러 홍보 하기 전에 다룹니다. 

1.  대상 서버가 시스템 요구 사항에 맞는지 확인 합니다. 
2.  응용 프로그램의 호환성을 확인 합니다. 
3.  Windows Server 2016으로 이동에 대 한 추천을 검토 
4.  보안 설정을 확인 합니다. 자세한 내용은 참조 [않음 기능과 동작 변경와 관련 Windows Server 2016에 AD DS](../../../get-started\deprecated-features.md)합니다. 
5.  설치를 실행 하려면 컴퓨터에서 대상 서버에 연결을 확인 합니다. 
6.  필요한 작업이 마스터 역할의 사용 가능 여부를 확인 합니다. 
    - 시스템 설치를 실행 하면 기존 도메인 및 숲 Windows Server 2016을 실행 하는 첫 번째 DC를 설치 하려면 연결성에 필요는 **스키마 마스터** adprep /domainprep 실행 하는 데 adprep /forestprep와 인프라 마스터 실행 해야 합니다. 
    - 첫 번째 DC 숲 스키마 이미 확장 된 도메인의를 설치 하려면 하기만 하면 infrastructure 마스터에 연결 됩니다. 
    - 에 대 한 연결을 설치 하거나 기존 숲 속의 도메인 제거 하려면 필요는 **도메인 이름 지정 마스터**합니다. 
    - 도메인 컨트롤러 설치 된 경우에 연결 해야는 **RID 마스터 합니다.** 
    - 기존 숲 속의 첫 번째 읽기 전용 도메인 컨트롤러를 설치 하는 경우 각 응용 디렉터리 파티션, 라고도 비 도메인 이름 상황에 맞는 또는 NDNC 인프라 마스터에 대 한 연결이 필요 합니다. 

### <a name="installation-steps-and-required-administrative-levels"></a>설치 단계와 필수 관리 수준을
다음 표에서 단계는 업그레이드 하 고 다음이 단계를 수행 하는 권한 요구 요약

|설치 알림|자격 증명 요구 사항|
| ----- | ----- |
|새 숲 설치|로컬 관리자 대상 서버에서|
|기존 숲 속의 새 도메인 설치|엔터프라이즈 관리|
|기존 도메인에 추가 DC 설치|도메인 관리|
|Adprep /forestprep 실행|스키마 관리, Enterprise 관리자 및 도메인 관리자|
|Adprep /domainprep 실행|도메인 관리|
|Adprep 하십시오를 실행합니다|도메인 관리|
|Adprep /rodcprep 실행|엔터프라이즈 관리|

Windows Server 2016의 새로운 기능에 대 한 자세한 내용은 참조 [Windows Server 2016의 새로운 기능](../../../get-started/what-s-new-in-windows-server-2016.md)합니다.



## <a name="supported-in-place-upgrade-paths"></a>지원 되는 업그레이드 경로 위치에서
Windows Server 2016에 64 비트 버전의 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 도메인 컨트롤러 업그레이드할 수 있습니다. 64 비트 버전의 Windows Server 2016만 제공 하기 때문에 64 비트 버전 업그레이드만 지원 됩니다.

|이 버전 실행 하는 경우|이러한 버전으로 업그레이드할 수 있습니다.|
| ----- | ----- |   
|Windows Server 2012 표준|Windows Server 2016 표준 또는 Datacenter|   
|Windows Server 2012 데이터 센터|Windows Server 2016 Datacenter| 
|Windows Server 2012 r 2 표준|Windows Server 2016 표준 또는 Datacenter|    
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|  
|Windows Server 2012 R2 Essentials|Windows Server 2016 필수 패키지|  
|Windows Storage Server 2012 표준|Windows Storage Server 2016 표준| 
|Windows Storage Server 2012 작업 그룹|Windows Storage Server 2016 작업 그룹|   
|Windows Storage Server 2012 r 2 표준|Windows Storage Server 2016 표준|  
|Windows Storage Server 2012 r 2 작업 그룹|Windows Storage Server 2016 작업 그룹|    

지원 되는 업그레이드 경로 대 한 자세한 내용은 참조 [업그레이드 경로 지원](../../../get-started/supported-upgrade-paths.md)

## <a name="adprep-and-domainprep"></a>Adprep 및 도메인 준비
Windows Server 2016 운영 체제에 기존 도메인 컨트롤러의 현재 위치에서 업그레이드를 수행 하는 경우 수동으로 adprep /forestprep 및 adprep /domainprep 실행 해야 합니다.  Adprep /forestprep 숲에서 한 번만 실행 해야 합니다.  Adprep /domainprep Windows Server 2016로 업그레이드 하는 도메인 컨트롤러 열어야 각 도메인에 한 번 실행 해야 합니다.

새로운 Windows Server 2016 서버를 홍보 하는 경우이 수동으로 실행할 필요는 없습니다.  PowerShell은에 통합 되어 이러한 및 서버 관리자 경험 합니다.

에 대 한 자세한 내용은 adprep 실행 [Adprep 실행](https://technet.microsoft.com/library/dd464018.aspx) 


## <a name="functional-level-features-and-requirements"></a>수준 기능 및 요구 사항
Windows Server 2016 Windows Server 2003 숲 기능 수준이 필요합니다. 즉, Windows Server 2016 기존 Active Directory 숲을 실행 하는 도메인 컨트롤러를 추가 하기 전에 숲 기능 수준 Windows Server 2003 이상 이어야 합니다. 숲 Windows Server 2003을 실행 하는 도메인 컨트롤러에 포함 된 경우 이상 기능 숲 있지만 수준은 Windows 2000 여전히, 설치도 차단 합니다. 

Windows Server 2016 도메인 컨트롤러에 숲에 추가 하기 전에 Windows 2000 도메인 컨트롤러를 제거 해야 합니다. 이 경우 다음 워크플로 고려 합니다. 


1. Windows Server 2003 이상을 실행 하는 도메인 컨트롤러를 설치 합니다. 이러한 도메인 컨트롤러의 Windows Server 평가판에 배포할 수 있습니다. 이 단계도 해당 운영 체제 릴리스에 대 한 adprep.exe 필수 실행 해야 합니다. 
2.  Windows 2000 도메인 컨트롤러를 제거 합니다. 특히, 정상적으로 내리기 또는 강제로 Windows 2000 Server 도메인 컨트롤러 도메인 하 고 사용 하는 Active Directory 사용자와 모든 제거 도메인 컨트롤러 도메인 컨트롤러 계정을 제거 하려면 컴퓨터에서 제거 합니다. 
3.  Windows Server 2003 이상 숲 기능 수준을 발생 합니다. 
4.  Windows Server 2016을 실행 하는 도메인 컨트롤러를 설치 합니다. 
5.  이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러를 제거 합니다. 

### <a name="rolling-back-functional-levels"></a>기능 수준 롤백하

숲 기능 수준을 (FFL) 특정 값을 설정한 후 롤백 하거나 구성원과 숲 기능 수준 낮추기 수 없습니다. 

- Windows Server 2012 r 2 FFL에서 업그레이드 하는 경우 Windows Server 2012 r 2에 다시을 줄일 수 있습니다. 
- Windows Server 2008 R2 FFL에서 업그레이드 하는 경우 Windows Server 2008 R2 다시을 줄일 수 있습니다.

도메인 기능 수준 특정 값을 설정한 후 롤백 하거나는 다음과 같은 차이점이 도메인 기능 수준 낮추기 수 없습니다. 

- Windows Server 2012 또는 Windows Server 2012 R2 도메인 기능 수준을 배포 하는 옵션이 다시 Windows Server 2016에 도메인 기능 수준을 발생 하 고 Windows Server 2012 또는 아래 숲 기능 수준을 경우합니다 

기능 하위 수준에서 사용할 수 있는 기능에 대 한 자세한 내용은 참조 [이해 Active Directory 도메인 서비스 (AD DS) 기능 수준](../active-directory-functional-levels.md)합니다. 
 
## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>광고 DS 상호 운용성 다른 서버 역할와 Windows 운영 체제
AD DS 다음 Windows 운영 체제에 사용할 수 없습니다. 


- Windows 다중 서버 
- Windows Server 2016 필수 패키지 

AD DS 또한 다음과 같은 서버 역할 나 역할 서비스를 실행 하는 서버에 설치할 수 없습니다. 

- Hyper-v 서버 2016 Microsoft
- 원격 데스크톱 연결 중개 업체 

## <a name="administration-of-windows-server-2016-servers"></a>Windows Server 2016 서버 관리
도메인 컨트롤러 및 Windows Server 2016을 실행 하는 다른 서버 관리 원격 서버 관리 도구에 대 한 Windows 10을 사용 합니다. Windows 10을 실행 하는 컴퓨터에서 Windows Server 2016 원격 서버 관리 도구를 실행할 수 있습니다. 

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Windows Server 2016로 업그레이드에 대 한 단계별
다음은 간단한 예로 Windows Server 2016에 Contoso 숲 Windows Server 2012 r 2에서 업그레이드 합니다.

![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1.  새로운 Windows Server 2016에 숲 가입 합니다. 메시지가 표시 되 면 다시 시작 합니다. 
![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)
2.  새로운 Windows Server 2016 도메인 관리자 계정으로 로그인 합니다.
3.  **서버 관리자**, **역할 추가 및 기능**, 설치 **Active Directory 도메인 서비스** 새로운 Windows Server 2016에 있습니다. Adprep 2012 r 2 숲 및 도메인에 자동으로 실행 됩니다.
![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png) 
4.  **서버 관리자**노란색 삼각형이 클릭 드롭다운 메뉴에서 **도메인 컨트롤러 서버 홍보**합니다. 
![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)
5.  에 **배포 구성** 화면에서 **도메인 컨트롤러 기존 숲에 추가** 다음을 클릭 합니다. 
![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)
6.  에 **도메인 컨트롤러 옵션** 화면에서 입력 하는 **DSRM 디렉터리 서비스 복원 모드 ()** 암호 및 클릭 다음 합니다. 
7.  클릭 하 고 화면이의 나머지 부분에 대 한 **다음**합니다. 
8.  에 **필수 확인** 화면에서 클릭 **설치**합니다. 다시 시작 하면 완료 되 면 수 기호 다시 끼웁니다.
9.  Windows Server 2012 R2 서버에서에 **서버 관리자**, 도구 선택 **Windows PowerShell에 대 한 Active Directory 모듈**합니다. 
![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)
10. PowerShell windows에서 이동 ADDirectoryServerOperationMasterRole FSMO 역할을 이동 하려면 사용 합니다. 각-OperationMasterRole의 이름을 입력 하거나 번호를 사용 하 여 역할 지정할 수 있습니다. 숫자 합니다. 자세한 내용은 참조 [ADDirectoryServerOperationMasterRole 이동](https://technet.microsoft.com/library/hh852302.aspx)

``` powershell
Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
```

![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)</br>
11. Windows Server 2016 서버에으로 이동 하 여 역할 이동 되었는지 확인 **서버 관리자**, **도구**선택 **Windows PowerShell에 대 한 Active Directory 모듈**합니다. 사용 하는 `Get-ADDomain` 및 `Get-ADForest` cmdlet FSMO 역할 소유자 볼 수 있습니다.
![업그레이드] (media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)
! [업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)
12. 내리기 및 Windows Server 2012 R2 도메인 컨트롤러를 제거 합니다. Dc 내리기에 내용은 [내리기 도메인 컨트롤러 및 도메인](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)
13. 서버 내리는 제거한 후 숲 기능 및 Windows Server 2016에 기능 수준 도메인을 발생 시킬 수 있습니다.


## <a name="next-steps"></a>다음 단계
-   [새로운 기능 Active Directory Domain Services 설치 및 제거](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)  
-   [설치 Active Directory 도메인 서비스 & #40; 수준을 100 & #41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)     
-   [Windows Server 2016 기능 수준](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
