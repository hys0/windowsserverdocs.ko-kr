---
title: Azure Site Recovery 서비스 통합
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/01/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 262701a6-8a97-4c4e-bfbf-9f8007c308d6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 94894cd9be06485bf842f96517172db709dbe93d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848744"
---
#<a name="azure-site-recovery-services-integration"></a>Azure Site Recovery 서비스 통합

>적용 대상: Windows Server 2016 Essentials

[Azure Site Recovery Services](https://docs.microsoft.com/azure/site-recovery/) Azure에서 백업 자격 증명 모음에는 virtual machines (VM)의 실시간 복제를 사용 하도록 설정 하는 Microsoft Azure에서 제공 하는 서비스입니다. 이벤트의 서버 또는 사이트 다운 되는 하드웨어 또는 다른 오류로 인해 있습니다 수 장애 조치 있는 백업 자격 증명 모음에 저장 된 VM 이미지 프로 비전 할 Azure에서 실행 중인 VM을 Azure로 합니다. Azure로 장애 조치 시 Azure 가상 네트워크를 함께 이전에 온-프레미스 서버에 연결 하는 Pc 클라이언트는 투명 하 게 연결할 Azure에서 실행 하는 서버.

Windows Server Essentials를 사용 하 여 Azure Site Recovery Services를 통합 하면 다음과 같은 방식으로 구성에서 시작 됩니다 [Azure 가상 네트워킹](azure-virtual-network-integration.md)합니다. **Microsoft 클라우드 서비스 통합** 대시보드에서 페이지에서 클릭 **Azure Site Recovery Services와 통합** 대시보드의 오른쪽에:

![Windows Server Essentials 대시보드 홈 페이지의 시작 탭을 보여 주는 스크린샷. 시작 탭의 Services 섹션을 선택한 후 문서를 나타내고 대시보드 Microsoft 클라우드 서비스 통합에서 Azure Recovery 현재 비활성화 되어 합니다.](media/azure-site-recovery-1.PNG)

Azure Virtual network 통합 및 Azure Backup 통합 하면 기존 Azure 계정을 사용 하 여 Azure에 로그인 하거나 새 계정을 만듭니다.

![Azure에 복제 사용 마법사를 Microsoft Azure 로그인 페이지를 보여 주는 스크린샷. 로그인 단추는 사용자가 Microsoft Azure에 아직 로그인 하지 때문에 표시 됩니다.](media/azure-site-recovery-2.PNG)

Azure를 성공적으로 로그인 한 후 VM을 저장 및 호스트 하려는 Azure 지역 뿐만 아니라 Azure Site Recovery 서비스를 사용 하 여 연결 하려는 구독을 요청 하는 화면이 표시 됩니다.

![Azure에 복제 사용 마법사를 Microsoft Azure 로그인 페이지를 보여 주는 스크린샷. 사용자가 Microsoft Azure에 로그인 하기 때문에이 페이지는 구독, 저장소 계정 및 지역을 선택 하는 옵션을 제공 합니다.](media/azure-site-recovery-3.PNG)

구독 및 지역 선택 후 새 탭에 표시 됩니다는 **Windows Server Essentials 대시보드** 호출 **Azure Recovery**합니다. 식별 하 여 지원 되는 호스트 서버를 열거 이루어집니다 네트워킹 검색 (Windows Server Hyper-v 2012 R2를 실행 이상) 개별 호스트에서 가상 머신 (게스트) 뿐만 아니라:

![Windows Server Essentials 대시보드의 Azure Recovery 페이지를 보여 주는 스크린샷. 두 Hyper-v 호스트는 이러한 호스트에서 실행 중인 가상 머신과 함께 표시 됩니다. RAM-h 1-7을 선택 하면 호스트에서 ramh157v01 라는 가상 머신과 Azure로 복제를이 가상 머신에 대 한 현재 비활성화 됩니다.](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>게스트 가상 컴퓨터 보호를 사용 하도록 설정

가상 컴퓨터에 Azure 복구 기간을 선택 하면 클릭할 수 있습니다 **Azure에 복제를 사용 하도록 설정** 준비 하 고 가상 머신 복사 대시보드의 오른쪽에™ Azure의 이미지:

![Azure에 복제를 사용 하도록 설정 대화 상자를 보여 주는 스크린샷. 호스트 추가 되 고 진행률 표시줄이 표시 됩니다.](media/azure-site-recovery-5.PNG)

이 과정에서 Azure Site Recovery 서비스 에이전트 vm 게스트의 이미지가 만들어지고, Azure에 이미지의 복제가 시작 됩니다 않았고 백업 자격 증명은 호스트 서버에 설치 됩니다. 복제 되 고 VM의 크기에 따라 복제 프로세스의 완료 시간 또는 며칠이 걸릴 수 있습니다. 최신 델타와 전체 VM 이미지는 Azure에 복제 될 때까지 장애 조치 작업을 사용할 수 없는 및 VM 보호 되지 않습니다. Azure Recovery 창에서 보호 상태 열에서 변경 되는 복제가 완료 되 면 **복제** 하 **Enabled**:

![Windows Server Essentials 대시보드의 Azure Recovery 페이지를 보여 주는 스크린샷. 두 Hyper-v 호스트는 이러한 호스트에서 실행 중인 가상 머신과 함께 표시 됩니다. 이 가상 머신에 RAM-h 1-2를 선택 하는 호스트에서 ramh12v02 라는 가상 머신과 Azure로 복제를 사용 중입니다.](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>게스트 VM에서 Azure로의 장애 조치

![Azure 페이지에 장애 조치 VM을 보여주는 스크린샷.](media/azure-site-recovery-7.PNG)

보호 실패 또는 실패를 Azure로 장애 조치 보호 된 가상 머신에서 실행 될 때까지 비즈니스 연속성을 유지 하기 위해 수행할 수 있는 호스트 서버의 가상 머신이 온-프레미스 가상 컴퓨터 또는 호스트 서버 복구는 제공 됩니다. 위의 그림에서으로 가지는 Azure Site Recovery Services를 사용 하 여에 지는 세 가지 유형의 장애 조치

-   **테스트 장애 조치** ƒA 좋은 재해 복구 계획 실제 재해 발생 시 최소 가동 중지 시간을 확인 하려면 재해 시뮬레이션 하는 기능을 통합 합니다. 테스트 장애 조치 복구 자격 증명 모음에 복제 되었는지와 Azure에서 실행 중인 가상 컴퓨터를 프로 비전 하 고, 비즈니스에 적용 되는 시나리오를 테스트 서버에 연결할 수 있습니다 하는 VM 이미지를 사용 합니다. 테스트 장애 조치 하는 동안 로컬 가상 머신을 계속 재해 복구 테스트를 사용 하는 동안 업무를 방해 하지 않도록 하는 것에 대 한 중단 없는 사용 하 여 실행 됩니다. 테스트 장애 조치 완료 되 면 가상 컴퓨터 프로 비전 해제 하 고 VHD를 삭제 하는 Azure 포털을 통해 테스트를 중지 됩니다. 전체 테스트 장애 조치 하는 동안 복구 자격 증명 모음에서 VM 이미지 사건 nothing 처럼 온사이트 VM에서 복제를 계속 합니다.

-   **계획 되지 않은 장애 조치** ƒAn 계획 되지 않은 장애 조치 보호 된 호스트 서버 또는 호스트 서버에서 실행 중인 VM을 사용 하 여 실제 오류가 있을 때 발생 합니다. 장애 조치 하거나 Windows Server Essentials 대시보드에서 수동으로 트리거되는 또는 실패 한 서버 자체에 Windows Server Essentials를 실행 하는 서버 이면 트리거할 수 있습니다 Azure Portal에서 직접. 이 경우 계획 되지 않은 장애 조치는 복구 자격 증명 모음에 복제 되었는지와 Azure에서 실행 중인 가상 컴퓨터를 프로 비전 하 고, 비즈니스에 적용 되는 시나리오를 테스트 서버에 연결할 수 있습니다 하는 VM 이미지를 사용 합니다. 온-프레미스 서버에 복원 되 면 VM 이미지를 로컬 서버까지 다시 복사 됩니다는 Azure Portal에서 수동 장애 복구를 트리거할 수 있습니다.

-   **계획 된 장애 조치** ƒA 계획 된 장애 조치는 하드웨어 유지 관리 등의 계획 된 작업을 수행 해야 합니다 서버 다운 정도 걸립니다 하는 경우에 수행할 수 있는 작업입니다. 계획된 된 장애 조치 시 동일한 프로세스를 사용 하면 Azure에서 복제 된 VM 이미지의 프로 비전 관련 하 여 이루어집니다. 그러나이 작업을 수행 하기 전에 로컬 서버에서에서 종료 되는 순차적 방식으로 종료 하기 전에 Azure에 모든 변경 내용이 복제 되도록 합니다. 계획된 된 유지 관리가 완료 되 면 Windows Server Essentials 대시보드 또는 Azure portal은 가져올 로컬 서버 및 다음 프로 비전 해제 하도록 Azure에 삭제 된 VM에서 장애 복구를 수동으로 트리거할 수 있습니다 합니다. VHD 파일입니다. 그런 다음 온-프레미스 VM에서 Azure로 복제는 정상적으로 다시 발생할 계속 됩니다.

위의 세 가지 경우 중 하나를 azure에 Windows Server Essentials 대시보드를 VM이 장애 조치는 경우 알아보겠습니다 새 VM을 아래 그림과 같이 실행 되는 Azure에서.

![Windows Server Essentials 대시보드의 Azure Recovery 페이지를 보여 주는 스크린샷. Essentials 및 Azure에서 실행 하는 명명 된 Essentials-테스트 나타냅니다는 호스트에 Azure로 장애 조치 가상 컴퓨터 호스트에 대 한 Azure로 복제 활성화 되었습니다.](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>참조
--------
[Windows Server Essentials를 사용 하 여 시작](get-started.md)
