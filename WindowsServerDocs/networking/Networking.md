---
title: 네트워킹
description: 이 항목에서는 Windows Server 2016에서 사용할 수 있는 소프트웨어 정의 네트워킹 및 네트워크 플랫폼 기술을 개략적으로 살펴봅니다.
ms.prod: windows-server-threshold
layout: LandingPage
ms.technology: networking
ms.topic: landing-page
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bb5a605ef6438bfa6a2afe4963b8206f9dc84a3a
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121402"
---
# 네트워킹

>[!TIP]
> 이전 버전의 Windows Server에 대한 자세한 내용이 궁금하십니까? docs.microsoft.com에서 다른 [Windows Server 라이브러리](/previous-versions/windows/)를 확인할 수 있습니다. 또한 특정 정보에 대해 [이 사이트를 검색할](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) 수 있습니다.

<HR />

네트워킹은 소프트웨어 정의 데이터 센터 \(SDDC\) 플랫폼의 기본 요소로, Windows Server 2016은 조직에서 완벽하게 구현된 SDDC 솔루션으로 마이그레이션하는 데 도움이 되도록 새롭게 개선된 소프트웨어 정의 네트워킹 \(SDN\) 기술을 제공합니다.

네트워크를 정의 하는 소프트웨어 리소스로 관리 하는 경우 한 번, 응용 프로그램의 인프라 요구 사항에 설명 하 고 다음 선택할 수 있는 응용 프로그램 실행-온-프레미스 또는 클라우드에서 합니다. 

이러한 일관성 덕분에 이제는 응용 프로그램을 보다 손쉽게 확장할 수 있게 되었습니다. 또한 보안, 성능, 서비스 품질 및 가용성에 대해 안심하면서 어디서나 원활하게 응용 프로그램을 실행할 수 있습니다.

<HR />

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h2><a href="../networking/What-s-New-in-Networking.md">네트워킹의 새로운 기능</a></h2>
                                        </div>
                                    </div>
                                </div>
                             </div>
                          </a>
                        </li>
                     </ul>
<HR />

<h2>소프트웨어 정의 네트워킹</h2>

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="https://docs.microsoft.com/windows-server/networking/sdn/">SDN(소프트웨어 정의 네트워킹)</a><hr /></h3>이 항목을 사용하여 Windows Server, System Center 및 Microsoft Azure에서 제공되는 SDN 기술에 대해 자세히 알아볼 수 있습니다.</p>
                        
                                        <p><b>참고:</b> 네트워크 컨트롤러 및 소프트웨어 부하 분산 노드 같은 SDN 인프라 서버를 실행하는 Hyper-V 호스트 및 가상 컴퓨터 \(VMs\)의 경우, 반드시 Windows Server Datacenter 버전을 설치해야 합니다. SDN\ 제어 네트워크에 연결된 테넌트 워크로드 VM만 포함하고 있는 Hyper-V 호스트의 경우에는 Windows Server Standard 버전을 실행할 수 있습니다.</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md">스크립트를 사용하여 소프트웨어 정의 네트워크 인프라 배포</a><hr /></h3>이 가이드에서는 테스트 랩 환경에서 가상 네트워크와 게이트웨이 사용 하 여 네트워크 컨트롤러를 배포 하는 방법을 설명 합니다.</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-controller/Network-Controller.md">네트워크 컨트롤러</a><hr /></h3>네트워크 컨트롤러 관리, 구성, 모니터링 및 데이터 센터의 가상 및 실제 네트워크 인프라의 문제를 해결 하는 자동화의 프로그래밍 가능한 중앙된 위치를 제공 합니다.</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md">SDN에서의 소프트웨어 부하 분산 &#40;SLB&#41;</a><hr /></h3>Windows Server 2016에 소프트웨어 정의 네트워킹(SDN)을 배포하고 있는 클라우드 서비스 공급자 \(CSP\)와 엔터프라이즈는 소프트웨어 부하 분산 \(SLB\)을 사용하여 가상 네트워크 리소스 간에 테넌트 및 테넌트 고객 네트워크 트래픽을 고르게 분산시킬 수 있습니다. Windows Server SLB 높은 가용성과 확장성이 같은 작업을 호스트 하는 여러 서버를 수 있습니다.</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md">SDN용 RAS 게이트웨이</a><hr /></h3>Windows Server 2016에서 소프트웨어 기반의 다중 테넌트 경계 게이트웨이 프로토콜 \(BGP\)을 지원하는 라우터인 RAS 게이트웨이는 Hyper-V 네트워크 가상화를 사용하여 여러 테넌트 가상 네트워크를 호스팅하고 있는 클라우드 서비스 공급자 \(CSPs\)와 엔터프라이즈를 위해 설계되었습니다.</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md">네트워크 기능 가상화</a><hr /></h3>소프트웨어 정의 데이터 센터에서는 하드웨어 어플라이언스 \(예: 부하 분산 장치, 방화벽, 라우터, 스위치 등\)가 수행하고 있는 네트워크 기능이 가상 어플라이언스로 점차 가상화되고 있습니다. 이 "네트워크 기능 가상화" 서버 가상화 및 네트워크 가상화의 자연 스러운 진행 됩니다.</p>                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md">데이터 센터 방화벽 개요</a><hr /></h3>데이터 센터 방화벽은 네트워크 계층, 5 개 튜플(프로토콜, 원본 및 대상 포트 번호, 원본 및 대상 IP 주소) 상태 저장, 다중 테넌트 방화벽입니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

<HR />

## <a name="bkmk_networking"></a>네트워킹 기술

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="branchcache/BranchCache.md">BranchCache</a><hr /></h3>
                                        <p>BranchCache는 광역 네트워크 \(WAN\) 대역폭 최적화 기술입니다. 사용자가 원격 서버의 콘텐츠에 액세스할 때 WAN 대역폭을 최적화하기 위해 BranchCache는 본사 또는 호스팅된 클라우드 콘텐츠 서버에서 콘텐츠를 가져와서 지점 사무실의 캐시에 해당 콘텐츠를 저장하기 때문에 지점 사무실의 클라이언트 컴퓨터가 WAN을 통해서가 아니라 로컬로 콘텐츠에 액세스할 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="core-network-guide/core-network-guide-windows-server.md">핵심 네트워크 가이드</a><hr /></h3>
                                        <p>핵심 네트워크 가이드를 통해 Windows Server 네트워크를 배포하는 방법을 확인하고 핵심 네트워크 부록 가이드를 통해 배포된 네트워크에 기능을 추가합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../remote/remote-access/directaccess/DirectAccess.md">DirectAccess</a><hr /></h3>
                                        <p>DirectAccess는 조직의 네트워크 리소스에 원격 사용자를 연결합니다. </p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="dns/dns-top.md">DNS(Domain Name System)"></a><hr /></h3>
                                        <p>도메인 이름 시스템 \(DNS\)은 TCP/IP를 구성하는 업계 표준 프로토콜 제품군의 하나로, DNS 클라이언트와 DNS 서버가 컴퓨터 및 사용자에게 컴퓨터 이름-IP 주소 매핑 이름 확인 서비스를 제공합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/dhcp/dhcp-top.md">동적 호스트 구성 프로토콜 &#40;DHCP&#41;</a><hr /></h3>
                                        <p>동적 호스트 구성 프로토콜 \(DHCP\)은 IP 주소 및 기타 관련 구성 정보(서브넷 마스크 및 기본 게이트웨이)와 함께 인터넷 프로토콜 \(IP\) 호스트를 자동으로 제공하는 클라이언트/서버 프로토콜입니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md">Hyper-V 네트워크 가상화</a><hr /></h3>
                                        <p>Hyper-V 네트워크 가상화 \(HNV\)는 공유되는 실제 네트워크 인프라를 기반으로 고객 네트워크를 가상화할 수 있도록 합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md">Hyper-V 가상 스위치</a><hr /></h3>
                                        <p>Hyper-V 가상 스위치는 Hyper-V 서버 역할을 설치할 때 Hyper-V 관리자에서 사용할 수 있는 소프트웨어 기반의 계층 2 이더넷 네트워크 스위치입니다. 스위치에는 프로그램 방식으로 관리되며 확장 가능한 기능이 포함되어 있어 가상 시스템을 가상 네트워크와 실제 네트워크에 모두 연결할 수 있습니다. 또한 Hyper-V 가상 스위치를 사용하여 보안, 격리 및 서비스 수준의 정책을 적용할 수 있습니다. </p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/ipam/ipam-top.md">IP 주소 관리 &#40;IPAM&#41;</a><hr /></h3>
                                        <p>IP 주소 관리 \(IPAM\)는 풍부한 사용자 서비스를 통해 IP 주소 인프라의 계획, 배포, 관리 및 모니터링을 총체적으로 지원하는 통합 도구 세트입니다. IPAM은 네트워크 상의 IP 주소 인프라 서버 및 도메인 이름 시스템 \(DNS\) 서버를 자동으로 검색하여 중앙 인프라에서 이들을 관리할 수 있도록 지원합니다. </p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/Network-Load-Balancing.md">네트워크 부하 분산</a><hr /></h3>
                                        <p>네트워크 부하 분산 \(NLB\)은 TCP/IP 네트워킹 프로토콜을 사용하여 여러 서버에 트래픽을 분산합니다. SDN이 아닌 배포의 경우, NLB는 부하의 증가에 따라 서버를 추가하여 인터넷 정보 서비스 \(IIS\)를 실행하는 웹 서버와 같은 상태 비저장 응용 프로그램을 확장할 수 있도록 해줍니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/hpn/hpn-top.md">고성능 네트워킹</a><hr /></h3>
                                        <p>Windows Server 2016의 네트워크 오프로드 및 최적화 기술에는 소프트웨어 전용(SO) 기능 및 기술과 소프트웨어 및 하드웨어(SH) 통합 기능 및 기술, 하드웨어 전용(HO) 기능 및 기술이 포함되어 있습니다.</p>

                                        <p>다음과 같은 오프로드 및 최적화 기술 설명서를 사용할 수도 있습니다.<p>
                                        <hr />
                                        <a href="technologies/conv-nic/cnic-top.md">고성능 네트워킹</a><hr />
                                        <a href="technologies/dcb/dcb-top.md">DCB(데이터 센터 브리징)</a><hr />
                                        <a href="technologies/vrss/vrss-top.md">가상 수신측 배율(vRSS)</a>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/nps/nps-top.md">네트워크 정책 서버</a><hr /></h3>
                                        <p>
네트워크 정책 서버(NPS)를 사용하면 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 생성하여 적용할 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/netsh/netsh.md">네트워크 셸(Netsh)</a><hr /></h3>
                                        <p>
네트워크 셸 \(netsh\) 네트워킹 유틸리티를 사용하여 Windows Server 2016 및 Windows 10에서 네트워킹 기술을 관리할 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/network-subsystem/net-sub-performance-top.md">네트워크 하위 시스템 성능 조정</a><hr /></h3>
                                        <p>
이 항목에서는 서버 워크로드에 적합한 네트워크 어댑터를 선택하고 네트워크 인터페이스, 네트워크 관련 성능 카운터 및 성능 조정 네트워크 어댑터, 수신측 배율 \(RSS\), 수신측 통합 \(RSC\) 같은 관련 네트워킹 기술을 주문하는 방법에 대한 정보를 제공합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/nic-teaming/NIC-Teaming.md">NIC 팀</a><hr /></h3>
                                        <p>
NIC 팀 기능을 사용하면 실제 이더넷 네트워크 어댑터를 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터로 그룹화할 수 있습니다. 이러한 가상 네트워크 어댑터는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/qos/qos-policy-top.md">서비스 품질(QoS) 정책</a><hr /></h3>
                                        <p>
그룹 정책을 통해 설정이 배포되는 QoS 프로필을 생성하여 Active Directory 인프라 전체에서 네트워크 대역폭을 관리하기 위한 중심점으로 QoS 정책을 사용할 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="technologies/wins/wins-top.md">WINS(Windows 인터넷 이름 서비스)</a><hr /></h3>
                                        <p>
Windows 인터넷 이름 서비스(WINS)는 IP 주소에 NetBIOS 이름을 매핑하는 기존의 컴퓨터 이름 등록 및 확인 서비스입니다. WINS를 사용하기 보다는 DNS를 사용하는 것이 좋습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../remote/remote-access/remote-access.md">원격 액세스</a><hr /></h3>
                                        <p>
DirectAccess 및 가상 사설망 \(VPN\) 같은 원격 액세스 기술을 사용하여 원격 작업자를 내부 네트워크 리소스에 연결할 수 있습니다. 또한, 근거리 네트워크 \(LAN\) 라우팅 및 웹 응용 프로그램 프록시를 위해 원격 액세스를 사용할 수 있습니다. 웹 응용 프로그램 프록시는 회사 네트워크 내부의 웹 응용 프로그램에 역방향 프록시 기능을 제공하여 모든 장치의 사용자가 회사 네트워크 권역을 벗어나서도 해당 네트워크에 액세스할 수 있도록 합니다.</p>

                                        <p>원격 액세스 서버 역할의 역할 서비스인 웹 응용 프로그램 프록시에 대한 자세한 내용은 <a href="https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server">Windows Server 2016의 웹 응용 프로그램 프록시를 참조하세요.</a></p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture">Windows 컨테이너 네트워킹</a><hr /></h3>
                                        <p>
Windows 컨테이너 네트워킹을 사용하면 업계 표준 도구 및 워크플로를 통해 Windows 10 및 Windows Server 호스트에서 컨테이너 끝점을 연결하도록 네트워크를 생성 및 관리할 수 있습니다. Windows 컨테이너 네트워크는 사설 플랫 L2와 라우팅된 L3를 포함하여 여러 토폴로지를 지원합니다.</p>

                                        <p>또한 Windows 호스트 네트워킹 서비스 \(HNS\)와 통신하는 플러그인을 통해 Docker, Kubernetes 또는 Windows PowerShell을 사용하여 호스트에서 로컬로 생성할 수 있는 오버레이도 지원됩니다. 로컬 에이전트를 거쳐 각 노드의 HNS와 통신함으로써 높은 수준의 오케스트레이션 시스템을 통해 다중\ 노드 클러스터 네트워크를 생성 및 관리할 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<HR />
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-network.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3><a href="../remote/remote-access/vpn/vpn-top.md">VPN(가상 사설망)</a><hr /></h3>
                                        <p>
DirectAccess 및 VPN은 원격 액세스 서버 역할의 역할 서비스입니다.</p>

                                        <p>원격 액세스를 VPN 서버로 설치하면 가상 사설망 \(VPN\)을 사용하여 인터넷을 통해 원격 작업자를 회사 네트워크에 연결하고 암호화된 연결을 통해 개인 정보 보호를 유지할 수 있습니다.</p>

                                       <p> Windows Server 원격 액세스 VPN과 Windows 10 클라이언트 컴퓨터에서는 Always On VPN을 배포할 수 있습니다. Always On VPN을 사용하면 항시 연결되는 원격 VPN 클라이언트를 관리할 수 있으며, VPN에서 회사 네트워크로의 연결을 수동으로 설정 및 해제할 필요가 없다는 점에서 원격 작업자에게 편의를 제공할 수 있습니다.</p>

                                       <p>자세한 내용은 <a href="https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy">Windows Server 2016 및 Windows 10을 위한 원격 액세스 Always On VPN 배포 가이드를 참조하세요.</a></p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

## 추가 리소스

Windows Server 2016 이전 버전의 운영 체제를 위한 네트워킹 리소스는 다음 위치에서 사용할 수 있습니다.

- Windows Server 2012 및 Windows Server 2012 R2 [네트워킹 개요](https://technet.microsoft.com/library/hh831357.aspx)
- Windows Server 2008 및 Windows Server 2008 R2 [네트워킹](https://technet.microsoft.com/library/cc753940)
- Windows Server 2003 [Windows Server 2003/2003 R2에서 사용 중지된 콘텐츠 ](https://www.microsoft.com/download/details.aspx?id=53314)
