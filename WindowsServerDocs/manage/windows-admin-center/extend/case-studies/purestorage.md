---
title: Windows Admin Center SDK 사례 연구 순수 저장소
description: Windows Admin Center SDK 사례 연구 순수 저장소
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: ebeec824f802f020d0ece17524ba43b1baeba893
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "8995369"
---
# 순수 저장소 확장

## Windows Admin Center에 대 한 종단 간 배열 관리를 제공합니다. 

[순수 저장소](https://www.purestorage.com/) 엔터프라이즈, 데이터 중심 아키텍처 경쟁 우위에 대 한 비즈니스 가속화를 제공 하는 모든 플래시 데이터 저장소 솔루션을 제공 합니다.  Pure Microsoft 골드 파트너는 Microsoft Windows Server에 대 한 인증 이며, Azure 등 주요 Microsoft 솔루션에 대 한 기술 통합 개발 Hyper-v, SQL Server, System Center, Windows PowerShell 및 Windows SMB 합니다. 최근에 Pure 순수 FlashArray 제품에는 단일 창 보기를 제공 하는 Windows Admin Center의 최신 버전을 지 원하는 확장의 기술 미리 보기를 발표 합니다.  이 확장에서 사용자가 모니터링 작업을 수행, 실시간 성능 메트릭 보기 및 저장소 볼륨 및 초기자 관리 도구에서 임 파워 됩니다.

를 초기에 Windows Admin Center "Project Honolulu" 이라고, Pure 본 고객에 게 제공할 수 있는 값 및 파트너를 통한 Windows Admin Center를 제공 하는 단일 창에서 여러 순수 저장소 FlashArrays를 관리 하는 기능.

Pure 시작 "Project Honolulu"를 사용 하 여 사용 사례 연구 FlashArray Windows Admin Center와 통합된 관리 환경을 제공 하기 위한 가능성이 즉시 실현 합니다. Pure와 밀접 하 게 기능에 대 한 구현 세부 정보를 정의 하는 데 도움이 되는 Windows Admin Center 엔지니어링 팀과 공동 합니다. Pure는 Windows Admin Center의 초기 단계에 피드백을 제공 하 고 Microsoft 팀에 기여 하도 못했습니다. 

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Windows Admin Center 내에서 직접 관리를 활성화 하는 FlashArray 웹 인터페이스를 모방 된 기능 집합에서는 통합 했습니다. 고객과 파트너가 돋보기와 두 개의 서로 다른 관리 도구와 함께 작동 하는 단일 창에서 도움이 됩니다. 관리는 단일 액세스 지점을 외에도 혜택 고객 됩니다 연관성이 FlashArray에 연결 된 Windows 서버를 관리할 수 없습니다. "</cite>
>
> -Barkz, 기술 감독 Microsoft 솔루션 및 통합을 순수 저장소

순수 저장소 솔루션 확장에 포함 된 기능은 다음과 같습니다.
- 여러 FlashArrays에 연결합니다.
- IOPs, 대역폭, 대기 시간, 데이터 감소 공간 관리를 비롯 한 FlashArray 세부 정보 보기 이들은 FlashArray 관리 GUI에서 가져온 모든 동일한 정보입니다.
- Windows Server 호스트와 클러스터 공유 볼륨 (Csv)에 대 한 공유 볼륨 액세스할 수 있도록 하는 데 사용 되는 구성 된 호스트 그룹을 봅니다.
- 보기 호스트-모든 연결 정보를 사용할 수 있는 iSCSI 호스트 이름을 포함 하 여 정규화 된 이름 (IQNs) 및 월드 와이드 이름 (WWNs).
- 볼륨 관리-만들기 볼륨을 삭제 하는 기능이 포함 됩니다. 볼륨 소멸 되 면 소멸 되 항목 보관 함에 배치 됩니다 및 Eradicate 주 FlashArray 관리 GUI에서 해야 합니다.
- 초기자 관리-이것이 Windows Admin Center 배포에서 관리 되는 개별 서버에 대 한 컨텍스트를 제공 하는 가장 흥미로운 기능 중 하나입니다. 다중 경로 IO (MPIO)는 새 볼륨을 설치 하 고 구성 하 고 만들기/탑재 하는 경우 확인 개별 Windows 서버에 연결 된 디스크 (볼륨)를 볼 수 있습니다.

모든 순수 저장소 솔루션 확장을 제공 하는 기능을 보여 주는 [데모 비디오](https://youtu.be/IFAeCAd6V2g) 작성 되었습니다. 

스크린샷 아래 어떤 디스크 (볼륨)는 특정 Windows Server 호스트에 연결 된 보기를 보여줍니다. 연결 세부 정보를 보는 것 외에 다중 경로 IO 구성 된 경우를 확인 합니다.

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-2.png)

디스크를 보는 것 외에 새 볼륨 만들고 즉시 Windows 디스크 관리 도구를 사용 하지 않고 호스트에 탑재 합니다.

![순수 저장소 확장](../../media/extend-case-study-purestorage/purestorage-3.png)

우리의 기술 미리 보기를 해제 하면 이후 지금까지 수집한 고객 피드백 확실히 되었으며 릴리스 나중에 추가 하려면 다른 기능에 대 한 정보 제공 수도 있습니다. 

추가 리소스:
- [순수 저장소 확장 발표 블로그 게시물](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) 팟캐스트
