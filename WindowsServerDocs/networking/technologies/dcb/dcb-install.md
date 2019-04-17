---
title: Windows의 (DCB) 브리지 설치 데이터 센터 서버 또는 클라이언트
description: 이 항목에서는 Windows Server 또는 Windows 클라이언트의 데이터 센터 브리지을 설치 하는 방법에 알아보세요.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 491bdeb1a7458be1f991be68724e7a7b51f67ecf
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>Windows 10 또는 Windows Server 2016 \(DCB\) 브리지 데이터 센터 설치

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 DCB Windows 10 또는 Windows Server 2016을 설치 하는 방법을 알아보려면 사용할 수 있습니다.

## <a name="prerequisites-for-using-dcb"></a>사용 하 여 DCB 사항

다음은 구성 하 고 관리 DCB 사항입니다.

### <a name="install-a-compatible-operating-system"></a>호환 되는 운영 체제 설치

이 가이드 DCB 명령 다음 운영 체제에 사용할 수 있습니다.

- Windows Server (세미콜론 연간 채널)
- Windows Server 2016
- Windows 10 \(all versions\)

다음 운영 체제에 Windows 10 및 Windows Server 2016 용 DCB 설명서에서 사용 되는 명령을와 호환 되지 않는 이전 버전의 DCB 포함 됩니다.

- Windows Server 2012 r 2
- Windows Server 2012

###  <a name="hardware-requirements"></a>하드웨어 요구 사항

다음은 DCB 위한 하드웨어 요구 사항 목록이 있습니다.

- 이더넷 네트워크 adapter\(s\) DCB\ 가능 DCB Windows Server 2016을 제공 하는 컴퓨터에 설치 되어야 합니다.
- 네트워크에서 DCB\ 가능 하드웨어 스위치를 배포 되어야 합니다.


## <a name="install-dcb-in-windows-server-2016"></a>Windows Server 2016에서 DCB 설치

다음 섹션 DCB Windows Server 2016을 실행 하는 컴퓨터에 설치에 사용할 수 있습니다.

**관리자 자격 증명**

이 절차를 수행 하려면의 회원 있어야 **관리자**합니다.

### <a name="install-dcb-using-windows-powershell"></a>DCB Windows PowerShell를 사용 하 여 설치

다음 절차 DCB Windows PowerShell를 사용 하 여 설치에 사용할 수 있습니다.

1. Windows Server 2016을 실행 하는 컴퓨터에서 클릭 **시작**, 다음 Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭 합니다. 에 메뉴가 나타납니다. 메뉴를 클릭 **더 많은**을 차례로 클릭 하 고 **관리자 권한으로 실행**합니다. 메시지가 표시 되 면 컴퓨터에서 관리자 권한이 있는 계정 자격 증명을 입력 합니다. Windows PowerShell을 관리자 권한으로 엽니다.
2. 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>DCB 서버 관리자를 사용 하 여 설치

다음 절차 DCB 서버 관리자를 사용 하 여 설치에 사용할 수 있습니다.

>[!NOTE]
>이 절차의 첫 번째 단계를 수행한 후는 **시작 하기 전에** 이전 선택한 경우 역할 추가 및 기능 마법사의 페이지가 표시 되지 않으면 **이 페이지 기본적으로 건너뛰기** 역할 추가 및 기능 마법사가 실행 될 때 합니다. 하는 경우는 **시작 하기 전에** 페이지가 표시 되지 않으면, 1 단계에서 3 단계로 이동 합니다.

1. 서버 관리자 d c 1 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. 역할 추가 및 기능 마법사가 열립니다.
2. **시작 하기 전에**, 클릭 **다음**합니다.
3. **설치 유형을 선택**, 되도록 **역할 또는 기능 기반 설치** 을 선택한 다음 클릭 **다음**합니다.
4. **선택 대상 서버**, 되도록 **서버 풀에서 서버를 선택** 을 선택 합니다. **서버 풀**, 로컬 컴퓨터 선택 되어 있는지 확인 합니다. 클릭 **다음**합니다.
5. **서버 역할 선택**, 클릭 **다음**합니다.
6. **기능 선택**에서 **기능**, 클릭 **데이터 센터 브리지**합니다. 대화 상자가 DCB 필요한 기능을 추가 하려면 요청 열립니다. 클릭 **기능을 추가**합니다.
7. **기능 선택**, 클릭 **다음**합니다. 
8. 7.에서 **설치 선택을 확인**, 클릭 **설치**합니다. **설치 진행률** 페이지 설치 과정에서 상태를 표시 합니다. 메시지가 나타나면 메시지가 해당 설치 했습니다를 클릭 **닫기**합니다.

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>커널 디버거 QoS \(Optional\) 수 있도록 구성

 기본적으로 커널 디버거 NetQos 차단 합니다. 커널 디버거 컴퓨터에 설치 되어 있는 경우 DCB, 설치 하는 데 사용 하는 방법에 관계 없이를 활성화 하 고 다음 명령을 실행에서 구성한 QoS 수 있도록 디버거를 구성 해야 합니다.

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Windows 10에서 DCB 설치

다음 절차는 Windows 10 컴퓨터에서 수행할 수 있습니다.

이 절차를 수행 하려면의 회원 있어야 **관리자**합니다.

### <a name="install-dcb"></a>DCB 설치

1. 클릭 **시작**클릭 한 다음 아래로 스크롤하여, **Windows 시스템**합니다.
2. 클릭 **제어판**합니다. **제어판** 대화 상자를 엽니다.
3. **제어판**, 클릭 **볼**를 다음 중 하나를 클릭 하 고 **큰 아이콘** 또는 **작은 아이콘**합니다.
4. 클릭 **프로그램 및 기능**합니다. 프로그램 및 기능 대화 상자를 엽니다.
5. **프로그램 및 기능**왼쪽된 창에서 클릭 **켜거나 끌 Windows 기능**합니다. **Windows 기능** 대화 상자를 엽니다.
6. **Windows 기능**, 클릭 **데이터 센터 브리지**을 차례로 클릭 하 고 **확인**합니다.

![Windows 기능 켜기 또는 대화 상자 끄기](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


