---
title: 데스크톱 호스팅을 위한 Azure 서비스 및 고려 사항
description: 원격 데스크톱 호스팅 솔루션을 사용 하 여 Azure에 고유한 고려 사항을 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f402ae3-5391-4c7d-afea-2c5c9044de46
author: heidilohr
manager: dougkim
ms.openlocfilehash: 37210a5d75399309c53364f5b8ee9e06d26d6f32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849804"
---
# <a name="azure-services-and-considerations-for-desktop-hosting"></a>데스크톱 호스팅을 위한 Azure 서비스 및 고려 사항

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 섹션에서는 Azure 인프라 서비스에 설명 합니다.
  
## <a name="azure-portal"></a>Azure Portal

공급자는 Azure 구독을 만든 후 Azure portal 수동으로 각 테 넌 트의 환경을 만들려면 사용할 수 있습니다. PowerShell 스크립트를 사용 하 여이 프로세스를 자동화할 수도 있습니다.  

자세한 내용은 참조는 [Microsoft Azure](https://www.azure.microsoft.com) 웹 사이트입니다.
  
## <a name="azure-load-balancer"></a>Azure 부하 분산 장치

테 넌 트의 구성 요소 가상 머신에서 실행 통신 하는 서로 격리 된 네트워크입니다. 배포 과정에서 이러한 가상 머신에 원격 데스크톱 프로토콜 끝점 또는 원격 PowerShell 끝점을 사용 하 여 Azure Load Balancer를 통해 외부에서 액세스할 수 있습니다. 배포가 완료 되 면 이러한 끝점 공격 노출 영역을 줄이기 위해 일반적으로 삭제 됩니다. 유일한 끝점 HTTPS 및 UDP 끝점은 RD 웹 및 RD 게이트웨이 구성 요소를 실행 하는 가상 컴퓨터에 대해 생성 됩니다. 이렇게 하면 테 넌 트의 데스크톱 호스팅 서비스에서 실행 되는 세션에 연결 하려면 인터넷에 클라이언트. 사용자가 웹 브라우저와 같은 인터넷에 연결 하는 응용 프로그램을 열면 연결 Azure Load Balancer를 통해 전달 됩니다.  
  
자세한 내용은 참조 하세요. [Azure Load Balancer 란?](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-load-balance/)
  
## <a name="security-considerations"></a>보안 고려 사항

이 Azure 데스크톱 호스팅 참조 아키텍처 가이드는 각 테 넌 트에 대 한 매우 안전 하 고 격리 된 환경을 제공 하도록 설계 되었습니다. 또한 시스템 보안 호스 티 드 서비스의 배포 및 운영 하는 동안 공급자가 수행 하는 보호 기능에 따라 달라 집니다. 다음은 공급자 보안이 참조 아키텍처에 따라 데스크톱 호스팅 솔루션을 유지 하기 위해 수행 해야 하는 몇 가지 고려 사항을 설명 합니다.

- 이상적으로 임의로 생성 된, 자주 변경 및 선택 몇 공급자 관리자만 액세스할 수 있는 안전한 중앙 위치에 저장 된 모든 관리 암호 강력한 이어야 합니다.  
- 새 테 넌 트에 대 한 테 넌 트 환경에 복제 하는 경우 동일 하거나 취약 한 관리자 암호를 사용 하지 마세요.
- 고유 하 고 스푸핑 공격을 방지 하려면 각 테 넌 트를 인식할 수 있는 RD 웹 액세스 사이트 URL, 이름 및 인증서 여야 합니다.  
- 데스크톱 호스팅 서비스의 일반적인 작업 중 사용자가 테 넌 트의 데스크톱 호스팅 클라우드 서비스를 안전 하 게 연결할 수 있는 RD 웹 및 RD 게이트웨이 가상 컴퓨터를 제외 하 고 모든 가상 머신에 대 한 모든 공용 IP 주소를 삭제 해야 합니다. 관리 작업을 위해 필요한 경우 공용 IP 주소 일시적으로 추가 될 수 있습니다 하지만 나중에 삭제 항상 해야 있습니다.  
  
자세한 내용은 다음 문서를 참조하세요.

- [보안 및 보호](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831778(v=ws.11))  
- [IIS 8에 대 한 보안 모범 사례](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj635855(v=ws.11))  
- [Secure Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831360(v=ws.11))  
  
## <a name="design-considerations"></a>디자인 고려 사항

Microsoft Azure 인프라 서비스의 제약 조건을 디자인할 때 고려해 야 하는 다중 테 넌 트 데스크톱 호스팅 서비스는 것이 반드시 합니다. 다음은 공급자 기능 및 비용 효과적인 데스크톱 호스팅 솔루션을이 참조 아키텍처를 기반으로 달성 하기 위해 수행 해야 하는 고려 사항을 설명 합니다.  
  
- Azure 구독에 가상 네트워크, VM 코어 및 사용할 수 있는 클라우드 서비스의 최대 수입니다. 공급자 보다 더 많은 리소스에서 필요한 경우 여러 구독을 만드는 해야 합니다.
- Azure 클라우드 서비스에 사용할 수 있는 가상 머신의 최대 수 있습니다. 공급자는 최대값을 초과 하는 더 큰 테 넌 트에 대 한 여러 클라우드 서비스를 만들 해야 합니다.  
- Azure 배포 비용 부분적으로 가상 머신의 크기와 수에 기반한 수 있습니다. 공급자 기능을 제공 하 고 보안이 강화 된 최저 비용으로 데스크톱 호스팅 환경에 수와 각 테 넌 트에 대 한 가상 머신의 크기를 최적화 해야 합니다.  
- Azure 데이터 센터에서 물리적 컴퓨터 리소스는 Hyper-v를 사용 하 여 가상화 됩니다. Virtual machines의 가용성은 Azure 인프라에서 사용 되는 개별 서버의 가용성에 종속 되므로 hyper-v 호스트 클러스터에 구성 되지 않습니다. 게스트 클러스터링은 가상 컴퓨터 내에서 구현할 수 있습니다 다음 각 역할 서비스 가상 컴퓨터의 여러 인스턴스 고가용성을 제공 하려면 가용성 집합에서 만들 있습니다.  
- 일반적인 저장소 구성에서 서비스 공급자는 단일 저장소 계정의 여러 컨테이너 (예를 들어 하나씩 각 테 넌 트) 및 각 컨테이너 내에서 여러 디스크를 사용 하 여 해야 합니다. 그러나 총 저장소를 단일 저장소 계정에 대 한 얻을 수 있는 성능에 제한이 있습니다. 많은 수의 테 넌 트 또는 테 넌 트에 높은 저장소 용량 또는 성능 요구 사항 지 원하는 서비스 공급자에 대 한 서비스 공급자를 여러 저장소 계정을 만드는 해야 합니다.  
  
자세한 내용은 다음 문서를 참조하세요.

- [Cloud Services 크기](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)  
- [Microsoft Azure 가상 컴퓨터 가격 정보](https://azure.microsoft.com/pricing/details/virtual-machines/)  
- [Hyper-v 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))  
- [Azure Storage 확장성 및 성능 목표](https://docs.microsoft.com/azure/storage/common/storage-scalability-targets)  

## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory 응용 프로그램 프록시

Azure Active Directory (AD) 응용 프로그램 프록시는 유료 Sku의 Azure AD 사용자가 Azure의 역방향 프록시 서비스를 통해 내부 응용 프로그램에 연결할 수 있도록에서 제공 하는 서비스입니다. 이렇게 하면 RD 웹 및 RD 게이트웨이 끝점을 공용 IP 주소를 통해 인터넷에 노출 될 필요가 없도록 하 여 가상 네트워크 내에서 숨길 수 있습니다. 호스팅 서비스 공급자는 Azure AD 응용 프로그램 프록시를 사용 하 여 전체 배포를 유지 하면서 테 넌 트의 환경에서 가상 머신의 수를 축소 하 수 있습니다. Azure AD 응용 프로그램 프록시를 사용 하면 다양 한 조건부 액세스 및 multi-factor authentication 등 Azure AD가 제공 하는 이점.

자세한 내용은 [커넥터를 설치 하 고 응용 프로그램 프록시를 사용 하 여 시작](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-enable)합니다.