---
title: Windows 관리 센터를 사용 하 여 Azure Virtual Machines 배포
description: Windows 관리 센터를 사용 하 여 Azure virtual machines 배포 Windows 관리 센터 관리 시나리오의 일부로 Azure virtual machines 구성
ms.technology: manage
ms.topic: article
author: nedpyle
ms.author: nedpyle
manager: jgerend
ms.date: 01/28/2020
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 2249a69f60fe87758c74a58aa13b47124da41361
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319378"
---
# <a name="deploy-azure-virtual-machines-from-within-windows-admin-center"></a>Windows 관리 센터 내에서 Azure virtual machines 배포

>적용 대상: Windows 관리 센터, Windows 관리 센터 미리 보기

Windows 관리 센터 버전 1910을 사용 하 여 Azure 가상 컴퓨터를 배포할 수 있습니다. 이렇게 하면 VM 배포가 [Storage Migration Service](../../../storage/storage-migration-service/overview.md) 및 [storage 복제본](../../../storage/storage-replica/storage-replica-overview.md)과 같은 Windows 관리 센터의 관리 되는 워크 로드에 통합 됩니다. 워크 로드를 배포 하기 전에 직접 Azure Portal에서 새 서버 및 Vm을 구축 하는 대신, 필요한 단계 및 구성이 누락 될 수 있습니다. Windows 관리 센터에서 Azure VM을 배포 하 고, 저장소를 구성 하 고, 도메인에 가입 하 고, 역할을 설치 하 고, 그런 다음 분산 시스템을 설정 합니다. Windows 관리 센터 연결 페이지에서 작업 없이 새 Azure Vm을 배포할 수도 있습니다.

Windows 관리 센터는 또한 다양 한 Azure 서비스를 관리 합니다. [Windows 관리 센터에서 사용할 수 있는 Azure 통합 옵션에 대해 자세히 알아보세요](../plan/azure-integration-options.md).

## <a name="scenarios"></a>시나리오

Windows 관리 센터 버전 1910 Azure VM 배포는 다음과 같은 시나리오를 지원 합니다.

- [저장소 마이그레이션 서비스](../../../storage/storage-migration-service/overview.md)
- [스토리지 복제본](../../../storage/storage-replica/storage-replica-overview.md)
- [새 독립 실행형 서버 (역할 없음)](index.md#extend-on-premises-capacity-with-azure)

## <a name="requirements"></a>요구 사항

Windows 관리 센터 내에서 새 Azure VM을 만들려면 다음이 필요 합니다.

- [Azure 구독](https://azure.microsoft.com).
- [Azure에 등록 된 Windows 관리 센터 게이트웨이](azure-integration.md)
- 만들기 권한이 있는 기존 [Azure 리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) 입니다.
- 기존 [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 및 서브넷.
- 가상 네트워크 및 서브넷에 연결 된 azure [Express 경로](https://azure.microsoft.com/services/expressroute/) 또는 azure [VPN 솔루션](https://azure.microsoft.com/services/vpn-gateway/) 은 azure vm에서 온-프레미스 클라이언트, 도메인 컨트롤러, Windows 관리 센터 컴퓨터 및이 VM과의 통신을 요구 하는 모든 서버에 연결 하 여 작업 배포의 일부로 사용할 수 있습니다. 예를 들어 저장소 마이그레이션 서비스를 사용 하 여 저장소를 Azure VM으로 마이그레이션하려면 orchestrator 컴퓨터와 원본 컴퓨터가 둘 다 마이그레이션할 대상 Azure VM에 연결할 수 있어야 합니다.

## <a name="usage"></a>사용법

Azure VM 배포 단계와 마법사는 시나리오에 따라 달라 집니다. 전반적인 시나리오에 대 한 자세한 내용은 워크 로드 설명서를 참조 하세요.

### <a name="deploying-azure-vms-as-part-of-storage-migration-service"></a>저장소 마이그레이션 서비스의 일부로 Azure Vm 배포

1. Windows 관리 센터 내의 *Storage Migration Service* 도구에서 하나 이상의 원본 서버에 대 한 인벤토리를 수행 합니다.
2. *데이터 전송* 단계를 완료 한 후 *대상 지정* 페이지에서 **새 Azure vm 만들기** 를 선택 하 고 **VM 만들기**를 클릭 합니다.<br><br>
이는 Windows Server 2012 R2, Windows Server 2016 또는 Windows Server 2019 Azure VM을 마이그레이션의 대상으로 선택 하는 단계별 만들기 도구를 시작 합니다. Storage Migration Service는 원본과 일치 하도록 권장 되는 VM 크기를 제공 하지만, **모든 크기 보기**를 클릭 하 여 재정의할 수 있습니다.
<br><br>또한 원본 서버 데이터는 새 Azure VM을 Active Directory 도메인에 가입 하는 것 뿐만 아니라 관리 디스크와 해당 파일 시스템을 자동으로 구성 하는 데 사용 됩니다. VM이 Windows Server 2019 (권장) 인 경우 Windows 관리 센터에서 저장소 마이그레이션 서비스 프록시 기능을 설치 합니다. Azure VM을 만든 후에는 Windows 관리 센터에서 일반 저장소 마이그레이션 서비스 전송 워크플로로 돌아갑니다.  

Storage Migration Service를 사용 하 여 Azure Vm으로 마이그레이션하는 방법을 보여 주는 비디오는 다음과 같습니다.

> [!VIDEO https://www.youtube-nocookie.com/embed/k8Z9LuVL0xQ] 

### <a name="deploying-azure-vms-as-part-of-storage-replica"></a>저장소 복제본의 일부로 Azure Vm 배포

1. Windows 관리 센터 내의 *저장소 복제본* 도구 *파트너 관계* 탭에서 **새로 만들기** 를 선택한 다음 *다른 서버와 복제* 에서 **새 Azure VM 사용** 을 선택 하 고 **다음**을 선택 합니다.
2. 원본 서버 정보 및 복제 그룹 이름을 지정 하 고 **다음**을 선택 합니다.<br><br>
그러면 Windows Server 2016 또는 Windows Server 2019 Azure VM을 마이그레이션 원본의 대상으로 자동으로 선택 하는 프로세스가 시작 됩니다. Storage Migration Service는 원본에 맞게 VM 크기를 권장 하지만 **모든 크기 보기**를 선택 하 여이를 재정의할 수 있습니다. 인벤토리 데이터는 새 Azure VM을 Active Directory 도메인에 가입 하는 것 뿐만 아니라 관리 디스크와 해당 파일 시스템을 자동으로 구성 하는 데 사용 됩니다. 
3. Windows 관리 센터에서 Azure VM을 만든 후 복제 그룹 이름을 제공 하 고 **만들기**를 선택 합니다. 그러면 Windows 관리 센터에서 일반 저장소 복제본 초기 동기화 프로세스를 시작 하 여 데이터 보호를 시작 합니다.

저장소 복제본을 사용 하 여 Azure Vm에 복제 하는 방법을 보여 주는 비디오는 다음과 같습니다.

> [!VIDEO https://www.youtube-nocookie.com/embed/_VqD7HjTewQ] 

### <a name="deploying-a-new-standalone-azure-vm"></a>새 독립 실행형 Azure VM 배포

1. Windows 관리 센터의 *모든 연결* 페이지에서 **추가**를 선택 합니다.
2. *AZURE VM* 섹션에서 **새로 만들기**를 선택 합니다.<br><br> 이를 통해 Windows Server 2012 R2, Windows Server 2016 또는 Windows Server 2019 Azure VM을 선택 하 고, 크기를 선택 하 고, 관리 디스크를 추가 하 고, 선택적으로 Active Directory 도메인에 가입할 수 있는 단계별 작성 도구를 시작 합니다.

Windows 관리 센터를 사용 하 여 Azure Vm을 만드는 방법을 보여 주는 비디오는 다음과 같습니다.

> [!VIDEO https://www.youtube-nocookie.com/embed/__A8J9aC_Jk] 
