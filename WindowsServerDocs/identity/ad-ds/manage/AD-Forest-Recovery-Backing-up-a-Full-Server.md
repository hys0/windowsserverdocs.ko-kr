---
title: AD 포리스트 복구-전체 서버 백업
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 4377c1d993b4f6d30cf8ca8a7d149b741d7f8d2f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369365"
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD 포리스트 복구-전체 서버 백업  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

전체 서버 백업은 다른 하드웨어 또는 다른 운영 체제 인스턴스로 복원할 수 있으므로 포리스트 복구를 준비 하는 데 권장 됩니다.  Windows Server 백업 사용 하 여 서버의 전체 백업을 수행할 수 있습니다. 

## <a name="windows-server-backup"></a>Windows Server 백업

Windows Server 백업는 기본적으로 설치 되지 않습니다. Windows Server 2016 및 Windows Server 2012 r 2에서 다음 단계에 따라 설치 합니다.

>[!NOTE]
>이러한 단계는 Windows Server 2016 및 Windows Server 2012 R2 사이에서 약간 다를 수 있습니다.

Windows Server 2008 및 Windows Server 2008 r 2에 설치 하는 단계는 [Windows Server 백업 설치](https://technet.microsoft.com/library/cc771232.aspx)를 참조 하세요.  

### <a name="to-install-windows-server-backup"></a>Windows Server 백업를 설치 하려면

1. **서버 관리자** 열고 **역할 및 기능 추가**를 클릭 합니다.
2. **역할 및 기능 추가 마법사** 에서 **다음**을 클릭 합니다.
3. **설치 유형** 화면에서 기본 **역할 기반 또는 기능 기반 설치** 를 그대로 두고 **다음**을 클릭 합니다.
4. **서버 선택** 화면에서 **다음**을 클릭 합니다.
5. **서버 역할** 화면에서 **다음**을 클릭 합니다.
6. **기능** 화면에서 **Windows Server 백업** 를 선택 하 고 **다음**
    @ no__t-4install Backup @ no__t-5를 클릭 합니다.
7. **설치**를 클릭합니다.
8. 설치가 완료 되 면 **닫기**를 클릭 합니다.

### <a name="to-perform-a-backup-with-windows-server-backup"></a>Windows Server 백업를 사용 하 여 백업을 수행 하려면

1. **서버 관리자**열고 **도구**를 클릭 한 다음 **Windows Server 백업**를 클릭 합니다.
   - Windows Server 2008 R2 및 Windows Server 2008에서 **시작**을 클릭 하 고 **관리 도구**를 가리킨 다음 **Windows Server 백업**를 클릭 합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 

2. 메시지가 표시 되 면 **사용자 계정 컨트롤** 대화 상자에서 백업 운영자 자격 증명을 입력 한 다음 **확인**을 클릭 합니다.
3. **로컬 백업**을 클릭 합니다.
4. **동작** 메뉴에서 **한 번 백업**을 클릭합니다.
5. 한 번 백업 마법사의 **백업 옵션** 페이지에서 **다른 옵션**을 클릭 한 후 **다음**을 클릭 합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. **백업 구성 선택** 페이지에서 **전체 서버 (권장)** 를 클릭 하 고 **다음**을 클릭 합니다.
7. **대상 유형 지정** 페이지에서 **로컬 드라이브** 또는 **원격 공유 폴더**를 클릭 한 후 **다음**을 클릭 합니다.
8. **백업 대상 선택** 페이지에서 백업 위치를 선택 합니다.  로컬 드라이브를 선택 하 여 로컬 드라이브를 선택 하거나 원격 공유를 선택한 경우 네트워크 공유를 선택 합니다.
9. 확인 화면에서 **백업**을 클릭 합니다.

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)

10. 이 작업이 완료 되 면 **닫기**를 클릭 합니다.
11. Windows Server 백업를 닫습니다.

>[!NOTE]
>백업 저장소 위치를 사용할 수 없다는 오류 메시지가 표시 되 면 선택한 볼륨 중 하나를 제외 하거나 새 볼륨 또는 원격 공유를 추가 해야 합니다.
>선택한 볼륨이 백업할 항목 목록에도 포함 되어 있음을 알리는 경고가 표시 되 면를 제거할지 여부를 결정 하 고 **확인**을 클릭 합니다.

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Wbadmin를 사용 하 여 windows server 백업

Wbadmin은 명령 프롬프트에서 운영 체제, 볼륨, 파일, 폴더 및 응용 프로그램을 백업 하 고 복원 하는 데 사용할 수 있는 명령줄 유틸리티입니다.

### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Wbadmin을 사용 하 여 전체 서버 백업을 수행 하려면
  
- 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   ```
   wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:
   ```

   ![백업 설치](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
