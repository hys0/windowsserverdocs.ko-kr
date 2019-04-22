---
title: Windows Server, 버전 1709의 새로운 기능
description: 계산, ID, 관리, 자동화, 네트워킹, 보안, 저장소의 새로운 기능입니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: medium
ms.openlocfilehash: 1d63721dde484756e67b68bcff078257c130ae36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825494"
---
# <a name="whats-new-in-windows-server-version-1709"></a>Windows Server, 버전 1709의 새로운 기능

>적용 대상: Windows Server(반기 채널)

<img src="../media/landing-icons/new.png" style='float:left; padding:.5em;' alt="Icon showing a newspaper">&nbsp;이 콘텐츠는 Windows Server, 버전 1709의 새로운 기능과 변경된 기능을 설명하는 내용입니다. 여기에 나열된 새로운 기능 및 변경 사항은 이 릴리스를 사용할 때 가장 많은 영향을 줄 수 있습니다. [Windows Server, 버전 1709](https://blogs.technet.microsoft.com/windowsserver/2017/08/24/sneak-peek-1-windows-server-version-1709/)도 참조하세요.
   

## <a name="new-cadence-of-releases"></a>새로운 릴리스 흐름

이 릴리스부터 Windows Server 기능 업데이트를 받는 방법은 두 가지입니다.
- **장기 서비스 채널 (LTSC)**: 5 년 간의 연장 지원 및 5 년 추가 지원으로 일반적인 방식으로 비즈니스입니다. 지난 20년 동안 지원되었던 것과 동일한 방법으로 2~3년마다 다음 LTSC로 업그레이드하는 옵션이 있습니다.
- **반기 채널 (SAC)**: Software Assurance 혜택 이며 프로덕션 환경에서 완전히 지원 됩니다. 차이점은 18개월 동안 지원되고 6개월마다 새 버전이 있다는 것입니다.

릴리스 채널에는 이와 관련된 요구 사항이 요약되어 있습니다.

|   | 반기 채널 | 장기 서비스 채널 |
| ------------- | ------------- | ------------ |
| 릴리스 흐름  | 1년에 2회(봄과 가을)  | 2~3년마다 |
| 지원 일정  | 18개월 일반 프로덕션 지원  | 5년 일반 지원 + 5년 추가 지원 |
| 가용성  | Software Assurance 또는 Azure(클라우드 호스트)  | 모든 채널 |
| 명명 규칙  | Windows Server, 버전 YYMM  | Windows Server YYYY |

자세한 내용은 [Windows Server 반기 채널 개요](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview)를 참조하세요.

## <a name="application-containers-and-micro-services"></a>응용 프로그램 컨테이너 및 마이크로 서비스

- Server Core 컨테이너 이미지가 기존 코드 베이스 또는 응용 프로그램을 최소한으로 변경되었고 60% 더 작은 컨테이너로 마이그레이션할 수 있는 리프트 앤 시프트 시나리오에 더욱 최적화되었습니다. 
- Nano 서버 컨테이너 이미지는 약 80% 더 작습니다.
    - Windows Server 반기 채널에서 컨테이너 기본 OS 이미지로서의 Nano 서버가 390MB에서 80MB로 줄었습니다.
- Hyper-V 격리가 포함된 Linux 컨테이너 

자세한 내용은 [Windows Server 다음 릴리스의 Nano 서버 변경 사항](https://docs.microsoft.com/windows-server/get-started/nano-in-semi-annual-channel) 및 [개발자용 Windows Server, 버전 1709](https://blogs.technet.microsoft.com/windowsserver/2017/09/13/sneak-peek-3-windows-server-version-1709-for-developers/)를 참조하세요.

## <a name="modern-management"></a>최신 관리

IT 관리자의 핵심 문제 해결, 구성 및 유지 관리 시나리오 관리를 돕는 간소화 및 통합된 안전한 환경을 위한 [Project Honolulu](https://docs.microsoft.com/windows-server/manage/honolulu/honolulu)를 확인하세요.  Project Honolulu에는 간소화 및 통합된 안전하고 확장 가능한 차세대 도구가 포함되어 있습니다.
Project Honolulu에는 PC, Windows 서버, 장애 조치 클러스터는 물론 저장소 공간 다이렉트 기반 하이퍼 컨버지드 인프라를 관리하고 운영 비용을 절감하기 위한 직관적인 새로운 관리 환경이 포함되어 있습니다.

## <a name="compute"></a>컴퓨팅

**Nano 컨테이너와 Server Core 컨테이너**: 최초 이자 응용 프로그램 혁신을 추진 하는 방법에 대 한이 릴리스는 합니다. Nano 서버 또는 호스트로서의 Nano는 사용되지 않고 컨테이너 이미지로서 Nano를 실행하는 Nano 컨테이너로 교체되었습니다. 

자세한 내용은 [컨테이너 네트워킹 개요](https://docs.microsoft.com/windows-server/networking/sdn/technologies/containers/container-networking-overview)를 참조하세요.

**컨테이너(및 인프라) 호스트로서의 Serrver Core**는 현대화 프로세스 아래 기존 애플리케이션에 대하여 더욱 뛰어난 유연성, 밀도 및 성능을 제공하고, 클라우드 모델을 사용하여 이미 개발된 새 앱을 브랜딩합니다.

**VM 시작 순서** 역시 OS 및 응용 프로그램 인식을 통해 개선되어 VM이 시작된 것으로 인식될 경우 다음 VM이 시작되기 전에 향상된 트리거를 호출합니다.

**VM에 대한 저장소 클래스 메모리 지원**은 NTFS 포맷 직접 액세스 볼륨이 비휘발성 DIMM에서 생성되고 Hyper-V VM에 노출되도록 합니다. 이를 통해 Hyper-V VM은 저장소 클래스 메모리 장치의 짧은 대기 시간 성능 이점을 활용할 수 있습니다.

**vPMEM(가상화 영구 메모리)** 은 호스트의 직접 액세스 볼륨에 VHD 파일(.vhdpmem)을 만들고, vPMEM 컨트롤러를 VM에 추가하고, 생성된 장치(.vhdpmem)를 VM에 추가하여 사용 설정됩니다. 호스트의 직접 액세스 볼륨에 있는 vhdpmem 파일을 사용하여 vPMEM을 지원하면 할당 유연성을 지원하고 디스크를 VM에 추가하는 익숙한 관리 모델을 활용합니다.

**컨테이너 스토리지 - CSV(클러스터 공유 볼륨)의 영구 데이터 볼륨**입니다. 최신 업데이트가 포함된 Windows Server 2016은 물론 Windows Server, 버전 1709에 저장소 공간 다이렉트의 CSV 등 CSV에 위치한 영구 데이터 볼륨으로의 컨테이너 액세스 지원이 추가되었습니다. 이를 통해 어떤 클러스터 노드에서 컨테이너 인스턴스가 실행 중인지와 관계없이 응용 프로그램 컨테이너의 볼륨에 대한 영구 액세스를 제공합니다. 자세한 내용은 [CSV(클러스터 공유 볼륨), S2D(저장소 공간 다이렉트), SMB 글로벌 매핑을 통한 컨테이너 저장소 지원](https://blogs.msdn.microsoft.com/clustering/2017/08/10/container-storage-support-with-cluster-shared-volumes-csv-storage-spaces-direct-s2d-smb-global-mapping/)을 참조하세요.

**컨테이너 스토리지 - SMB 글로벌 매핑이 포함된 영구 데이터 볼륨**입니다. Windows Server, 버전 1709에 컨테이너 내 드라이브 문자(SMB 글로벌 매핑)에 대한 SMB 파일 공유 매핑 지원이 추가되었습니다. 이 매핑된 드라이브는 로컬 서버의 모든 사용자가 액세스할 수 있어 데이터 볼륨의 컨테이너 I/O는 탑재된 드라이브를 통과하여 기본 파일 공유로 향합니다. 자세한 내용은 [CSV(클러스터 공유 볼륨), S2D(저장소 공간 다이렉트), SMB 글로벌 매핑을 통한 컨테이너 저장소 지원](https://blogs.msdn.microsoft.com/clustering/2017/08/10/container-storage-support-with-cluster-shared-volumes-csv-storage-spaces-direct-s2d-smb-global-mapping/)을 참조하세요.

**VM 구성 파일 형식(업데이트)**. 구성 버전이 8.2 이상인 VM에 추가 파일(.vmgs)이 추가되었습니다. VM 게스트 상태(VMGS)는 이전에 VM 런타임 상태 파일의 일부였던 장치 상태를 포함하는 새로운 내부 파일입니다.

## <a name="security-and-assurance"></a>보안 및 보증

**네트워크 암호화**를 통해 소프트웨어 정의 네트워킹 인프라의 네트워크 세그먼트를 빠르게 암호화하여 보안 및 규정 준수 요구 사항을 충족할 수 있습니다.

보호된 VM으로서의 **HGS(호스트 보호 서비스)** 가 사용 설정되었습니다. 이 릴리스 이전에는 3노드 실제 클러스터 배포가 권장되었습니다. 이를 통해 HGS 환경이 관리자에 의해 손상되지 않았지만 엄청난 비용이 드는 경우가 잦았습니다.

**보호된 VM으로서의 Linux**가 이제 지원됩니다.

자세한 내용은 [보호된 패브릭 및 보호된 VM 개요](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)를 참조하세요.

**SMBLoris 취약점** 서비스 거부를 일으킬 수 있는, “SMBLoris”라고 알려진 문제가 해결되었습니다.

## <a name="storage"></a>스토리지

**저장소 복제본**: Windows Server 2016에서 저장소 복제본에서 추가 재해 복구 보호는 이제 포함 하도록 확장 됩니다.
- **테스트 장애 조치**: 대상 저장소를 탑재하는 옵션이 이제 테스트 장애 조치 기능을 통해 이용 가능합니다. 테스트 및 백업을 목적으로 대상 노드에 있는 복제된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다.  Microsoft 업데이트에 대한 자세한 내용은 [저장소 복제본 관련 질문과 대답](https://aka.ms/srfaq)을 참조하세요. 
- **프로젝트 브라 티 지원**: 그래픽 관리 서버 간 복제에 대 한 지원 프로젝트 브라 티에서 출시 되었습니다. 이를 통해 PowerShell을 사용하여 일반 재해 보호 워크로드를 관리해야 하는 필요성을 없앱니다.

**SMB**: 
- **SMB1 및 게스트 인증 제거**: Windows Server 버전 1709 이상 SMB1 클라이언트와 서버는 기본적으로 설치 합니다. 추가로 SMB2 이상의 게스트 인증 기능이 기본적으로 해제됩니다. 자세한 내용은 [SMBv1이 Windows 10, 버전 1709 및 Windows Server, 버전 1709에 기본적으로 설치되지 않음](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server)을 검토하세요. 

- **SMB2/SMB3 보안과 호환성**: 레거시 응용 프로그램에 대 한 SMB2 + oplock 해제 수 있을 뿐만 아니라 서명 또는 클라이언트에서 각 연결 단위로 암호화를 요구 하는 기능을 포함 하 여 보안 및 응용 프로그램 호환성에 대 한 옵션이 추가 되었습니다. 자세한 내용은 SMBShare PowerShell 모듈 도움말을 검토하세요.

**데이터 중복 제거** 
- **이제 데이터 중복 제거 지원 ReFS**: 더 이상 ReFS 사용 하 여 최신 파일 시스템의 장점 및 데이터 중복 제거 간에 선택 해야 합니다: 이제 ReFS를 설정할 수 없습니다. 어디서 나 데이터 중복 제거 활성화할 수 없습니다. ReFS를 통해 저장소 효율이 95% 증가합니다.
- **데이터 중복 제거 된 볼륨에 최적화 된 수신/송신 API**: 개발자 기술 자료 데이터 중복 제거 볼륨의 경우 서버 간에 데이터를 이동 하는 효율적으로 데이터를 저장 하는 방법에 대 한 및 클러스터를 효율적으로 활용을 사용할 수 있습니다.

## <a name="remote-desktop-services-rds"></a>RDS(원격 데스크톱 서비스)

**RDS가 Azure AD에 통합**되었습니다. 이제 고객은 조건부 액세스 정책, 다단계 인증, Azure AD를 사용한 기타 SaaS 앱 통합 인증 등을 활용할 수 있습니다. 자세한 내용은 [RDS 배포에 Azure AD Domain Services 통합](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds)을 참조하세요.

>[!TIP]
>RDS 다른 흥미로운 변경 기능 살펴보기를 참조 하세요. [원격 데스크톱 서비스: 업데이트 및 예정 된 혁신](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/20/first-look-at-updates-coming-to-remote-desktop-services/)

## <a name="networking"></a>네트워킹

**Docker의 라우팅 메시** 지원됩니다. 라우팅 메시 수신은 Docker의 컨테이너용 기본 제공 오케스트레이션 솔루션인 [Swarm 모드](https://docs.docker.com/engine/swarm/)의 일부입니다. 자세한 내용은 [Windows Server, 버전 1709에서 Docker의 라우팅 메시 이용 가능](https://blogs.technet.microsoft.com/virtualization/2017/09/26/dockers-ingress-routing-mesh-available-with-windows-server-version-1709/)을 참조하세요.

**Docker에 대한 새 기능**이 이용 가능합니다. 자세한 내용은 [Windows Server, 버전 1709의 Docker에 대한 흥미로운 새 기능](https://blog.docker.com/2017/09/docker-windows-server-1709/)을 참조하세요.

**Windows Kubernetes에 대 한 Linux와 동등한 수준 네트워킹**: Windows는 네트워킹 측면에서 Linux와 동등한 사용 합니다. 고객은 혼합 OS인 Kubernetes 클러스터를 Azure, 온-프레미스 및 Linux에서 지원되는 동일한 네트워크 원형 및 토폴로지가 포함된 타사 클라우드 스택을 포함한 모든 환경에 배포할 수 있습니다. 문제 해결이나 스위치 확장을 할 필요는 없습니다.

**핵심 네트워크 스택을**: 핵심 네트워크 스택의 몇 가지 기능이 개선 되었습니다. 이러한 기능에 관한 자세한 내용은 [Windows 10 크리에이터스 업데이트의 핵심 네트워크 스택 기능](https://blogs.technet.microsoft.com/networking/2017/07/13/core-network-stack-features-in-the-creators-update-for-windows-10/)을 참조하세요.
- **TCP 빠른 열기 (TFO)**: TCP 3 방향 핸드셰이크 프로세스를 최적화 하기 위해 TFO에 대 한 지원이 추가 되었습니다. TFO는 최초 연결 시 표준 3단계 핸드셰이크를 사용하여 보안 TFO 쿠키를 설정합니다.  이후 동일한 서버로의 연결 시 3단계 핸드셰이크 대신 TFO 쿠키를 사용하여 왕복 시간 없이 연결합니다.
- **입방 형 3**: 실험적 Windows 네이티브의 입방 형 3, TCP 정체 제어 알고리즘 구현은 사용할 수 있습니다. 다음 명령은 CUBIC을 각각 사용 또는 사용하지 않도록 설정합니다.

    ```
    netsh int tcp set supplemental template=internet congestionprovider=cubic
    netsh int tcp set supplemental template=internet congestionprovider=compound
    ```

- **수신 창 자동 조정**: TCP 자동 조정 논리는 TCP 연결의 "창 수신" 매개 변수를 계산합니다.  고속 및/또는 긴 지연 시간 연결에서 좋은 성능 특성을 달성하려면 이 알고리즘이 필요합니다.  이 릴리스에서 알고리즘이 수정되어 주어진 연결에 대한 최대 수신 창 값에 모이는 단계 기능을 사용합니다.
- **TCP 통계 API**: 새 API 도입 SIO_TCP_INFO를 호출 합니다.  SIO_TCP_INFO를 통해 개발자는 소켓 옵션을 사용하여 개별 TCP 연결의 많은 정보를 쿼리할 수 있습니다.
- **IPv6**: 이 릴리스의 IPv6에서 향상 된 여러 기능이 있습니다.
    - **RFC 6106** 지원: 라우터 알림의 (RAs)를 통해 DNS 구성을 허용 하는 RFC 6106 합니다. 다음 명령을 사용하여 RFC 6106 지원을 사용하거나 사용하지 않도록 설정할 수 있습니다.

    ```
    netsh int ipv6 set interface <ifindex> rabaseddnsconfig=<enabled | disabled>
    ```

    - **레이블 흐름**: TCP 및 UDP 아웃 바운드 크리에이터 스 업데이트를 사용 하 여 시작 IPv6 통한 패킷에이 필드가 5 튜플 (원본 IP, 대상 IP, Src 포트, 대상 포트)의 해시를 설정 합니다.  이를 통해 IPv6 only 데이터 센터의 부하 분산 또는 흐름 분류를 더욱 효율적으로 수행하도록 합니다. 흐름 레이블 사용 설정:

    ```
    netsh int ipv6 set flowlabel=[disabled|enabled] (enabled by default)
    netsh int ipv6 set global flowlabel=<enabled | disabled>
    ```

    - **ISATAP 및 6to4**: 이후 사용 중단 향한 단계로 크리에이터 스 업데이트를 이러한 기술은 기본적으로 사용 하지 않도록 설정 해야 합니다.
- **작동 하지 않는 게이트웨이 검색 (DGD)**: DGD 알고리즘으로 자동 전환 연결을 통해 다른 게이트웨이 현재 게이트웨이에 연결할 수 없는 경우. 이 릴리스에서 알고리즘이 개선되어 주기적으로 네트워크 환경을 다시 검색합니다.
- [Test-NetConnection](https://technet.microsoft.com/itpro/powershell/windows/nettcpip/test-netconnection)은 다양한 네트워크 진단을 수행하는 Windows PowerShell 내 기본 제공 cmdlet입니다.  이 릴리스에서 경로 선택 및 원본 주소 선택 관련 세부 정보를 제공하도록 cmdlet이 향상되었습니다.

**소프트웨어 정의 네트워킹**

- **가상 네트워크 암호화**는 "암호화 사용 설정됨"으로 표시된 서브넷 내에서 서로 통신하는 가상 컴퓨터 간 가상 네트워크 트래픽이 암호화되도록 하는 기능을 제공하는 새로운 기능입니다. 이 기능은 가상 서브넷의 DTLS(데이터그램 전송 계층 보안)를 활용하여 패킷을 암호화합니다.  DTLS는 실제 네트워크에 액세스할 수 있는 누군가에 의한 도청, 변조 및 위조를 방지합니다.
 
**Windows 10 VPN**

- **Pre-Logon 인프라 터널**. 기본적으로 Windows 10 VPN은 사용자가 컴퓨터 또는 장치에 로그인하지 않았을 때 자동적으로 인프라 터널을 생성하지 않습니다. Windows 10 VPN이 VPN 프로필의 장치 터널(prelogon) 기능을 사용하여 Pre-Logon 인프라 터널을 자동적으로 생성하도록 구성할 수 있습니다.
- **원격 컴퓨터 및 장치 관리**  VPN 프로필의 장치 터널(prelogon) 기능을 구성하여 Windows 10 VPN 클라이언트를 관리할 수 있습니다. 또한 VPN 연결이 내부 DNS 서비스 포함 VPN 인터페이스 할당되는 IP 주소를 동적으로 등록하도록 구성해야 합니다.
- **Pre-Logon 게이트웨이 지정**. 회사 네트워크의 어떤 관리 시스템이 장치 터널을 통해 액세스할 수 있는지 제어하는 트래픽 필터가 결합된 VPN 프로필의 장치 터널(prelogon) 기능을 포함한 Pre-Logon 게이트웨이를 지정할 수 있습니다.

