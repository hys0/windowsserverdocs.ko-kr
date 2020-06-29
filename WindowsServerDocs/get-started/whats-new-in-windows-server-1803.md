---
title: Windows Server 버전 1803의 새로운 기능
description: 컴퓨팅, ID, 관리, 자동화, 네트워킹, 보안, 스토리지의 새로운 기능입니다.
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.date: 05/07/2018
ms.openlocfilehash: c4676ee720780ac7f347d98048c920bd4ce68e59
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473190"
---
# <a name="whats-new-in-windows-server-version-1803"></a>Windows Server 버전 1803의 새로운 기능

>적용 대상: Windows Server(반기 채널)

<img src=../media/landing-icons/new.png style='float:left; padding:.5em;' alt=Icon showing a newspaper>&nbsp;Windows의 최신 기능을 알아보려면 [Windows Server의 새로운 기능](whats-new-in-windows-server.md)을 참조하세요. 이 콘텐츠는 Windows Server, 버전 1803의 새로운 기능과 변경된 기능을 설명하는 내용입니다. 여기에 나열된 새로운 기능 및 변경 사항은 이 릴리스를 사용할 때 가장 많은 영향을 줄 수 있습니다. 또한 [Windows Server 반기 채널 업데이트](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/)를 참조하세요.

## <a name="windows-admin-center"></a>Windows Admin Center

Project Honolulu의 명칭이 **Windows Admin Center**가 되었습니다.
<br>&nbsp;
> [!video https://www.youtube.com/embed/WCWxAp27ERk?autoplay=false]

[Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview)는 로컬 및 원격 서버 관리의 모든 측면을 통합합니다. Windows Admin Center는 Windows Server 배포의 모든 측면에 대해 전체 제어를 제공하는 인터넷 연결이 필요하지 않은 로컬로 배포되는 브라우저 기반 관리 환경입니다.

## <a name="windows-server-release-strategy"></a>Windows Server 릴리스 전략

Windows Server 버전 1709는 반기 채널의 최초 버전으로 2017년 9월에 출시되었습니다. 반기 채널에는 더 빠른 릴리스 흐름이 있으며 몇 개월마다 신속한 혁신을 원하는 사용자의 피드백을 해결합니다. 이는 릴리스 흐름이 매 2~3년인 장기 서비스 채널을 보완합니다.

원격 분석 및 피드백에 따르면 이러한 채널은 다음과 같은 일반적인 전략을 정상적으로 따르는지 설명합니다.
- 반기 채널은 컨테이너 및 마이크로서비스 등의 최신 애플리케이션 및 혁신 시나리오에 적합합니다.
- 장기 서비스 채널은 소프트웨어 정의 데이터 센터 및 하이퍼 컨버지드 인프라(HCI) 등의 핵심 인프라 시나리오에 대한 기본 버전입니다.

반기 채널 및 장기 서비스 채널에 대한 구체적인 시나리오는 다음과 같습니다.

|   | 장기 서비스 채널 |  반기 채널 |
| ------------- | ------------- | ------------ |
| 권장 시나리오     | 일반 목적의 파일 서버, 자사 및 타사 워크로드, 기존 앱, 인프라 역할, 소프트웨어 정의 데이터 센터, 하이퍼 컨버지드 인프라  | 더 빠른 혁신을 통해 혜택을 얻는 컨테이너화된 애플리케이션, 컨테이너 호스트 및 애플리케이션 시나리오 |
| 새 릴리스  | 2~3년마다  | 6개월마다 |
| Support(지원)  | 일반 지원 5년 + 확장 지원 5년  | 18개월 |
| 버전  | 모든 Windows Server 버전 사용 가능  | Standard 및 Datacenter 버전 |
| 사용할 수 있는 사람  | 모든 채널을 통한 모든 고객 | Software Assurance 및 클라우드 고객만 |
| 설치 옵션  | Server Core 및 데스크톱 환경 포함 서버  | 컨테이너 호스트, 컨테이너 이미지, Nano 서버 컨테이너 이미지용 Server Core |

## <a name="application-platform-and-containers"></a>애플리케이션 플랫폼 및 컨테이너

- Optimization
    - Server Core 기본 컨테이너 이미지는 Windows Server 버전 1709에서 30% 감소됩니다.
    - 기존 애플리케이션의 컨테이너화를 위해 애플리케이션 호환성도 향상됩니다.
    - 다양한 수정 및 최적화 덕분에 컨테이너 부팅 성능 및 런타임 성능이 개선됩니다.
- 컨테이너 네트워킹: Localhost 및 http 프록시 지원이 추가되었으며 컨테이너 확장성이 향상하고 시작 시간이 단축됩니다.
- 도구: 빌드 및 디버깅 시나리오에 대한 PowerShell을 보완하기 위해 Curl.exe, Tar.exe 및 SSH에 대한 지원이 향상되었습니다.

### <a name="server-core-container-image"></a>Server Core 컨테이너 이미지

이제 더 나은 애플리케이션 호환성으로 더 작은 Server Core 컨테이너를 사용할 수 있습니다. 자세한 정보는 [여기](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)에서 알아볼 수 있습니다.

- 사용하지 않는 선택적 기능 및 역할이 제거되었습니다. 자세한 내용은 [Server Core 컨테이너에 없는 역할, 역할 서비스 및 기능](../administration/server-core/server-core-container-removed-roles.md)을 참조하세요.
    - 다운로드 크기가 1.58GB로, Windows Server 버전 1709에서 30% 줄어들었습니다.
    - 디스크 크기가 3.61GB로, Windows Server 버전 1709에서 20% 줄어들었습니다.
- Nano 서버 컨테이너 이미지는 100MB 미만

### <a name="windows-subsystem-for-linux-wsl"></a>WSL(Linux용 Windows 하위 시스템)

WSL을 통해 서버 관리자는 Windows Server에서 Linux의 기존 도구 및 스크립트를 사용할 수 있습니다. 백그라운드 작업, DriveFS, WSLPath 등의 [명령줄 블로그](https://blogs.msdn.microsoft.com/commandline/tag/wsl/)에 소개된 여러 개선 사항이 이제 Windows Server의 일부가 됩니다.

### <a name="kubernetes"></a>Kubernetes

Kubernetes(일반적으로 K8s라고 함)는 [Cloud Native Computing Foundation](https://www.cncf.io)의 책임 아래 개발된 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하는 오픈 소스 시스템입니다.

Windows Server 버전 1709에서 사용자는 다음을 비롯한 Windows 네트워킹 기능에서 Kubernetes를 활용할 수 있었습니다.
- 포드 구획 공유: 인프라 및 작업자 포드가 이제 네트워크 구획(Linux 네임스페이스와 유사)을 공유합니다.
- 엔드포인트 최적화: 구획 공유 덕분에 컨테이너 서비스는 엔드포인트를 절반만큼만 추적하면 됩니다.
- 데이터 경로 최적화: 가상 필터링 플랫폼 및 호스트 네트워킹 서비스가 개선되어 커널 기반 부하 분산이 가능합니다.

Windows Server 버전 1803을 통해 더 많은 기능을 이후 Kubernetes 릴리스에서 사용할 수 있습니다.
- Kubernetes에 의해 오케스트레이션된 Windows 컨테이너용 [스토리지 플러그 인](https://github.com/Microsoft/K8s-Storage-Plugins).
- [프로젝트 Calico의 Tigera](https://cloudblogs.microsoft.com/windowsserver/2017/12/07/securing-modernized-apps-and-simplified-networking-on-windows-with-calico/) 지원과의 파트너 관계와 같은 이니셔티브를 통한 클라우드 네트워킹 확장.
- 포드당 여러 컨테이너가 있는 Hyper-V 격리 포드에 대한 Windows 플랫폼 지원.

### <a name="application-compatibility-and-feature-parity-issues-fixed"></a>애플리케이션 호환성 및 기능 패리티 문제 해결됨

- Microsoft 메시지 큐(MSMQ)가 지금 Server Core 컨테이너에 설치합니다.
- ASP.net 성능 카운터를 해제하는 문제가 해결되었습니다.
- 컨테이너에서 실행되는 서비스가 종료 알림을 수신하지 않는 문제가 해결되었습니다.
    - 특히, 알림은 Server Core와 Nano 서버 컨테이너 기반 이미지에 대해 CTRL_SHUTDOWN_EVENT로 변경됩니다. 또한 컨테이너에서 실행되는 서비스에 서비스 종료 알림 메시지를 보내는 등 Server Core 컨테이너 기반 이미지의 알림이 컨테이너에서 실행되는 모든 프로세스에 영향을 미치도록 확장됩니다.
- 고정된 데이터 드라이브를 쓸 수 있도록 하는 데(FDVDenyWriteAccess) BitLocker 보호가 필요한지 여부를 결정하는 정책 설정과 docker pull 및 docker load의 비호환성 문제가 해결되었습니다.

## <a name="storage"></a>스토리지

이 릴리스에서 서비스가 시작되면 모든 볼륨에 File Server Resource Manager 서비스가 변경 저널(USN 저널이라고도 함)을 만드는 것을 방지할 수 있습니다. 이를 통해 각 볼륨의 공간을 절약할 수 있지만 실시간 파일 분류를 사용할 수 없게 됩니다. 자세한 내용은 [파일 서버 리소스 관리자 개요](https://docs.microsoft.com/windows-server/storage/fsrm/fsrm-overview)를 참조하세요.

## <a name="features-added-to-server-core"></a>Server Core에 추가된 기능

Windows 배포 서비스(WDS)의 전송 서버 역할이 Server Core에 추가되었습니다.

전송 서버는 WDS의 핵심 네트워크 부분만을 포함합니다. 전송 서버를 사용하여 독립 실행형 서버에서 데이터(운영 체제 이미지 포함)를 전송하는 멀티캐스트 네임스페이스를 만들 수 있습니다. 클라이언트가 PXE 부팅하고 고유한 사용자 지정 설치 애플리케이션을 다운로드할 수 있도록 PXE 서버를 준비하려는 경우에도 이 방법을 사용할 수 있습니다. 이러한 시나리오 중 하나를 사용하려는 경우 이 옵션을 사용해야 합니다.

Server Core에서 전송 서버 서비스를 사용하도록 설정하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

```
Install-WindowsFeature -Name WDS
```

## <a name="additional-references"></a>추가 참조

[Windows Server 릴리스 정보](https://docs.microsoft.com/windows-server/get-started/windows-server-release-info)<br>
[Windows 10 버전 1803 IT 전문가 콘텐츠의 새로운 내용](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1803)
