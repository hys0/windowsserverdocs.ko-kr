---
title: MultiPoint 서버에서 서버 백업 설치
description: 백업 및 복구 도구를 설치 하는 단계를 안내
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4331370-ba07-4529-92ab-db14a41bfc3b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 51932c5f0796cfd757d3322e10c17de2a3081f4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832494"
---
# <a name="install-server-backup-on-your-multipoint-server"></a>MultiPoint 서버에서 서버 백업 설치
MultiPoint 서버에 대 한 백업 및 복구 계획을 고려 하는 것이 좋습니다.
  
적합 한 백업 및 복구 계획이 크기 환경에 중요 합니다. Windows Server Backup은 마법사 및 설치 된 서버에 대 한 기본 백업 및 복구 작업을 수행 하는 다른 도구 집합을 제공 하는 Windows Server 2016의 기능입니다. 백업을 사용 하 여 Windows Server 전체 서버 (모든 볼륨), 선택한 볼륨, 시스템 상태 또는 특정 파일 또는 폴더를 백업 하 고 시스템을 다시 작성 하는 데 사용할 수 있는 백업을 만들 수 있습니다.  
  
볼륨, 폴더, 파일, 특정 응용 프로그램 및 시스템 상태를 복구할 수 있습니다. 그리고 하드 디스크 오류 등, 재해에 대 한 시스템을 처음부터 만들거나 대체 하드웨어를 사용 하 여를 다시 작성할 수 있습니다. 이렇게 하려면 전체 서버 또는 운영 체제 파일과 Windows 복구 환경을 포함 하는 볼륨의 백업을 해야 합니다. 이렇게 하면 이전 시스템에 나 새 하드 디스크에 전체 시스템을 복원 합니다.  
  
Windows Server Backup의 키 기능은 자동으로 실행 되도록 백업을 예약 하는 기능입니다.  
  
필요한 백업 유형을 설정 하려면 다음 절차를 사용 합니다.  
  
## <a name="install-backup-and-recovery-tools"></a>백업 및 복구 도구 설치  
  
1.  **시작** 화면이 열리면서 **서버 관리자**합니다.  
  
2.  클릭 **역할 및 기능 추가** 역할 추가 마법사를 시작 합니다. 클릭 **다음** 검토 한 후 합니다 **시작 하기 전에** 정보입니다.  
  
3.  선택 된 **역할 기반 또는 기능 기반 설치** 옵션을 선택한 다음 클릭 **다음**합니다.  
  
4.  관리 하는를 클릭 하는 로컬 컴퓨터 선택 **다음**합니다.  
  
    추가 기능 마법사가 열립니다.  
  
5.  에 **기능 선택** 페이지, Windows Server 백업 기능을 확장 한 다음에 대 한 확인란을 선택 **Windows Server Backup** 하 고 **명령줄 도구**를 를클릭하고 **다음**합니다.  
  
    > [!NOTE]  
    > 확장 스냅인 및 Wbadmin 명령줄 도구를 설치 하려는 경우 또는 **Windows Server 백업 기능**를 선택한 후 합니다 **Windows Server Backup** 확인란만-했는지를 **명령줄 도구** 확인란이 선택 취소 되어 있습니다.  
  
6.  에 **설치 선택 확인** 페이지에서 선택 내용을 검토 하 고 클릭 **설치**합니다.  
  
    설치 하는 동안 오류가 발생 하는 경우는 **설치 결과** 페이지 오류를 확인 합니다.  
  
7.  설치가 성공적으로 완료 된 후에 이러한 백업 및 복구 도구에 액세스할 수 해야 합니다.  
  
    -   에 Windows Server Backup 스냅인을 열려면 합니다 **시작** 화면에서 입력 **백업**를 클릭 하 고 **Windows Server Backup** 결과에 합니다.  
  
    -   Wbadmin 도구를 시작한 명령 구문을 보려면: 에 **시작** 화면에서 입력 **명령**입니다. 결과에서 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 **관리자 권한으로 실행** 클릭 한 다음 확인 하 고 페이지 맨 아래에 **예** 확인 프롬프트에서. 명령 프롬프트에서 입력 **wbadmin /?** ENTER를 누릅니다. 명령 구문 및 도구에 대 한 설명을 표시 됩니다.  
  
## <a name="configure-backups-using-windows-server-backup"></a>Windows Server Backup을 사용 하 여 백업 구성  
  
-   지침을 따르세요 [서버 백업](https://technet.microsoft.com/library/cc753528.aspx)합니다. 