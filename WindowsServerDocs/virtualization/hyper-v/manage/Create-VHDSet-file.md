---
title: Hyper-v VHD 설정 파일 만들기
description: 하이퍼-v 2016 VHDset 파일을 만드는 단계
author: jiwool
ms.author: jiwool
manager: senthilr
ms.date: 01/26/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: compute-hyper-v
ms.assetid: 444e1496-9e5a-41cf-bfbc-306e2ed8e00a
audience: IT Pros
ms.reviewer: kathydav
ms.openlocfilehash: a5a6f79d362b9058ca29d979457a1dcdfc0c9f82
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445694"
---
# <a name="create-hyper-v-vhd-set-files"></a>Hyper-v VHD 설정 파일 만들기
VHD 설정 파일에는 Windows Server 2016에서 게스트 클러스터에 대 한 새 공유 가상 디스크 모델은입니다. VHD 설정 파일 공유 가상 디스크의 온라인 크기 조정 지원 Hyper-v 복제본을 지원 하며 응용 프로그램 일치 검사점에서 포함 될 수 있습니다. 

VHD 설정 파일에는 새 VHD 파일 형식을 사용합니다. VHD입니다. VHD 설정 파일의 메타 데이터 형태로 게스트 클러스터에 사용 되는 그룹 가상 디스크에 대 한 검사점 정보를 저장 합니다.

Hyper-v가 검사점 체인을 관리 하는 모든 측면을 처리 하 고 설정 공유 VHD를 병합 합니다. 관리 소프트웨어에 적용 되는 동일한 방식으로 설정 하는 VHD 파일의 온라인 크기 조정 등의 디스크 작업을 실행할 수 있습니다. VHDX 파일입니다. 즉, 관리 소프트웨어를 설정 하는 VHD 파일 형식에 대 한 알 필요가 없습니다.

## <a name="create-a-vhd-set-file-from-hyper-v-manager"></a>Hyper-v 관리자에서 VHD 설정 파일 만들기

1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.
2.  작업 창에서 클릭 **새로 만들기**를 클릭 하 고 **하드 디스크**합니다.
3.  에 **디스크 형식 선택** 페이지에서 **VHD 설정** 가상 하드 디스크의 형식으로 합니다.
4.  가상 하드 디스크를 사용자 지정 마법사 페이지를 계속 진행 합니다. 클릭할 수 **다음** 마법사의 각 페이지를 통해 이동 하려면 해당 페이지로 직접 이동 하려면 왼쪽된 창에서 페이지의 이름을 클릭 수 있습니다.
5.  가상 하드 디스크를 구성 했으면 클릭 **완료**합니다.

## <a name="create-a-vhd-set-file-from-windows-powershell"></a>Windows PowerShell에서 VHD 설정 파일 만들기

사용 된 [NEW-VHD](https://technet.microsoft.com/library/hh848503.aspx) 파일 형식 사용 하 여 cmdlet. 파일 경로 있는 VHD입니다. 이 예제에서는 10 기가바이트 크기에 있는 base.vhds 라는 VHD 설정 파일을 만듭니다.

``` PowerShell
PS c:\>New-VHD -Path c:\base.vhds -SizeBytes 10GB
```

## <a name="migrate-a-shared-vhdx-file-to-a-vhd-set-file"></a>VHD 설정 파일에 공유 VHDX 파일 마이그레이션

기존 공유 VHDX를 VHD로 VM을 오프 라인 해야 합니다. 다음은 Windows PowerShell을 사용 하는 권장 되는 프로세스입니다.

1. VM에서 VHDX를 제거 합니다. 예를 들어, 실행 합니다. 
   ``` PowerShell
   PS c:\>Remove-VMHardDiskDrive existing.vhdx
   ```
  
2. VHDX를 VHD로 변환 합니다. 예를 들어, 실행 합니다.
   ``` PowerShell
   PS c:\>Convert-VHD existing.vhdx new.vhds
   ```
  
3. VM에 VHD를 추가 합니다. 예를 들어, 실행 합니다.
   ``` PowerShell
   PS c:\>Add-VMHardDiskDrive new.vhds
   ```
  



