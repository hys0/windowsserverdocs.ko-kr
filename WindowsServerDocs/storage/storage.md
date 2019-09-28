---
title: 스토리지
description: ''
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 03/08/2019
ms.openlocfilehash: eadac31cb623a15dd308f7e33f984fe1fb46ffe5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365934"
---
# <a name="storage"></a>스토리지

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

>[!TIP]
> 이전 버전의 Windows Server에 대한 자세한 내용이 궁금하십니까? docs.microsoft.com에서 다른 [Windows Server 라이브러리](/previous-versions/windows/)를 확인할 수 있습니다. 또한 특정 정보에 대해 [이 사이트를 검색](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)할 수 있습니다.

<hr />
Windows Server의 저장소는 가상화된 워크로드에 집중하는 SDDC(소프트웨어 정의 데이터 센터) 고객을 위한 새롭고 향상된 기능을 제공합니다. Windows Server는 또한 기존 워크로드에 파일 서버를 사용하는 기업 고객을 위한 폭넓은 지원을 제공합니다.

<hr />
<ul class="cardsF panelContent">
<li>
 <a href="whats-new-in-storage.md">
                            <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                            <h2>새로운 기능</h2>
                                            <p>Windows Server 저장소의 새로운 기능 알아보기</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
<hr />
<ul class="cardsF panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>가상화된 워크로드를 위한 소프트웨어 정의 저장소</h3>
<HR />
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">스토리지 공간 다이렉트</a></h3> 새 실제 디스크를 추가 하 고 가상 디스크 복구 시간을 단축 하기 위해 SATA 및 NVME 장치를 비롯 한 직접 연결 된 로컬 저장소를 사용 하 여 디스크 사용을 최적화 합니다. 또한 공유 SAS 및 독립 실행형 저장소 공간에 대한 정보는 <a href="storage-spaces/overview.md">저장소 공간</a>을 참조하십시오.</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">스토리지 복제본</a></h3> 재해 준비 및 복구를 위해 클러스터 또는 서버 간에 저장소에 상관 없는 블록 수준의 동기 복제를 지원 하며 고가용성을 위해 사이트 간에 장애 조치 (failover) 클러스터를 확장 합니다. 동기 복제를 사용하면 파일 시스템 수준에서 데이터가 손실되지 않고 크래시 일관성이 있는 볼륨을 사용하여 실제 사이트의 데이터를 미러링할 수 있습니다.</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">저장소 QoS (서비스 품질)</a></h3> Hyper-v를 사용 하 여 가상 컴퓨터의 저장소 성능을 중앙에서 모니터링 및 관리 하 고 스케일 아웃 파일 서버 역할은 동일한 파일 서버 클러스터를 사용 하 여 여러 가상 컴퓨터 간에 저장소 리소스 공평을 improveing 자동으로 관리 합니다.</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">데이터 중복 제거</a></h3> 복제를 위해 볼륨의 데이터를 검사 하 여 볼륨의 사용 가능한 공간을 최적화 합니다. 식별된 경우 볼륨의 데이터 집합에서 중복된 부분이 한 번 저장되며 필요한 경우 추가적인 절약을 위해 압축됩니다. 데이터 중복 제거는 데이터 충실도 또는 무결성을 손상시키지 않고 중복성을 최적화합니다.</p>
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
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>일반용 파일 서버</h3>
<HR />
                        <p><h3><a href="storage-migration-service/overview.md">저장소 마이그레이션 서비스</a></h3>서버에서 데이터를 인벤토리 하는 그래픽 도구를 사용 하 여 서버를 최신 버전의 Windows Server로 마이그레이션하고, 데이터 및 구성을 최신 서버로 전송 하 고, 필요에 따라 이전 서버의 id를 새 서버로 이동 하 여 앱과 사용자를 새 서버로 이동 합니다. 아무것도 변경할 필요가 없습니다.</p>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">클라우드 폴더</a></h3> 회사 Pc 외에도 개인 컴퓨터 및 장치 (BYOD)에 작업 파일을 저장 하 고 액세스 합니다. 사용자는 작업 파일을 저장하고 어디에서나 액세스할 수 있는 편리한 위치를 얻을 수 있습니다. 조직은 중앙에서 관리 되는 파일 서버에 파일을 저장하고 선택적으로 사용자 장치 정책(예: 암호화 및 잠금 화면 암호)을 지정하여 회사 데이터에 대한 제어를 유지합니다.</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">오프라인 파일 및 폴더 리디렉션</a></h3> 로컬 폴더 (예: Documents 폴더)의 경로를 네트워크 위치로 리디렉션하고, 속도 및 가용성을 높이기 위해 콘텐츠를 로컬로 캐시 합니다.</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">로밍 사용자 프로필</a></h3> 사용자 프로필을 네트워크 위치로 리디렉션합니다.</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">DFS 네임스페이스</a></h3> 서로 다른 서버에 있는 공유 폴더를 논리적으로 구성 된 하나 이상의 네임 스페이스로 그룹화 합니다. 사용자에게 각 네임스페이스는 일련의 하위 폴더가 있는 하나의 공유 폴더로 보입니다. 그러나 네임스페이스의 기본 구조는 다양한 서버 및 여러 사이트에 있는 많은 수의 파일 공유로 구성될 수 있습니다.</p>
<HR />
                        <p><h3><a href="dfs-replication/dfsr-overview.md">DFS 복제</a></h3> 여러 서버 및 사이트에서 폴더 (DFS 네임 스페이스 경로에 참조 된 폴더 포함)를 복제 합니다. DFS 복제에서는 RDC(원격 차등 압축)라는 압축 알고리즘을 사용합니다. RDC는 파일의 데이터에 대한 변경 내용을 검색하고 DFS 복제가 전체 파일 대신 변경된 파일 블록만 복제할 수 있게 합니다.</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">파일 서버 리소스 관리자</a></h3> 파일 서버에 저장 된 데이터를 관리 및 분류 합니다.<p>
<HR />
                        <p><h3><a href="iscsi/iscsi-target-server.md">iSCSI 대상 서버</a></h3> iSCSI(인터넷 SCSI) 표준을 사용하여 네트워크의 다른 서버 및 응용 프로그램에 대한 블록 저장소를 제공합니다.</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">iSCSI 대상 서버</a></h3> 는 중앙 위치에 저장 된 단일 운영 체제 이미지에서 수백 대의 컴퓨터를 부팅할 수 있습니다. 이를 통해 효율성, 가용성, 보안 및 관리 효율성을 높일 수 있습니다.</p>
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
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>파일 시스템, 프로토콜 등</h3>
<HR />
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> 데이터 가용성을 극대화 하 고, 다양 한 워크 로드에서 매우 큰 데이터 집합으로 효율적으로 확장 하 고, 소프트웨어 또는 하드웨어 오류에 상관 없이 손상 복구를 통해 데이터 무결성을 제공 하는 복원 력 파일 시스템입니다.<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">SMB (서버 메시지 블록) 프로토콜</a></h3> 컴퓨터의 응용 프로그램에서 파일을 읽고 쓸 수 있으며 컴퓨터 네트워크의 서버 프로그램에서 서비스를 요청할 수 있도록 하는 네트워크 파일 공유 프로토콜입니다. SMB 프로토콜은 해당 TCP/IP 프로토콜이나 기타 네트워크 프로토콜상에서 사용될 수 있습니다. SMB 프로토콜을 사용하면 응용 프로그램이나 응용 프로그램의 사용자가 원격 서버에 있는 파일이나 기타 리소스를 액세스할 수 있습니다. 즉, 원격 서버의 파일을 읽고 만들며 업데이트할 수 있습니다. 또한 SMB 클라이언트 요청을 수신하도록 설정된 서버 프로그램과 통신할 수 있습니다.<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">저장소 클래스 메모리</a></h3> 컴퓨터 메모리 (매우 빠름)와 비슷한 성능을 제공 하지만 일반 저장소 드라이브의 데이터 지 속성을 제공 합니다. Windows는 저장소 클래스 메모리를 일반 드라이브(빠름)처럼 취급하지만, 장치 상태를 관리하는 방식에서 약간 차이가 있습니다.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">BitLocker 드라이브 암호화</a></h3> 는 컴퓨터가 변조 되거나 운영 체제가 실행 되 고 있지 않은 경우에도 볼륨에 데이터를 암호화 된 형식으로 저장 합니다. 이는 오프라인 공격, 설치된 운영 체제를 비활성화하거나 우회하는 공격, 데이터를 별도로 공격하기 위해 하드 드라이브를 물리적으로 제거하여 이루어지는 공격을 차단하는 데 도움이 됩니다.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">N</a></h3> 최신 버전의 Windows 및 Windows Server에 대 한 주 파일 시스템-보안 설명자, 암호화, 디스크 할당량 및 다양 한 메타 데이터를 비롯 한 전체 기능 집합을 제공 하며, CSV (클러스터 공유 볼륨)와 함께 사용 하 여 지속적으로 제공할 수 있습니다. 장애 조치 (Failover) 클러스터의 여러 노드에서 동시에 액세스할 수 있는 사용 가능한 볼륨입니다.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">NFS (네트워크 파일 시스템)</a></h3> 는 Windows 및 비 Windows 컴퓨터를 구성 하는 유형이 다른 환경을 제공 하는 기업에 대 한 파일 공유 솔루션을 제공 합니다.<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## <a name="in-azure"></a>Azure에서

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure StorSimple](https://www.microsoft.com/en-us/cloud-platform/azure-storsimple)
