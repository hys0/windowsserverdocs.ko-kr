---
title: Windows Server 또는 클라이언트에 DCB (데이터 센터 브리징) 설치
description: 이 항목에서는 Windows Server 또는 Windows 클라이언트에서 데이터 센터 브리징을 설치 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: edca8269178d9e1de9f8d57abac04400da0ac5c1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312799"
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 또는 Windows 10에서 데이터 센터 브리징 \(DCB\) 설치

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016 또는 Windows 10에서 DCB을 설치 하는 방법을 배울 수 있습니다.

## <a name="prerequisites-for-using-dcb"></a>DCB 사용을 위한 필수 구성 요소

DCB를 구성 하 고 관리 하기 위한 필수 구성 요소는 다음과 같습니다.

### <a name="install-a-compatible-operating-system"></a>호환 되는 운영 체제 설치

다음 운영 체제에서이 가이드의 DCB 명령을 사용할 수 있습니다.

- Windows Server(반기 채널)
- Windows Server 2016
- Windows 10 \(모든 버전\)

다음 운영 체제에는 Windows Server 2016 및 Windows 10의 DCB 설명서에 사용 되는 명령과 호환 되지 않는 이전 버전의 DCB가 포함 되어 있습니다.

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>하드웨어 요구 사항

다음은 DCB에 대 한 하드웨어 요구 사항 목록입니다.

- DCB\-지원 되는 이더넷 네트워크 어댑터\(s\) Windows Server 2016를 제공 하는 컴퓨터에 설치 해야 합니다.
- DCB\-가능 하드웨어 스위치를 네트워크에 배포 해야 합니다.


## <a name="install-dcb-in-windows-server-2016"></a>Windows Server 2016에 DCB 설치

다음 섹션을 사용 하 여 Windows Server 2016를 실행 하는 컴퓨터에 DCB를 설치할 수 있습니다.

**관리 자격 증명**

이러한 절차를 수행 하려면 **관리자**의 구성원 이어야 합니다.

### <a name="install-dcb-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 DCB 설치

Windows PowerShell을 사용 하 여 DCB을 설치 하려면 다음 절차를 사용할 수 있습니다.

1. Windows Server 2016를 실행 하는 컴퓨터에서 **시작**을 클릭 한 다음 windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭 합니다. 메뉴가 나타납니다. 메뉴에서 **자세히**를 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다. 메시지가 표시 되 면 컴퓨터에 대 한 관리자 권한이 있는 계정에 대 한 자격 증명을 입력 합니다. 관리자 권한으로 Windows PowerShell이 열립니다.
2. 다음 명령을 입력한 후 Enter 키를 누릅니다.

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>서버 관리자를 사용 하 여 DCB 설치

서버 관리자를 사용 하 여 DCB을 설치 하려면 다음 절차를 사용할 수 있습니다.

>[!NOTE]
>이 절차의 첫 번째 단계를 수행한 후에는 역할 및 기능 추가 마법사의 **시작 하기 전** 페이지가 표시 되지 않습니다 .이 페이지는 역할 및 기능 추가 마법사가 실행 될 때 **기본적으로이 페이지 건너뛰기** 를 선택 했습니다. **시작 하기 전** 페이지가 표시 되지 않는 경우 1 단계에서 3 단계로 건너뜁니다.

1. D c 1의 서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭 합니다. 역할 및 기능 추가 마법사가 열립니다.
2. **시작하기 전**에서 **다음**을 클릭합니다.
3. **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.
4. **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.
5. **서버 역할 선택**에서 **다음**을 클릭합니다.
6. **기능 선택**의 **기능**에서 **데이터 센터 브리징**을 클릭 합니다. DCB 필요한 기능을 추가할 것인지 묻는 대화 상자가 열립니다. **기능 추가**를 클릭합니다.
7. **기능 선택**, 클릭 **다음**합니다. 
8. 7.In **설치 선택 확인**에서 **설치**를 클릭 합니다. 설치 **진행률** 페이지에는 설치 과정 중에 상태가 표시 됩니다. 설치가 완료 되었다는 메시지가 표시 되 면 **닫기**를 클릭 합니다.

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>선택적\) QoS \(를 허용 하도록 커널 디버거를 구성 합니다.

 기본적으로 커널 디버거는 NetQos를 차단 합니다. DCB를 설치 하는 데 사용한 방법에 관계 없이 컴퓨터에 커널 디버거가 설치 되어 있는 경우 다음 명령을 실행 하 여 QoS를 사용 하도록 설정 하 고 구성할 수 있도록 디버거를 구성 해야 합니다.

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Windows 10에서 DCB 설치

Windows 10 컴퓨터에서 다음 절차를 수행할 수 있습니다.

이 절차를 수행 하려면 **관리자**의 구성원 이어야 합니다.

### <a name="install-dcb"></a>DCB 설치

1. **시작**을 클릭 하 고 아래로 스크롤하여 **Windows 시스템**을 클릭 합니다.
2. **제어판**을 클릭합니다. **제어판** 대화 상자가 열립니다.
3. **제어판**에서 **보기 기준**을 클릭 한 다음 **크게 아이콘** 또는 **작은 아이콘**중 하나를 클릭 합니다.
4. **프로그램 및 기능**을 클릭합니다. 프로그램 및 기능 대화 상자가 열립니다.
5. **프로그램 및 기능**의 왼쪽 창에서 **Windows 기능 사용/사용 안 함**을 클릭 합니다. **Windows 기능** 대화 상자가 열립니다.
6. **Windows 기능**에서 **데이터 센터 브리징**을 클릭 한 다음 **확인**을 클릭 합니다.

![Windows 기능 사용/사용 안 함 대화 상자](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


