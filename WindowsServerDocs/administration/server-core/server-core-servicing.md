---
title: Server Core 패치
description: Windows Server의 Server Core 설치를 업데이트 하는 방법 알아보기
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: b19512a6f34e13469433aba6051f1232824beb0e
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034150"
---
# <a name="patch-a-server-core-installation"></a>Server Core 설치를 패치 합니다.

> 적용 대상: Windows Server (반기 채널) 및 Windows Server 2016

다음과 같은 방법으로 Server Core 설치를 실행 하는 서버를 패치할 수 있습니다.

- **Windows 업데이트를 사용 하 여 자동으로 또는 Windows Server Update Services (WSUS) 사용한**합니다. 중 자동으로 또는 사용 하 여 명령줄 도구 또는 Windows Server Update Services (WSUS), Windows 업데이트를 사용 하 여 Server Core 설치를 실행 하는 서버 서비스할 수 있습니다.

- **수동**. Windows 업데이트나 WSUS를 사용 하지 않는 조직에도 수동으로 업데이트를 적용할 수 있습니다.

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Server Core 서버에 설치 된 업데이트 보기
Server Core에 새 업데이트를 추가 하기 전에 어떤 업데이트가 이미 설치 되었는지 확인 하려면는 것이 좋습니다.

Windows PowerShell을 사용 하 여 업데이트를 보려면 실행 **Get-hotfix**합니다.

명령을 실행 하 여 업데이트를 보려면 실행 **systeminfo.exe**합니다. 도구는 시스템을 검사 하는 동안 짧은 지연이 수 있습니다.

실행할 수도 있습니다 **wmic qfe 목록과** 명령줄에서. 

## <a name="patch-server-core-automatically-with-windows-update"></a>Windows 업데이트로 자동으로 패치 Server Core

Windows 업데이트로 자동으로 서버에 패치를 다음 단계를 사용 합니다.

1. 현재 Windows 업데이트 설정을 확인 합니다.
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

서버가 도메인 구성원인 경우 그룹 정책을 사용하여 Windows 업데이트를 구성할 수도 있습니다. 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=192470 를 참조하세요. 그러나이 메서드를 사용 하는 경우만 옵션 4 ("자동으로 다운로드 및 설치를 예약")은 Server Core 설치와 관련 그래픽 인터페이스의 부족으로 인해 합니다. 설치되는 업데이트 및 업데이트 설치 시기를 보다 자세하게 제어하려면 대부분의 Windows 업데이트 그래픽 인터페이스와 동일한 역할을 수행하는 명령줄을 제공하는 스크립트를 사용합니다. 스크립트에 대 한 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=192471합니다.

Windows 업데이트가 강제로 사용 가능한 업데이트를 즉시 검색하고 설치하도록 하려면 다음 명령을 실행합니다.

```
Wuauclt /detectnow 
```

설치된 업데이트에 따라 시스템에서 알림 메시지를 제공하지 않은 경우에도 컴퓨터를 다시 시작해야 할 수 있습니다. 설치 프로세스가 완료 된 경우를 확인 하려면 확인 하려면 작업 관리자를 사용 하는 **Wuauclt** 또는 **신뢰할 수 있는 설치자** 프로세스가 적극적으로 실행 합니다. 메서드를 사용할 수도 있습니다 [Server Core 서버에 설치 된 업데이트 보기](#view-the-updates-installed-on-your-server-core-server) 설치 된 업데이트 목록을 확인 합니다.

## <a name="patch-the-server-with-wsus"></a>WSUS 사용 하 여 서버 패치 

Server Core 서버가 도메인의 구성원인 경우 그룹 정책을 통해 WSUS 서버를 사용하도록 이 서버를 구성할 수 있습니다. 자세한 내용은 다운로드 합니다 [그룹 정책 참조 정보](https://www.microsoft.com/download/details.aspx?id=25250)합니다. 검토할 수도 있습니다 [자동 업데이트에 대 한 그룹 정책 설정 구성](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md)

## <a name="patch-the-server-manually"></a>서버에 수동으로 패치

업데이트를 다운로드 하 고 Server Core 설치에 사용할 수 있도록 합니다.
명령 프롬프트에서 다음 명령을 실행 합니다.

```
Wusa <update>.msu /quiet 
```

설치된 업데이트에 따라 시스템에서 알림 메시지를 제공하지 않은 경우에도 컴퓨터를 다시 시작해야 할 수 있습니다.

업데이트를 수동으로 제거 하려면 다음 명령을 실행 합니다.

```
Wusa /uninstall <update>.msu /quiet 
```

