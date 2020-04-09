---
title: MultiPoint server에 서버 백업 설치
description: 백업 및 복구 도구를 설치 하는 단계를 안내 합니다.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: e4331370-ba07-4529-92ab-db14a41bfc3b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: f8fe5ac8b57105d421af431b12c8dc17250b622d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820336"
---
# <a name="install-server-backup-on-your-multipoint-server"></a>MultiPoint server에 서버 백업 설치
MultiPoint server에 대 한 백업 및 복구 계획을 고려 하는 것이 좋습니다.
  
적절 한 백업 및 복구 계획은 모든 규모 환경에서 중요 합니다. Windows Server 백업는 설치 된 서버에 대 한 기본 백업 및 복구 작업을 수행할 수 있는 마법사 및 기타 도구 집합을 제공 하는 Windows Server 2016의 기능입니다. Windows Server 백업를 사용 하 여 전체 서버 (모든 볼륨), 선택한 볼륨, 시스템 상태 또는 특정 파일이 나 폴더를 백업 하 고 시스템을 다시 작성 하는 데 사용할 수 있는 백업을 만들 수 있습니다.  
  
볼륨, 폴더, 파일, 특정 애플리케이션 및 시스템 상태를 복구할 수 있습니다. 그리고 하드 디스크 오류와 같은 재해의 경우 시스템을 처음부터 다시 작성 하거나 대체 하드웨어를 사용 하 여 다시 작성할 수 있습니다. 이렇게 하려면 전체 서버의 백업이 나 운영 체제 파일이 포함 된 볼륨과 Windows 복구 환경이 있어야 합니다. 그러면 전체 시스템이 기존 시스템이 나 새 하드 디스크로 복원 됩니다.  
  
Windows Server 백업의 핵심 기능은 자동으로 실행 되도록 백업 일정을 예약 하는 기능입니다.  
  
필요한 백업 유형을 설정 하려면 다음 절차를 따르십시오.  
  
## <a name="install-backup-and-recovery-tools"></a>백업 및 복구 도구 설치  
  
1.  **시작** 화면에서 **서버 관리자**를 엽니다.  
  
2.  **역할 및 기능 추가** 를 클릭 하 여 역할 추가 마법사를 시작 합니다. 그런 다음 메모를 **시작 하기 전에** 를 검토 한 후 **다음** 을 클릭 합니다.  
  
3.  **역할 기반 또는 기능 기반 설치** 옵션을 선택 하 고 **다음**을 클릭 합니다.  
  
4.  관리 중인 로컬 컴퓨터를 선택 하 고 **다음**을 클릭 합니다.  
  
    추가 기능 마법사가 열립니다.  
  
5.  **기능 선택** 페이지에서 Windows Server 백업 기능을 확장 하 고 **Windows Server 백업** 및 **명령줄 도구**에 대 한 확인란을 선택한 후 **다음**을 클릭 합니다.  
  
    > [!NOTE]  
    > 또는 스냅인과 Wbadmin 명령줄 도구를 설치 하려는 경우 **Windows Server 백업 기능**을 확장 한 다음 **Windows Server 백업** 확인란만 선택 합니다. **명령줄 도구** 확인란이 선택 취소 되어 있는지 확인 합니다.  
  
6.  **설치 선택 확인** 페이지에서 선택 사항을 검토 한 다음 **설치**를 클릭 합니다.  
  
    설치 하는 동안 오류가 발생 하는 경우 **설치 결과** 페이지에서 오류를 기록 합니다.  
  
7.  설치가 성공적으로 완료 되 면 다음 백업 및 복구 도구에 액세스할 수 있습니다.  
  
    -   Windows Server 백업 스냅인을 열려면 **시작** 화면에서 **Backup**을 입력 한 다음 결과에서 **Windows Server 백업** 를 클릭 합니다.  
  
    -   Wbadmin 도구를 시작 하 고 명령에 대 한 구문을 보려면 **시작** 화면에서 **command**를 입력 합니다. 결과에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 하 고 페이지 맨 아래에서 **관리자 권한으로 실행** 을 클릭 한 다음 확인 메시지가 **나타나면 예** 를 클릭 합니다. 명령 프롬프트에 **wbadmin/?** 를 입력 합니다. ENTER 키를 누릅니다. 도구에 대 한 명령 구문 및 설명이 표시 됩니다.  
  
## <a name="configure-backups-using-windows-server-backup"></a>Windows Server 백업를 사용 하 여 백업 구성  
  
-   [서버 백업](https://technet.microsoft.com/library/cc753528.aspx)의 지침을 따릅니다. 