---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: iSCSI 대상 부팅 개요
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 9c359c7929ff90968d16e92b1128f4fc8ebde37c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402985"
---
# <a name="iscsi-target-boot-overview"></a>iSCSI 대상 부팅 개요

> 적용 대상: Windows Server 2016

Windows Server의 iSCSI 대상 서버에서는 중앙 위치에 저장된 단일 운영 체제 이미지에서 수백 대의 컴퓨터를 부팅할 수 있습니다. 이를 통해 효율성, 가용성, 보안 및 관리 효율성을 높일 수 있습니다.  
  
## <a name="BKMK_OVER"></a>기능 설명  
차이점 보관용 가상 하드 디스크 \(VHDs @ no__t-1을 사용 하면 단일 운영 체제 이미지 @no__t "마스터 이미지" \)을 사용 하 여 최대 256 대의 컴퓨터를 부팅할 수 있습니다. 예를 들어, 약 20gb의 운영 체제 이미지를 사용 하 여 Windows Server를 배포 하 고 부팅 볼륨 역할을 하는 두 개의 미러된 디스크 드라이브를 사용 한다고 가정해 보겠습니다. 256대의 컴퓨터를 부팅하려면 운영 체제 이미지에만 약 10TB의 저장소가 필요합니다. ISCSI 대상 서버를 사용 하는 경우 운영 체제 기본 이미지에 40 GB를, 서버 인스턴스당 차이점 보관용 가상 하드 디스크의 경우 2gb를 사용 하 고, 운영 체제 이미지의 경우 총 552 GB를 사용 합니다. 따라서 운영 체제 이미지 자체에 대해서만 저장소를 90% 이상 절약할 수 있습니다.  
  
## <a name="BKMK_APP"></a>실용적인 응용 프로그램  
제어된 운영 체제 이미지를 사용하면 다음과 같은 이점이 있습니다.  
  
**안전성 및 관리성 향상** 일부 회사에서는 중앙 위치의 저장소에 대해 물리적으로 잠금을 설정하여 데이터를 보호해야 합니다. 이 시나리오에서는 서버가 원격으로 데이터(운영 체제 이미지 포함)에 액세스합니다. iSCSI 대상 서버를 사용하는 경우 관리자는 운영 체제 부팅 이미지를 중앙에서 관리하고 마스터 이미지에 사용할 응용 프로그램을 제어할 수 있습니다.  
  
**신속한 배포.** 마스터 이미지는 Sysprep을 사용하여 준비되므로 마스터 이미지에서 부팅되는 컴퓨터는 Windows 설치 시 수행되는 파일 복사 및 설치 단계를 건너뛰고 바로 사용자 지정 단계로 이동합니다. Microsoft 내부 테스트 결과 256대의 컴퓨터가 34분만에 배포되었습니다.  
  
**빠른 복구.** 운영 체제 이미지가 iSCSI 대상 서버를 실행하는 컴퓨터에서 호스트되므로 디스크 없는 클라이언트를 교체해야 하는 경우 새 컴퓨터가 운영 체제 이미지를 가리키고 즉시 부팅될 수 있습니다.  
  
> [!NOTE]  
> 다양한 공급업체에서 SAN\(저장 영역 네트워크\) 부팅 솔루션을 제공하며 이는 상용 하드웨어의 Windows Server에서 iSCSI 대상 서버에 의해 사용될 수 있습니다.  
  
## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
iSCSI 대상 서버는 특수한 하드웨어가 없어도 작동을 확인할 수 있습니다. 대규모 @ no__t-0scale 배포가 포함 된 데이터 센터에서는 특정 하드웨어에 대해 디자인의 유효성을 검사 해야 합니다. 참조용으로 Microsoft 내부 테스트에서 256 컴퓨터 배포에는 저장소에 대 한 RAID 10 구성에서 15k @ no__t-0RPM 디스크가 필요 하다 고 표시 되었습니다. 네트워크 대역폭은 10GB가 가장 적절합니다. 일반적으로는 1GB 네트워크 어댑터당 iSCSI 부팅 서버 60대를 할당하면 됩니다.  
  
이 시나리오에서는 네트워크 어댑터가 필요하지 않으며 소프트웨어 부트 로더\(예: iPXE 오픈 소스 부트 펌웨어\)를 사용할 수 있습니다.  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
iSCSI 대상 서버는 서버 관리자의 파일 및 iSCSI 서비스 역할 서비스 일부로 설치할 수 있습니다.

> [!NOTE]
> iSCSI(Windows iSCSI 대상 서버 또는 타사 대상 구현 중 하나)에서의 Nano Server 부팅은 지원되지 않습니다.

## <a name="see-also"></a>참조
* [iSCSI 대상 서버](https://technet.microsoft.com/library/hh848272(v=ws.11).aspx)
* [iSCSI 초기자 cmdlet](https://technet.microsoft.com/library/hh826099(v=wps.640).aspx)
* [iSCSI 대상 서버 cmdlet](https://technet.microsoft.com/library/jj612803(v=wps.630).aspx)