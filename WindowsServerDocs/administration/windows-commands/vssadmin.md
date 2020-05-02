---
title: List
description: Vssadmin 명령의 개요입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9cc3f40b5d1e7e83f1aecdc26a54ffc4f1839bc7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720229"
---
# <a name="vssadmin"></a>List

> 적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows server 2012, windows Server 2008 R2, Windows Server 2008

현재 볼륨 섀도 복사본 백업과 설치 된 모든 섀도 복사본 작성기 및 공급자를 표시 합니다. 다음 표에서 명령 이름을 선택 하 여 명령 구문을 확인 합니다.

|명령|설명|가용성
|---|---|---
|[Vssadmin add shadowstorage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788051(v%3dws.11))|볼륨 섀도 복사본 저장소 연결을 추가 합니다.| 서버만
|[Vssadmin create shadow](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788055(v%3dws.11))|새 볼륨 섀도 복사본을 만듭니다.| 서버만
|[Vssadmin delete 그림자](vssadmin-delete-shadows.md)|볼륨 섀도 복사본을 삭제 합니다.| 클라이언트 및 서버
|[Vssadmin delete shadowstorage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc785461(v%3dws.11))|볼륨 섀도 복사본 저장소 연결을 삭제 합니다.| 서버만
|[Vssadmin list providers](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788108(v%3dws.11))|등록 된 볼륨 섀도 복사본 공급자를 나열 합니다.| 클라이언트 및 서버
|[Vssadmin list 그림자](vssadmin-list-shadows.md)|기존 볼륨 섀도 복사본을 나열 합니다.| 클라이언트 및 서버
|[Vssadmin list shadowstorage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788045(v%3dws.11))|시스템의 모든 섀도 복사본 저장소 연결을 나열 합니다.| 클라이언트 및 서버
|[Vssadmin list 볼륨](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc788064(v%3dws.11))|섀도 복사본에 적합 한 볼륨을 나열 합니다.| 클라이언트 및 서버
|[Vssadmin list writer](vssadmin-list-writers.md)|시스템의 모든 구독 된 볼륨 섀도 복사본 기록기를 나열 합니다.| 클라이언트 및 서버
|[Vssadmin resize shadowstorage](vssadmin-resize-shadowstorage.md)|섀도 복사본 저장소 연결의 최대 크기를 조정 합니다.| 클라이언트 및 서버
