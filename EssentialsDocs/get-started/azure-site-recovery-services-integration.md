---
title: "Azure 사이트 복구 서비스 통합"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 85e681cfc19241941773dd94f05ba59759aaf62a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
#<a name="azure-site-recovery-services-integration"></a>Azure 사이트 복구 서비스 통합

>Windows Server 2016 Essentials에 적용 됩니다.

[Azure 사이트 복구 서비스](https://azure.microsoft.com/en-us/documentation/services/site-recovery/) 백업 보관소 Azure에서은 서비스 여 VM (가상 컴퓨터)의 실시간 복제 Microsoft Azure에서 제공 됩니다. 서버 또는 사이트 하드웨어를 또는 기타 실패 인해 내려간 금액입니다는 하면 수 장애 조치 저장실 백업에 저장 된 VM 이미지는 Azure에서 실행 중인 VM로 프로 비전 않는 azure 합니다. 장애 조치를 azure 시는 Azure 가상 네트워크와 함께 클라이언트 이전에 온-프레미스 서버에 연결 하는 Pc 투명 하 게 서버에 연결 하는 Azure에서 실행 됩니다.

동일한 방식으로 구성 시작 Azure 사이트 복구 서비스 Windows Server Essentials의 통합 [Azure 가상 네트워킹](azure-virtual-network-integration.md)합니다. **Microsoft 클라우드 서비스 통합** 대시보드에서 페이지, 클릭 **Azure 사이트 복구 서비스와 통합** 대시보드의 오른쪽에:

![Windows Server Essentials 대시보드의 홈페이지에서 시작 탭을 보여 주는 스크린샷 합니다. 시작 탭 서비스 섹션을 선택한 후 하 고 Azure 복구를 현재 사용할 수 없음을 Microsoft 클라우드 서비스 통합 아래 대시보드 나타냅니다.](media/azure-site-recovery-1.PNG)

Azure 가상 네트워크 통합 및 Azure 백업 통합와 마찬가지로 Azure 하면 기존 Azure 계정으로 로그인 하거나 새 계정을 만들지 다음과 같습니다.

![Azure 복제 사용 마법사의 기호에 하려면 Microsoft Azure 페이지를 보여 주는 스크린샷 합니다. 사용자가 Microsoft Azure에 아직 로그인 하지 로그인 단추 표시 됩니다.](media/azure-site-recovery-2.PNG)

Azure를 성공적으로 로그인 한 후 사용자 VM를 저장 및 호스트 되는 Azure 지역 뿐만 아니라 Azure 사이트 복구 서비스에 연결 하려는 어떤 구독 묻는 화면이 표시 됩니다.

![Azure 복제 사용 마법사의 기호에 하려면 Microsoft Azure 페이지를 보여 주는 스크린샷 합니다. 사용자가 Microsoft Azure에 로그인 하기 때문에이 페이지 구독, 저장소 계정 및 지역을 선택 하기 위한 옵션을 제공 합니다.](media/azure-site-recovery-3.PNG)

구독을 지역 선택 후 새 탭에 나타납니다는 **Windows Server Essentials 대시보드** 라고 **Azure 복구**합니다. 네트워킹 검사를 식별 하 고 지원 되는 호스트 서버 열거 완료 (Windows Server Hyper-v 2012 r 2 실행 이상) 개별 호스트에서 가상 컴퓨터 (게스트) 뿐만 아니라:

![Windows Server Essentials 대시보드의 Azure 복구 페이지를 보여 주는 스크린샷 합니다. 두 명의 Hyper-v 호스트 이러한 호스트 실행 가상 컴퓨터와 함께 표시 됩니다. RAM-h 1-7 선택 되어 호스트 ramh157v01 이라는 가상 컴퓨터 및 복제 azure 가상 컴퓨터가에 대 한 현재 불가능 합니다.](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>게스트 가상 컴퓨터에 대 한 보호를 사용합니다.

가상 컴퓨터의 Azure 복구 창에 있는 선택 하면 눌러도 **azure 복제 사용** 대시보드를 준비 하 고 복사 가상 컴퓨터의 오른쪽에™ azure s 이미지:

![Azure 복제 사용 하도록 설정 대화 상자를 보여 주는 스크린샷 합니다. 진행률 표시줄 추가 되는 호스트도 표시 됩니다.](media/azure-site-recovery-5.PNG)

이 과정에서 Azure 사이트 복구 서비스 담당자는 VM 저장 되는 게스트 이미지를 만든 장소와 azure 이미지의 복제 시작 백업 저장소 호스트 서버에 설치 됩니다. 복제 VM의 크기에 따라 복제 프로세스를 완료 시간 또는 며칠이 걸릴 수 있습니다. 전체 VM 이미지 및 최신 델타 azure 복제는 시작할 때까지 작업 장애 조치를 사용할 수 없는 하 고 VM 보호 되지 않은 합니다. Azure 복구 창에 보호 상태 열에서 변경 되는 복제 완료 되 면 **복제** 에 **사용**:

![Windows Server Essentials 대시보드의 Azure 복구 페이지를 보여 주는 스크린샷 합니다. 두 명의 Hyper-v 호스트 이러한 호스트 실행 가상 컴퓨터와 함께 표시 됩니다. RAM-h 1-2 선택 되어 호스트 ramh12v02 이라는 가상 컴퓨터 및 복제 azure 가상 컴퓨터가에 대 한 사용 중입니다.](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>VM azure 게스트 장애

![Azure 페이지로 VM 장애 조치를 보여 주는 스크린샷 합니다.](media/azure-site-recovery-7.PNG)

보호 된 실패 또는 실패 장애 조치 azure에서 보호 된 가상 컴퓨터 실행 될 때까지 비즈니스 연속성을 유지 하기 위해 할 수 있는 호스트 서버 된 가상 컴퓨터에 프레미스 가상 컴퓨터 또는 호스트 서버는 복구 하 고 사용할 수 있습니다. 프로그램 위의 그림,으로 사이트 복구 서비스 Azure 지원 되는 세 가지 유형의 장애 조치는 다음과 같습니다.

-   **장애 조치를 테스트** ƒA 좋은 오류 복구 계획 시뮬레이트 장애 실제 장애 발생 했을 때의 업무 중단 되도록 하는 기능이 통합 되어 있습니다. 테스트 장애 조치 복구 보관소 복제 Azure에서 실행 중인 가상 컴퓨터도 제공 하 고 업무에 적용 되는 시나리오가 테스트 하는 서버에 연결할 수 있게 해 주는 VM 이미지를 걸립니다. 장애 조치를 테스트 하는 동안 계속 로컬 가상 컴퓨터 복구 장애 테스트 하는 동안 업무를 방해 하지에 대 한 방해 하지으로 실행 됩니다. 테스트 장애 조치 완료 되 면 VHD 삭제 하는 정보를 제거 가상 컴퓨터를 제공 하는 Azure 포털을 통해 테스트를 중지 됩니다. 전체 테스트 장애 조치 중 복구 보관소에서 VM 이미지 아무것도 적이 발생 하는 경우 현장 VM에서 복제 계속 합니다.

-   **예상치 못한 장애 조치** ƒAn 예상치 못한 장애 보호 되는 호스트 서버 또는 VM 호스트 서버에서 실행 되는 실제 오류가 있을 때 발생 합니다. 장애 조치 중 Windows Server Essentials 대시보드에서 수동으로 트리거됩니다 또는 자체 실패 서버 서버, Windows Server Essentials 실행 하는 경우 발생할 수 있습니다 Azure 포털에서 직접 합니다. 이 경우 계획 장애 조치는 복구 보관소 복제 Azure에서 실행 중인 가상 컴퓨터도 제공 하 고 업무에 적용 되는 시나리오가 테스트 하는 서버에 연결할 수 있게 해 주는 VM 이미지를 사용 합니다. 온-프레미스 서버 복원 되 면 수동 장애 로컬 서버 나타날 때까지 아래로 다시 VM 이미지 복사할는 Azure 포털에서 트리거되지 수 있습니다.

-   **장애 조치 계획** 계획 ƒA 장애 조치 같은 하드웨어 유지 관리 계획 된 활동을 수행 해야 아래로 서버 수행 되는 수행할 수 있는 작업은 합니다. 계획된 장애 조치 발생 하는 경우 동일한 프로세스를 사용 하면 관련 하 여 Azure에서 복제 VM 이미지의 공급 이루어집니다. 그러나 이렇게 전에 로컬 서버 종료 될 수 있도록 모든 변경 내용이 종료 되기 전에 azure 복제 순서 대로 합니다. Windows Server Essentials 대시보드 또는 것 가져올 로컬 서버 접속과 다음 Azure 및 삭제 VM 정보를 제거 준비 하는 Azure 포털 장애 계획 된 유지 관리 완료 되 면 수동으로 시작할 수는 있습니다. VHD 파일입니다. Azure 복제 온-프레미스 VM에서 다음 정상적으로 다시 발생 하 여 계속 합니다.

세 개의 위의 사례에 때 VM 장애 조치 되 Azure, Windows Server Essentials 대시보드에에서 표시 됩니다 새 VM Azure 그림 아래와 같이 실행 합니다.

![Windows Server Essentials 대시보드의 Azure 복구 페이지를 보여 주는 스크린샷 합니다. Azure에서 실행 명명된 Essentials 테스트 azure 위로 호스트에 실패 했음을 나타냅니다 가상 컴퓨터 및 Essentials 라는 호스트 azure 복제 설정 되었습니다.](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>참조 하십시오
--------
[Windows Server Essentials 시작](get-started.md)
