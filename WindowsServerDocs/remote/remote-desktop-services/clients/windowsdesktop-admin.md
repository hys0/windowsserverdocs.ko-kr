---
title: 관리자용 Windows 데스크톱 클라이언트
description: Windows 데스크톱 클라이언트에 대한 정보는 주로 관리자에게 유용합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 09/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 202b39c33896f6b5e570c8abcf630dad436466c3
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80861426"
---
# <a name="windows-desktop-client-for-admins"></a>관리자용 Windows 데스크톱 클라이언트

>적용 대상: Windows 10 및 Windows 7

이 항목에는 관리자가 유용하게 사용할 수 있는 Windows 데스크톱 클라이언트에 대한 추가 정보가 포함되어 있습니다. 기본 사용에 대한 자세한 내용은 [Windows 데스크톱 클라이언트 시작](windowsdesktop.md)을 참조하세요.

## <a name="installation-options"></a>설치 옵션

사용자가 클라이언트를 다운로드하는 즉시 설치할 수 있지만, 여러 디바이스에 배포하는 경우 클라이언트를 다른 방법으로 배포할 수도 있습니다. 그룹 정책 또는 Microsoft Endpoint Configuration Manager를 사용하여 배포하면 명령줄을 통해 설치 관리자를 자동으로 실행할 수 있습니다. 다음 명령을 실행하여 클라이언트를 디바이스 단위 또는 사용자 단위로 배포합니다.

### <a name="per-device-installation"></a>디바이스 단위 설치

```
msiexec.exe /I <path to the MSI> /qn ALLUSERS=1
```

### <a name="per-user-installation"></a>사용자 단위 설치

```
msiexec.exe /i `<path to the MSI>` /qn ALLUSERS=2 MSIINSTALLPERUSER=1
```

## <a name="configuration-options"></a>구성 옵션

이 섹션에서는 이 클라이언트에 대한 새 구성 옵션에 대해 설명합니다.

### <a name="configure-update-notifications"></a>업데이트 알림 구성

기본적으로 업데이트가 있을 때마다 클라이언트에서 사용자에게 알려줍니다. 알림을 해제하려면 레지스트리 정보를 다음과 같이 설정합니다.

- **키:** HKLM\Software\Microsoft\MSRDC\Policies
- **종류:** REG_DWORD
- **이름:** AutomaticUpdates
- **데이터:** 0 = 알림을 사용하지 않도록 설정합니다. 1 = 알림을 표시합니다.

### <a name="configure-user-groups"></a>사용자 그룹 구성

클라이언트에서 업데이트를 받는 시기를 결정하는 다음 유형의 사용자 그룹 중 하나에 대해 해당 클라이언트를 구성할 수 있습니다.

#### <a name="insider-group"></a>참가자 그룹

참가자 그룹은 초기 유효성 검사를 위한 것이며, 관리자와 이들이 선택한 사용자로 구성됩니다. 참가자 그룹은 퍼블릭 그룹에 릴리스되기 전에 성능에 영향을 줄 수 있는 업데이트의 문제를 검색하기 위한 테스트 실행을 수행합니다.

> [!NOTE]
> 각 조직에서는 참가자 그룹의 일부 사용자가 업데이트를 테스트하고 문제를 조기에 파악하는 것이 좋습니다.

참가자 그룹에서는 새 버전의 클라이언트가 매월 두 번째 화요일에 사용자에게 릴리스되어 초기 유효성 검사를 수행합니다. 업데이트에 문제가 없으면 2주 후에 퍼블릭 그룹에 릴리스됩니다. 업데이트가 준비될 때마다 참가자 그룹의 사용자는 업데이트 알림을 자동으로 받게 됩니다. [Windows 데스크톱 클라이언트의 새로운 기능](windowsdesktop-whatsnew.md)에서 클라이언트의 변경 내용에 대한 자세한 정보를 확인할 수 있습니다.

참가자 그룹용 클라이언트를 구성하려면 레지스트리 정보를 다음과 같이 설정합니다.

- **키:** HKLM\Software\Microsoft\MSRDC\Policies
- **종류:** REG_SZ
- **이름:** ReleaseRing
- **데이터:** insider

#### <a name="public-group"></a>퍼블릭 그룹

이 그룹은 모든 사용자를 위한 것이며 가장 안정적인 버전입니다. 이 그룹을 구성하기 위해 아무 작업도 수행할 필요가 없습니다.

퍼블릭 그룹은 매월 네 번째 화요일마다 참가자 그룹에서 테스트한 클라이언트의 버전을 받습니다. 해당 설정을 사용하면 퍼블릭 그룹의 모든 사용자가 업데이트 알림을 받게 됩니다.
