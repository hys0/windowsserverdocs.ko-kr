---
title: NPS(네트워크 정책 서버) 설치
description: Windows PowerShell 또는 Windows Server 2016의 역할 및 기능 추가 마법사를 사용 하 여 NPS (네트워크 정책 서버)를 설치 하려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 4842a4ab-70bb-4744-bea7-70f2ac892ad1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 25b8586d370865dd3ae4393c2536c348a5d0810f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396186"
---
# <a name="install-network-policy-server"></a>NPS(네트워크 정책 서버) 설치

Windows PowerShell 또는 역할 및 기능 추가 마법사를 사용 하 여 NPS (네트워크 정책 서버)를 설치 하려면이 항목을 사용할 수 있습니다. NPS는 네트워크 정책 및 액세스 서비스 서버 역할의 역할 서비스입니다.

> [!NOTE]
> 기본적으로 NPS는 설치된 모든 네트워크 어댑터의 포트 1812, 1813, 1645 및 1646에서 RADIUS 트래픽을 수신 대기합니다. NPS를 설치할 때 고급 보안이 포함 된 Windows 방화벽을 사용 하는 경우 인터넷 프로토콜 버전 6 \(IPv6\)와 IPv4 트래픽 모두에 대 한 설치 프로세스 중에 이러한 포트에 대 한 방화벽 예외가 자동으로 생성 됩니다. 네트워크 액세스 서버가 이러한 기본값 이외의 포트를 통해 RADIUS 트래픽을 보내도록 구성 된 경우에는 NPS 설치 중에 고급 보안이 설정 된 Windows 방화벽에서 생성 된 예외를 제거 하 고에서 사용 하는 포트에 대 한 예외를 만듭니다. RADIUS 트래픽

**관리 자격 증명**

이 절차를 완료하려면 **Domain Admins** 그룹의 구성원이어야 합니다.

## <a name="to-install-nps-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 NPS를 설치 하려면

Windows PowerShell을 사용 하 여이 절차를 수행 하려면 관리자 권한으로 Windows PowerShell을 실행 하 고 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

`Install-WindowsFeature NPAS -IncludeManagementTools`

## <a name="to-install-nps-by-using-server-manager"></a>서버 관리자를 사용 하 여 NPS를 설치 하려면

1.  NPS1의 서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.

2.  **시작하기 전**에서 **다음**을 클릭합니다.

    > [!NOTE]
    > 이전에 역할 및 기능 추가 마법사를 실행할 때 **항상 이 페이지 건너뛰기**를 선택한 경우에는 역할 및 기능 추가 마법사의 **시작하기 전** 페이지가 표시되지 않습니다.

3.  **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.

4.  **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.

5.  **서버 역할 선택**의 **역할**에서 **네트워크 정책 및 액세스 서비스**를 선택 합니다. 네트워크 정책 및 액세스 서비스에 필요한 기능을 추가 해야 하는지 여부를 묻는 대화 상자가 열립니다. **기능 추가**를 클릭 한 후 **다음** 을 클릭 합니다.

6.  **기능 선택**에서 **다음**을 클릭하고 **네트워크 정책 및 액세스 서비스**에서 제공된 정보를 검토한 후 **다음**을 클릭합니다.

7.  **역할 서비스 선택**에서 **네트워크 정책 서버**를 클릭합니다.  **네트워크 정책 서버에 필요한 기능 추가**에서 **기능 추가**를 클릭합니다. **다음**을 클릭합니다.

8.  **설치 선택 확인**에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 클릭합니다. 이 선택을 확인하라는 메시지가 표시되면 **예**를 클릭한 다음 **설치**를 클릭합니다. 설치 프로세스가 진행되는 동안 설치 진행률 페이지에 상태가 표시됩니다. 프로세스가 완료 되 면 " *computername*에서 설치가 완료 되었습니다." 라는 메시지가 표시 됩니다. 여기서 *Computername* 은 네트워크 정책 서버를 설치한 컴퓨터의 이름입니다. **닫기**를 클릭합니다.

자세한 내용은 [NPSs 관리](nps-manage-servers.md)를 참조 하세요.