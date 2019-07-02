---
title: Management
description: Windows Server 관리에 대한 도구, 권장 사항 및 지침 알아보기
ms.prod: windows-server-threshold
layout: LandingPage
ms.technology: manage
ms.topic: landing-page
author: lizap
ms.author: elizapo
ms.localizationpriority: high
ms.openlocfilehash: e6a5357e3e33b3d3318a3e281bbb5c80be842155
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63721376"
---
# <a name="management"></a>Management


>[!TIP]
> 이전 버전의 Windows Server에 대한 정보를 찾으시나요? docs.microsoft.com에서 다른 [Windows Server 라이브러리](/previous-versions/windows/)를 확인하세요. [이 사이트에서 특정 정보를 검색](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)할 수도 있습니다.

<hr />

필요한 기능에 대한 특정 역할을 포함하여 사용자 환경에 Windows Server를 배포했다면, 이제 다음 단계는 이러한 서버를 관리하는 것입니다. Windows Server에는 Windows Server 환경을 이해하고 특정 서버를 관리하며 성능을 미세 조정하여 결국은 많은 관리 작업을 자동화할 수 있도록 도와주는 다양한 도구들이 포함되어 있습니다. 

Windows Server 인스턴스를 관리하는 데 사용하는 도구는 배포한 시스템 유형(데스크톱 환경 포함 Windows Server 또는 Server Core), 실제 머신이냐 가상 머신이냐, 서버가 어디에 위치하냐에 따라 크게 달라집니다. 다음 정보를 사용하여 Windows Server에서 기본적인 관리 작업을 수행합니다.

다음 표를 사용하여 어떤 도구를 사용할 것인지 결정합니다.

| 본인 상태   | Windows Admin Center 설치 및 실행 | Windows Server에서 서버 관리자 실행 | Windows 10의 RSAT에서 서버 관리자 실행 |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Windows 10 PC 사용 중 | X  |                                      | X                                        |
| 데스크톱 환경을 실행하는 Windows Server 시스템 사용 중 | X | X | X |
| Server Core를 실행하는 Windows Server 시스템 사용 중 |X(Windows 10에 설치, Server Core 관리에 사용) | | X |
| 내 Windows Server 시스템에서 멀리 떨어진 곳에 위치 |X | | X |
| Windows Server 시스템에서 멀리 떨어진 곳에 위치해 있지만, 데스크톱 환경을 갖추고 있음 |X | RDS를 사용하여 서버에 원격 연결한 다음, 서버 관리자를 사용 | X |

아래에 설명된 도구 외에도 [원격 데스크톱 서비스](../remote/remote-desktop-services/welcome-to-rds.md)를 사용하여 온-프레미스, 원격 및 가상 서버에 액세스할 수 있습니다. 서버 관리자를 사용하여 관리 작업을 수행할 수 있습니다.

<HR />

<ul class="cardsI panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server 시스템 및 환경 관리</h3>
<HR />
                        <p><h3><a href="../manage/windows-admin-center/overview.md">Windows Admin Center로 온-프레미스 시스템, 원격 시스템 및 UI가 없는 시스템 관리</a></h3>Azure 또는 클라우드 종속성 없이 Windows Server의 온-프레미스 관리를 활성화하는 브라우저 기반 관리 앱입니다. Windows Admin Center(이전에 "Project Honolulu"로 불림)는 서버 인프라의 모든 측면에 대한 모든 제어를 제공하고 인터넷에 연결되지 않은 개인 네트워크에서의 관리에 특히 유용합니다. 게이트웨이 서버에서 Windows 10에 Windows Admin Center를 설치하거나 관리할 Windows Server 시스템에 직접 설치할 수 있습니다.</p>
<HR />
                        <p><h3><a href="server-manager/server-manager.md">서버 관리자를 사용하여 온-프레미스 시스템 관리</a></h3>관리 콘솔은 Windows Server 전체 설치에 포함되어 있습니다. (UI를 설치하지 않는 경우 사용할 수 없습니다. Server Core는 서버 관리자를 포함하지 않습니다.) 서버 관리자를 사용하여 서버 역할을 설치 및 제거하고, 원격 서버를 추가 및 제거하고, 서비스를 시작 및 중지하고 사용자 환경에 대해 수집된 데이터를 봅니다.</p>
<HR />
                        <p><h3><a href="../remote/remote-server-administration-tools.md">RSAT(원격 서버 관리 도구)를 사용하여 원격 시스템과 UI가 포함되지 않은 시스템을 관리</a></h3>환경에 Server Core 또는 원격 서버(온-프레미스 또는 가상 머신) 설치가 포함된 경우 RSAT를 사용하여 시스템을 관리할 수 있습니다. RSAT에는 서버 관리자가 포함되어 있기 때문에 이를 사용하여 모든 서버를 관리할 수 있습니다. RSAT는 Windows 10에서 실행됩니다. Windows Server Core에 RSAT를 설치할 수 없습니다. 명령줄에서 Server Core 설치를 관리할 수도 있습니다. <a href="server-core/server-core-administer.md">Server Core의 기본 관리 작업</a>을 참조하세요.
<HR />
                        <p><h3><a href="windows-server-update-services/get-started/windows-server-update-services-wsus.md">Windows Server 시스템에 대한 업데이트 관리</a></h3>WSUS(Windows Server Update Services)를 사용하여 Windows Server 환경의 시스템에 대한 업데이트를 관리 및 배포합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>환경에 대한 정보 수집</h3>
<HR />
                        <p><h3><a href="get-started-with-setup-and-boot-event-collection.md">이벤트 컬렉션 설치 및 부팅</a></h3>설치 및 부팅 이벤트 수집을 사용하면 "수집기" 컴퓨터를 지정하여 부팅을 할 때나 설정 프로세스를 진행할 때 다른 컴퓨터에서 발생하는 중요 이벤트를 다양하게 수집할 수 있습니다. 그런 다음 이벤트 뷰어, 메시지 분석기, Wevtutil, 또는 Windows PowerShell cmdlet 통해 수집 된 이벤트를 나중에 분석할 수 있습니다. </p>
<HR />
                        <p><h3><a href="software-inventory-logging/get-started-with-software-inventory-logging.md">소프트웨어 인벤토리 로깅(SIL)</a></h3>Windows Server의 소프트웨어 인벤토리 로깅은 서버 관리자가 서버에 설치된 Microsoft 소프트웨어 목록을 검색하는 데 도움이 되는 간단한 PowerShell cmdlet 집합이 포함된 기능입니다. 또한 이 데이터를 수집하고 집계를 위해 HTTPS 프로토콜을 사용하여 네트워크를 통해 정기적으로 대상 웹 서버에 전달하는 기능을 제공합니다. 주로 시간별 수집 및 전달을 위한 기능 관리도 PowerShell 명령을 통해 수행됩니다.</p>
<HR />
                        <p><h3><a href="user-access-logging/get-started-with-user-access-logging.md">사용자 액세스 로깅(UAL)</a></h3>사용자 액세스 로깅은 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행하는 컴퓨터에서 로깅된 고유한 클라이언트 디바이스 및 사용자 요청 이벤트를 로컬 데이터베이스로 집계합니다. 이렇게 레코드는 서버 관리자가 쿼리를 통해 서버 역할, 사용자, 장치, 로컬 서버 및 날짜를 기준으로 수량과 인스턴스를 검색하는 데 사용할 수 있습니다. 또한 UAL은 타사 소프트웨어 개발자가 집계할 UAL 이벤트를 계측할 수 있도록 해줍니다. </a>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>성능을 위해 Windows Server 환경 조정</h3>
<HR />
                        <p><h3><a href="performance-tuning/index.md">성능 튜닝 지침</a></h3>특히 시간이 지나면서 워크로드의 성격이 약간 달라지는 경우에는 일련의 가이드라인을 검토하여 Windows Server에서 서버 설정을 조정하여 성능 또는 에너지 효율성을 높일 수 있습니다.</p>
<HR />
                        <p><h3><a href="server-performance-advisor/microsoft-server-performance-advisor.md">Microsoft Server Performance Advisor</a></h3>Microsoft Server Performance Advisor(SPA)를 사용하면 메트릭을 수집하여 소프트웨어 에이전트를 추가하거나 프로덕션 환경의 서버를 재구성하지 않고도 Windows Server에서 손쉽게 성능 문제를 진단할 수 있습니다. SPA는 권장 사항과 함께 포괄적인 성능 보고서와 기록 차트를 생성합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server 관리 자동화</h3>
<HR />
                        <p><h3><a href="https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-5.1">Windows PowerShell</a></h3>Windows PowerShell은 관리 작업을 신속하게 자동화할 수 있도록 설계된 명령줄 셸 및 스크립트 언어입니다. </p>
<HR />
                        <p><h3><a href="windows-commands/windows-commands.md">Windows 명령</a></h3>Windows 명령줄 도구는 Windows에서 관리 작업을 수행하는 데 사용됩니다. 명령 참조를 사용하면 명령줄 도구를 숙지하고 명령 셸을 자세하게 이해하며 배치 파일이나 스크립트 도구를 사용하여 명령줄 작업을 자동화할 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server 관리 자동화</h3>
<HR />
                        <p><h3><a href="..\manage\system-insights\overview.md">시스템 인사이트</h3></a>기본 예측 분석은 로컬에서 성능 카운터 및 ETW 이벤트와 같은 Windows Server 시스템 데이터를 분석하여 IT 관리자가 자체 배포에서 문제가 되는 동작을 사전 예방적으로 감지하고 처리하는 것을 돕습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>