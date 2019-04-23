---
title: 호스트 캐시 이동 및 크기 조정(선택 사항)
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cb75e06b5da8ff95fcf763b22c5160ea200035f3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853534"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>이동 및 호스트 캐시 크기 조정 \(옵션\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이브와 폴더를 원하는 경우 호스트 캐시를 이동 하 고 호스트 캐시 서버 호스트 캐시에 사용할 수 있는 디스크 공간의 크기를 지정 하려면이 절차를 사용할 수 있습니다.

이 절차는 선택 사항입니다. 기본 위치를 캐시 하는 경우 \(%windir%\\ServiceProfiles\\NetworkService\\AppData\\로컬\\PeerDistPub\) 및 – 되는 총 하드 디스크 공간이 5%-크기는 배포에 적합 한, 자격 증명을 변경할 필요가 없습니다.

이 절차를 수행 하려면 Administrators 그룹의 구성원 이어야 합니다.

### <a name="to-move-and-resize-the-hosted-cache"></a>이동 하 고 호스트 캐시 크기

1. 관리자 권한으로 Windows PowerShell을 엽니다.

2. 로컬 컴퓨터에서 호스트 캐시를 다른 위치로 이동 하려면 다음 명령을 입력 하 고 enter 키를 누릅니다.

    > [!IMPORTANT]
    > 다음 명령을 실행 하기 전에 예: – – MoveTo, 및 경로 매개 변수 값을 배포에 적합 한 값으로 바꿉니다.

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  호스팅된 크기를 조정 하려면 다음 명령을 입력 캐시-datacache 특히 \- 로컬 컴퓨터에 있습니다. Enter 키를 누릅니다.

    > [!IMPORTANT]
    > 다음 명령을 실행 하기 전에 매개 변수 값을 같은 대체 \-배포에 적합 한 값의 백분율입니다.  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  호스트 캐시 서버 구성을 확인 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ``` 
    Get-BCStatus
    ``` 

    명령의 결과 BranchCache 설치의 모든 측면에 대 한 상태를 표시합니다. 다음은 몇 가지 BranchCache 설정 및 각 항목에 대 한 올바른 값입니다.

    -   DataCache | CacheFileDirectoryPath: SetBCCache 명령의 – MoveTo 매개 변수와 함께 제공 된 값과 일치 하는 하드 디스크 위치를 표시 합니다. 예를 들어, d: 값을 제공 하는 경우\\datacache를 값이 명령 출력에 표시 됩니다.

    -   DataCache | MaxCacheSizeAsPercentageOfDiskVolume: SetBCCache 명령의 – 백분율 매개 변수와 함께 제공 된 값과 일치 하는 번호를 표시 합니다. 예를 들어 값 20을 제공한 경우 해당 값은 명령 출력에 표시 됩니다.

이 가이드를 계속 하려면 참조 [Prehash 및 호스트 캐시 서버 & #40; 옵션 & #41;에서 미리 콘텐츠](7-Bc-Prehash-Preload.md)합니다.