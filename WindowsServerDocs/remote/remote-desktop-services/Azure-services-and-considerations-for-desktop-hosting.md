---
title: 데스크톱 호스팅을 위한 Azure 서비스 및 고려 사항
description: 원격 데스크톱 호스팅 솔루션을 사용하는 Azure 고유의 고려 사항을 알아보세요.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.topic: article
ms.assetid: 0f402ae3-5391-4c7d-afea-2c5c9044de46
author: heidilohr
manager: lizross
ms.openlocfilehash: f73f28500c136ec8bdd32084cc5949f5e9804699
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818526"
---
# <a name="azure-services-and-considerations-for-desktop-hosting"></a>데스크톱 호스팅을 위한 Azure 서비스 및 고려 사항

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

다음 섹션에서는 Azure 인프라 서비스를 설명합니다.
  
## <a name="azure-portal"></a>Azure Portal

서비스 공급자가 Azure 구독을 만든 후 Azure Portal을 사용하여 각 테넌트의 환경을 수동으로 만들 수 있습니다. 또한 PowerShell 스크립트를 사용하여 이 프로세스를 자동화할 수도 있습니다.  

자세한 내용을 보려면 [Microsoft Azure](https://www.azure.microsoft.com) 웹 사이트를 방문하세요.
  
## <a name="azure-load-balancer"></a>Azure 부하 분산 장치

테넌트의 구성 요소는 격리된 네트워크에서 서로 통신하는 가상 머신에서 실행됩니다. 배포 프로세스 중에 원격 데스크톱 프로토콜 엔드포인트 또는 원격 PowerShell 엔드포인트를 사용하여 Azure Load Balancer를 통해 외부에서 이러한 가상 머신에 액세스할 수 있습니다. 배포가 완료되면 공격 노출 영역을 줄이기 위해 일반적으로 이러한 엔드포인트가 삭제됩니다. 유일한 엔드포인트는 RD 웹 및 RD 게이트웨이 구성 요소를 실행 중인 가상 머신용으로 생성되는 HTTPS 및 UDP 엔드포인트입니다. 이를 통해 인터넷상의 클라이언트가 테넌트의 데스크톱 호스팅 서비스에서 실행 중인 세션에 연결할 수 있습니다. 사용자가 웹 브라우저와 같은 인터넷에 연결하는 애플리케이션을 열면 Azure Load Balancer를 통해 연결이 전달됩니다.  
  
자세한 내용은 [Azure Load Balancer란?](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-load-balance/)을 참조하세요.
  
## <a name="security-considerations"></a>보안 고려 사항

이 Azure 데스크톱 호스팅 참조 아키텍처 가이드는 각 테넌트에 매우 안전하고 격리된 환경을 제공하도록 설계되었습니다. 또한 시스템 보안은 호스팅된 서비스의 배포 및 작동 중에 서비스 공급자가 수행한 보호 조치에 따라 달라집니다. 다음 목록은 이러한 참조 아키텍처에 따라 데스크톱 호스팅 솔루션을 안전하게 보호하기 위해 서비스 공급자가 고려해야 할 몇 가지 사항을 설명합니다.

- 모든 관리자 암호는 강력해야 하며, 무작위로 생성된 것이 이상적이며, 자주 변경해야 하고, 선택된 일부 서비스 공급자 관리자만 액세스할 수 있는 안전한 중앙 위치에 저장해야 합니다.  
- 새 테넌트의 테넌트 환경을 복제할 때는 동일하거나 약한 관리자 암호를 사용하지 않도록 하세요.
- 스푸핑 공격을 방지하려면 RD 웹 액세스 사이트 URL, 이름 및 인증서가 동일해야 하며, 각 테넌트에서 인식할 수 있어야 합니다.  
- 데스크톱 호스팅 서비스가 정상적으로 작동하는 동안에는 사용자가 테넌트의 데스크톱 호스팅 클라우드 서비스에 안전하게 연결할 수 있도록 RD 웹 및 RD 게이트웨이 가상 머신을 제외한 모든 가상 머신의 모든 공개 IP 주소를 삭제해야 합니다. 관리 작업에 필요한 경우 공개 IP 주소를 임시로 추가할 수 있지만 이후에는 항상 삭제해야 합니다.  
  
자세한 내용은 다음 문서를 참조하세요.

- [보안 및 보호](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831778(v=ws.11))  
- [IIS 8 보안 모범 사례](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj635855(v=ws.11))  
- [Windows Server 2012 R2 보안](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831360(v=ws.11))  
  
## <a name="design-considerations"></a>디자인 고려 사항

다중 테넌트 데스크톱 호스팅 서비스를 설계할 때는 Microsoft Azure 인프라 서비스의 제약 조건을 고려해야 합니다. 다음 목록은 이러한 참조 아키텍처에 따라 실용적이고 비용 효과적인 데스크톱 호스팅 솔루션을 구현하기 위해 서비스 공급자가 고려해야 할 몇 가지 사항을 설명합니다.  
  
- Azure 구독에는 사용 가능한 최대 가상 네트워크 수, VM 코어 수 및 Cloud Services 수가 정해져 있습니다. 이보다 많은 리소스가 필요한 서비스 공급자는 여러 개의 구독을 만들어야 합니다.
- Azure 클라우드 서비스에는 사용 가능한 최대 가상 머신 수가 정해져 있습니다. 서비스 공급자는 최댓값을 초과하는 대규모 테넌트를 위한 여러 Cloud Services를 만들어야 할 수 있습니다.  
- Azure 배포 비용은 가상 머신의 개수와 크기에 일부 영향을 받습니다. 서비스 공급자는 각 테넌트의 가상 머신 수와 크기를 최적화하여 가장 저렴한 비용으로 실용적이고 매우 안전한 데스크톱 호스팅 환경을 제공해야 합니다.  
- Azure 데이터 센터의 실제 컴퓨터 리소스는 Hyper-V를 사용하여 가상화됩니다. Hyper-V 호스트는 호스트 클러스터에 구성되지 않으므로 가상 머신의 가용성은 Azure 인프라에서 사용되는 개별 서버의 가용성에 따라 다릅니다. 더 높은 가용성을 제공하려면 각 역할 서비스 가상 머신의 여러 인스턴스를 가용성 세트에 만든 후 가상 머신 내에 게스트 클러스터링을 구현하면 됩니다.  
- 일반적인 스토리지 구성에서 서비스 공급자는 여러 컨테이너, 각 컨테이너 내에 있는 여러 디스크와 단일 스토리지 계정(예: 각 테넌트당 하나)을 사용합니다. 하지만 단일 스토리지 계정에 구현할 수 있는 총 스토리지와 성능에는 제한이 있습니다. 매우 많은 테넌트 또는 스토리지 용량이나 성능 요구 사항이 높은 테넌트를 지원하는 서비스 공급자의 경우 여러 스토리지 계정을 만들어야 할 수 있습니다.  
  
자세한 내용은 다음 문서를 참조하세요.

- [Cloud Services의 크기](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)  
- [Microsoft Azure 가상 머신 가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/virtual-machines/)  
- [Hyper-V 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))  
- [Azure Storage 확장성 및 성능 목표](https://docs.microsoft.com/azure/storage/common/storage-scalability-targets)  

## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory 애플리케이션 프록시

Azure Active Directory(AD) 애플리케이션 프록시는 사용자가 Azure의 자체 역방향 프록시 서비스를 통해 내부 애플리케이션에 연결할 수 있게 해주는 Azure AD의 유료 SKU에 제공되는 서비스입니다. 따라서 RD 웹 및 RD 게이트웨이 엔드포인트를 공개 IP 주소로 인터넷에 공개할 필요 없이 가상 네트워크 내부에 숨길 수 있습니다. 호스팅 서비스 공급자는 Azure AD 애플리케이션 프록시를 사용하여 테넌트 환경의 가상 머신 수를 줄이면서 전체 배포는 계속 유지할 수 있습니다. Azure AD 애플리케이션 프록시는 또는 조건부 액세스 및 다단계 인증과 같이 Azure AD가 제공하는 여러 이점을 지원합니다.

자세한 내용은 [애플리케이션 프록시를 시작하고 커넥터 설치](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-enable)를 참조하세요.