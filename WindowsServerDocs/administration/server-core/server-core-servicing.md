---
title: Server Core에 패치를 적용
description: Windows Server의 Server Core 설치를 업데이트 하는 방법을 설명 합니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: f51ffae5ed8f91cca386eb209e7a1d8cc664ceeb
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448132"
---
# <a name="patch-a-server-core-installation"></a>패치 Server Core 설치

> 적용 대상: Windows Server (세미콜론 연간 회의 채널) 및 Windows Server 2016

다음과 같은 방법으로의 Server Core 설치를 실행 하는 서버를 패치 수 있습니다.

- **자동으로 또는 Windows Server Update Services (WSUS)와 사용 하 여 Windows 업데이트**합니다. 중 자동으로 또는와 명령줄 도구 또는 Windows Server Update Services (WSUS), Windows Update를 사용 하 여 Server Core 설치를 실행 하는 서버 서비스 수 있습니다.

- **수동으로**합니다. Windows update 또는 WSUS를 사용 하지 않는 조직에서는에 수동으로 업데이트를 적용할 수 있습니다.

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Server Core 서버에 설치 된 업데이트 보기
Server Core를 새 업데이트를 추가 하기 전에 것 어떤 업데이트가 이미 설치 되었는지 확인 하는 것이 좋습니다.

Windows PowerShell을 사용 하 여 업데이트를 보려면, **Get-핫픽스**를 실행 합니다.

명령을 실행 하 여 업데이트를 보려면 **systeminfo.exe**를 실행 합니다. 시스템을 검사 하는 도구는 동안 약간의 지연이 수 있습니다.

명령줄에서 **wmic qfe 목록** 를 실행할 수도 있습니다. 

## <a name="patch-server-core-automatically-with-windows-update"></a>Windows Update를 통해 자동으로 패치 Server Core

다음 단계를 사용 하 여 Windows Update를 사용 하 여 자동으로 서버 패치를 적용 하려면:

1. 현재 Windows Update 설정을 확인 합니다.
   ```
   %systemroot%\system32\Cscript scregedit.wsf /AU /v 
   ```

2. 자동 업데이트할 수 있도록 합니다.

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 4 
   Net start wuauserv
   ```  

3. 자동 업데이트를 사용 하지 않으려면 다음을 실행 합니다.

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 1 
   Net start wuauserv 
   ```

서버는 도메인의 구성원 인 경우에 그룹 정책을 사용 하 여 Windows Update를 구성할 수 있습니다. 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=192470을 참조하세요. 그러나이 메서드를 사용 하는 경우 4 ("자동으로 다운로드 및 설치 예약")는 으로만 Server Core 설치에 관련 된 그래픽 인터페이스를 부족으로 인해 합니다. 업데이트를 설치 하는 보다 효율적으로 제어에 대 한 및 때, Windows Update 그래픽 인터페이스는 대부분의 명령줄과 같은 기능을 제공 하는 스크립트를 사용할 수 있습니다. 스크립트에 대 한 정보를 참조 하십시오. https://go.microsoft.com/fwlink/?LinkId=192471합니다.

즉시를 감지 하 고 모든 사용 가능한 업데이트를 설치 하려면 Windows Update를 강제 실행 하려면 다음 명령을 실행 합니다.

```
Wuauclt /detectnow 
```

설치 된 업데이트를에 따라 시스템에 게 알리지이 수 있지만 컴퓨터를 다시 시작 해야 확인 메시지가 나타납니다. 설치 프로세스를 완료 하는 경우를 확인 하려면 작업 관리자를 사용 하 여 **Wuauclt** 또는 **신뢰할 수 있는 설치 관리자** 프로세스 적극적으로 실행 하지 않는 확인 합니다. 설치 된 업데이트 목록을 확인 하려면 [Server Core 서버에 설치 된 업데이트 보기](#view-the-updates-installed-on-your-Server-Core-server) 에 메서드를 사용할 수 있습니다.

## <a name="patch-the-server-with-wsus"></a>WSUS 사용 하 여 서버 패치를 적용합니다 

Server Core 서버는 도메인의 구성원 인 경우에 그룹 정책을 사용 하 여 WSUS 서버를 사용 하도록 구성할 수 있습니다. 자세한 내용은 [그룹 정책 참조 정보](https://www.microsoft.com/download/details.aspx?id=25250)를 다운로드 합니다. [자동 업데이트에 대 한 그룹 정책 설정 구성](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md) 을 검토할 수 있습니다.

## <a name="patch-the-server-manually"></a>서버에 수동으로 패치

업데이트를 다운로드 하 고 Server Core 설치에 사용할 수 있게 합니다.
명령 프롬프트에서 다음 명령을 실행 합니다.

```
Wusa <update>.msu /quiet 
```

설치 된 업데이트를에 따라 시스템에 게 알리지이 수 있지만 컴퓨터를 다시 시작 해야 확인 메시지가 나타납니다.

업데이트를 수동으로 제거 하려면 다음 명령을 실행 합니다.

```
Wusa /uninstall <update>.msu /quiet 
```

