---
title: 이동 및 크기 조정 호스트 캐시 (선택 사항)
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2a3ed1d6de1281575b33cdf75a5970d2ed033085
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>이동 및 크기 조정 호스트 캐시 \(Optional\)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 절차를 사용 하 여 호스팅된 캐시 드라이브 및 사용자가 선호 하는 폴더를 이동 하 고 여 호스팅된 캐시 서버 호스트 캐시에 사용할 수 있는 디스크 공간의 크기를 지정할 수 수 있습니다.

이 절차 선택 사항입니다. 기본 캐시 위치 \(%windir%\\ServiceProfiles\\NetworkService\\AppData\\Local\\PeerDistPub\) 및 크기-5% 전체 하드 디스크 공간의 – 배포에 대 한 적절 한 경우 변경 필요는 없습니다.

이 절차를 수행 하려면 관리자가 그룹의 회원 있어야 합니다.

### <a name="to-move-and-resize-the-hosted-cache"></a>이동 하 여 호스팅된 캐시 크기 조정

1. Windows PowerShell을 관리자 권한으로 엽니다.

2. 호스트 캐시 로컬 컴퓨터에서 다른 위치로 이동 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    > [!IMPORTANT]
    > 다음 명령을 실행 하기 전에 등 – 경로 및 – MoveTo, 매개 값 배포에 대 한 적절 한 값으로 교체 합니다.

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  다음 명령을 입력 하 여 호스팅된 크기 조정 캐시 – datacache 특히 \-로컬 컴퓨터에서 합니다. ENTER 키를 누릅니다.

    > [!IMPORTANT]
    > 다음 명령을 실행 하기 전에 매개 변수 값을 \-Percentage, 배포에 대 한 적절 한 값으로 교체 합니다.  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  호스트 캐시 서버 구성을 확인 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ``` 
    Get-BCStatus
    ``` 

    명령 결과가 BranchCache 설치의 모든 측면에 대 한 상태를 표시 합니다. 다음은 몇 가지 BranchCache 설정 하 고 각 항목에 대 한 올바르지 값 다음과 같습니다.

    -   DataCache | CacheFileDirectoryPath: – MoveTo 매개 변수와 SetBCCache 명령 함께 제공 되는 값와 일치 하는 하드 디스크 위치를 표시 합니다. 예를 들어, D:\\datacache 가치를 제공 하는 경우 해당 값 명령 출력에 표시 됩니다.

    -   DataCache | MaxCacheSizeAsPercentageOfDiskVolume: SetBCCache 명령 – 비율 매개 제공 되는 값와 일치 하는 번호를 표시 합니다. 예를 들어, 20 가치를 제공 하는 경우 해당 값 명령 출력에 표시 됩니다.

이 가이드를 계속 참조 [Prehash 및 미리 로드 콘텐츠를 호스트 캐시 서버 & #40; 옵션 & #41; ](7-Bc-Prehash-Preload.md).