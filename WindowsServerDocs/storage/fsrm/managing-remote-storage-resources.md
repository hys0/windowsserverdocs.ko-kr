---
title: 원격 저장소 리소스 관리
description: 이 문서에서는 원격 컴퓨터에서 저장소 리소스를 관리하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 29870c33e17c75fe25601237d7de47302662d21f
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476165"
---
# <a name="managing-remote-storage-resources"></a>원격 저장소 리소스 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

원격 컴퓨터에서 저장소 리소스를 관리하는 데는 두 가지 옵션이 있습니다.

-   파일 서버 리소스 관리자 MMC(Microsoft<sup>®</sup> Management Console) 스냅인(원격 리소스를 관리하는 데 사용)에서 원격 컴퓨터에 연결합니다.
-   파일 서버 리소스 관리자와 함께 설치된 명령줄 도구를 사용합니다.

두 옵션 모두 할당량을 관리하고, 파일을 차단하고, 분류를 관리하고, 파일 관리 작업을 예약하고, 이러한 원격 리소스로 보고서를 생성할 수 있습니다.

> [!Note]
> 파일 서버 리소스 관리자는 로컬 컴퓨터나 원격 컴퓨터의 리소스를 관리할 수 있지만 동시에 두 리소스를 관리할 수는 없습니다.

예를 들어 다음 작업을 할 수 있습니다.

-   파일 서버 리소스 관리자 MMC 스냅인을 사용하여 도메인의 다른 컴퓨터에 연결하고, 원격 컴퓨터에 위치한 볼륨 또는 폴더의 저장소 활용을 검토합니다.
-   로컬 서버에 할당량과 파일 차단 템플릿을 만들고 명령줄 도구를 사용하여 지점에 있는 파일 서버로 이러한 템플릿을 가져옵니다.

이 섹션에서는 다음 항목을 다룹니다.

-   [원격 컴퓨터에 연결](connect-to-remote-computer.md)
-   [명령줄 도구](command-line-tools.md)
