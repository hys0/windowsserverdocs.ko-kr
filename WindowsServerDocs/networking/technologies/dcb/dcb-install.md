---
title: 설치 데이터 센터 브리징 (DCB) windows에서 Server 또는 클라이언트
description: 이 항목에서는 Windows Server 또는 Windows 클라이언트에서 데이터 센터 브리징를 설치 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7c20ef027279780181ff176afa39a19f2976c4c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845444"
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>설치 데이터 센터 브리징 \(DCB\) Windows Server 2016 또는 Windows 10에서

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016 또는 Windows 10에서 DCB를 설치 하는 방법을 알아보려면이 항목에서는 사용할 수 있습니다.

## <a name="prerequisites-for-using-dcb"></a>DCB를 사용 하기 위한 필수 구성 요소

다음은 구성 및 DCB를 관리 하기 위한 필수 구성 요소입니다.

### <a name="install-a-compatible-operating-system"></a>호환 되는 운영 체제를 설치 합니다.

이 가이드에서 DCB 명령을 다음 운영 체제에서 사용할 수 있습니다.

- Windows Server(반기 채널)
- Windows Server 2016
- Windows 10 \(모든 버전\)

다음 운영 체제는 Windows Server 2016 및 Windows 10에 대 한 DCB 설명서에 사용 되는 명령과 호환 되지 않는 이전 버전의 DCB 포함 합니다.

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>하드웨어 요구 사항

다음은 DCB에 대 한 하드웨어 요구 사항 목록입니다.

- DCB\-가능 이더넷 네트워크 어댑터가\(s\) Windows Server 2016 DCB를 제공 하는 컴퓨터에 설치 해야 합니다.
- DCB\-가능 하드웨어 스위치를 네트워크에 배포 되어야 합니다.


## <a name="install-dcb-in-windows-server-2016"></a>Windows Server 2016에서에서 DCB를 설치 합니다.

Windows Server 2016을 실행 하는 컴퓨터에 DCB를 설치 하려면 다음 섹션에서는 사용할 수 있습니다.

**관리자 자격 증명**

이러한 절차를 수행 하려면의 구성원 이어야 **관리자**합니다.

### <a name="install-dcb-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 DCB를 설치 합니다.

Windows PowerShell을 사용 하 여 DCB를 설치 하려면 다음 절차를 사용할 수 있습니다.

1. Windows Server 2016을 실행 하는 컴퓨터를 클릭 **시작**, Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭 합니다. 메뉴가 나타납니다. 메뉴에서 클릭 **자세한**를 클릭 하 고 **관리자 권한으로 실행**합니다. 메시지가 표시 되 면 컴퓨터에 대 한 관리자 권한이 있는 계정의 자격 증명을 입력 합니다. Windows PowerShell 관리자 권한으로 엽니다.
2. 다음 명령을 입력한 후 Enter 키를 누릅니다.

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>서버 관리자를 사용 하 여 DCB를 설치 합니다.

서버 관리자를 사용 하 여 DCB를 설치 하려면 다음 절차를 사용할 수 있습니다.

>[!NOTE]
>이 절차에서는 첫 번째 단계를 수행 하 고 나면 합니다 **시작 하기 전에** 이전에 선택한 경우에 추가 역할 및 기능 마법사의 페이지가 표시 되지 않습니다 **기본적으로이 페이지 건너뛰기** 때 추가 역할 및 기능 마법사를 실행 합니다. 경우는 **시작 하기 전에** 페이지가 표시 되지 않으면, 1 단계의 3 단계로 건너뜁니다.

1. Dc1에서 서버 관리자에서 클릭 **관리**를 클릭 하 고 **역할 및 기능 추가**합니다. 역할 및 기능 추가 마법사가 열립니다.
2. **시작하기 전**에서 **다음**을 클릭합니다.
3. **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.
4. **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.
5. **서버 역할 선택**에서 **다음**을 클릭합니다.
6. **기능 선택**의 **기능**, 클릭 **데이터 센터 브리징**합니다. DCB는 데 필요한 기능을 추가 하려는 경우 요청 하는 대화 상자가 열립니다. 클릭 **기능 추가**합니다.
7. **기능 선택**, 클릭 **다음**합니다. 
8. 7에서 **설치 선택 확인**, 클릭 **설치**합니다. 합니다 **설치 진행률** 페이지 설치 과정에서 상태를 표시 합니다. 설치 성공 메시지가 나타납니다 후, 클릭 **닫기**합니다.

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>커널 디버거가 QoS를 허용 하도록 구성할 \(옵션\)

 기본적으로 커널 디버거 NetQos를 차단합니다. 커널 디버거를 컴퓨터에 설치 된 경우 DCB를 설치 하는 데 사용 하는 방법에 관계 없이 사용 하도록 설정 하 고 다음 명령을 실행 하 여 구성 하는 QoS를 허용 하도록 디버거를 구성 해야 합니다.

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Windows 10에서에서 DCB를 설치 합니다.

Windows 10 컴퓨터에서 다음 절차를 수행할 수 있습니다.

이 절차를 수행 하려면의 구성원 이어야 **관리자**합니다.

### <a name="install-dcb"></a>DCB 설치

1. 클릭 **시작**, 한 다음 아래로 스크롤하여 클릭 **Windows 시스템**입니다.
2. **제어판**을 클릭합니다. 합니다 **제어판** 대화 상자가 열립니다.
3. **Control Panel**, 클릭 **하 여 볼**, 중 하나를 클릭 하 고 **큰 아이콘** 또는 **작은 아이콘**합니다.
4. 클릭 **프로그램 및 기능**합니다. 프로그램 및 기능 대화 상자가 열립니다.
5. **프로그램 및 기능**, 왼쪽된 창에서 클릭 **설정 하는 Windows 기능 사용 /** 합니다. 합니다 **Windows 기능** 대화 상자가 열립니다.
6. **Windows 기능**, 클릭 **데이터 센터 브리징**를 클릭 하 고 **확인**합니다.

![Windows 기능을 켜거나 대화 상자 닫기](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


