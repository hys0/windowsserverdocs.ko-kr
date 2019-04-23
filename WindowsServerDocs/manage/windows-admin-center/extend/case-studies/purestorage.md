---
title: Windows Admin Center SDK 사례 연구-순수 저장소
description: Windows Admin Center SDK 사례 연구-순수 저장소
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849924"
---
# <a name="pure-storage-extension"></a>순수 저장소 확장

## <a name="providing-end-to-end-array-management-for-windows-admin-center"></a>Windows Admin Center 대 한 종단 간 배열 관리를 제공합니다. 

[순수 저장소](https://www.purestorage.com/) enterprise, 경쟁 우위에 대 한 비즈니스를 가속화 하는 데이터 중심 아키텍처를 제공 하는 모든 플래시 데이터 저장소 솔루션을 제공 합니다.  순수형 Microsoft Windows Server에 대해 인증 하는 Microsoft Gold Partner 인 이며 Azure와 같은 핵심 Microsoft 솔루션에 대 한 기술 통합 개발 Hyper-v, SQL Server, System Center, Windows PowerShell 및 Windows SMB 합니다. 순수형 순수 FlashArray 제품에는 단일 창 보기를 제공 하는 Windows Admin Center 최신 릴리스를 지 원하는 확장의 기술 미리 보기 발표.  이 확장 프로그램에서 사용자가 모니터링 작업을 수행 하 고 실시간 성능 메트릭을 보고 저장소 볼륨 및 초기자를 관리 하는 하나의 도구에서 제공 됩니다.

초기에 Windows Admin Center "프로젝트 브라 티"로 알려져 있었습니다, 순수형 고객에 게 제공할 수 있는 값을 확인 및 파트너 Windows Admin Center 제공 하는 단일 창에서 여러 순수 저장소 FlashArrays를 관리할 수 있습니다.

순수형 "프로젝트 브라 티"를 사용 하 여 사용 사례 연구를 시작할 때 Windows Admin Center 사이의 FlashArray 통합된 관리 환경을 제공 하는 것에 대 한 잠재적인을 즉시 깨달았습니다. 순수형은 Windows Admin Center 기능에 대 한 세부 구현을 정의 기여한 엔지니어링 팀과 밀접 하 게 공동 작업 합니다. 순수형은 Windows Admin Center 초기 단계에서 피드백을 제공 하 여 Microsoft 팀에 참여 수도 있었습니다. 

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Windows Admin Center 내에서 직접 관리를 사용 하도록 설정 하려면 FlashArray 웹 인터페이스를 모방 하는 기능 집합을 통합 한 것입니다. 고객 및 파트너 필요 없이 두 개의 다른 관리 도구를 사용 하 여 작업을 단일 창에서 도움이 됩니다. 관리의 단일 지점 외에도 고객 혜택 됩니다 컨텍스트는 FlashArray에 연결 된 Windows 서버를 관리할 수 있습니다. "</cite>
>
> -Barkz, 기술 책임자로 Microsoft 솔루션 및 통합, 순수 저장소

순수 저장소 솔루션 확장에 포함 된 기능은 다음과 같습니다.
- 여러 FlashArrays에 연결합니다.
- IOPs, 대역폭, 대기 시간, 데이터 감소 및 공간 관리를 포함 하 여 FlashArray 세부 정보를 볼 수 있습니다. 이들은 FlashArray 관리 GUI에서 가져올 모든 동일한 정보입니다.
- Windows Server 호스트 및 클러스터 된 공유 볼륨 (Csv)에 대 한 공유 볼륨 액세스를 사용 하도록 설정 하는 데 사용 되는 구성 된 호스트 그룹을 봅니다.
- 보기 호스트-모든 연결 정보를 사용할 iSCSI 호스트 이름을 포함 한 정규화 된 이름 (Iqn) 및 World Wide Name (Wwn).
- 볼륨 관리-여기에 만들고 볼륨을 삭제할 수 있습니다. 볼륨 제거 되 면 소멸 되 항목 버킷에 배치 됩니다 및 주 FlashArray 관리 GUI에서 Eradicate 해야 합니다.
- 초기자 관리-이것이 Windows Admin Center 배포를 통해 관리 되는 개별 서버에 대 한 컨텍스트를 제공 하는 가장 흥미로운 기능 중 하나입니다. 다중 경로 IO (MPIO)는 새 볼륨을 설치/구성 및 만들기/탑재 하는 경우 확인 개별 Windows 서버에 연결 된 디스크 (볼륨)를 볼 수 있습니다.

A [데모 비디오](https://youtu.be/IFAeCAd6V2g) 만들었습니다는 순수 저장소 솔루션 확장을 제공 하는 기능의 일부를 보여 줍니다. 

아래 스크린샷에서 디스크 (볼륨)는 특정 Windows Server 호스트에 연결 된 보기 보여 줍니다. 연결 세부 정보를 보는 것 외에도 다중 경로 IO 구성 되어 있는지 확인 합니다.

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-2.png)

디스크를 보는 것 외에 새 볼륨 수 만들어지고 즉시 Windows 디스크 관리 도구를 사용 하지 않고 호스트에 탑재 합니다.

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-3.png)

이후 기술 미리 보기 릴리스를 지금까지 수집한 고객의 의견은 매우 긍정적 되어 릴리스 나중에 추가할 다른 기능에 대 한 정보 제공에 미국. 

추가 리소스:
- [순수 저장소 확장 공지 블로그 게시물](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) 포드캐스트
