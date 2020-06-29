---
title: 시스템 인사이트 개요
description: System Insights는 Windows Server 2019의 새로운 예측 분석 기능입니다. 시스템 정보 예측 기능-기계 학습 모델에 의해 지원 되는 각각은 성능 카운터 및 이벤트와 같은 Windows Server 시스템 데이터를 로컬로 분석 하 여 서버 기능에 대 한 통찰력을 제공 하 고 배포의 대응적 문제를 관리 하는 것과 관련 된 운영 비용을 줄이는 데 도움을 줍니다.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: b1f0fc5343c5228a02369a64bff2de50ab3f863e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471768"
---
# <a name="system-insights-overview"></a>시스템 인사이트 개요

>적용 대상: Windows Server 2019

System Insights는 Windows Server 2019의 새로운 예측 분석 기능입니다. 시스템 정보 예측 기능-기계 학습 모델에 의해 지원 되는 각각은 성능 카운터 및 이벤트와 같은 Windows Server 시스템 데이터를 로컬로 분석 하 여 서버 기능에 대 한 통찰력을 제공 하 고 배포의 대응적 문제를 관리 하는 것과 관련 된 운영 비용을 줄이는 데 도움을 줍니다.

Windows Server 2019에서 System Insights는 용량 예측에 초점을 맞춘 네 가지 기본 기능을 제공 하며, 이전 사용 패턴을 기반으로 계산, 네트워킹 및 저장소에 대 한 향후 리소스를 예측 합니다. 또한 system Insights는 [확장 가능한 인프라](adding-and-developing-capabilities.md)를 제공 하므로 Microsoft와 타사는 운영 체제를 업데이트 하지 않고도 새로운 예측 기능을 System Insights에 추가할 수 있습니다.

직관적인 [Windows 관리 센터](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview) 확장을 통해 또는 [PowerShell을 통해 직접](https://aka.ms/SystemInsightsPowerShell)시스템 정보를 관리할 수 있으며, system insights를 사용 하면 배포의 요구에 따라 각 예측 기능을 별도로 구성할 수 있습니다. 모든 예측 결과가 이벤트 로그에 게시 되므로 [Azure Monitor](https://azure.microsoft.com/services/monitor/) 또는 [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) 를 사용 하 여 컴퓨터 그룹에서 예측을 쉽게 집계 하 고 확인할 수 있습니다.

![Windows 관리 센터의 시스템 정보 확장-예측을 그리는 그래프를 사용 하 여 CPU 용량 예측 기능을 보여 줍니다.](media/cpu-forecast-2.png)

## <a name="local-functionality"></a>로컬 기능
시스템 정보는 Windows Server에서 로컬로 실행 됩니다. Windows Server 2019에 도입 된 새로운 기능을 사용 하 여 모든 데이터를 컴퓨터에서 직접 수집, 유지 및 분석 하므로 클라우드를 연결 하지 않고도 예측 분석 기능을 실현할 수 있습니다.

시스템 데이터는 컴퓨터에 저장 되며,이 데이터는 클라우드에서 다시 학습 하지 않아도 되는 예측 기능을 통해 분석 됩니다. 시스템 정보를 사용 하 여 사용자의 컴퓨터에 데이터를 유지할 수 있으며 예측 분석 기능을 활용할 수 있습니다.

## <a name="get-started"></a>시작하기

<iframe src=https://www.youtube-nocookie.com/embed/AJxQkx5WSaA width=560 height=315 allowfullscreen></iframe>

>[!TIP]
>이러한 짧은 비디오를 시청 하 여 시작 하 고, 시스템 정보를 안전 하 게 관리 하는 데 필요한 정보를 알아보세요. [10 분 이내에 System insights 시작](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

### <a name="requirements"></a>요구 사항
Windows Server 2019 인스턴스에서는 System Insights를 사용할 수 있습니다. 호스트와 게스트 컴퓨터, 모든 하이퍼바이저 및 모든 클라우드에서 실행 됩니다.

### <a name="install-system-insights"></a>시스템 정보 설치
>[!IMPORTANT]
>System Insights는 최대 1 년 분량의 데이터를 로컬로 수집 하 고 저장 합니다. 운영 체제를 업그레이드할 때 데이터를 유지 하려면 **전체 업그레이드를 사용**해야 합니다.

#### <a name="install-the-feature"></a>기능 설치
Windows 관리 센터 내에서 확장을 사용 하 여 System Insights를 설치할 수 있습니다.

![시스템 정보 확장에 대 한 0 일 환경](media/day-0-2.png)

**시스템 정보** 기능을 추가 하거나 PowerShell을 사용 하 여 서버 관리자 통해 직접 시스템 정보를 설치할 수도 있습니다.

```PowerShell
Add-WindowsFeature System-Insights -IncludeManagementTools
```

## <a name="provide-feedback"></a>피드백 제공
이 기능을 개선 하는 데 도움이 되는 사용자 의견을 보내 주시기 바랍니다. 다음 채널을 사용 하 여 피드백을 제출할 수 있습니다.
- **피드백 허브**: Windows 10의 피드백 허브 도구를 사용 하 여 버그 또는 피드백을 파일에 작성 합니다. 이렇게 하려면 다음을 지정 하십시오.
    - **범주**: 서버
    - **하위 범주**: 시스템 정보
- **Uservoice**: [uservoice 페이지](https://windowsserver.uservoice.com/forums/295071-management-tools)를 통해 기능 요청을 제출 합니다. 동료와 공유 하 여 중요 한 항목을 시작 하세요.
- **전자 메일**: 기능 팀에 개인적으로 피드백을 제출 하려면로 전자 메일을 보내세요 system-insights-feed@microsoft.com . 여전히 피드백 허브 또는 UserVoice를 사용 하도록 요청할 수 있다는 점에 유의 하세요.

## <a name="additional-references"></a>추가 참조
시스템 정보에 대 한 자세한 내용을 보려면 다음 리소스를 사용 하세요.

- [기능 이해](understanding-capabilities.md)
- [기능 관리](managing-capabilities.md)
- [기능 추가 및 개발](adding-and-developing-capabilities.md)
- [시스템 정보 FAQ](faq.md)