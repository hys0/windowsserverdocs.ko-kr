---
title: Windows 관리 센터 SDK 사례 연구-순수 저장소
description: Windows 관리 센터 SDK 사례 연구-순수 저장소
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c6ab75a2375368d7c87d9dffd6175eb611508dd5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406952"
---
# <a name="pure-storage-extension"></a>순수 저장소 확장

## <a name="providing-end-to-end-array-management-for-windows-admin-center"></a>Windows 관리 센터에 대 한 종단 간 배열 관리 제공 

[순수 저장소](https://www.purestorage.com/) 는 데이터 중심 아키텍처를 제공 하 여 경쟁 우위의 비즈니스를 가속화 하는 엔터프라이즈급 데이터 저장소 솔루션을 제공 합니다.  Pure는 microsoft Windows Server에 대해 인증 된 Microsoft 골드 파트너 이며, Azure, Hyper-v, SQL Server, System Center, Windows PowerShell 및 Windows SMB와 같은 주요 Microsoft 솔루션에 대 한 기술 통합을 개발 합니다. 순수한 최근에는 순수 FlashArray 제품에 대 한 단일 창 보기를 제공 하는 최신 버전의 Windows 관리 센터를 지 원하는 확장의 기술 미리 보기를 발표 했습니다.  이 확장을 통해 사용자는 모니터링 작업을 수행 하 고, 실시간 성능 메트릭을 보고, 저장소 볼륨 및 초기자를 관리 하는 한 가지 도구를 사용할 수 있습니다.

초기에, Windows 관리 센터를 "Project Honolulu"로 알려진 경우 순수한는 고객 및 파트너에 게 Windows 관리 센터에서 제공 하는 단일 유리 창에서 여러 순수한 Storage FlashArrays를 관리 하는 기능을 제공할 수 있는 기능을 제공 합니다.

순수한 "Project Honolulu"를 사용 하 여 사용 사례를 조사 하기 시작 하면 Windows 관리 센터와 FlashArray 간에 통합 된 관리 환경을 제공할 가능성이 즉시 실현 됩니다. 순수한는 기능에 대 한 구현 세부 정보를 정의 하는 데 도움이 되는 Windows 관리 센터 엔지니어링 팀과 긴밀 하 게 협력. 또한 Pure는 Windows 관리 센터의 초기 단계에서 피드백을 제공 하 고 Microsoft 팀에 기여 합니다. 

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite> "Windows 관리 센터 내에서 직접 관리할 수 있도록 FlashArray 웹 인터페이스를 모방 하는 기능 집합을 통합 했습니다. 고객 및 파트너는 단일 창에서 두 가지 관리 도구를 사용 하 여 작업 해야 하는 이점을 누릴 수 있습니다. 단일 관리 이점 외에도 고객은 FlashArray에 연결 된 Windows Server를 컨텍스트 관리할 수 있습니다. " </cite>
>
> --바 kz, 기술 감독 Microsoft Solutions & 통합, 순수 저장소

순수 저장소 솔루션 확장에 포함 된 기능은 다음과 같습니다.
- 여러 FlashArrays에 연결 합니다.
- IOPs, 대역폭, 대기 시간, 데이터 감소 및 공간 관리를 포함 하는 FlashArray 세부 정보 보기 이러한 세부 정보는 모두 FlashArray Management GUI에서 얻을 수 있습니다.
- Windows Server 호스트 및 Csv (클러스터 공유 볼륨)에 대 한 공유 볼륨 액세스를 사용 하도록 설정 하는 데 사용 되는 구성 된 호스트 그룹을 표시 합니다.
- 호스트 보기-모든 연결 정보는 호스트 이름, iSCSI 정규화 된 이름 (Iqn으로) 및 Wwpn (Wide Names)을 비롯 한 모든 연결 정보를 사용할 수 있습니다.
- 볼륨 관리-볼륨을 만들고 삭제 하는 기능을 포함 합니다. 볼륨이 제거 되 면 제거 된 항목 버킷에 배치 되며 main FlashArray Management GUI에서 Xamarin.mac 제품과 해야 합니다.
- 초기자 관리-Windows 관리 센터 배포에서 관리 하는 개별 서버에 대 한 컨텍스트를 제공 하는 가장 흥미로운 기능 중 하나입니다. 개별 Windows 서버에 대 한 연결 된 디스크 (볼륨)를 확인 하 고 MPIO (다중 경로 IO)가 설치/구성 되었는지 확인 하 고 새 볼륨을 만들고 탑재 합니다.

순수 저장소 솔루션 확장에서 제공 하는 모든 기능을 보여 주는 [데모 비디오가](https://youtu.be/IFAeCAd6V2g) 생성 되었습니다. 

아래 스크린샷에서는 특정 Windows Server 호스트에 연결 된 디스크 (볼륨)를 보는 방법을 보여 줍니다. 연결 세부 정보를 보는 것 외에도 다중 경로-IO가 구성 되었는지 확인 합니다.

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-2.png)

디스크를 보는 것 외에도 Windows 디스크 관리 도구를 사용 하지 않고도 새 볼륨을 만들어 호스트에 즉시 탑재할 수 있습니다.

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-3.png)

Technical Preview를 릴리스 했으므로 지금까지 수집 된 고객 피드백은 매우 긍정적 이며 향후 릴리스에 추가 될 다양 한 기능에 대 한 통찰력을 제공 하 고 있습니다. 

추가 리소스:
- [순수 저장소 확장 알림 블로그 게시물](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) 포드캐스트
