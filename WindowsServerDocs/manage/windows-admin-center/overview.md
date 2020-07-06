---
title: Windows Admin Center 개요
description: Windows Admin Center(Project Honolulu)를 사용하여 Windows Server를 관리하는 방법을 설명합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 01/07/2020
ms.localizationpriority: high
ms.prod: windows-server
ms.openlocfilehash: cb91b884edfbd105bc9e88a9d11b3b96055247c9
ms.sourcegitcommit: c40c29683d25ed75b439451d7fa8eda9d8d9e441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85833336"
---
# <a name="windows-admin-center"></a>Windows Admin Center

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 Windows 서버, 클러스터, 하이퍼 컨버지드 인프라는 물론 Windows 10 PC를 관리하기 위해 로컬로 배포된 브라우저 기반 앱입니다. Windows 이외의 추가 비용 없이 제공되며 프로덕션 환경에서 사용할 준비가 되었습니다.

새로운 기능을 알아보려면 [릴리스 기록](support/release-history.md)을 참조하세요.

## <a name="download-now"></a>지금 다운로드

Microsoft Evaluation Center에서 **[Windows Admin Center](https://www.microsoft.com/evalcenter/evaluate-windows-admin-center)를 다운로드합니다.** 비록 "평가 시작"이라고 하지만, 이는 일반적으로 프로덕션용으로 사용 가능한 버전입니다.

설치에 대한 도움말은 [설치](deploy/install.md)를 참조하세요. Windows Admin Center 시작에 대한 팁은 [시작](use/get-started.md)을 참조하세요.

Microsoft 업데이트를 사용하거나 Windows Admin Center를 수동으로 다운로드하여 설치하여 비 미리 보기 Windows Admin Center 버전을 업데이트할 수 있습니다. 미리 보기가 아닌 Windows Admin Center 버전은 각각 미리 보기가 아닌 다음 버전이 출시된 후 30일까지 지원됩니다. 자세한 내용은 [지원 정책](support/index.md)을 참조하세요.

## <a name="windows-admin-center-scenarios"></a>Windows Admin Center 시나리오

다음은 Windows Admin Center를 사용할 수 있는 몇 가지 방법입니다.

|     |     |
| --- | --- |
| ![](media/simple-icon.png)| **서버 관리 간소화** <br/> 서버 매니저와 같은 친숙한 도구의 현대화된 버전으로 서버와 클러스터를 관리합니다. 환경에서 서버를 5분 내에 바로 설치하고 관리하며, 추가 구성이 필요하지 않습니다. 자세한 내용은 [Windows Admin Center란?](understand/what-is.md)을 참조하세요. |
| ![](media/future-icon.png)| **하이브리드 솔루션 작업** <br/> Azure와 통합하면 선택적으로 온-프레미스 서버를 관련 클라우드 서비스와 선택적으로 연결할 수 있습니다. 자세한 내용은 [Azure 하이브리드 서비스](azure/index.md)를 참조하세요. |
| ![](media/secure-icon.png)| **하이퍼 컨버지드 관리 간소화** <br/> Azure Stack HCI 또는 Windows Server 하이퍼 컨버지드 클러스터의 관리를 간소화합니다. 간소화된 워크로드를 사용하여 VM, 스토리지 공간 다이렉트 볼륨, 소프트웨어 정의 네트워킹 등을 생성하고 관리합니다. 자세한 내용은 [Windows Admin Center를 사용하여 하이퍼 컨버지드 인프라 관리](use/manage-hyper-converged.md)를 참조하세요.|

다음은 개요를 보여주는 비디오와 이어서 자세한 정보를 제공하는 포스터입니다.
>[!VIDEO https://www.youtube.com/embed/WCWxAp27ERk]

[![Windows Admin Center 포스터](media/WAC1910Poster_thumb_small.PNG)](media/WAC1910Poster_thumb.png)

[PDF 다운로드](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1910Poster.pdf)


## <a name="contents-at-a-glance"></a>개념 개요

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>이해</h3>
            <ul>
            <li><a href="understand/what-is.md">Windows Admin Center란?</a>
            <li><a href="understand/faq.md">FAQ</a>
            <li><a href="understand/case-studies.md">사례 연구</a>
            <li><a href="understand/related-management.md">관련 관리 제품</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>계획</h3>
            <ul>
            <li><a href="plan/installation-options.md">나에게 적합한 설치 유형은 무엇인가요?</a>
            <li><a href="plan/user-access-options.md">사용자 액세스 옵션</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>배포 게스트 클러스터에</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">사용자 환경 준비</a>
            <li><a href="deploy/install.md">Windows Admin Center 설치</a>
            <li><a href="deploy/high-availability.md">고가용성 구현</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>구성</h3>
            <ul>
            <li><a href="configure/settings.md">Windows Admin Center 설정</a>
            <li><a href="configure/user-access-control.md">사용자 액세스 제어 및 사용 권한</a>
            <li><a href="configure/shared-connections.md">공유 연결</a>
            <li><a href="configure/using-extensions.md">확장</a>
            <li><a href="configure/use-powershell.md">PowerShell으로 자동화</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Windows Server Update Services와 함께</h3>
            <ul>
            <li><a href="use/get-started.md">연결 시작 및 추가</a>
            <li><a href="use/manage-servers.md">서버 관리</a>
            <li><a href="use/deploy-hyperconverged-infrastructure.md">하이퍼 컨버지드 인프라 배포</a>
            <li><a href="use/manage-hyper-converged.md">하이퍼 컨버지드 인프라 관리</a>
            <li><a href="use/manage-failover-clusters.md">장애 조치(failover) 클러스터 관리</a>
            <li><a href="use/manage-virtual-machines.md">가상 머신 관리</a>
            <li><a href="use/logging.md">로깅</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Azure 연결</h3>
            <ul>
            <li><a href="azure/index.md">Azure 하이브리드 서비스</a></li>
            <li><a href="azure/azure-integration.md">Azure에 Windows Admin Center 연결</a></li>
            <li><a href="azure/deploy-wac-in-azure.md">Azure에서 Windows Admin Center 배포</a></li>
            <li><a href="azure/manage-azure-vms.md">Windows Admin Center를 사용하여 Azure VM 관리</a></li>
            </ul>
        </td>
    </tr>
    <tr>
            <td style="vertical-align: top;">
            <h3>Support(지원)</h3>
            <ul>
            <li><a href="support/release-history.md">릴리스 기록</a>
            <li><a href="support/index.md">지원 정책</a>
            <li><a href="support/troubleshooting.md">일반적인 문제 해결 단계</a>
            <li><a href="support/known-issues.md">알려진 문제</a>
            </ul>
        </td>
            <td style="vertical-align: top;">
            <h3>확장</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">확장 개요</a>
            <li><a href="extend/understand-extensions.md">확장의 이해</a>
            <li><a href="extend/developing-extensions.md">확장 개발</a>
            <li><a href="extend/publish-extensions.md">가이드</a>
            <li><a href="extend/publish-extensions.md">확장 게시</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="video-based-learning"></a>비디오 기반 학습

다음은 Microsoft Ignite 2019 세션의 일부 비디오입니다.

- [Windows Admin Center: Azure Hybrid 가치 발견](https://aka.ms/WAC-BRK3165)
- [Windows Admin Center: 새로운 기능 및 다음 단계](https://aka.ms/WAC-BRK2048)
- [Windows Admin Center를 사용하여 Azure로부터 온-프레미스 서버를 자동으로 모니터링, 보안 및 업데이트](https://aka.ms/WAC-THR2146)
- [Windows Admin Center 타사 확장을 사용하여 더 많은 작업 수행](https://aka.ms/WAC-THR2140)
- [Windows Admin Center 전문가 되기: 배포, 구성 및 보안에 대한 모범 사례](https://aka.ms/WAC-THR2135)
- [Windows Admin Center: System Center 및 Microsoft Azure 조합으로 성능 개선](https://aka.ms/WAC-THR2176)
- [Windows Admin Center 및 Windows Server와 함께 Microsoft Azure 하이브리드 서비스를 사용하는 방법](https://aka.ms/WAC-THR2073)
- [라이브 Q&A: Windows Admin Center를 사용하여 하이브리드 서버 환경 관리](https://aka.ms/WAC-MLS1055)
- [학습 경로: 하이브리드 관리 기술](https://aka.ms/WAC-HybridMgmtTech)
- [실습 교육: Windows Admin Center 및 하이브리드](https://aka.ms/WAC-HOL2019)

다음은 Windows Server Summit 2019 세션의 일부 비디오입니다.

- [Windows Admin Center를 사용하여 하이브리드로 전환](https://aka.ms/WAC-WSS2019-GoHybridWAC)
- [Windows Admin Center v1904의 새로운 기능](https://aka.ms/WAC-WSS2019-WhatsNewv1904)

다음은 몇 가지 추가 리소스입니다.

- [새로워진 Windows Admin Center 서버 관리](https://aka.ms/WAC-ServerMgmtReimagined)
- [Windows Admin Center를 사용하여 어디서나 서버 및 가상 머신 관리](https://aka.ms/WAC-Webinar2019)
- [Windows Admin Center를 시작하는 방법](https://www.youtube.com/embed/PcQj6ZklmK0)

## <a name="see-how-customers-are-benefitting-from-windows-admin-center"></a>Windows Admin Center에서 고객이 혜택을 얻는 방법을 확인하세요.

|     |
| --- |
| "[Windows Admin Center]를 사용하여 관리 시스템을 관리하는 시간/노력이 75% 이상 줄어들었습니다."<br> *- Rand Morimoto, 사장, Convergent Computing* |
| "[Windows Admin Center] 덕분에 문제 없이 HTML5 포털에서 고객을 원격으로 관리할 수 있으며 Azure Active Directory와 완벽하게 통합되어 Multi-Factor Authentication 덕분에 보안을 향상시킬 수 있습니다."<br/> *- Silvio Di Benedetto, 설립자이자 수석 컨설턴트, Inside Technologies* |
| "보다 효과적인 방법으로 [Server Core] SKU를 배포하여 자원 효율성, 보안 및 자동화를 개선하는 동시에 여전히 좋은 수준의 생산성을 실현하고 스크립팅에만 의존하는 경우 발생할 수 있는 오류를 줄일 수 있었습니다." <br/> *- Guglielmo Mengora, 창립자 및 CEO, VaiSulWeb* |
| "[Windows Admin Center]를 통해 이제 고객은 특히 SMB 시장에서 내부 인프라를 관리하는 사용하기 쉬운 도구를 갖추게 되었습니다. 이를 통해 노력을 최소화하고 시간을 많이 단축했습니다. 또한 제일 좋은 것은 [Windows Admin Center]에 대한 추가 라이선스 비용이 없다는 점입니다!" <br/> *- Helmut Otto, 관리 이사, SecureGUARD* |

[프로덕션 환경에서 Windows Admin Center를 사용하는 회사에 대해 자세히 알아보세요.](understand/case-studies.md)

## <a name="related-products"></a>관련 제품

Windows Admin Center는 단일 서버 또는 클러스터를 관리하기 위해 설계되었습니다. 이는 RSAT(원격 서버 관리 도구), System Center, Intune, 또는 Azure Stack 등 기존의 Microsoft 모니터링 및 관리 솔루션을 기능을 보완하지만 대체하지 않습니다.

[Windows Admin Center가 다른 Microsoft 관리 솔루션을 보완하는 방법에 대해 알아봅니다.](understand/related-management.md)

## <a name="stay-updated"></a>최근 소식 받기

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR)[Twitter에서 Microsoft 팔로우](https://twitter.com/servermgmt)

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw)[블로그 읽기](https://techcommunity.microsoft.com/t5/windows-admin-center-blog/bg-p/Windows-Admin-Center-Blog)
