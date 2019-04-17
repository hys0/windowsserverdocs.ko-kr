---
title: Windows Server 반기 채널 개요
description: Microsoft는 운영 체제 업데이트를 더 간단하게 테스트, 관리, 배포할 수 있도록 하도록 Windows Server의 서비스를 간소화하고 있습니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: high
ms.date: 05/07/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cf87597-b15d-4f43-8aa1-91e60367f011
ms.openlocfilehash: 2995fca3085d6611ecce083685dca0e587913f17
ms.sourcegitcommit: fcc26ec5a2cc73b59c5752377b39c070d288655e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "8976729"
---
# Windows Server 반기 채널 개요

>적용 대상: Windows Server(반기 채널)

Windows Server 릴리스 모델은 [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) 및 [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US)에 대해 유사한 릴리스 및 서비스 모델에 맞추기 위한 새로운 옵션을 제공합니다. Windows 10 또는 Office 365 ProPlus를 사용해 보았다면 이러한 개선에 이미 친숙할 것입니다.

**Windows Server 고객, 장기 서비스 채널 및 반기 채널에 사용할 수 있는 두 기본 릴리스 채널이 있습니다.** 장기 서비스 채널(LTSC)에서 서버를 유지하고, 사용자의 요구에 따라 반기 채널로 이동하거나, 두 트랙에 일부 서버를 보유할 수 있습니다.


## 장기 서비스 채널(LTSC)
이는 2~3년마다 Windows Server의 주 버전이 출시되는, 이미 여러분에게 친숙한 릴리스 모델(이전의 “장기 서비스 *분기*”)입니다. 사용자는 5년 동안 일반 지원을 받고 지원 기간을 5년 연장할 수 있습니다. 이 채널은 보다 장기적인 서비스 옵션과 기능적 안정성이 요구되는 시스템에 적절합니다. Windows Server 2016 이하 버전의 Windows Server 배포는 새로운 반기 채널 릴리스의 영향을 받지 않습니다. 장기 서비스 채널은 보안 및 비보안 업데이트를 계속해서 수신하지만, 새로운 기능은 수신하지 않습니다.

> [!Note]  
> **현재 LTSC 제품은 Windows Server 2016입니다**. 이 채널을 유지하고자 하는 경우 Windows Server 2016을 설치(또는 계속 사용)해야 하고, Server Core 설치 옵션 또는 Desktop 환경 포함 서버 설치 옵션으로 설치할 수 있습니다. 자세한 내용은 [Windows Server 2016 시작](server-basics.md)을 참조하십시오. 



## 반기 채널 
반기 채널은 컨테이너 및 마이크로 서비스에 빌드된 응용 프로그램은 물론이고 소프트웨어 정의 하이브리드 데이터 센터에서 새로운 운영 체제 기능을 보다 신속하게 활용할 수 있도록 혁신에 박차를 가하고 있는 고객에게 가장 적합합니다. 반기 채널의 Windows Server 제품은 1년에 두 번, 봄과 가을에 새 릴리스가 제공됩니다. 이 채널의 각 릴리스는 최초 릴리스 후 18개월 동안 지원됩니다.

반기 채널에 도입된 대부분의 기능은 Windows Server의 차기 LTSC 릴리스로 롤업됩니다. 에디션, 기능 및 지원 내용은 고객 피드백에 따라 릴리스마다 달라질 수 있습니다.

반기 채널은 [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)가 포함된 볼륨 라이선스 고객에게 제공되며, Azure Marketplace 또는 기타 클라우드/호스팅 서비스 공급자와 Visual Studio 구독과 같은 구독 프로그램을 통해서도 이용할 수 있습니다.

> [!Note]  
> **현재 반기 채널 릴리스는 Windows Server 버전 1803입니다**. 이 채널에 서버를 배치하려는 경우 Server Core 모드에서 또는 컨테이너에서 Nano 서버 실행으로 설치할 수 있는 Windows Server 버전 1803을 설치해야 합니다. Windows Server 버전 1803을 얻고 활성화하는 방법을 알아보려면 [Windows Server 버전 1803 소개](get-started-with-1803.md)를 참조하십시오. Windows Server 2016에서 Windows Server 버전 1803으로 현재 위치 업그레이드는 지원되지 않습니다. 두 버전이 **다른 릴리스 채널**에 있기 때문입니다. Windows Server 버전 1803은 Windows Server 2016에 대한 업데이트가 아니라 반기 채널의 다음 Windows Server 릴리스입니다.



이 모델에서는 Windows Server 릴리스는 릴리스의 연도 및 월에 의해 식별됩니다. 예를 들어 2017년에 9번째 달(9월)의 릴리스는 **버전 1709**로 식별됩니다. 반기 채널에서 Windows Server 릴리스는 연간 두 번 업데이트됩니다. 각 릴리스의 지원 수명 주기는 18개월입니다.

## 서버를 LTSC에 유지하거나 반기 채널로 이동시켜야 합니까?
다음과 같은 주요 차이점을 고려해야 합니다.

- 혁신에 박차를 가해야 합니까? 최신 Windows Server 기능을 먼저 이용해야 합니까? 릴리스 흐름이 빠른 하이브리드 응용 프로그램, DevOps 및 Hyper-V 패브릭을 지원해야 합니까? 이럴 경우 [Windows Server, 버전 1803](get-started-with-1803.md)를 설치하여 **반기 채널에 가입**하는 방법을 고려해야 합니다. 이 항목에 설명된 대로, 1년에 두 번 새로운 버전을 받아보고 릴리스당 18개월 동안 프로덕션 환경에서 일반 지원을 받게 됩니다. 볼륨 라이선스, Azure 또는 Visual Studio 구독 서비스를 통해 이용이 가능합니다. 현재, 반기 채널의 릴리스들은 프로덕션 환경에서 제품을 실행하고자 할 경우 볼륨 라이선스와 Software Assurance가 필요합니다.
- 안정성과 예측 가능성이 필요합니까? VM 및 실제 서버의 기존 워크로드를 실행해야 합니까? 이럴 경우 **LTSC에 이들 서버를 유지**하는 방법을 고려해야 합니다. 최신 LTSC 릴리스는 [Windows Server 2016](server-basics.md)입니다. 이 항목에 설명된 대로, 2~3년마다 새로운 버전에 액세스할 수 있고 5년 동안 일반 지원을 받으며, 릴리스당 5년까지 지원 기간을 연장할 수 있습니다. LTSC 릴리스는 모든 릴리스 메커니즘을 통해 사용할 수 있습니다. LTSC 릴리스는 사용 중인 라이선스 모델에 관계 없이 모든 사용자에게 제공됩니다. 

다음 표는 Windows Server 버전 1803부터 시작하는 채널 간의 주요 차이점을 요약합니다.

|  | 장기 서비스 채널(Windows Server 2016) |반기 채널(Windows Server) |
| ------------------- | ------------------------------------ | ------------------------------------------------- |
|권장 시나리오 | 일반 목적의 파일 서버, Microsoft 및 비 Microsoft 워크로드, 기존 앱, 인프라 역할, 소프트웨어 정의 데이터 센터 및 하이퍼 컨버지드 인프라 | 더 빠른 혁신을 통해 혜택을 얻는 컨테이너화된 응용 프로그램, 컨테이너 호스트 및 응용 프로그램 시나리오 |
| 새 릴리스 | 2-3년마다 |6개월마다 |
| 지원 |일반 지원 5년 + 연장 지원 5년 | 18개월 |
| 에디션 | 모든 Windows Server 에디션 사용 가능 | Standard 및 Datacenter 에디션 |
| 사용할 수 있는 사람 | 모든 채널을 통한 모든 고객 | Software Assurance 및 클라우드 고객만 |
| 설치 옵션 | Server Core 및 데스크톱 환경 포함 서버 | 컨테이너 호스트 및 이미지 및 Nano 서버 컨테이너 이미지용 Server Core |                |


## 장치 호환성
다른 전달 사항이 없는 한, 반기 채널 릴리스를 실행하기 위한 최소 하드웨어 요구 사항은 최신 버전의 Windows Server용 LTSC 릴리스와 동일합니다. 예를 들어, **최신 LTSC 릴리스는 Windows Server 2016입니다**. 대부분의 하드웨어 드라이버가 이러한 릴리스에서 계속 작동합니다.

## 서비스
LTSC 및 반기 채널 릴리스 모두 보안 업데이트와 비보안 업데이트에서 지원됩니다. 차이는 위에서 설명한 대로 릴리스가 지원되는 기간입니다.

### 서비스 도구
IT 전문가가 Windows Server를 서비스하는 데 사용할 수 있는 도구가 많이 있습니다. 각 옵션에는 기능과 컨트롤부터 단순성과 낮은 관리 요구 사항에 이르는 장단점이 있습니다. 다음은 서비스 업데이트를 관리하는 데 사용할 수 있는 서비스 도구의 예입니다.

- **Windows 업데이트(독립 실행형)**: 이 옵션은 인터넷에 연결되어 있고 Windows 업데이트를 사용하도록 설정된 서버에만 사용할 수 있습니다.
- **WSUS(WindowsServer Update Services)** 는 Windows10 및 Windows Server 업데이트에 대한 포괄적인 제어를 제공하며 WindowsServer 운영 체제에서 기본적으로 사용 가능합니다. 업데이트 지연 기능 외에도 조직에서는 업데이트의 승인 계층을 추가하고 준비될 때마다 특정 컴퓨터나 컴퓨터 그룹에 업데이트를 배포하도록 선택할 수 있습니다.
- **System Center Configuration Manager**는 서비스에 대한 최상의 컨트롤을 제공합니다. IT 전문가가 업데이트를 지연하고 승인할 수 있으며, 배포의 대상을 지정하고 대역폭 사용 및 배포 시간을 관리하는 여러 옵션이 있습니다.

아마도 이미 리소스, 직원 및 전문성에 따라 이러한 옵션 중 하나를 사용하도록 선택했을 것입니다. 반기 채널 릴리스에도 같은 프로세스를 계속 사용할 수 있습니다. 예를 들어 이미 System Center Configuration Manager를 사용하여 업데이트를 관리한다면, 계속 사용할 수 있습니다. 마찬가지로 WSUS를 사용한다면, 계속 사용하면 됩니다.

## Windows 참가자 프로그램을 통해 미리 보기 릴리스 얻기
Windows Server의 초기 빌드를 테스트하는 것은 릴리스 전에 가능한 문제를 발견할 수 있는 기회이기 때문에 Microsoft와 고객 모두에게 도움이 됩니다. 또한 고객이 제품의 기능에 직접 영향을 줄 수 있는 특별한 기회도 제공합니다. 

Microsoft는 개발 프로세스 전체 동안 피드백을 받아 최대한 빨리 조정될 수 있도록 합니다. 초기 테스트와 피드백은 신속한 릴리스 모델에 필수적입니다.

Windows 참가자 프로그램에 참여하는 방법에 대한 자세한 내용은 [서버용 Windows 참가자 프로그램 문서](https://docs.microsoft.com/windows-insider/at-work/)를 참조하십시오.
# 관련 항목
[Windows Server 2019 서비스 채널: LTSC 및 SAC](https://docs.microsoft.com/windows-server/get-started-19/servicing-channels-19)

[Windows Server 반기 채널의 Nano 서버 변경 사항](nano-in-semi-annual-channel.md)

[Windows Server 지원 수명 주기](https://support.microsoft.com/en-us/lifecycle)

[Windows Server 2016 시스템 요구 사항](https://docs.microsoft.com/windows-server/get-started/system-requirements) 




