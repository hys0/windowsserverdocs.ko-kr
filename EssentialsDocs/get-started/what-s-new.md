---
title: Windows Server 2016 Essentials의 새로운 기능
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: affff774-5fa6-4944-887a-9bfde05f6a3f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1d5176a69136e9bad36e22472b8fadbd6d0e9e79
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310301"
---
# <a name="whats-new-in-windows-server-2016-essentials"></a>Windows Server 2016 Essentials의 새로운 기능

> 적용 대상: Windows Server 2016 Essentials

다음은 Windows Server 2016 Essentials의 새로운 기능 및 향상 된 기능입니다.

## <a name="integration-with-azure-site-recovery-services"></a>[Azure Site Recovery 서비스와 통합](azure-site-recovery-services-integration.md)

**수행 하는 작업** -보호 되는 가상 컴퓨터가 실패 하거나 보호 된 가상 컴퓨터가 실행 되는 호스트 서버가 실패 하는 경우 온-프레미스 가상 컴퓨터 또는 호스트 서버를 복구 하 고 사용할 수 있을 때까지 Azure Site Recovery Services로 장애 조치 (failover) 하면 비즈니스 연속성을 유지 합니다. 

**작동 방식** -Microsoft Azure에서 제공 되는 Azure Site Recovery 서비스를 사용 하면 VM (가상 머신)을 Azure의 백업 자격 증명 모음으로 실시간으로 복제할 수 있습니다. 하드웨어 또는 기타 오류로 인해 서버 또는 사이트가 중단 되는 경우 백업 자격 증명 모음에 저장 된 VM 이미지가 Azure에서 실행 중인 VM으로 프로 비전 되도록 Azure Site Recovery 서비스로 장애 조치 (failover) 할 수 있습니다. Azure 가상 네트워크와 결합 된 이전에 온-프레미스 서버에 연결 된 클라이언트 Pc는 Azure에서 실행 되는 서버에 투명 하 게 연결 됩니다.     
                                                                                                                                                                                                                                                                                                               

## <a name="integration-with-azure-virtual-network"></a>[Azure Virtual network와 통합](azure-virtual-network-integration.md)

조직에서 클라우드 컴퓨팅에 대 한 작업을 수행 하는 경우 모든 리소스를 한 번에 이동 하는 경우가 거의 **없습니다**. 대신 일부 리소스를 클라우드로 이동 하 고 온-프레미스에 유지 합니다. 이렇게 하면 시간에 따라 단계별로 조직을 클라우드로 쉽게 이동할 수 있습니다. Azure virtual Network 통합은 프로세스를 원활 하 고 관리할 수 있도록 하는 네트워크 인프라를 제공 합니다.

**작동 방법** -azure 가상 네트워킹은 azure에서 실행 되는 리소스 (예: 가상 머신 및 저장소)가 원활한 응용 프로그램 및 리소스 액세스를 위해 로컬 네트워크에 있는 것 처럼 보이지만, 조직에서 P2P (지점 간) 또는 S2S (사이트 간) 가상 개인 네트워크를 만들 수 있도록 하는 Microsoft Azure 제공 되는 서비스입니다.



## <a name="support-for-larger-deployments"></a>[대규모 배포에 대 한 지원](support-for-larger-deployments.md) 

일부 대규모 중소기업에는 Windows Server Essentials를 효과적으로 구현 하기 위한 더 많은 기능과 용량이 필요 합니다. Windows Server 2016 Essentials는를 사용 하 여 더 큰 배포에 대 한 지원을 추가 함으로써 도메인, 사용자 및 장치의 관리 효율성을 향상 시킵니다.                                                                                                                                                                                                 

 - 여러 도메인
 - 여러 도메인 컨트롤러                                                                                                                                                                                                                                        
 - 지정 된 도메인 컨트롤러를 지정 하는 기능                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

<a name="see-also"></a>참고 항목
--------

[Windows Server Essentials 시작](get-started.md)
