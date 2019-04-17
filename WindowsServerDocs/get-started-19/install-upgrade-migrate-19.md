---
title: 설치 | 업그레이드 | Windows Server 2019로 마이그레이션
description: 새로 설치, 바로 업그레이드 또는 Windows Server 2019로 마이그레이션하는 방법입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4e99cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 58c363fc0a1e336519bc6ec4276651345cc2b5eb
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121392"
---
# 설치 | 업그레이드 | Windows Server 2019로 마이그레이션

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 및 Windows Server 2008에 대한 연장 지원이 2020년 1월에 종료됩니다. [업그레이드 옵션에 자세히 알아보세요](http://aka.ms/upgradecenter).

Windows Server 새 버전으로 전환할 시점입니까? 현재 무엇을 실행 중인가에 따라 다양한 옵션이 있습니다.

## 새로 설치
이전 버전의 Windows Server 2019 동일한 하드웨어에서 Windows Server에서 이동 하려는 경우는 **새로 설치**, 새 운영 체제 따라서 삭제 하는 동일한 하드웨어에서 확실 바로 위에 바로 설치를 수행 해야 합니다 이전 운영 체제입니다. 가장 간단한 방법이지만 먼저 데이터를 백업하고 나중에 응용 프로그램을 재설치할 계획을 세워야 합니다. 몇 가지 방법으로 인식 같은 시스템 요구 사항, [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124), [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418)및 [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)에 대 한 세부 정보를 확인 해야 합니다.

## 바로 업그레이드
**바로 업그레이드**를 기울기 보면 이전 운영 체제에서 새 컴퓨터로 설정, 서버 역할을 유지 하려고 동일한 하드웨어 및 서버를 병합 하지 않고 설정한 서버 역할을 모두 유지 하려는 경우 및 데이터를 그대로 유지 합니다. 예를 들어 서버가 Windows Server 2012 r 2를 실행 하는 경우 Windows Server 2016 또는 Windows Server 2019 업그레이드할 수 있습니다. 그러나 모든 기존 운영 체제가 모든 새 운영 체제로 업그레이드될 수 있는 것은 아닙니다. 사용 가능한 업그레이드 경로 대 한 다음 다이어그램을 참조 하세요.

![Windows 서버 바로 업그레이드 경로 다이어그램](media/upgrade-paths.png)

업그레이드에 대 한 단계별 지침, [Windows Server 업그레이드 센터](http://aka.ms/upgradecenter)를 참조 하세요.

<a href="http://aka.ms/upgradecenter"><img src="media/upgrade-center.png" alt="Screenshot of Windows Upgrade Center" title="Windows 서버 업그레이드 센터"></a>

## 클러스터 운영 체제 롤링 업그레이드
클러스터 OS 롤링 업그레이드 관리자가 Hyper-v 또는 스케일 아웃 파일 서버 워크 로드를 중지 하지 않고 Windows Server 2012 R2 및 Windows Server 2016에서 클러스터 노드의 운영 체제를 업그레이드할 수 있습니다. 이 기능을 사용하면 서비스 수준 계약에 영향을 줄 수 있는 가동 중지 시간을 방지할 수 있습니다. 이 새로운 기능은 [클러스터 운영 체제 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)에 자세히 설명되어 있습니다.

## 마이그레이션

Windows Server 마이그레이션 때 Windows Server, 동일 하거나 최신 버전을 실행 하는 다른 대상 컴퓨터에 Windows Server를 실행 하는 원본 컴퓨터에서 한 번에 하나의 역할 또는 기능을 이동 합니다. 이와 같은 목적일 때 마이그레이션은 동일한 컴퓨터에서 기능을 업그레이드하는 작업이 아니라 하나의 역할 또는 기능과 그 데이터를 다른 컴퓨터로 옮기는 작업으로 정의됩니다. 

## 라이선스 변환
일부 운영 체제 릴리스에서는 해당 릴리스의 특정 버전을 간단한 명령과 적절한 라이선스 키만으로 동일한 릴리스의 다른 버전으로 한 번에 변환할 수 있습니다. 이를 **라이선스 변환**이라 합니다. 예를 들어 서버가 Windows Server 2016 Standard를 실행하는 경우 Windows Server 2016 Datacenter로 변환할 수 있습니다. 또한 일부 Windows Server 릴리스에서는 동일한 명령과 적절한 키를 이용하여 OEM, 볼륨 라이선스 및 일반 정품 버전 사이에서 자유롭게 변환할 수도 있습니다.


 
 
