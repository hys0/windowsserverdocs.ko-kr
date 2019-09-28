---
title: Hyper-v VHD 세트 파일 만들기
description: Hyper-v 2016에 VHDset 파일을 만드는 단계
author: jiwool
ms.author: jiwool
manager: senthilr
ms.date: 01/26/2017
ms.topic: article
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.assetid: 444e1496-9e5a-41cf-bfbc-306e2ed8e00a
audience: IT Pros
ms.reviewer: kathydav
ms.openlocfilehash: f5c9b932cabfea8df55ba8622165bbb04b4a4113
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392724"
---
# <a name="create-hyper-v-vhd-set-files"></a>Hyper-v VHD 세트 파일 만들기
VHD 세트 파일은 Windows Server 2016의 게스트 클러스터에 대 한 새로운 공유 가상 디스크 모델입니다. VHD 세트 파일은 공유 가상 디스크의 온라인 크기 조정을 지원 하 고 Hyper-v 복제본을 지원 하며 응용 프로그램 일치 검사점에 포함 될 수 있습니다. 

VHD 세트 파일은 새 VHD 파일 유형인를 사용 합니다. Vhd. VHD 세트 파일은 게스트 클러스터에서 사용 되는 그룹 가상 디스크에 대 한 검사점 정보를 메타 데이터 형식으로 저장 합니다.

Hyper-v는 검사점 체인을 관리 하 고 공유 VHD 집합을 병합 하는 모든 측면을 처리 합니다. 관리 소프트웨어는에서 수행 하는 것과 같은 방식으로 VHD 세트 파일의 온라인 크기 조정과 같은 디스크 작업을 실행할 수 있습니다. VHDX 파일. 즉, 관리 소프트웨어에서 VHD 세트 파일 형식을 알 필요가 없습니다.

## <a name="create-a-vhd-set-file-from-hyper-v-manager"></a>Hyper-v 관리자에서 VHD 세트 파일 만들기

1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.
2.  작업 창에서 **새로 만들기**를 클릭 한 다음 **하드 디스크**를 클릭 합니다.
3.  **디스크 형식 선택** 페이지에서 VHD를 가상 하드 디스크의 형식으로 **설정** 을 선택 합니다.
4.  마법사의 페이지를 계속 진행 하 여 가상 하드 디스크를 사용자 지정 합니다. **다음** 을 클릭 하 여 마법사의 각 페이지를 이동 하거나 왼쪽 창에서 페이지의 이름을 클릭 하 여 해당 페이지로 직접 이동할 수 있습니다.
5.  가상 하드 디스크 구성을 완료 한 후 **마침**을 클릭 합니다.

## <a name="create-a-vhd-set-file-from-windows-powershell"></a>Windows PowerShell에서 VHD 세트 파일 만들기

파일 형식과 함께 [새 VHD](https://technet.microsoft.com/library/hh848503.aspx) cmdlet을 사용 합니다. 파일 경로에 있는 VHD입니다. 이 예제에서는 크기가 10 기가바이트 인 VHD 집합 파일을 만듭니다.

``` PowerShell
PS c:\>New-VHD -Path c:\base.vhds -SizeBytes 10GB
```

## <a name="migrate-a-shared-vhdx-file-to-a-vhd-set-file"></a>공유 VHDX 파일을 VHD 세트 파일로 마이그레이션

기존 공유 VHDX를 VHD로 마이그레이션하려면 VM을 오프 라인으로 전환 해야 합니다. Windows PowerShell을 사용 하 여 권장 되는 프로세스입니다.

1. VM에서 VHDX를 제거 합니다. 예를 들어 다음을 실행 합니다. 
   ``` PowerShell
   PS c:\>Remove-VMHardDiskDrive existing.vhdx
   ```
  
2. VHDX를 VHD로 변환 합니다. 예를 들어 다음을 실행 합니다.
   ``` PowerShell
   PS c:\>Convert-VHD existing.vhdx new.vhds
   ```
  
3. VM에 VHD를 추가 합니다. 예를 들어 다음을 실행 합니다.
   ``` PowerShell
   PS c:\>Add-VMHardDiskDrive new.vhds
   ```
  



