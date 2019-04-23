---
title: WSUS 복제본 모드 실행
description: 'Windows Server Update Service (WSUS) 항목-복제본 모드를 구성 하는 방법 '
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d218cd6b-3b6b-4429-913b-31d412ce3356
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b4139354a3f0f7b1f1a97107d2f6b28db2b02c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878744"
---
# <a name="running-wsus-replica-mode"></a>WSUS 복제본 모드 실행

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

복제 모드에서 실행 되는 WSUS 서버는 관리 서버에 만들어진 컴퓨터 그룹 및 업데이트 승인을 상속 합니다. 복제 모드를 사용 하는 시나리오에서 일반적으로 단일 관리 서버가 고 하나 이상의 하위 복제 WSUS 서버, 사이트 또는 조직 지형에 따라 조직 전반에 걸쳐 분산 됩니다. 업데이트를 승인 하 고 복제 모드 서버에서 미러 다음 관리 서버의 컴퓨터 그룹을 만듭니다. WSUS 설치 중에 복제 모드 서버를 설정할 수 있습니다 하 고이 시나리오를 구현 하기 호스팅되고 업데이트 승인 하는 조직에서 중요 한 있기 때문에 컴퓨터 그룹을 중앙에서 관리 합니다.

WSUS 서버를 복제 모드에서 실행 하는 경우 기본적으로 이루어져 있습니다 서버의 제한 된 관리 기능을 수행할 수 있습니다.

-   추가 하 고 컴퓨터 그룹에서 컴퓨터를 제거 합니다. 컴퓨터 그룹 구성원 복제 서버에 배포 되지 않은, 자체 컴퓨터만 그룹화 합니다. 따라서 복제 모드 서버에서 관리 서버에서 만든 컴퓨터 그룹을 상속 합니다. 그러나 컴퓨터 그룹은 비어 있게 됩니다. 그런 다음 컴퓨터 그룹에 복제본 서버에 연결 하는 컴퓨터 클라이언트를 할당 해야 있습니다.

-   동기화 일정 설정

-   프록시 서버 설정 지정

-   업데이트 원본을 지정합니다. 이 관리 서버 이외의 서버 수 있습니다.

-   사용 가능한 업데이트 보기

-   업데이트, 동기화, 컴퓨터 상태 및 서버에서 WSUS 설정 모니터링

-   복제 모드 서버에서 사용할 수 있는 보고서 모든 표준 WSUS를 실행 합니다.



