---
title: 시스템 Insights 개요
description: 시스템 정보에는 Windows Server 2019에 새 예측 분석 기능입니다. 시스템 Insights 예측 기능--기계 학습 모델에 의해 각 백업된에 로컬 서버의 작동 하 고 줄일 수에 대 한 정보를 제공 하는 이벤트, 성능 카운터 등의 Windows Server 시스템 데이터를 분석 합니다 사후 배포의 문제를 관리와 관련 된 운영 비용입니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: ca471e5e747c7aaa369f5725290e16deab7a6660
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887244"
---
# <a name="system-insights-overview"></a>시스템 Insights 개요

>적용 대상: Windows Server 2019

시스템 정보에는 Windows Server 2019에 새 예측 분석 기능입니다. 시스템 Insights 예측 기능--기계 학습 모델에 의해 각 백업된에 로컬 서버의 작동 하 고 줄일 수에 대 한 정보를 제공 하는 이벤트, 성능 카운터 등의 Windows Server 시스템 데이터를 분석 합니다 사후 배포의 문제를 관리와 관련 된 운영 비용입니다. 

Windows Server 2019에 시스템 Insights는 용량을 계산, 네트워킹 및 저장소에 이전 사용 패턴을 기반으로 하는 것에 대 한 향후의 리소스를 예측 하는 예측에 집중 하는 네 가지 기본 기능을 사용 하 여 제공 됩니다. 시스템 정보 또한와 함께 제공 되는 [확장 가능한 인프라](adding-and-developing-capabilities.md)이므로 Microsoft 및 타사 기능을 추가할 수 새 예측 Insights 시스템에 운영 체제를 업데이트 하지 않고 합니다. 

직관적인를 통해 시스템 정보를 관리할 수 있습니다 [Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview) 확장 하거나 [PowerShell을 통해 직접](https://aka.ms/SystemInsightsPowerShell), 시스템 정보를 사용 하면 각 예측 기능을 구성할 수 있습니다 배포의 요구 사항에 따라 개별적으로 합니다. 모든 예측 결과를 사용할 수 있는 이벤트 로그에 게시 됩니다 [Azure Monitor](https://azure.microsoft.com/services/monitor/) 하거나 [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) 쉽게 집계 하 고 그룹 컴퓨터에 대해 예측을 참조 하세요.

![Windows Admin Center, 그리기를 예측 하는 그래프와 기능을 예측 하는 CPU 용량을 보여 주는 시스템 Insights 확장](media/cpu-forecast-2.png)

## <a name="local-functionality"></a>로컬 기능
Windows Server에서 시스템 Insights 완전히 로컬로 실행 됩니다. Windows Server 2019에 도입 된 새 기능을 사용 하 여 모든 데이터 수집, 유지 하 고 분석 직접 컴퓨터에 모든 클라우드 연결 없이 예측 분석 기능을 실현할 수 있습니다.

시스템 데이터는 컴퓨터에 저장 됩니다 하 고 클라우드에서 재 학습 되지 않아도 되는 예측 분석 기능에서이 데이터를 분석 합니다. 시스템 정보를 사용 하 여 컴퓨터에 데이터를 유지할 수 있으며 예측 분석 기능에서 혜택을 얻을 수 있습니다. 

## <a name="get-started"></a>시작

<iframe src="https://www.youtube-nocookie.com/embed/AJxQkx5WSaA" width="560" height="315" allowfullscreen></iframe>

>[!TIP]
>시작 하 고 자신 있게 시스템 정보를 관리 하는 데 필요한 정보를 알아보려면이 짧은 비디오를 시청 하세요. [10 분 후에 시스템 정보를 사용 하 여 시작](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

### <a name="requirements"></a>요구 사항
시스템 Insights는 모든 Windows Server 2019 인스턴스에서 사용할 수 있습니다. 모든 클라우드 및 모든 하이퍼바이저에서 호스트와 게스트 컴퓨터에서 실행 됩니다.

### <a name="install-system-insights"></a>시스템 정보를 설치 합니다.
>[!IMPORTANT]
>시스템 정보를 수집 하 고 최대 1 년 분량의 데이터를 로컬로 저장 합니다. 운영 체제를 업그레이드 하는 경우 데이터를 유지 하려는 경우 **전체 업그레이드를 사용 해야**합니다.

#### <a name="install-the-feature"></a>기능 설치
Windows Admin Center 내에서 확장을 사용 하 여 시스템 정보를 설치할 수 있습니다.

![시스템 Insights 확장에 대 한 Day 0 환경입니다.](media/day-0-2.png)

시스템 Insights 직접 서버 관리자를 통해 추가 하 여 설치할 수도 있습니다는 **Insights 시스템** 기능 또는 PowerShell을 사용 하 여:

```PowerShell
Add-WindowsFeature System-Insights -IncludeManagementTools
```

## <a name="provide-feedback"></a>피드백 제공
이 기능 개선에 참여 하는 데 피드백을 듣고 자 합니다. 피드백을 제출 하려면 다음 채널을 사용할 수 있습니다.
- **피드백 허브**: 버그 또는 사용자 의견 파일에 Windows 10에서 피드백 허브 도구를 사용 합니다. 이 작업을 수행 하는 경우를 지정 하세요.
    - **범주**: 서버 
    - **Subcategory**: 시스템 인사이트
- **UserVoice**: 기능을 통해 요청을 제출 하세요 [UserVoice 페이지](https://windowsserver.uservoice.com/forums/295071-management-tools)합니다. 중요 한 찬성 항목 동료와 공유 합니다.
- **Email**: 개인적으로 기능 팀에 의견을 제출 하려는 경우 전자 메일을 보내 system-insights-feed@microsoft.com합니다. 여전히 요청할 수 있습니다 피드백 허브 또는 UserVoice를 사용 하는 점을 고려 하세요.

## <a name="see-also"></a>참조
시스템 정보에 대 한 자세한 내용은 다음 리소스를 사용 합니다.

- [이해 기능](understanding-capabilities.md)
- [관리 기능](managing-capabilities.md)
- [추가 및 기능 개발](adding-and-developing-capabilities.md)
- [System Insights FAQ](faq.md)