---
title: 네트워크 정책 서버 설치
description: 이 항목을 사용 하 여 네트워크 NPS 정책 서버 () Windows Server 2016에서 Windows PowerShell 또는 역할 추가 및 기능 마법사 중 하나를 사용 하 여 설치
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4842a4ab-70bb-4744-bea7-70f2ac892ad1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b76654fa01b68b5a8c9ea1efc80dfbc47e6a62f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-network-policy-server"></a>네트워크 정책 서버 설치

Windows PowerShell 또는 역할 추가 및 기능 마법사 중 하나를 사용 하 여 네트워크 NPS 정책 서버 ()를 설치 하려면이 항목을 사용할 수 있습니다. NPS는 액세스 서비스 및 네트워크 정책 서버 역할의 역할 서비스입니다.

> [!NOTE]
> 기본적으로 NPS RADIUS 트래픽을 모든 설치 된 네트워크 어댑터에 1812 민 1813, 1645 1646 포트에서 수신합니다. 고급 보안이 포함된 Windows 방화벽 NPS 설치할 때 사용 하는 경우 이러한 포트에 대 한 예외 방화벽 인터넷 프로토콜 버전 6 \(IPv6\) 및 IPv4 교통 설치 과정에서 자동으로 만들어집니다. 네트워크 액세스 서버 RADIUS 교통 이러한 기본값 이외의 포트를 통해 전송 하도록 구성 된, NPS 설치 하는 동안 고급 보안이 포함된 Windows 방화벽에서 만든 예외 제거한 포트 RADIUS 교통량 사용 하려면에 대 한 예외 만듭니다.

**관리자 자격 증명**

이 절차를 완료 하려면의 회원 있어야는 **도메인 관리자** 그룹입니다.

## <a name="to-install-nps-by-using-windows-powershell"></a>NPS Windows PowerShell를 사용 하 여 설치

Windows PowerShell를 Windows PowerShell을 관리자 권한으로 실행을 사용 하 여이 절차를 수행 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

`Install-WindowsFeature NPAS -IncludeManagementTools`

## <a name="to-install-nps-by-using-server-manager"></a>NPS 서버 관리자를 사용 하 여 설치

1.  서버 관리자 NPS1 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. 역할 추가 및 기능 마법사가 열립니다.

2.  **시작 하기 전에**, 클릭 **다음**합니다.

    > [!NOTE]
    > **시작 하기 전에** 이전 선택한 경우 역할 추가 및 기능 마법사의 페이지가 표시 되지 않으면 **이 페이지 기본적으로 건너뛰기** 역할 추가 및 기능 마법사가 실행 될 때 합니다.

3.  **설치 유형을 선택**, 되도록 **역할 또는 기능 기반 설치** 을 선택한 다음 클릭 **다음**합니다.

4.  **선택 대상 서버**, 되도록 **서버 풀에서 서버를 선택** 을 선택 합니다. **서버 풀**, 로컬 컴퓨터 선택 되어 있는지 확인 합니다. 클릭 **다음**합니다.

5.  **서버 역할 선택**에 **역할**선택 **액세스 서비스 및 네트워크 정책**합니다. 대화 상자가 경우 네트워크 정책 및 액세스 서비스에 필요한 기능을 추가 해야 묻는 열립니다. 클릭 **기능 추가**을 차례로 클릭 하 고 **다음**

6.  **기능을 선택**, 클릭 **다음**의 **액세스 서비스 및 네트워크 정책**, 클릭 한 다음을 제공 하는 정보를 검토 **다음**합니다.

7.  **역할 서비스 선택**, 클릭 **네트워크 정책 서버**합니다.  **네트워크 정책 서버에 필요한 기능을 추가**, 클릭 **기능 추가**합니다. 클릭 **다음**합니다.

8.  **설치 선택을 확인**, 클릭 **필요한 경우 자동으로 목적지 서버를 다시 시작**합니다. 이 선택을 확인 하는 메시지가 나타나면 클릭 **예**을 차례로 클릭 하 고 **설치**합니다. 설치 진행률 페이지 설치 과정에서 상태를 표시합니다. 때 프로세스가 완료 되 면 메시지 "에 설치 했습니다 *ComputerName*" 표시 되 면 여기서 *ComputerName* 네트워크 정책 서버 설치 하는 컴퓨터의 이름입니다. 클릭 **닫기**합니다.

자세한 내용은 참조 [NPS 서버 관리](nps-manage-servers.md)합니다.