---
title: 패치 서버 코어
description: Windows Server의 Server Core 설치를 업데이트 하는 방법 알아보기
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: eacb80d89e7bcc95d6b5c12269d7587dc7d6870c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383322"
---
# <a name="patch-a-server-core-installation"></a>Server Core 설치 패치

> 적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

다음과 같은 방법으로 Server Core 설치를 실행 하는 서버를 패치할 수 있습니다.

- **Windows 업데이트를 자동으로 사용 하거나 Windows Server Update Services (WSUS)를 사용**합니다. 자동으로 또는 명령줄 도구를 사용 하 여 Windows 업데이트를 사용 하거나 WSUS (Windows Server Update Services)를 사용 하 여 Server Core 설치를 실행 하는 서버에 서비스를 사용할 수 있습니다.

- **수동**. Windows update 또는 WSUS를 사용 하지 않는 조직 에서도 업데이트를 수동으로 적용할 수 있습니다.

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Server Core 서버에 설치 된 업데이트 보기
Server Core에 새 업데이트를 추가 하기 전에 이미 설치 된 업데이트를 확인 하는 것이 좋습니다.

Windows PowerShell을 사용 하 여 업데이트를 보려면 **핫픽스**를 실행 합니다.

명령을 실행 하 여 업데이트를 보려면 **printbrm.exe**를 실행 합니다. 도구에서 시스템을 검사 하는 동안 약간의 지연이 있을 수 있습니다.

명령줄에서 **wmic qfe 목록을** 실행할 수도 있습니다. 

## <a name="patch-server-core-automatically-with-windows-update"></a>Windows 업데이트를 사용 하 여 자동으로 Server Core 패치

Windows 업데이트를 사용 하 여 서버를 자동으로 패치 하려면 다음 단계를 수행 합니다.

1. 현재 Windows 업데이트 설정을 확인 합니다.
   ```
   %systemroot%\system32\Cscript scregedit.wsf /AU /v 
   ```

2. 자동 업데이트를 사용 하도록 설정 하려면

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 4 
   Net start wuauserv
   ```  

3. 자동 업데이트를 사용 하지 않도록 설정 하려면 다음을 실행 합니다.

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 1 
   Net start wuauserv 
   ```

서버가 도메인 구성원인 경우 그룹 정책을 사용하여 Windows 업데이트를 구성할 수도 있습니다. 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=192470 을 참조하세요. 그러나이 방법을 사용 하는 경우 그래픽 인터페이스가 없기 때문에 옵션 4 ("자동 다운로드 및 설치 예약")만 Server Core 설치와 관련 됩니다. 설치되는 업데이트 및 업데이트 설치 시기를 보다 자세하게 제어하려면 대부분의 Windows 업데이트 그래픽 인터페이스와 동일한 역할을 수행하는 명령줄을 제공하는 스크립트를 사용합니다. 스크립트에 대 한 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=192471 을 참조 하세요.

Windows 업데이트가 강제로 사용 가능한 업데이트를 즉시 검색하고 설치하도록 하려면 다음 명령을 실행합니다.

```
Wuauclt /detectnow 
```

설치된 업데이트에 따라 시스템에서 알림 메시지를 제공하지 않은 경우에도 컴퓨터를 다시 시작해야 할 수 있습니다. 설치 프로세스가 완료 되었는지 확인 하려면 작업 관리자를 사용 하 여 **wuauclt.exe** 또는 **신뢰할 수 있는 설치 관리자** 프로세스가 적극적으로 실행 되 고 있지 않은지 확인 합니다. [Server Core 서버에 설치 된 업데이트 보기](#view-the-updates-installed-on-your-server-core-server) 의 방법을 사용 하 여 설치 된 업데이트 목록을 확인할 수도 있습니다.

## <a name="patch-the-server-with-wsus"></a>WSUS를 사용 하 여 서버 패치 

Server Core 서버가 도메인의 구성원인 경우 그룹 정책을 통해 WSUS 서버를 사용하도록 이 서버를 구성할 수 있습니다. 자세한 내용은 [그룹 정책 참조 정보](https://www.microsoft.com/download/details.aspx?id=25250)를 다운로드 하세요. [자동 업데이트에 대 한 그룹 정책 설정 구성](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md) 을 검토할 수도 있습니다.

## <a name="patch-the-server-manually"></a>수동으로 서버 패치

업데이트를 다운로드 하 여 Server Core 설치에 사용할 수 있도록 설정 합니다.
명령 프롬프트에서 다음 명령을 실행 합니다.

```
Wusa <update>.msu /quiet 
```

설치된 업데이트에 따라 시스템에서 알림 메시지를 제공하지 않은 경우에도 컴퓨터를 다시 시작해야 할 수 있습니다.

수동으로 업데이트를 제거 하려면 다음 명령을 실행 합니다.

```
Wusa /uninstall <update>.msu /quiet 
```

