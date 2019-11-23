---
title: iSCSI Target Server Overview
TOCTitle: iSCSI Target Server
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 638343abf782983020a3301898920470ffcd5952
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403052"
---
# <a name="iscsi-target-server-overview"></a>iSCSI 대상 서버 개요

적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 iscsi 프로토콜을 통해 저장소를 사용할 수 있도록 하는 Windows Server의 역할 서비스인 iSCSI 대상 서버에 대 한 간략 한 개요를 제공 합니다. 이는 기본 Windows 파일 공유 프로토콜인 SMB를 통해 통신할 수 없는 클라이언트에 대해 Windows server 저장소에 대 한 액세스를 제공 하는 데 유용 합니다.

iSCSI 대상 서버는 다음에 적합합니다.

* **네트워크 및 디스크 없는 부팅**   부팅 가능 네트워크 어댑터 또는 소프트웨어 로더를 사용 하 여 수백 개의 디스크 없는 서버를 배포할 수 있습니다. iSCSI 대상 서버를 사용하면 신속하게 배포할 수 있습니다. Microsoft 내부 테스트 결과 256대의 컴퓨터가 34분만에 배포되었습니다. 차이점 보관용 가상 하드 디스크를 사용하면 운영 체제 이미지용 저장소 공간을 90%까지 절약할 수 있습니다. 이는 Hyper-V 또는 HPC(고성능 컴퓨팅) 클러스터를 실행하는 가상 컴퓨터 같이 동일한 운영 체제 이미지의 대규모 배포에 적합합니다.

* **서버 응용 프로그램 저장소**   일부 응용 프로그램에는 블록 저장소가 필요 합니다. iSCSI 대상 서버는 지속적으로 사용 가능한 블록 저장소를 이러한 응용 프로그램에 제공할 수 있습니다. 이 저장소는 원격으로 액세스 가능하므로 iSCSI 소프트웨어 대상은 중앙 또는 지점 사무실 위치에 대한 블록 저장소를 통합할 수도 있습니다.

* **다른 유형의 저장소**   Iscsi 대상 서버는 타사 iscsi 초기자를 지원 하므로 혼합 소프트웨어 환경의 서버에서 저장소를 쉽게 공유할 수 있습니다.

* **개발, 테스트, 데모 및 랩 환경**   ISCSI 대상 서버를 사용 하는 경우 Windows Server 운영 체제를 실행 하는 컴퓨터는 네트워크에서 액세스할 수 있는 블록 저장 장치가 됩니다. 따라서 SAN(저장 영역 네트워크)에 배포하기 전에 응용 프로그램을 테스트할 때 유용합니다.

## <a name="block-storage-requirements"></a>블록 저장소 요구 사항

iSCSI 대상 서버에서 블록 저장소를 제공하도록 하면 기존 이더넷 네트워크를 활용합니다. 추가 하드웨어는 필요하지 않습니다. 고가용성이 중요 조건인 경우에는 고가용성 클러스터를 설정할 수 있습니다. 고가용성 클러스터를 사용하려면 파이버 채널 저장소용 하드웨어나 SAS(Serial Attached SCSI) 저장소 배열 등의 고가용성 클러스터용 공유 저장소가 필요합니다.

게스트 클러스터링을 사용하도록 설정하는 경우에는 블록 저장소를 제공해야 합니다. iSCSI 대상 서버가 포함된 Windows Server 소프트웨어를 실행하는 모든 서버는 블록 저장소를 제공할 수 있습니다.

## <a name="see-also"></a>참고 항목

[iSCSI 대상 블록 저장소, 방법](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848268(v%3dws.11))  
[Windows Server에서 제공 되는 iSCSI 대상 서버의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn305893(v%3dws.11))

