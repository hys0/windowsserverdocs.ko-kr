---
title: Azure Stack HCI 개요
description: Azure Stack HCI는 정품 확인된 하드웨어를 사용하여 온-프레미스에서 가상화된 워크로드를 실행하고, 선택적으로 클라우드 기반 백업, 사이트 복구 등을 위해 Azure 서비스에 연결하는 하이퍼 컨버전스 Windows Server 2019 클러스터입니다. Azure Stack HCI 솔루션은 Microsoft에서 정품 확인된 하드웨어를 사용하여 최적 성능과 안정성을 보장하며 NVMe 드라이브, 영구 메모리, RDMA(원격 직접 메모리 액세스) 네트워킹 같은 기술에 대한 지원을 포함합니다.
ms.technology: storage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 05/22/2019
ms.openlocfilehash: 92d600eeb833cd70bd714702b1fd950c4fe2cd87
ms.sourcegitcommit: b190fac4bfa5599751a60d3fc3b4c4a64dd9afd7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66008973"
---
# <a name="azure-stack-hci-overview"></a>Azure Stack HCI 개요

>적용 대상: 시작

Azure Stack HCI는 정품 확인된 하드웨어를 사용하여 온-프레미스에서 가상화된 워크로드를 실행하고, 선택적으로 클라우드 기반 백업, 사이트 복구 등을 위해 Azure 서비스에 연결하는 하이퍼 컨버전스 Windows Server 2019 클러스터입니다. Azure Stack HCI 솔루션은 Microsoft에서 정품 확인된 하드웨어를 사용하여 최적 성능과 안정성을 보장하며 NVMe 드라이브, 영구 메모리, RDMA(원격 직접 메모리 액세스) 네트워킹 같은 기술에 대한 지원을 포함합니다.

Azure Stack HCI는 다음과 같은 여러 제품을 결합하는 솔루션입니다.

- OEM 파트너의 하드웨어

- Windows Server 2019 Datacenter Edition

- Windows Admin Center

- Azure 서비스(선택 사항)

![Azure Stack HCI는 광범위한 하드웨어 파트너가 제공하는 Microsoft의 하이퍼 컨버전스 솔루션입니다.](media/AS_HCI_solution.png)

Azure Stack HCI는 광범위한 하드웨어 파트너가 제공하는 Microsoft의 하이퍼 컨버전스 솔루션입니다. Azure Stack HCI가 요구에 가장 부합하는 솔루션인지 판단하기 위해 하이퍼 컨버전스 솔루션에 대한 다음 시나리오를 고려해 봅니다.

- **노후한 하드웨어를 새로 고칩니다.** 오래된 서버 및 스토리지 인프라를 교체하고 기존 IT 기술과 도구를 사용하여 Windows 및 Linux 가상 머신을 온-프레미스와 에지에서 실행합니다.

- **가상화된 워크로드를 통합합니다.** 효율적인 하이퍼 컨버전스 인프라에 레거시 앱을 통합합니다. Microsoft Azure 등, 대규모 데이터센터를 실행하기 위한 것과 같은 수준의 클라우드 효율성을 활용합니다.

- **하이브리드 클라우드 서비스를 위해 Azure에 연결합니다.** 오프사이트 백업, 사이트 복구, 클라우드 기반 모니터링 등, Azure의 클라우드 관리 및 보안 서비스에 대한 액세스를 간소화합니다.

## <a name="the-azure-stack-family"></a>Azure Stack 제품군

Azure Stack HCI는 Azure 및 Azure Stack 제품군의 일원으로, Azure Stack과 동일한 소프트웨어 정의 컴퓨팅, 스토리지 및 네트워킹 소프트웨어를 사용합니다. 다음은 다양한 솔루션에 대한 요약입니다.

- [Azure](https://azure.microsoft.com) - 공용 클라우드 서비스 사용
- [Azure Stack](https://azure.microsoft.com/overview/azure-stack) - 온-프레미스 클라우드 서비스 운영
- [Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci) - 선택적으로 Azure에 연결하여 온-프레미스에서 가상화된 앱 실행

![Azure 및 Azure Stack은 클라우드 서비스를 실행하고, Azure Stack HCI가 가상화된 애플리케이션을 온-프레미스에서 실행](media/azure_family.png)

|Azure: 공용 클라우드 서비스 사용|Azure Stack: 온-프레미스 클라우드 서비스 운영|Azure Stack HCI: 온-프레미스에서 가상화된 앱 실행|
|-----------------|-----------------|-----------------|
|기존 앱을 마이그레이션 및 현대화하고 새 클라우드 네이티브 앱을 빌드하는 주문형 셀프 서비스 컴퓨팅 리소스용입니다.|연결이 끊어지거나 규정 요구 사항에 부합하면 일관된 Azure 서비스를 온-프레미스에서 사용하여 에지에서 클라우드 애플리케이션을 빌드 및 실행합니다.| 가상화된 애플리케이션을 온-프레미스에서 실행하고, 노후한 서버 인프라를 교체 및 통합하며, 클라우드 서비스를 위해 Azure에 연결합니다.|
|전세계 54개 지역에서 100여 개의 서비스를 사용할 수 있습니다.|Azure VMs For Windows 및 Linux, Azure Web Apps 및 Functions, Azure Key Vault, Azure Resource Manager, Azure Marketplace, Containers, Azure IoT 및 Event Hubs, 관리 도구(플랜, 제품, RBAC)|Azure 서비스에 대한 통합 액세스 및 관리를 위해 Windows Server 2019 및 Windows Admin Center에서 Hyper V 및 Storage Spaces Direct가 제공하는 정품 확인된 HCI 솔루션입니다.|

자세한 정보:

- 자세한 정보는 [Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci) 솔루션 웹 사이트에서 확인하세요.
- Microsoft 전문가 Jeff Woolsey와 Vijay Tewari가 [새 Azure Stack HCI 솔루션](https://aka.ms/AzureStackOverviewVideo)에 대해 설명합니다.

## <a name="hyperconverged-efficiencies"></a>하이퍼 컨버전스 효율성

Azure Stack HCI 솔루션은 업계 표준 x86 서버 및 구성 요소에서 고도로 가상화된 컴퓨팅, 스토리지 및 네트워킹을 통합합니다. 동일한 클러스터에서 리소스를 결합하면 배포, 관리 및 확장이 용이해집니다. 원하는 명령줄 자동화 또는 Windows Admin Center를 사용하여 관리합니다.

Microsoft 클라우드의 기본 하이퍼바이저 기술인 Hyper-V와, NVMe, 영구 메모리, RDMA(원격 디렉터리 메모리 액세스) 네트워킹을 기본 지원하는 Storage Spaces Direct 기술로 서버 애플리케이션을 위한 업계 최고 수준의 가상 머신 성능을 달성할 수 있습니다.

미사용 및 전송 중인 데이터에 대해 보호되는 가상 머신, 네트워크 마이크로 분할, 네이티브 암호화를 통해 앱과 데이터를 안전하게 유지합니다.

## <a name="hybrid-capabilities"></a>하이브리드 기능

공용 클라우드에서 하이퍼 컨버전스 인프라 플랫폼을 통해 함께 작동하는 클라우드 및 온-프레미스를 활용할 수 있습니다. 팀에서는 다음과 같이 Azure 인프라 관리 서비스에 대한 기본 제공 통합을 통해 클라우드 기술을 구축할 수 있습니다.

- Azure Site Recovery - 고가용성과 DRaaS(Disaster Recovery as a Service)를 수행합니다.

- Azure Monitor - AI가 제공하는 고급 분석을 통해 애플리케이션, 네트워크 및 인프라 전체에서 발생하는 일을 추적하는 중앙 집중식 허브입니다.

- Cloud Witness - Azure를 클러스터 쿼럼에 대한 경량 타이 브레이커로 사용합니다.

- Azure Backup - 오프 사이트 데이터를 보호하고 랜섬웨어로부터 보호합니다.

- Azure Update Management - Azure 및 온-프레미스에서 실행되는 Windows VM에 대한 업데이트 평가와 업데이트 배포를 수행합니다.

- Azure Network Adapter - 지점-사이트 간 VPN을 통해 Azure의 VM과 온-프레미스 리소스를 연결합니다.

- Azure 파일 동기화를 사용하여 파일 서버를 클라우드에 동기화합니다.

세부 정보는 [Windows Server를 Azure 하이브리드 서비스에 연결](..\manage\windows-admin-center\azure\index.md)을 참조하세요.

## <a name="management-tools-and-system-center"></a>관리 도구 및 System Center

Azure Stack HCI는 Azure Stack과 동일한 가상화와 소프트웨어 정의 스토리지 및 네트워킹 소프트웨어를 사용합니다. Azure Stack HCI에서는 클러스터에 대한 전체 관리 권한을 갖습니다. 즉 [Windows Admin Center](..\manage\windows-admin-center\overview.md), [System Center](https://www.microsoft.com/cloud-platform/system-center)와 [Hyper-V](../virtualization/hyper-v/hyper-v-on-windows-server.md), [Storage Spaces Direct](..\storage\storage-spaces\storage-spaces-direct-overview.md), PowerShell 및 타사 도구(예: 5Nine Manager)의 모든 기능을 사용할 수 있습니다.

Microsoft Azure는 Windows Server에 포함된 동일한 Windows Server 및 Hyper-V 플랫폼에서 실행됩니다. Windows Server 및 System Center에는 Microsoft Azure 같은 세계적인 규모의 데이터 센터 네트워크 운영에 대한 Microsoft의 경험으로부터의 개선 사항 및 모범 사례가 포함되어 있으며 이는 소프트웨어로 설계된 네트워킹 기술을 사용할 때 유연성, 자동화 및 제어를 위해 동일한 기술을 배포할 수 있도록 합니다.

System Center VMM(Virtual Machine Management)과 System Center Operations Manager로 인프라를 배포 및 관리합니다. VMM을 사용하여 가상 머신을 만들어 프라이빗 클라우드에 배포하는 데 필요한 리소스를 프로비저닝 및 관리합니다. Operations Manager에서는 기업 전체의 서비스, 디바이스, 작업을 모니터하여 즉각적으로 조치할 수 있게 문제를 식별합니다.

## <a name="hardware-partners"></a>하드웨어 파트너

15개 파트너로부터 Windows Server 2019를 실행하는 정품 확인된 Azure Stack HCI 솔루션을 구매할 수 있습니다. 사용자가 원하는 Microsoft 파트너가 긴 설계 및 빌드 시간 없이 실행할 수 있게 지원하며 구현 및 지원 서비스를 위한 단일 연락 지점을 제공합니다.

[Azure Stack HCI 웹 사이트](https://azure.microsoft.com/overview/azure-stack/hci)에서 현재 다음과 같은 Microsoft 파트너에서 제공하는 70여 Azure Stack HCI 솔루션을 확인하세요. ASUS, Axellio, bluechip, DataON, Dell EMC, Fujitsu, HPE, Hitachi, Huawei, Lenovo, NEC, primeLine Solutions, QCT, SecureGUARD 및 Supermicro

## <a name="faq"></a>FAQ

### <a name="what-do-azure-stack-and-azure-stack-hci-solutions-have-in-common"></a>Azure Stack과 Azure Stack HCI 솔루션의 공통점

Azure Stack HCI 솔루션은 Azure Stack과 동일한 Hyper-V 기반 소프트웨어 정의 컴퓨팅, 스토리지 및 네트워크 기술을 제공합니다. 두 제품 모두 안정성과 기본 하드웨어 플랫폼과의 호환성을 위해 엄격한 테스트 및 유효성 검사 기준에 부합합니다.

### <a name="how-are-they-different"></a>어떻게 다를까요?

Azure Stack에서는 온-프레미스 클라우드 서비스를 운영합니다. Azure IaaS 및 PaaS 서비스를 온-프레미스에서 실행하여 어디서나 일관되게 클라우드 애플리케이션을 빌드 및 실행하고 Azure Portal을 통해 온-프레미스로 관리할 수 있습니다.

Azure Stack HCI에서는 가상화된 워크로드를 온-프레미스로 실행하고 Windows Admin Center 및 친숙한 Windows Server 도구를 통해 관리합니다. 클라우드 기반 사이트 복구, 모니터링 등을 비롯한 하이브리드 시나리오에서 선택적으로 Azure에 연결할 수 있습니다.

### <a name="why-is-microsoft-bringing-its-hci-offering-to-the-azure-stack-family"></a>Microsoft가 Azure Stack 제품군에 HCI를 제공하는 이유는 무엇인가요?

Microsoft의 하이퍼 컨버전스 기술은 이미 Azure Stack의 기초입니다.

많은 Microsoft 고객이 복잡한 IT 환경에 직면하고 있기에 우리는 적합한 비즈니스 요구에 적합한 기술로 고객에게 맞는 솔루션을 제공하고자 합니다. Azure Stack HCI는 이전에 하드웨어 파트너가 제공하던 Windows Server 2016 기반 WSSD(Windows Server Software-Defined) 솔루션의 진화된 버전입니다. 인프라 관리 서비스를 위해 원활히 Azure에 연결되는 새 옵션을 제공하기 시작했으므로 Azure Stack 제품군에 포함한 것입니다.

### <a name="does-azure-stack-hci-need-to-be-connected-to-azure"></a>Azure Stack HCI를 Azure에 연결해야 하나요?

아니요, 완전히 선택 사항입니다. 오프사이트 백업 및 재해 복구, 클라우드 기반 모니터링 및 업데이트 관리 같은 하이브리드 시나리오에서 Azure 통합을 활용할 수 있으나 선택 사항입니다. 연결을 끊은 상태로 실행하고자 하거나 그래야 하는 상황이 충분히 있을 수 있고 이를 수용합니다.

### <a name="how-does-azure-stack-hci-relate-to-windows-server"></a>Azure Stack HCI와 Windows Server는 어떤 관계가 있나요?

Windows Server 2019는 거의 모든 Azure 제품의 기초입니다. Windows Server에서 중요한 모든 기능이 계속하여 탑재 및 지원될 것입니다. Azure Stack HCI는 파트너가 제공하는 Microsoft 정품 확인 하드웨어를 통해 HCI를 온-프레미스에 배포하는 데 권장되는 방법입니다.

### <a name="will-i-be-able-to-upgrade-from-azure-stack-hci-to-azure-stack"></a>Azure Stack HCI에서 Azure Stack으로 업그레이드할 수 있나요? 

아니요. 그러나 Azure Stack HCI의 워크로드를 Azure Stack 또는 Azure에 마이그레이션할 수 있습니다.

### <a name="what-azure-services-can-i-connect-to-azure-stack-hci"></a>Azure Stack HCI에 연결할 수 있는 Azure 서비스는 무엇인가요?

Azure Stack HCI에 연결할 수 있는 Azure 서비스의 업데이트된 목록은 [Windows Server를 Azure 하이브리드 서비스에 연결](../azure-hybrid-services/index.md)을 참조하세요.

### <a name="how-does-the-cost-of-azure-stack-hci-compare-to-azure-stack"></a>Azure Stack HCI의 비용은 Azure Stack과 비교하여 어떤가요? 

Azure Stack은 서비스와 지원을 포함하는 완전 통합 시스템으로 판매됩니다. 직접 관리하는 시스템의 형태로, 또는 파트너로부터 완전 관리형 서비스 형태로 Azure Stack을 구매할 수 있습니다. 기본 시스템 외에도 Azure Stack이나 Azure에서 실행되는 Azure 서비스는 종량제 기준으로 판매됩니다.

Azure Stack HCI 솔루션은 기존 구매 모델을 따릅니다. Azure Stack HCI 파트너로부터 정품 확인된 하드웨어와, 여러 기존 채널로부터 소프트웨어(소프트웨어 정의 데이터 센터 기능을 포함한 Windows Server 2019 Datacenter Edition 및 Windows Admin Center)를 구매할 수 있습니다. Windows Admin Center를 사용할 수 있는 Azure 서비스는 Azure 구독을 통해 결제합니다.

### <a name="how-do-i-buy-azure-stack-hci-solutions"></a>Azure Stack HCI 솔루션을 구입하는 방법

다음 단계를 수행하십시오.

1. 원하는 하드웨어 파트너로부터 Microsoft 정품 확인된 하드웨어 시스템을 구매합니다.
1. 클라우드 서비스를 위한 Azure 연결 및 관리를 위해 Windows Server 2019 Datacenter Edition 및 Windows Admin Center 설치
1. 선택적으로 Azure 계정을 사용하여 클라우드 기반 관리 및 보안 서비스를 워크로드에 연결합니다.

![Azure Stack HCI 솔루션을 구입하려면 필요에 가장 잘 맞는 하드웨어 파트너와 구성을 선택합니다.](media/howbuy_ashci.png)

## <a name="compare-azure-stack-and-azure-stack-hci"></a>Azure Stack 및 Azure Stack HCI 비교

조직의 디지털 변환 과정에서 공용 클라우드 서비스를 사용하여 최신 아키텍처를 기반으로 빌드하고 레거시 앱을 새로 고치는 게 더 빠르게 진행되는 것을 확인할 수 있습니다. 그러나 기술 및 규정상의 장애 같은 이유로 많은 워크로드가 온-프레미스에 그대로 남게 됩니다. 다음 표를 통해 어떤 Microsoft 하이브리드 클라우드 전략이 무엇을 제공하여 요구에 어떻게 부합하고 해당하는 워크로드에서 클라우드 혁신을 제공하는지 판단할 수 있습니다.

|Azure 스택|Azure Stack HCI|
|--------|-------|
|새로운 기술, 혁신적인 프로세스|동일한 기술, 친숙한 프로세스|
|데이터 센터의 Azure 서비스|데이터 센터를 Azure 서비스에 연결|

### <a name="when-to-use-azure-stack"></a>Azure Stack을 사용하는 경우

|Azure 스택|Azure Stack HCI|
|--------|-------|
|강력한 격리 및 정확한 사용자 추적과 다중 공동 배치 테넌트에 대한 환불을 통해 셀프 서비스 IaaS(Infrastructure-as-a-Service)에 Azure Stack을 사용합니다. 서비스 공급자 및 엔터프라이즈 프라이빗 클라우드에 적합합니다. Azure Marketplace의 템플릿입니다.|Azure Stack HCI는 다중 테넌트 지원을 기본적으로 적용하거나 제공하지 않습니다.|
|Azure Stack을 사용하여 온-프레미스의 Web Apps, Functions 또는 Event Hubs 같은 PaaS(Platform-as-a-Service) 기반의 앱을 개발 및 실행합니다. 이러한 서비스는 Azure에서와 정확히 같게 Azure Stack에서 실행되므로 일관된 하이브리드 개발 및 런타임 환경을 제공합니다.|Azure Stack HCI는 온-프레미스에서 PaaS 서비스를 실행하지 않습니다.
|Azure Stack을 사용하여 코드 방식 인프라, CI/CD(지속적인 통합 및 지속적인 배포) 등과 같은 DevOps 업무와 일관된 Azure VM 확장 등의 편리한 기능으로 앱 배포 및 운영을 현대화합니다. 개발 및 DevOps 팀에 적합합니다.|Azure Stack HCI는 기본적으로 DevOps 도구를 포함하지 않습니다.

### <a name="when-to-use-azure-stack-hci"></a>Azure Stack HCI를 사용하는 경우

|Azure 스택|Azure Stack HCI|
|---------------|---------------|
|Azure Stack에는 최소 4개의 노드와 자체 네트워크 스위치가 필요합니다.|Azure Stack HCI를 사용하여 ROBO(원격 오피스/지사)의 공간을 최소화합니다. 단 두 개의 서버 노드와 스위치 없는 연속 네트워킹에서 출발하여 최고의 단순성과 경제성을 구현합니다. 하드웨어 제품은 4개 드라이브, 64GB 메모리부터 있으며 노드당 $10k 미만으로 가능합니다.
|Azure Stack은 Azure와의 일관성을 위해 Hyper V 구성 및 기능을 제한합니다.|Exchange, SharePoint, SQL Server 같은 클래식 엔터프라이즈 앱을 Hyper-V로 가상화 하는 과정에서 군더더기를 없애거나 파일 서버, DNS, DHCP, IIS, AD 같은 Windows Server 기능을 가상화하는 데 Azure Stack HCI를 사용합니다. 보호된 VM 등, 모든 Hyper-V 기능에 제한 없이 액세스합니다.|
|Azure Stack은 이러한 인프라 기술을 노출하지 않습니다.|Azure Stack HCI를 사용하여 노후한 스토리지 어레이나 네트워크 장비를 별다른 아키텍처 재구성 과정 없이 소프트웨어 정의 인프라로 수월하게 대체합니다. 기본 제공 Storage Spaces Direct 및 SDN(소프트웨어 정의 네트워킹)이 Hyper-V 환경과의 자연스러운 통합을 보장합니다.|