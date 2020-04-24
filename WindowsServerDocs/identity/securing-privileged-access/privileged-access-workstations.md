---
title: Privileged Access Workstation이 조직의 보안을 유지하는 데 도움이 되는 이유
description: PAW에서 조직의 보안 상태를 향상시키는 방법입니다.
ms.prod: windows-server
ms.topic: article
ms.assetid: 93589778-3907-4410-8ed5-e7b6db406513
ms.date: 03/13/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 36988b8ed3d61fe97f4e1018b4ec1b6340cb4fae
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80855146"
---
# <a name="privileged-access-workstations"></a>Privileged Access Workstation

>적용 대상: Windows Server

PAW(Privileged Access Workstation)는 인터넷 공격 및 위협 벡터로부터 보호되는 중요한 작업에 대한 전용 운영 체제를 제공합니다. 매일 사용하는 워크스테이션과 디바이스에서 이러한 중요한 작업과 계정을 분리하면 피싱 공격, 애플리케이션/OS 취약성, 다양한 가장 공격, 자격 증명 탈취 공격(예: 키 입력 로깅, [Pass-the-Hash](https://aka.ms/pth) 및 Pass-The-Ticket)으로부터 매우 강력하게 보호할 수 있습니다.

## <a name="what-is-a-privileged-access-workstation"></a>Privileged Access Workstation이란?

간단히 말해, PAW는 중요한 계정 및 작업에 대한 높은 수준의 보안 보증을 제공하도록 설계된 강화되고 잠긴 워크스테이션입니다.  PAW는 ID 시스템, 클라우드 서비스 및 프라이빗 클라우드 패브릭뿐만 아니라 중요한 비즈니스 기능을 관리하는 데 권장됩니다.

> [!NOTE]
> PAW 아키텍처에는 계정과 워크스테이션의 일반적인 1:1 매핑이 필요하지 않습니다. PAW는 하나 이상의 계정에서 사용할 수 있는 신뢰할 수 있는 워크스테이션 환경을 만듭니다.

최고 수준의 보안을 제공하기 위해 PAW는 항상 최신의 안전한 운영 체제를 실행해야 합니다. Microsoft는 다른 버전에서 사용할 수 없는 몇 가지 추가 보안 기능(특히 [Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) 및 [Device Guard](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx))이 포함된 Windows 10 Enterprise를 적극적으로 추천합니다.

> [!NOTE]
> Windows 10 Enterprise에 액세스할 수 없는 조직에서는 신뢰할 수 있는 부팅, BitLocker, 원격 데스크톱 등 PAW에 중요한 많은 기본 기술이 포함된 Windows 10 Pro를 사용해도 됩니다.  교육 기관 고객은 Windows 10 Education을 사용할 수 있습니다.  Windows 10 Home을 PAW에 사용해서는 안 됩니다.
>
> Windows 10의 다양한 에디션에 대한 비교 표는 [이 문서](https://www.microsoft.com/WindowsForBusiness/Compare)를 참조하세요.

PAW 보안 제어는 손상에 따른 높은 영향과 높은 확률 위험을 완화하는 데 중점을 둡니다. 여기에는 환경에 대한 공격 및 시간 경과에 따라 PAW 제어의 효과를 저하시킬 수 있는 위험에 대한 완화가 포함됩니다.

* **인터넷 공격** - 대부분의 공격은 인터넷 원본에서 직접 또는 간접적으로 발생하며, 탈출 및 C2(명령 및 제어)에 인터넷을 사용합니다. 개방된 인터넷에서 PAW를 격리하는 것은 PAW가 손상되지 않도록 하기 위한 주요 요소입니다.
* **유용성 위험** - PAW가 일상적인 작업에 사용하기에 너무 어려운 경우 관리자는 작업을 보다 쉽게 수행할 수 있는 해결책을 만들어야 합니다. 종종 이러한 해결책은 관리 워크스테이션 및 계정을 상당한 보안 위험에 노출시키므로 이러한 유용한 문제를 안전하게 완화하기 위해 PAW 사용자를 참여시키고 권한을 부여하는 것이 중요합니다. 이를 위해 의견을 듣고, 작업을 수행하는 데 필요한 도구와 스크립트를 설치하고, 모든 관리 직원이 PAW를 사용해야 하는 이유, PAW의 기본 사항 및 PAW를 올바르게 성공적으로 사용하는 방법을 알고 있어야 합니다.
* **환경 위험** - 환경 내의 다른 많은 컴퓨터와 계정이 인터넷 위험에 직접 또는 간접적으로 노출되기 때문에 프로덕션 환경 내 손상된 자산의 공격으로부터 PAW를 보호해야 합니다. 이렇게 하려면 이러한 특수 워크스테이션을 보호하고 모니터링하기 위해 PAW에 액세스할 수 있는 관리 도구와 계정의 사용을 최소화해야 합니다.
* **공급망 변조** - 하드웨어 및 소프트웨어 공급망에서 가능한 모든 변조 위험을 제거하는 것은 불가능하지만 몇 가지 주요 조치를 통해 공격자가 쉽게 접근할 수 있는 중요한 공격 벡터를 완화할 수 있습니다. 여기에는 모든 설치 미디어의 무결성 확인([클린 소스 원칙](https://aka.ms/cleansource)) 및 신뢰할 수 있고 평판 좋은 하드웨어 및 소프트웨어 공급업체 이용 등이 포함됩니다.
* **물리적 공격** - PAW는 실제로 이동이 가능하고 물리적으로 안전한 시설 외부에서 사용될 수 있기 때문에 컴퓨터에 물리적으로 무단 액세스하는 공격으로부터 보호되어야 합니다.

> [!NOTE]
> PAW는 Active Directory 포리스트를 통해 이미 관리 액세스 권한을 얻은 악의적 사용자로부터 환경을 보호하지 못합니다.
> 대부분의 기존 Active Directory 도메인 서비스 구현은 자격 증명 도난 위험이 도사리는 환경에서 몇 년간 운영되어 왔기 때문에 조직에서는 위반이 있을 수 있음을 가정하고 도메인 또는 엔터프라이즈 관리자 자격 증명의 감지되지 않은 손상 가능성을 고려해야 합니다. 도메인 손상을 의심하는 조직에서는 전문적인 사건 대응 서비스의 이용을 고려해야 합니다.
>
> 대응 및 복구 지침에 대한 자세한 내용은 [Pass-the-Hash 및 기타 자격 증명 도난 완화](https://aka.ms/pth) 버전 2의 "의심스러운 활동 대응" 및 "위반 복구" 섹션을 참조하세요.
>
> 자세한 내용은 [Microsoft의 사고 대응 및 복구 서비스](https://www.microsoft.com/microsoftservices/campaigns/cybersecurity-protection.aspx) 페이지를 참조하세요.

### <a name="paw-hardware-profiles"></a>PAW 하드웨어 프로필

관리 직원도 표준 사용자입니다. 이메일을 확인하고, 웹을 검색하고, 회사의 기간 업무 애플리케이션에 액세스하려면 PAW와 표준 사용자 워크스테이션이 필요합니다.  관리자의 생산성과 보안을 둘 다 유지하는 것은 모든 PAW 배포의 성공에 필수적입니다.  사용자는 생산성을 현격히 제한하는 보안 솔루션 대신 보안이 보장되지 않더라도 생산성을 향상시키는 솔루션을 선택할 것입니다.

보안의 필요성과 생산성의 필요성에 대한 균형을 유지하려면 다음 PAW 하드웨어 프로필 중 하나를 사용하는 것이 좋습니다.

* **전용 하드웨어** - 사용자 작업과 관리 작업을 위한 별도의 전용 디바이스
* **동시 사용** - OS 또는 프레젠테이션 가상화를 활용하여 사용자 작업과 관리 작업을 동시에 실행할 수 있는 단일 디바이스

조직에서는 하나의 프로필만 사용하거나 두 프로필을 모두 사용할 수 있습니다. 하드웨어 프로필 간에 상호 운용성 문제는 없으므로 조직에서는 지정된 관리자의 상황 및 특정 요구 사항에 맞게 하드웨어 프로필을 유연하게 선택할 수 있습니다.

> [!NOTE]
> 이러한 모든 시나리오에서는 관리 직원에게 지정된 관리 계정과는 별개인 표준 사용자 계정을 발급하는 것이 중요합니다. 관리 계정은 PAW 관리 운영 체제에만 사용해야 합니다.

다음 표에는 운영상의 사용 편의성과 생산성 및 보안 측면에서 각 하드웨어 프로필의 상대적인 장점과 단점이 요약되어 있습니다.  두 하드웨어 접근 방식 모두 자격 증명 도난 및 재사용으로부터 관리 계정을 보호하는 강력한 보안을 제공합니다.

|**시나리오**|**장점**|**단점**|
|--------|---------|-----------|
|전용 하드웨어|-   작업의 민감도에 대한 강력한 신호<br />-   가장 강력한 보안 분리|-   추가 데스크 공간<br />-   추가 중량(원격 작업의 경우)<br />-   하드웨어 비용|
|동시 사용|-   보다 저렴한 하드웨어 비용<br />-   단일 디바이스 환경|-   단일 키보드/마우스 공유로 인한 의도치 않은 오류/위험 발생|

이 지침에는 전용 하드웨어 접근 방식에 대한 PAW 구성의 자세한 지침이 포함되어 있습니다. 동시 사용 하드웨어 프로필이 필요한 경우 이 지침을 기반으로 하는 지침을 직접 도입하거나 Microsoft와 같은 전문 서비스 조직의 지원을 받을 수 있습니다.

#### <a name="dedicated-hardware"></a>전용 하드웨어

이 시나리오에서는 전자 메일, 문서 편집, 개발 작업 등 일상적인 작업에 사용되는 PC와 완전히 분리된 관리에 PAW가 사용됩니다. 모든 관리 도구와 애플리케이션은 PAW에 설치되고 모든 생산성 애플리케이션은 표준 사용자 워크스테이션에 설치됩니다. 이 지침의 단계별 설명은 이 하드웨어 프로필을 기반으로 합니다.

#### <a name="simultaneous-use---adding-a-local-user-vm"></a>동시 사용 - 로컬 사용자 VM 추가

이 동시 사용 시나리오에서는 전자 메일, 문서 편집 및 개발 작업과 같은 일상적인 작업과 관리 작업 모두에 단일 PC가 사용됩니다. 이 구성에서는 연결이 끊어진 동안 문서 편집 및 로컬로 캐시된 전자 메일 작업에 사용자 운영 체제를 사용할 수 있지만 이 연결이 끊어진 상태를 수용할 수 있는 하드웨어 및 지원 프로세스가 필요합니다.

![동시 사용 시나리오에서 관리 작업과 일상적인 작업(예: 전자 메일, 문서 편집 및 개발 작업) 모두에 단일 PC를 사용함을 보여 주는 다이어그램](../media/privileged-access-workstations/PAWFig10.JPG)

물리적 하드웨어는 로컬로 다음 두 운영 체제를 실행합니다.

* **관리자 OS** - 물리적 호스트는 관리 작업용으로 PAW 호스트에서 Windows 10을 실행합니다.
* **사용자 OS** - Windows 10 client Hyper-V 가상 머신 게스트는 회사 이미지를 실행합니다.

Windows 10 Hyper-V를 사용하면 게스트 가상 머신(Windows 10도 실행함)에서 소리, 비디오 및 인터넷 통신 애플리케이션(예: 비즈니스용 Skype)과 같은 풍부한 사용자 환경을 갖출 수 있습니다.

이 구성에서 관리 권한이 필요 없는 일상적인 작업은 일반 회사 Windows 10 이미지를 포함하고 PAW 호스트에 적용되는 제한 사항이 없는 사용자 OS 가상 머신에서 수행됩니다. 모든 관리 작업은 관리자 OS에서 수행됩니다.

이렇게 구성하려면 PAW 호스트에 대한 이 지침의 설명에 따라 클라이언트 Hyper-V 기능을 추가하고 사용자 VM을 만든 다음 사용자 VM에 Windows 10 회사 이미지를 설치합니다.

이 기능에 대한 자세한 내용은 [클라이언트 Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index) 문서를 참조하세요. 게스트 가상 컴퓨터의 운영 체제는 [여기](https://download.microsoft.com/download/9/8/D/98D6A56C-4D79-40F4-8462-DA3ECBA2DC2C/Licensing_Windows_Desktop_OS_for_Virtual_Machines.pdf)에 설명된 대로 [Microsoft 제품 라이선스](https://www.microsoft.com/Licensing/product-licensing/products.aspx)에 따라 라이선스를 받아야 합니다.

#### <a name="simultaneous-use---adding-remoteapp-rdp-or-a-vdi"></a>동시 사용 - RemoteApp, RDP 또는 VDI 추가

이 동시 사용 시나리오에서는 관리 작업과 일상적인 작업(예: 전자 메일, 문서 편집 및 개발 작업) 모두에 단일 PC를 사용합니다. 이 구성에서는 사용자 운영 체제가 중앙(클라우드 또는 데이터 센터)에서 배포되고 관리되지만 연결이 끊긴 동안에는 사용할 수 없습니다.

![동시 사용 시나리오에서 관리 작업과 일상적인 작업(예: 전자 메일, 문서 편집 및 개발 작업) 모두에 단일 PC를 사용함을 보여 주는 그림](../media/privileged-access-workstations/PAWFig11.JPG)

물리적 하드웨어는 관리 작업을 위해 단일 PAW 운영 체제를 로컬로 실행하고, 전자 메일, 문서 편집 및 LOB(기간 업무) 애플리케이션과 같은 사용자 애플리케이션은 Microsoft 또는 타사 원격 데스크톱 서비스에 문의합니다.

이 구성에서 관리 권한이 필요 없는 일상적인 작업은 PAW 호스트에 적용되는 제한 사항이 없는 원격 OS 및 애플리케이션에서 수행됩니다. 모든 관리 작업은 관리자 OS에서 수행됩니다.

이렇게 구성하려면 PAW 호스트에 대한 이 지침의 설명에 따라 원격 데스크톱 서비스에 대한 네트워크 연결을 허용하고 PAW의 사용자 데스크톱에 애플리케이션 액세스를 위한 바로 가기를 추가합니다. 원격 데스크톱 서비스는 다음과 같은 여러 가지 방법으로 호스트될 수 있습니다.

* 기존 원격 데스크톱 또는 VDI 서비스(온-프레미스 또는 클라우드)
* 온-프레미스 또는 클라우드에 설치한 새 서비스
* 미리 구성된 Office 365 템플릿 또는 사용자 고유의 설치 이미지를 사용하는 Azure RemoteApp

Azure RemoteApp에 대한 자세한 내용은 [이 페이지](https://www.remoteapp.windowsazure.com)를 참조하세요.

## <a name="how-microsoft-is-using-administrative-workstations"></a>Microsoft에서 관리 워크스테이션을 사용하는 방법

Microsoft에서는 내부 시스템뿐만 아니라 고객에게도 PAW 아키텍처 접근 방식을 사용합니다. Microsoft는 Microsoft IT 인프라 관리, Microsoft 클라우드 패브릭 인프라 개발 및 운영, 기타 고부가가치 자산의 관리를 포함한 여러 기능에서 내부적으로 관리 워크스테이션을 사용합니다.

이 지침은 사이버 보안 공격으로부터 고객을 보호하기 위해 Microsoft의 사이버 보안 전문 서비스 팀이 배포한 PAW(Privileged Access Workstation) 참조 아키텍처를 직접 기반으로 합니다. 관리 워크스테이션은 도메인 관리 작업의 가장 강력한 보호 아키텍처인 ESAE(Enhanced Security Administrative Environment) 관리 포리스트 참조 아키텍처의 주요 요소이기도 합니다.

ESAE 관리 포리스트에 대한 자세한 내용은 [권한 있는 액세스 보안 참조 자료](../securing-privileged-access/securing-privileged-access-reference-material.md#esae-administrative-forest-design-approach)의 *ESAE 관리 포리스트 디자인 방법* 섹션을 참조하세요.

## <a name="architecture-overview"></a>아키텍처 개요

아래 다이어그램에는 별도의 전용 관리 계정 및 워크스테이션을 유지할 경우에 생성되는 별도의 관리(매우 중요한 작업)용 "채널"이 나와 있습니다.

![별도의 전용 관리 계정 및 워크스테이션을 유지할 경우에 생성되는 별도의 관리(매우 중요한 작업)용 "채널"을 보여 주는 다이어그램](../media/privileged-access-workstations/PAWFig1.JPG)

이 아키텍처 접근 방식은 Windows 10 [Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) 및 [Device Guard](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx) 기능에 있는 보호를 기반으로 하며 중요한 작업 및 계정에 대해 이보다 강력한 보호를 제공합니다.

이 방법론은 매우 소중한 자산에 액세스할 수 있는 계정에 적합합니다.

* **관리자 권한** - PAW는 영향력이 큰 IT 관리 역할 및 작업에 대한 향상된 보안을 제공합니다. 이 아키텍처는 Active Directory 도메인 및 포리스트, Microsoft Azure Active Directory 테넌트, Office 365 테넌트, PCN(Process Control Network), SCADA(Supervisory Control and Data Acquisition) 시스템, ATM(현금 자동 인출기), PoS(Point of Sale) 디바이스 등 다양한 유형의 시스템을 관리하는 데 적용될 수 있습니다.
* **민감도가 높은 정보 근로자** - PAW에 사용되는 접근 방식은 사전 공지 인수 합병 활동, 공개 전 재무 보고서, 조직의 소셜 미디어 현재 상태, 경영진 커뮤니케이션, 특허 받지 않은 영업 비밀, 중요한 연구 또는 기타 독점적이거나 중요한 데이터와 관련된 매우 민감한 정보 근로자 작업 및 직원을 보호할 수도 있습니다. 이 지침에서는 이러한 정보 근로자의 구성에 대해 자세히 다루지 않으며 이 시나리오가 기술 지침에 포함되어 있지도 않습니다.

    > [!NOTE]
    > Microsoft IT에서는 PAW(내부적으로 "보안 관리 워크스테이션" 또는 SAW라고 함)를 사용하여 Microsoft 내의 내부 중요 시스템에 대한 보안 액세스를 관리합니다. 이 지침에는 "Microsoft에서 관리 워크스테이션을 사용하는 방법" 섹션에 나와 있는 Microsoft에서의 PAW 사용에 대한 추가 정보가 포함되어 있습니다. 이 중요 자산 환경 접근 방식에 대한 자세한 내용은 [보안 관리 워크스테이션을 사용하여 중요 자산 보호](https://msdn.microsoft.com/library/mt186538.aspx) 문서를 참조하세요.

이 문서에서는 매우 중요한 권한 있는 계정을 보호하는 데 이 방식이 권장되는 이유, 이러한 PAW 솔루션의 관리자 권한 보호 방식, 도메인 및 클라우드 서비스 관리용 PAW 솔루션을 신속하게 배포하는 방법 등을 설명합니다.

이 문서에서는 여러 PAW 구성을 구현하는 방법에 대한 자세한 지침과 매우 중요한 계정을 보호하기 위한 자세한 구현 지침을 제공합니다.

* [**1단계 - Active Directory 관리자를 위한 즉시 배포**](#phase-1-immediate-deployment-for-active-directory-administrators) 온-프레미스 도메인 및 포리스트 관리 역할을 보호할 수 있는 PAW를 빠르게 제공합니다.
* [**2단계 - 모든 관리자로 PAW 확장**](#phase-2-extend-paw-to-all-administrators) 클라우드 서비스(예: Office 365 및 Azure), 엔터프라이즈 서버, 엔터프라이즈 애플리케이션 및 워크스테이션의 관리자를 보호할 수 있습니다.
* [**3단계 - 고급 PAW 보안**](#phase-3-extend-and-enhance-protection) PAW 보안 추가 보호 및 고려 사항에 대해 설명합니다.

### <a name="why-dedicated-workstations"></a>전용 워크스테이션이 필요한 이유

조직의 현재 위협 환경은 정교한 피싱 및 기타 인터넷에 노출된 계정과 워크스테이션에 대한 지속적인 보안 침해 위험을 초래하는 인터넷 공격으로 가득 차 있습니다.

이 위협 환경에서는 조직에서 관리자 계정 및 중요한 비즈니스 자산과 같은 고부가가치 자산에 대한 보호를 설계할 때 "위반 가정" 보안 상태를 채택해야 합니다. 이러한 중요 자산은 직접적인 인터넷 위협뿐만 아니라 환경 내 다른 워크스테이션, 서버 및 디바이스에서 탑재되는 공격으로부터 모두 보호되어야 합니다.

![공격자가 중요한 자격 증명이 사용되는 사용자 워크스테이션에 대한 제어 권한을 획득한 경우 관리되는 자산에 대한 위험을 보여 주는 그림](../media/privileged-access-workstations/PAWFig2.JPG)

이 그림에서는 공격자가 중요한 자격 증명이 사용되는 사용자 워크스테이션에 대한 제어 권한을 획득한 경우 관리되는 자산에 대한 위험을 보여 줍니다.

운영 체제를 제어하는 공격자는 수많은 방법으로 워크스테이션의 모든 작업에 대한 액세스 권한을 불법적으로 얻고 적법한 계정을 가장할 수 있습니다. 알려지거나 알려지지 않은 다양한 공격 기술을 사용하여 이러한 수준의 액세스 권한을 얻을 수 있습니다. 사이버 공격의 규모와 정교성이 증가함에 따라 이러한 분리 개념을 확장하여 중요한 계정에 대한 클라이언트 운영 체제를 완전히 분리해야 할 필요성이 커졌습니다. 정보 백서, 비디오 등 이러한 유형의 공격에 대한 자세한 내용은 [Pass The Hash 웹 사이트](https://www.microsoft.com/pth)를 참조하세요.

PAW 접근 방식은 기존의 권장 방식을 관리 직원에 대해 별도의 관리자 계정과 사용자 계정을 사용하도록 확장한 것입니다. 이 방식에서는 사용자의 표준 사용자 계정과 완전히 분리되어 개별적으로 할당된 관리자 계정을 사용합니다. PAW는 이러한 계정 분리 방식을 기반으로 중요한 계정을 위한 신뢰할 수 있는 워크스테이션을 제공합니다.

이 PAW 지침은 높은 권한의 IT 관리자 및 매우 중요한 비즈니스 계정과 같은 중요 계정을 보호하는 이 기능을 구현하도록 도와주기 위해 마련되었습니다. 이 지침은 다음 작업을 수행하는 데 도움이 됩니다.

* 신뢰할 수 있는 호스트로만 자격 증명 노출 제한
* 관리 작업을 쉽게 수행할 수 있도록 관리자에게 높은 수준의 보안 워크스테이션 제공

중요한 계정을 강화된 PAW만 사용하도록 제한하면 관리자에게 매우 유용하면서도 악의적 사용자가 공격하기 매우 까다로운 보호를 손쉽게 구축할 수 있습니다.

### <a name="alternate-approaches"></a>대체 접근 방식

이 섹션에서는 대체 접근 방식의 보안을 PAW와 비교하는 방법 및 이러한 접근 방식을 PAW 아키텍처 내에 올바르게 통합하는 방법에 대한 정보를 제공합니다. 이러한 접근 방식이 모두 개별적으로 구현되는 경우 심각한 위험을 수반하지만, 일부 시나리오에서는 PAW 구현에 가치를 추가할 수 있습니다.

#### <a name="credential-guard-and-windows-hello-for-business"></a>Credential Guard 및 비즈니스용 Windows Hello

Windows 10에 도입된 [Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx)는 하드웨어 및 가상화 기반 보안을 사용하여 파생된 자격 증명을 보호하는 방식으로 Pass-the-Hash와 같은 일반적인 자격 증명 도난 공격을 완화합니다. 또한 [비즈니스용 Windows Hello](https://aka.ms/passport)에서 사용하는 자격 증명의 프라이빗 키는 TPM(신뢰할 수 있는 플랫폼 모듈)을 통해 보호할 수 있습니다.

이는 강력한 완화 방법이지만, Credential Guard 또는 비즈니스용 Windows Hello에서 자격 증명을 보호하는 경우에도 워크스테이션이 여전히 특정 공격에 취약할 수 있습니다. 이러한 공격으로 손상된 디바이스에서의 직접적인 권한 남용 및 자격 증명 사용, 도난된 자격 증명을 다시 사용하여 Credential Guard를 사용하도록 설정, 워크스테이션의 관리 도구 및 취약한 애플리케이션 구성의 남용이 있을 수 있습니다.

이 섹션의 PAW 지침에는 민감도가 높은 계정 및 작업에 이러한 여러 기술을 사용하는 방법이 포함되어 있습니다.

#### <a name="administrative-vm"></a>관리 VM

관리 VM(관리 가상 머신)은 표준 사용자 데스크톱에서 호스팅되는 관리 작업을 위한 전용 운영 체제입니다. 이 접근 방식은 관리 작업 전용 OS를 제공한다는 점에서 PAW와 유사하지만 관리 VM은 보안상 표준 사용자 데스크톱을 기반으로 한다는 점에서 심각한 결함이 있습니다.

아래 다이어그램에서는 공격자가 사용자 워크스테이션의 관리 VM을 통해 제어 체인을 따라 관심 있는 대상 개체에 접근할 수 있다는 점과 역방향 구성에서는 경로를 만들기가 어렵다는 점을 보여 줍니다.

PAW 아키텍처에서는 사용자 워크스테이션에서 관리 VM을 호스팅할 수 없지만, 관리 VM에서 표준 회사 이미지를 사용하는 사용자 VM을 호스팅하여 단일 PC를 사용하는 직원에게 모든 책임을 부여할 수 있습니다.

![PAW 아키텍처 다이어그램](../media/privileged-access-workstations/PAWFig9.JPG)

#### <a name="shielded-vm-based-paws"></a>보호된 VM 기반 PAW

관리 VM 모델의 보안 변형은 [보호된 가상 머신](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)을 사용하여 사용자 VM과 함께 하나 이상의 관리 VM을 호스팅하는 것입니다.
보호된 VM은 물리적 머신의 표준 사용자 데스크톱에서 잠재적으로 신뢰할 수 없는 사용자 또는 코드를 실행할 수 있는 환경에서 보안 작업을 실행하도록 설계되었습니다.
보호된 VM에는 자체의 저장 데이터를 암호화할 수 있는 가상 TPM이 있으며, 기본 콘솔 액세스, PowerShell Direct 및 VM 디버그 기능과 같은 여러 관리 컨트롤을 사용하지 않도록 설정하여 표준 사용자 데스크톱 및 기타 VM에서 VM을 추가로 격리할 수 있습니다.
보호된 VM의 키는 신뢰할 수 있는 키 관리 서버에 저장됩니다. 이를 위해 VM을 시작하기 위해 키를 해제하기 전에 물리적 디바이스에서 해당 ID와 상태를 증명해야 합니다.
이렇게 하면 보호된 VM이 의도한 디바이스에서만 시작할 수 있고, 해당 디바이스에서 알려진 신뢰할 수 있는 소프트웨어 구성을 실행합니다.

보호된 VM은 서로 격리되어 있고 표준 사용자 데스크톱에서 격리되므로 이러한 관리 VM에서 서로 다른 계층을 관리하는 경우에도 단일 호스트에서 여러 보호된 PAW VM을 실행할 수 있습니다.

자세한 내용은 아래의 [보호된 패브릭을 사용하여 PAW 배포](#deploy-paws-using-a-guarded-fabric) 섹션을 참조하세요.

#### <a name="jump-server"></a>점프 서버

관리용 "점프 서버" 아키텍처는 소수의 관리 콘솔 서버를 설정하며 직원이 관리 작업에 이러한 서버를 사용하도록 제한합니다. 이는 일반적으로 원격 데스크톱 서비스, 타사 프레젠테이션 가상화 솔루션 또는 VDI(가상 데스크톱 인프라) 기술을 기반으로 합니다.

이 접근 방식은 종종 관리 위험을 완화하기 위해 제안되며 몇 가지 보안 보증을 제공하지만 점프 서버 접근 방식 자체는 ["클린 소스" 원칙](../securing-privileged-access/securing-privileged-access-reference-material.md#clean-source-principle)에 위배되므로 특정 공격에 취약합니다. 클린 소스 원칙에서는 모든 보안 종속성이 보안 개체와 같이 신뢰할 수 있어야 합니다.

![간단한 제어 관계를 보여 주는 그림](../media/privileged-access-workstations/PAWFig3.JPG)

이 그림에서는 간단한 제어 관계를 보여 줍니다. 개체를 제어하는 주체는 해당 개체의 보안 종속성입니다. 악의적 사용자가 대상 개체의 보안 종속성(주체)을 제어할 수 있는 경우에는 해당 개체를 제어할 수 있습니다.

점프 서버의 관리 세션은 해당 점프 서버에 액세스하는 로컬 컴퓨터의 무결성에 의존합니다. 이 컴퓨터가 피싱 공격 및 다른 인터넷 기반 공격 벡터를 받기 쉬운 사용자 워크스테이션인 경우 관리 세션도 이러한 위험에 노출됩니다.

![공격자가 설정된 제어 체인을 따라 관심 있는 대상 개체에 접근할 수 있는 방법을 보여 주는 그림](../media/privileged-access-workstations/PAWFig4.JPG)

위 그림에서는 공격자가 설정된 제어 체인을 따라 관심 있는 대상 개체에 접근할 수 있는 방법을 보여 줍니다.

다단계 인증과 같은 일부 고급 보안 제어는 공격자가 사용자 워크스테이션에서 이 관리 세션을 제어하기 더욱 어렵게 만들 수 있지만 공격자가 원본 컴퓨터에 대한 관리 액세스 권한을 가진 경우 기술적 공격(예: 합법적 세션에 불법적 명령 삽입, 합법적 프로세스 하이재킹 등)으로부터 완벽하게 보호할 수 있는 보안 기능은 없습니다.

이 PAW 지침의 기본 구성은 PAW에 관리 도구를 설치하지만 필요한 경우 점프 서버 아키텍처를 추가할 수도 있습니다.

![공격자에게 대상 개체에 대한 어떤 경로도 제공하지 않도록 제어 관계를 반대로 전환하고 관리 워크스테이션에서 사용자 응용 프로그램에 액세스하는 방법을 보여 주는 그림](../media/privileged-access-workstations/PAWFig5.JPG)

이 그림에서는 공격자에게 대상 개체에 대한 어떤 경로도 제공하지 않도록 제어 관계를 반대로 전환하고 관리 워크스테이션에서 사용자 응용 프로그램에 액세스하는 방법을 보여 줍니다. 사용자 점프 서버는 여전히 위험에 노출되어 있으므로 해당 인터넷 연결 컴퓨터에 적절한 보호 제어, 감지 제어 및 응답 프로세스를 적용해야 합니다.

이 구성에서는 관리자가 데스크톱의 사용자 세션에 실수로 관리자 자격 증명을 입력하지 않도록 운영 방침을 철저히 준수해야 합니다.

![관리 자산에 공격자의 경로가 추가되지 않도록 PAW에서 관리 점프 서버에 액세스하는 방법을 보여 주는 그림](../media/privileged-access-workstations/PAWFig6.JPG)

이 그림에서는 관리 자산에 공격자의 경로가 추가되지 않도록 PAW에서 관리 점프 서버에 액세스하는 방법을 보여 줍니다. 이 방법을 사용하면 PAW가 있는 점프 서버에서 관리 작업을 모니터링하고 관리 애플리케이션 및 도구를 배포할 위치를 통합할 수 있습니다. 이 경우 디자인 복잡성이 증가하지만 PAW 구현에 많은 계정 및 워크스테이션이 사용되는 경우 보안 모니터링 및 소프트웨어 업데이트가 간소화될 수 있습니다. PAW와 유사한 보안 표준에 맞게 점프 서버를 구축하고 구성해야 합니다.

#### <a name="privilege-management-solutions"></a>권한 관리 솔루션

권한 관리 솔루션은 특정 권한 또는 권한 있는 계정에 대한 임시 액세스를 제공하는 애플리케이션입니다. 권한 관리 솔루션은 권한 있는 액세스의 보안을 유지하고 관리 작업의 중요한 가시성 및 책임감을 제공하기 위한 전체 전략의 매우 중요한 구성 요소입니다.

이러한 솔루션은 일반적으로 유연한 워크플로를 사용하여 액세스 권한을 부여하며, 대부분 서비스 계정 암호 관리 및 관리 점프 서버와의 통합과 같은 추가 보안 기능을 갖추고 있습니다. 권한 관리 기능을 제공하는 솔루션은 시중에 많이 있으며, 그 중 하나가 MIM(Microsoft Identity Manager) PAM(Privileged Access Management)입니다.

PAW를 사용하여 권한 관리 솔루션에 액세스하는 것이 좋습니다. 이러한 솔루션에 대한 액세스 권한은 PAW에만 부여되어야 합니다. 이러한 솔루션을 PAW 대체용으로 사용하지 않는 것이 좋습니다. 잠재적으로 손상된 사용자 데스크톱에서 이러한 솔루션을 사용하여 권한에 액세스하는 것은 아래 다이어그램에 나와 있듯이 [클린 소스](https://aka.ms/cleansource)에 위배되기 때문입니다.

![이러한 솔루션을 PAW 대체용으로 사용하지 않는 것이 좋은데, 잠재적으로 손상된 사용자 데스크톱에서 이러한 솔루션을 사용하여 권한에 액세스하는 것은 클린 소스에 위배되기 때문임을 보여 주는 다이어그램](../media/privileged-access-workstations/PAWFig7.JPG)

PAW에 이러한 솔루션에 대한 액세스 권한을 제공하면 이 다이어그램에 설명된 대로 PAW와 권한 관리 솔루션 모두의 보안 이점을 얻을 수 있습니다.

![PAW에 이러한 솔루션에 대한 액세스 권한을 제공하면 PAW와 권한 관리 솔루션 모두의 보안 이점을 얻을 수 있음을 보여 주는 다이어그램](../media/privileged-access-workstations/PAWFig8.JPG)

> [!NOTE]
> 이러한 시스템은 해당 시스템에서 관리하는 권한의 최상위 계층에서 분류되고 해당 보안 수준 이상으로 보호되어야 합니다. 일반적으로 계층 0 솔루션 및 계층 0 자산을 관리하도록 구성되며 계층 0에서 분류되어야 합니다.
> 계층 모델에 대한 자세한 내용은 [https://aka.ms/tiermodel](https://aka.ms/tiermodel)을 참조하고, 계층 0 그룹에 대한 자세한 내용은 [권한 있는 액세스 보안 참조 자료](../securing-privileged-access/securing-privileged-access-reference-material.md)의 계층 0 동일성을 참조하세요.

MIM(Microsoft Identity Manager) PAM(Privileged Access Management)을 배포하는 방법에 대한 자세한 내용은 [https://aka.ms/mimpamdeploy](https://aka.ms/mimpamdeploy)를 참조하세요.

## <a name="paw-scenarios"></a>PAW 시나리오

이 섹션에는 이 PAW 지침이 적용되는 시나리오에 대한 지침이 포함되어 있습니다. 모든 시나리오에서 관리자는 원격 시스템을 지원하는 데에만 PAW를 사용하도록 교육을 받아야 합니다. 성공적이고 안전한 사용을 장려하기 위해 모든 PAW 사용자에게도 PAW 환경 개선을 위한 피드백을 제공하도록 장려해야 합니다. 이 피드백은 PAW 프로그램과의 통합을 위해 신중히 검토해야 합니다.

모든 시나리오에서 이후 단계의 추가 강화 및 이 지침의 다른 하드웨어 프로필을 사용하여 역할의 유용성 및 보안 요구 사항을 충족할 수 있습니다.

> [!NOTE]
> 이 지침에서는 인터넷의 특정 서비스(예: Azure 및 Office 365 관리 포털)에 대한 액세스 요구와 모든 호스트 및 서비스의 "오픈 인터넷"을 명시적으로 구분합니다.

계층 지정에 대한 자세한 내용은 [계층 모델 페이지](https://aka.ms/tiermodel)를 참조하세요.

|**시나리오**|**PAW 사용 여부**|**범위 및 보안 고려 사항**|
|---------|--------|---------------------|
|Active Directory 관리자 - 계층 0|예|1단계 지침에 따라 구축한 PAW면 이 역할에 충분합니다.<p>-   이 시나리오에 가장 강력한 보호를 제공하기 위해 관리 포리스트를 추가할 수 있습니다. ESAE 관리 포리스트에 대한 자세한 내용은 [ESAE 관리 포리스트 디자인 방법](../securing-privileged-access/securing-privileged-access-reference-material.md#esae-administrative-forest-design-approach)을 참조하세요.<br />-   PAW를 사용하여 관리되는 여러 도메인 또는 여러 포리스트를 관리할 수 있습니다.<br />-   도메인 컨트롤러가 IaaS(Infrastructure as a Service) 또는 온-프레미스 가상화 솔루션에서 호스팅되는 경우 해당 솔루션의 관리자를 위해 PAW 구현의 우선 순위를 지정해야 합니다.|
|Azure IaaS 및 PaaS 서비스 관리자 - 계층 0 또는 계층 1(범위 및 디자인 고려 사항 참조)|예|2단계에서 제공된 지침에 따라 구축된 PAW면 이 역할에 충분합니다.<p>-   최소한 전역 관리자 및 구독 비용 청구 관리자에게 PAW를 사용해야 합니다. 중요하거나 민감한 서버의 위임된 관리자에게도 PAW를 사용해야 합니다.<br />-   [Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) 및 ADFS(Active Directory Federation Services)와 같은 클라우드 서비스를 위해 디렉터리 동기화 및 ID 페더레이션을 제공하는 운영 체제 및 애플리케이션을 관리하는 데 PAW를 사용해야 합니다.<br />-   아웃바운드 네트워크 제한에서 2단계의 지침을 사용하는 권한 있는 클라우드 서비스에 대한 연결만 허용해야 합니다. 공개 인터넷 액세스는 PAW에서 허용되어서는 안 됩니다.<br />-   Windows Defender Exploit Guard는 워크스테이션에서 구성해야 합니다. **참고:**     도메인 컨트롤러 또는 다른 계층 0 호스트가 구독에 있는 경우 해당 구독은 포리스트의 계층 0으로 간주됩니다. Azure에서 호스트되는 계층 0 서버가 없는 경우 구독은 계층 1입니다.|
|Office 365 테넌트 관리자 <br />- 계층 1|예|2단계에서 제공된 지침에 따라 구축된 PAW면 이 역할에 충분합니다.<p>-   최소한 구독 비용 청구 관리자, 전역 관리자, Exchange 관리자, SharePoint 관리자 및 사용자 관리 관리자 역할에 PAW를 사용해야 합니다. 또한 매우 중요하거나 민감한 데이터의 위임된 관리자에게도 PAW를 사용하는 것이 좋습니다.<br />-   Windows Defender Exploit Guard는 워크스테이션에서 구성해야 합니다.<br />-   아웃바운드 네트워크 제한에서 2단계의 지침을 사용하는 Microsoft 서비스에 대한 연결만 허용해야 합니다. 공개 인터넷 액세스는 PAW에서 허용되어서는 안 됩니다.|
|다른 IaaS 또는 PaaS 클라우드 서비스 관리자<br />- 계층 0 또는 계층 1(범위 및 디자인 고려 사항 참조)|예|2단계에서 제공된 지침에 따라 구축된 PAW면 이 역할에 충분합니다.<p>-   에이전트 설치 권한, 하드 디스크 파일 내보내기 권한, 운영 체제, 민감한 데이터 또는 비즈니스에 중요한 데이터가 저장된 스토리지 액세스 권한 등 클라우드 호스트된 VM에 대한 관리 권한을 가진 모든 역할에 PAW를 사용해야 합니다.<br />-   아웃바운드 네트워크 제한에서 2단계의 지침을 사용하는 Microsoft 서비스에 대한 연결만 허용해야 합니다. 공개 인터넷 액세스는 PAW에서 허용되어서는 안 됩니다.<br />-   Windows Defender Exploit Guard는 워크스테이션에서 구성해야 합니다. **참고:** 도메인 컨트롤러 또는 다른 계층 0 호스트가 구독에 있는 경우 해당 구독은 포리스트의 계층 0입니다. Azure에서 호스트되는 계층 0 서버가 없는 경우 구독은 계층 1입니다.|
|가상화 관리자<br />- 계층 0 또는 계층 1(범위 및 디자인 고려 사항 참조)|예|2단계에서 제공된 지침에 따라 구축된 PAW면 이 역할에 충분합니다.<p>-   에이전트 설치 권한, 가상 하드 디스크 파일 내보내기 권한, 게스트 운영 체제 정보, 민감한 데이터 또는 비즈니스에 중요한 데이터가 저장된 스토리지 액세스 권한 등 VM에 대한 관리 권한을 가진 모든 역할에 PAW를 사용해야 합니다. **참고:** 도메인 컨트롤러 또는 다른 계층 0 호스트가 구독에 있는 경우 가상화 시스템(및 해당 관리자)은 포리스트의 계층 0으로 간주됩니다. 가상화 시스템에서 호스트되는 계층 0 서버가 없는 경우 구독은 계층 1입니다.|
|서버 유지 관리 관리자<br />- 계층 1|예|2단계에서 제공된 지침에 따라 구축된 PAW면 이 역할에 충분합니다.<p>-   Windows Server, Linux 및 기타 운영 체제를 실행하는 엔터프라이즈 서버 및 응용 프로그램에 대해 업데이트, 패치, 문제 해결 등을 수행하는 관리자에게 PAW를 사용해야 합니다.<br />-   PAW에서 보다 대규모의 관리자를 처리하려면 전용 관리 도구를 추가해야 할 수도 있습니다.|
|사용자 워크스테이션 관리자 <br />- 계층 2|예|2단계에서 제공된 지침에 따라 구축된 PAW면 최종 사용자 디바이스(예: 지원 센터 및 데스크 측 지원 역할)에 대한 관리 권한이 있는 역할에 충분합니다.<p>-   티켓 관리 및 기타 지원 기능을 사용하려면 PAW에 추가 애플리케이션을 설치해야 할 수도 있습니다.<br />-   Windows Defender Exploit Guard는 워크스테이션에서 구성해야 합니다.<br />    PAW에서 보다 대규모의 관리자를 처리하려면 전용 관리 도구를 추가해야 할 수도 있습니다.|
|SQL, SharePoint 또는 LOB(기간 업무) 관리자<br />- 계층 1|예|2단계 지침에 따라 구축한 PAW면 이 역할에 충분합니다.<p>-   관리자가 서버에 연결하지 않고도 원격 데스크톱을 사용하여 애플리케이션을 관리할 수 있도록 하려면 PAW에 추가 관리 도구를 설치해야 할 수도 있습니다.|
|소셜 미디어 현재 상태를 관리하는 사용자|부분적으로|2단계에서 제공된 지침에 따라 구축한 PAW를 시작점으로 사용하여 이러한 역할에 대한 보안을 제공할 수 있습니다.<p>-   소셜 미디어 계정에 대한 액세스를 공유, 보호 및 추적하는 데 AAD(Azure Active Directory)를 사용하여 소셜 미디어 계정을 보호하고 관리합니다.<br />    이 기능에 대한 자세한 내용은 [이 블로그 게시물](https://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)을 참조하세요.<br />-   아웃바운드 네트워크 제한에서 이러한 서비스에 대한 연결을 허용해야 합니다. 공개 인터넷 연결을 허용(많은 PAW 보증을 부정하므로 보안 위험이 훨씬 높음)하거나 서비스에 필요한 DNS 주소만 허용(가져오기 어려울 수 있음)하면 됩니다.|
|표준 사용자|아니요|많은 강화 단계를 표준 사용자에게 사용할 수 있지만 PAW는 대부분의 사용자가 작업에 필요한 공개 인터넷 액세스로부터 계정을 격리하도록 설계되었습니다.|
|게스트 VDI/키오스크|아니요|많은 강화 단계를 게스트용 키오스크 시스템에 사용할 수 있지만 PAW 아키텍처는 민감도가 높은 계정에는 높은 보안을 제공하고 민감도가 낮은 계정에는 낮은 보안을 제공하도록 설계되었습니다.|
|VIP 사용자(임원, 연구원 등)|부분적으로|2단계에서 제공된 지침에 따라 구축한 PAW는 이러한 역할에 대한 보안을 제공하기 위한 시작점으로 사용할 수 있습니다.<p>-   이 시나리오는 표준 사용자 데스크톱과 유사하지만 일반적으로 애플리케이션 프로필이 더 작고 단순하며 잘 알려져 있습니다. 이 시나리오에서는 일반적으로 중요한 데이터, 서비스 및 애플리케이션(데스크톱에 설치되거나 설치되지 않은)을 검색하고 보호해야 합니다.<br />-   이러한 역할에는 일반적으로 높은 보안 수준과 매우 높은 유용성 수준이 필요하므로 사용자 요구 사항을 충족하려면 디자인 변경이 필요합니다.|
|산업용 제어 시스템(예: SCADA, PCN 및 DC)|부분적으로|대부분의 ICS 콘솔(SCADA 및 PCN과 같은 일반적인 표준 포함)에서는 공개 인터넷을 검색하고 전자 메일을 확인할 필요가 없으므로 2단계에서 제공된 지침에 따라 구축한 PAW를 시작점으로 사용하여 이러한 역할에 대한 보안을 제공할 수 있습니다.<p>-   물리적 머신을 제어하는 데 사용되는 애플리케이션은 통합하고, 호환성을 테스트하고, 적절히 보호해야 합니다.|
|임베디드 운영 체제|아니요|PAW의 많은 강화 단계를 임베디드 운영 체제에 사용할 수 있지만 이 시나리오의 강화를 위해서는 사용자 지정 솔루션을 개발해야 합니다.|

> [!NOTE]
> **조합 시나리오** 일부 직원에게 여러 시나리오에 걸친 관리 책임이 있을 수 있습니다.
> 이러한 경우 유의해야 하는 주요 규칙은 항상 계층 모델 규칙을 따라야 한다는 것입니다. 자세한 내용은 계층 모델 페이지를 참조하세요.

> [!NOTE]
> **PAW 프로그램 크기 조정** 더 많은 관리자와 역할을 수용하기 위해 PAW 프로그램이 확장되므로 보안 표준과 유용성을 지속적으로 준수해야 합니다. 그러러면 IT 지원 구조를 업데이트하거나 PAW 관련 문제(예: PAW 온보딩 프로세스, 사고 관리, 구성 관리, 유용성 문제를 해결하기 위한 피드백 수집)를 해결할 수 있는 새로운 IT 지원 구조를 만들어야 할 수 있습니다.  예를 들어 관리자의 재택 근무를 허용하기로 결정한 경우 데스크톱 PAW에서 랩톱 PAW로 전환해야 하며 여기에는 추가 보안 고려 사항이 필요할 수 있습니다.  또 따른 예로는 새로운 관리자를 위한 교육을 만들거나 업데이트해야 하는 경우입니다. 이 교육에는 PAW의 적절한 사용(PAW가 중요한 이유 및 PAW에 해당하는 것과 PAW에 해당하지 않는 것 포함)에 관한 콘텐츠가 포함되어야 합니다.  PAW 프로그램을 확장할 때 해결해야 하는 고려 사항에 대한 자세한 내용은 지침의 2단계를 참조하세요.

이 지침에는 위 시나리오와 관련된 PAW 구성의 자세한 지침이 포함되어 있습니다. 다른 시나리오에 대한 요구 사항이 있는 경우 이 지침을 기반으로 하는 지침을 직접 도입하거나 Microsoft와 같은 전문 서비스 조직의 지원을 받을 수 있습니다.

사용자 환경에 맞춤화된 PAW를 디자인하기 위해 Microsoft 서비스를 참여시키는 방법에 대한 자세한 내용은 Microsoft 담당자에게 문의하거나 [이 페이지](https://www.microsoft.com/microsoftservices/campaigns/cybersecurity-protection.aspx)를 방문하세요.

## <a name="paw-phased-implementation"></a>단계별 PAW 구현

PAW는 관리를 위한 안전하고 신뢰할 수 있는 토대를 제공하므로 구축 프로세스가 안전하고 신뢰할 수 있어야 합니다.  이 섹션에서는 Microsoft IT 조직과 Microsoft 클라우드 엔지니어링 및 서비스 관리 조직에서 사용하는 것과 매우 유사한 일반적인 원칙 및 개념을 사용하여 사용자 고유의 PAW를 구축할 수 있는 자세한 지침을 제공합니다.

이러한 지침은 가장 중요한 마이그레이션을 신속하게 구축한 다음 기업에서 PAW 사용을 점진적으로 늘리고 확장하는 데 중점을 둔 세 단계로 구성되어 있습니다.

* [1단계 - Active Directory 관리자를 위한 즉시 배포](#phase-1-immediate-deployment-for-active-directory-administrators)
* [2단계 - 모든 관리자로 PAW 확장](#phase-2-extend-paw-to-all-administrators)
* [3단계 - 고급 PAW 보안](#phase-3-extend-and-enhance-protection)

동일한 전체 프로젝트의 일부로 계획하고 구현한 경우에도 항상 단계를 순서대로 수행해야 합니다.

### <a name="phase-1-immediate-deployment-for-active-directory-administrators"></a>1단계: Active Directory 관리자를 위한 즉시 배포

용도: 온-프레미스 도메인 및 포리스트 관리 역할을 보호할 수 있는 PAW를 빠르게 제공합니다.

범위: Enterprise Admins, Domain Admins(모든 도메인) 및 기타 신뢰할 수 있는 ID 시스템의 관리자를 포함한 계층 0 관리자

1단계는 온-프레미스 Active Directory 도메인을 관리하는 관리자에 중점을 둡니다. 이러한 관리자는 공격자가 자주 대상으로 삼는 매우 중요한 역할입니다. 이러한 ID 시스템은 Active Directory DC(도메인 컨트롤러)가 온-프레미스 데이터 센터에서 호스트되든, Azure IaaS(Infrastructure as a Service)에서 호스트되든, 다른 IaaS 공급자에서 호스트되든 상관없이 이러한 관리자를 보호하는 데 효과적으로 작동합니다.

이 단계에서는 PAW(Privileged Access Workstation)를 호스트하고 PAW를 직접 배포할 보안 관리 Active Directory OU(조직 구성 단위) 구조를 만듭니다.  이 구조에는 PAW를 지원하는 데 필요한 그룹 정책 및 그룹도 포함됩니다.  [TechNet 갤러리](https://aka.ms/pawmedia)에서 제공되는 PowerShell 스크립트를 사용하여 대부분의 구조를 만듭니다.

스크립트는 다음 OU 및 보안 그룹을 만듭니다.

* OU(조직 구성 단위)
   * 새로운 6개 최상위 OU:  Admin, Groups, Tier 1 Servers, Workstations, User Accounts 및 Computer Quarantine.  각 최상위 OU에는 여러 자식 OU가 포함됩니다.
* 그룹
   * 새로운 6개 보안 사용 글로벌 그룹:  Tier 0 Replication Maintenance, Tier 1 Server Maintenance, Service Desk Operators, Workstation Maintenance, PAW Users, PAW Maintenance

또한 여러 그룹 정책 개체, 즉 PAW Configuration - Computer, PAW Configuration - User, RestrictedAdmin Required - Computer, PAW Outbound Restrictions, Restrict Workstation Logon, Restrict Server Logon도 만듭니다.

1단계에는 다음과 같은 단계가 포함됩니다.

#### <a name="complete-the-prerequisites"></a>필수 구성 요소 완료

1. **모든 관리자가 관리 및 최종 사용자 활동에 별도의 개별 계정을 사용하는지 확인합니다**(전자 메일, 인터넷을 검색, LOB(기간 업무) 애플리케이션 및 기타 비관리 활동 포함).  특정 계정만 PAW 자체에 로그온할 수 있으므로 권한 있는 각 직원에게 표준 사용자 계정과 다른 관리 계정을 할당하는 것은 PAW 모델의 기본 사항입니다.

   > [!NOTE]
   > 각 관리자는 관리에 자신의 계정을 사용해야 합니다.  관리 계정을 공유해서는 안 됩니다.

2. **계층 0 권한 있는 관리자 수 최소화합니다**.  각 관리자는 PAW를 사용해야 하므로 관리자 수를 줄이면 이들을 지원하는 데 필요한 PAW 수 및 관련 비용이 감소합니다. 또한 관리자 수가 적을수록 이러한 권한 및 관련 위험에 대한 노출도 줄어듭니다. 한 곳에 있는 관리자들은 PAW를 공유할 수 있지만 별도의 물리적 위치에 있는 관리자들에게는 별도의 PAW가 필요합니다.
3. **모든 기술 요구 사항을 충족하는 신뢰할 수 있는 공급자로부터 하드웨어를 구입합니다**. [Credential Guard를 사용하여 도메인 자격 증명 보호](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) 문서의 기술 요구 사항을 충족하는 하드웨어를 구입하는 것이 좋습니다.

   > [!NOTE]
   > 이러한 기능이 없는 하드웨어에 설치된 PAW는 상당한 보호를 제공할 수 있지만 Credential Guard 및 Device Guard와 같은 고급 보안 기능을 사용할 수 없습니다.  Credential Guard와 Device Guard는 1단계 배포에는 필요 없지만 3단계(고급 강화)의 일부로 적극 권장됩니다.
   >
   > PAW에 사용되는 하드웨어를 조직에서 신뢰할 수 있는 보안 방식을 갖춘 제조업체 및 공급업체로부터 구입했는지 확인하세요. 이것이 바로 공급망 보안에 클린 소스 원칙을 적용하는 것입니다.
   >
   > 공급망 보안의 중요성에 대한 자세한 배경은 [이 사이트](https://www.microsoft.com/security/cybersecurity/)를 참조하세요.

4. **필요한 Windows 10 Enterprise Edition 및 애플리케이션 소프트웨어를 획득하고 유효성을 검사합니다**. PAW에 필요한 소프트웨어를 구입하고 [설치 미디어에 대한 클린 소스](https://aka.ms/cleansource)의 지침에 따라 유효성을 검사합니다.

   * Windows 10 Enterprise Edition
   * Windows 10용 [원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520)
   * [Windows 10 보안 기준](https://aka.ms/win10baselines)

      > [!NOTE]
      > Microsoft에서는 모든 운영 체제 및 애플리케이션에 대한 MD5 해시를 MSDN에 게시하지만 일부 소프트웨어 공급업체는 이와 유사한 설명서를 제공하지 않습니다.  이 경우 다른 전략이 필요합니다.  소프트웨어 유효성 검사에 대한 자세한 내용은 설치 미디어에 대한 [클린 소스](https://aka.ms/cleansource)를 참조하세요.

5. **인트라넷에서 사용 가능한 WSUS 서버가 있는지 확인합니다**. PAW에 대한 업데이트를 다운로드하고 설치하려면 인트라넷에 WSUS 서버가 필요합니다. Windows 10에 대한 모든 보안 업데이트를 자동으로 승인하도록 이 WSUS 서버를 구성하거나, 관리 직원이 소프트웨어 업데이트를 신속하게 승인하는 책임을 맡아야 합니다.

   > [!NOTE]
   > 자세한 내용은 [업데이트 승인 지침](https://technet.microsoft.com/library/cc708458(v=ws.10).aspx)의 "업데이트 설치 자동 승인" 섹션을 참조하세요.

#### <a name="deploy-the-admin-ou-framework-to-host-the-paws"></a>PAW를 호스트할 관리자 OU 프레임 워크 배포

1. [TechNet 갤러리](https://aka.ms/PAWmedia)에서 PAW 스크립트 라이브러리를 다운로드합니다.

   > [!NOTE]
   > 모든 파일을 다운로드하여 동일한 디렉터리에 저장하고, 아래에 지정된 순서대로 실행합니다.  Create-PAWGroups는 Create-PAWOUs를 통해 만들어진 OU에 따라 달라지고, Set-PAWOUDelegation은 Create-PAWGroups를 통해 만들어진 그룹에 따라 달라집니다.
   > 스크립트 또는 쉼표로 구분된 값(CSV) 파일을 수정하지 마세요.

2. **Create-PAWOUs.ps1 스크립트를 실행합니다**.  이 스크립트는 Active Directory에 새 OU(조직 구성 단위) 구조를 만들고 필요에 따라 새 OU의 GPO 상속을 차단합니다.
3. **Create-PAWGroups.ps1 스크립트를 실행합니다**.  이 스크립트는 적절한 OU에 새 글로벌 보안 그룹을 만듭니다.

   > [!NOTE]
   > 이 스크립트는 새 보안 그룹을 만들지만 이러한 그룹을 자동으로 채우지는 않습니다.

4. **Set-PAWOUDelegation.ps1 스크립트를 실행합니다**.  이 스크립트는 적절한 그룹에 새 OUI에 대한 사용 권한을 할당합니다.

#### <a name="move-tier-0-accounts-to-the-admintier-0accounts-ou"></a>계층 0 계정을 Admin\Tier 0\Accounts OU로 이동

Domain Admin, Enterprise Admin 또는 이와 동등한 계층 0 그룹(중첩 구성원 포함)의 구성원인 각 계정을 이 OU로 이동합니다. 조직에 이러한 그룹에 추가된 고유의 그룹이 있는 경우 Admin\Tier 0\Groups OU로 이동해야 합니다.

   > [!NOTE]
   > 계층 0인 그룹에 대한 자세한 내용은 [권한 있는 액세스 보안 참조 자료](../securing-privileged-access/securing-privileged-access-reference-material.md)에서 "계층 0 동일성"을 참조하세요.

#### <a name="add-the-appropriate-members-to-the-relevant-groups"></a>관련 그룹에 적절한 구성원 추가

1. **PAW Users** - 1단계의 1에서 식별한 Domain 또는 Enterprise Admin 그룹의 계층 0 관리자를 추가합니다.
2. **PAW Maintenance** - PAW 유지 관리 및 문제 해결 작업에 사용할 계정을 하나 이상 추가합니다. PAW Maintenance 계정은 매우 드물게 사용됩니다.

   > [!NOTE]
   > 동일한 사용자 계정이나 그룹을 PAW Users와 PAW Maintenance 둘 다에 추가하지 마세요.  PAW 보안 모델은 부분적으로 PAW 사용자 계정에 관리되는 시스템과 PAW 자체 중 하나(둘 다가 아님)에 대한 권한이 있다는 가정을 기반으로 합니다.
   >
   > * 이는 1단계에서 적절한 관리 방식 및 습관을 구축하는 데 중요합니다.
   > * 또한 2단계 이상에서는 PAW를 통한 권한 상승을 방지하는 데 매우 중요합니다(PAW는 계층에 걸쳐 있기 때문).
   >
   > 이상적으로는 업무 분리의 원칙을 적용하여 어떤 직원에게도 여러 계층의 업무를 할당하지 않는 것이 좋지만 Microsoft에서는 많은 조직에 인력이 제한되어 있어(또는 다른 조직의 요구 사항으로 인해) 완전히 분리하지 못한다는 것을 인식하고 있습니다. 이러한 경우 같은 직원을 두 역할에 할당할 수 있지만 각각의 역할에 별도의 계정을 사용해야 합니다.

#### <a name="create-paw-configuration---computer-group-policy-object-gpo"></a>"PAW Configuration - Computer" GPO(그룹 정책 개체) 만들기

이 섹션에서는 이러한 PAW에 대한 특정 보호를 제공하는 새 "PAW Configuration - Computer" GPO를 만들고, 이를 계층 0 디바이스 OU(Tier 0\Admin 아래의 "Devices")에 연결합니다.

   > [!NOTE]
   > **이러한 설정을 기본 도메인 정책에 추가하지 마세요**.  잠재적으로 전체 Active Directory 환경에서 작업에 영향을 줄 수 있습니다.  여기에 설명된 새로 만든 GPO에서 이러한 설정을 구성하고 PAW OU에만 적용하세요.

1. **PAW 유지 관리 액세스** - 이 설정은 PAW의 특정 권한 있는 그룹의 구성원을 특정 사용자 집합으로 설정합니다. *컴퓨터 구성\기본 설정\제어판 설정\로컬 사용자* 및 그룹으로 이동하여 아래 단계를 따릅니다.
   1. **새로 만들기**를 클릭한 다음 **로컬 그룹**을 클릭합니다.
   2. **업데이트** 작업을 선택한 다음 "Administrators(기본 제공)"를 선택합니다. 찾아보기 단추를 사용하여 Administrators 도메인 그룹을 선택하지 마세요.
   3. **모든 구성원 사용자 삭제** 및 **모든 구성원 그룹 삭제** 확인란을 선택합니다.
   4. PAW Maintenance(pawmaint) 및 Administrator를 추가합니다. 찾아보기 단추를 사용하여 Administrator를 선택하지 마세요.

      > [!NOTE]
      > PAW Users 그룹을 로컬 Administrators 그룹의 구성원 목록에 추가하지 마세요.  PAW Users가 실수로 또는 의도적으로 PAW 자체의 보안 설정을 수정할 수 없도록 하려면 이들이 로컬 Administrators 그룹의 구성원이 아니어야 합니다.
      >
      > 그룹 정책 기본 설정을 사용하여 그룹 구성원 자격을 수정하는 방법에 대한 자세한 내용은 [로컬 그룹 항목 구성](https://technet.microsoft.com/library/cc732525.aspx) TechNet 문서를 참조하세요.

2. **로컬 그룹 구성원 제한** - 이 설정은 워크스테이션의 로컬 관리자 그룹의 구성원이 항상 비어 있도록 합니다.
   1. 컴퓨터 구성\기본 설정\제어판 설정\로컬 사용자 및 그룹으로 이동하여 아래 단계를 따릅니다.
      1. **새로 만들기**를 클릭한 다음 **로컬 그룹**을 클릭합니다.
      2. **업데이트** 작업을 선택한 다음 "Backup Operators(기본 제공)"를 선택합니다. 찾아보기 단추를 사용하여 Backup Operators 도메인 그룹을 선택하지 마세요.
      3. **모든 구성원 사용자 삭제** 및 **모든 구성원 그룹 삭제** 확인란을 선택합니다.
      4. 그룹에 구성원을 추가하지 마세요.  **확인**을 클릭하기만 하면 됩니다.  빈 목록을 할당하면 그룹 정책에서 모든 구성원을 자동으로 제거하며 그룹 정책을 새로 고칠 때마다 구성원 목록이 비어 있게 됩니다.
   2. 다음 추가 그룹에 대해 위 단계를 완료합니다.
      * Cryptographic Operators
      * Hyper-V 관리자
      * Network Configuration Operators
      * Power Users
      * Remote Desktop Users
      * Replicators
   3. **PAW 로그온 제한** - PAW에 로그온 할 수 있는 계정을 제한합니다. 이 설정을 구성하려면 아래 단계를 따릅니다.
      1. 컴퓨터 구성\정책\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당\로컬 로그온 허용으로 이동합니다.
      2. [이 정책 설정 정의]를 선택하고, "PAW Users" 및 Administrators를 추가합니다(다시 말하지만, [찾아보기] 단추를 사용하여 Administrators를 선택하지 않음).
   4. **인바운드 네트워크 트래픽 차단** - 이 설정은 무단 인바운드 네트워크 트래픽이 PAW에 허용되지 않도록 합니다. 이 설정을 구성하려면 아래 단계를 따릅니다.
      1. 컴퓨터 구성\정책\Windows 설정\보안 설정\고급 보안이 포함된 Windows 방화벽\고급 보안이 포함된 Windows 방화벽으로 이동하여 아래 단계를 따릅니다.
         1. 고급 보안이 포함된 Windows 방화벽을 마우스 오른쪽 단추로 클릭하고 **정책 가져오기**를 선택합니다.
         2. **예**를 클릭하여 기존 방화벽 정책을 덮어쓰는 데 동의합니다.
         3. PAWFirewall.wfw로 이동하여 **열기**를 선택합니다.
         4. **확인**을 클릭합니다.

            > [!NOTE]
            > 이제 무단 트래픽으로 PAW에 연결해야 하는 주소 또는 서브넷을 추가할 수 있습니다(예: 보안 검사 또는 관리 소프트웨어).
            > WFW 파일의 설정은 모든 방화벽 프로필에 대해 "차단 - 기본값" 모드의 방화벽을 사용하도록 설정하고, 규칙 병합을 해제하며, 삭제된 패킷과 성공한 패킷을 둘 다 기록하도록 합니다. 이러한 설정은 PAW에서 시작된 연결에서의 양방향 통신을 계속 허용하면서 무단 트래픽을 차단하고, 로컬 관리자 권한이 있는 사용자가 GPO 설정을 재정의하고 PAW에서 들어오고 나가는 트래픽이 기록되도록 하는 로컬 방화벽 규칙을 만들지 못하도록 합니다.
            > **이 방화벽을 열면 PAW의 공격에 대한 취약성이 확장되고 보안 위험이 증가합니다. 따라서 주소를 추가하기 전에 이 지침의 PAW 관리 및 운영 섹션을 참조하세요**.

   5. **WSUS에 대한 Windows 업데이트 구성** - 아래 단계에 따라 설정을 변경하여 PAW에 대한 Windows 업데이트를 구성합니다.
      1. 컴퓨터 구성\정책\관리 템플릿\Windows 구성 요소\Windows 업데이트로 이동하여 아래 단계를 수행합니다.
         1. **자동 업데이트 구성 정책**을 사용하도록 설정합니다.
         2. **4 - 자동으로 다운로드하고 설치를 예약** 옵션을 선택합니다.
         3. **예약된 설치 날짜** 옵션을 **0 - 매일**로 변경하고 **예약된 설치 시간** 옵션을 조직에서 원하는 시간으로 변경합니다.
         4. **인트라넷 Microsoft 업데이트 서비스 위치 지정** 정책 옵션을 사용하도록 설정하고, 두 옵션 모두에서 ESAE WSUS 서버의 URL을 지정합니다.
   6. 다음과 같이 "PAW Configuration - Computer" GPO를 연결합니다.

         |정책|링크 위치|
         |-----|---------|
         |PAW Configuration - Computer |Admin\Tier 0\Devices|

#### <a name="create-paw-configuration---user-group-policy-object-gpo"></a>"PAW Configuration - User" GPO(그룹 정책 개체) 만들기

이 섹션에서는 이러한 PAW에 대한 특정 보호를 제공하는 새 "PAW Configuration - User" GPO를 만들고, 계층 0 계정 OU(Tier 0\Admin 아래의 "Accounts")에 연결합니다.

   > [!NOTE]
   > 이러한 설정을 기본 도메인 정책에 추가하지 마세요.

1. **인터넷 검색 차단** - 의도치 않은 인터넷 검색을 방지하기 위해 루프백 주소의 프록시 주소(127.0.0.1)를 설정합니다.
   1. 사용자 구성\기본 설정\Windows 설정\레지스트리로 이동합니다. 마우스 오른쪽 단추로 [레지스트리]를 클릭하고, **새로 만들기** > **레지스트리 항목**을 차례로 선택하고, 다음 설정을 구성합니다.
      1. 작업:  바꾸기
      2. Hive: HKEY_CURRENT_USER
      3. 키 경로:  Software\Microsoft\Windows\CurrentVersion\Internet Settings
      4. 값 이름: ProxyEnable

         > [!NOTE]
         > 값 이름 왼쪽에 있는 기본값 상자를 선택하지 마세요.

      5. 값 형식: REG_DWORD
      6. 값 데이터: 1
         1. 일반 탭을 클릭하고 **이 항목을 더 이상 적용하지 않을 때 제거**를 선택합니다.
         2. 일반 탭에서 **항목 수준 대상**을 선택하고 **대상**을 클릭합니다.
         3. **새 항목**을 클릭하고 **보안 그룹**을 선택합니다.
         4. "..." 단추를 선택하고 PAW Users 그룹을 찾습니다.
         5. **새 항목**을 클릭하고 **보안 그룹**을 선택합니다.
         6. "..." 단추를 선택하고 **Cloud Services Admins** 그룹을 찾습니다.
         7. **Cloud Services Admins** 항목을 클릭하고 **항목 옵션**을 클릭합니다.
         8. **아님**을 선택합니다.
         9. 대상 창에서 **확인**을 클릭합니다.
      7. **확인**을 클릭하여 ProxyServer 그룹 정책 설정을 완료합니다.
   2. 사용자 구성\기본 설정\Windows 설정\레지스트리로 이동합니다. 마우스 오른쪽 단추로 [레지스트리]를 클릭하고, **새로 만들기** > **레지스트리 항목**을 차례로 선택하고, 다음 설정을 구성합니다.

      * 작업: 바꾸기
      * Hive: HKEY_CURRENT_USER
      * 키 경로: Software\Microsoft\Windows\CurrentVersion\Internet Settings
         * 값 이름: ProxyServer

            > [!NOTE]
            > 값 이름 왼쪽에 있는 기본값 상자를 선택하지 마세요.

         * 값 형식: REG_SZ
         * 값 데이터: 127.0.0.1:80
            1. **일반** 탭을 클릭하고 **이 항목을 더 이상 적용하지 않을 때 제거**를 선택합니다.
            2. **일반** 탭에서 **항목 수준 대상**을 선택하고 **대상**을 클릭합니다.
            3. **새 항목**을 클릭하고 보안 그룹을 선택합니다.
            4. "..." 단추를 선택하고 PAW Users 그룹을 추가합니다.
            5. **새 항목**을 클릭하고 보안 그룹을 선택합니다.
            6. "..." 단추를 선택하고 **Cloud Services Admins** 그룹을 찾습니다.
            7. **Cloud Services Admins** 항목을 클릭하고 **항목 옵션**을 클릭합니다.
            8. **아님**을 선택합니다.
            9. 대상 창에서 **확인**을 클릭합니다.

   3. **확인**을 클릭하여 ProxyServer 그룹 정책 설정을 완료합니다.
2. 사용자 구성\정책\관리 템플릿\Windows 구성 요소\Internet Explorer로 이동하여 아래 옵션을 사용하도록 설정합니다. 이러한 설정은 관리자가 프록시 설정을 수동으로 재정의하는 것을 방지합니다.
   1. **자동 구성 설정 변경할 수 없음** 설정을 사용하도록 설정합니다.
   2. **프록시 설정 변경 방지** 설정을 사용하도록 설정합니다.

#### <a name="restrict-administrators-from-logging-onto-lower-tier-hosts"></a>관리자가 하위 계층 호스트에 로그온하지 못하도록 제한

이 섹션에서는 권한 있는 관리 계정에서 하위 계층 호스트에 로그온하는 것을 방지하도록 그룹 정책을 구성합니다.

1. 새 **Restrict Workstation Logon** GPO를 만듭니다. 이 설정은 계층 0 및 계층 1 관리자 계정이 표준 워크스테이션에 로그온하지 못하도록 제한합니다.  이 GPO는 최상위 "Workstations" OU에 연결되고 다음과 같은 설정을 갖습니다.
   * 컴퓨터 구성\정책\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당\일괄 작업으로 로그온 거부에서 **이 정책 설정 정의**를 선택하고, 계층 0 및 계층 1 그룹을 추가합니다.
     ```
     Enterprise Admins
     Domain Admins
     Schema Admins
     BUILTIN\Administrators
     Account Operators
     Backup Operators
     Print Operators
     Server Operators
     Domain Controllers
     Read-Only Domain Controllers
     Group Policy Creators Owners
     Cryptographic Operators
     ```

     > [!NOTE]
     > 기본 제공 계층 0 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Other Delegated Groups

     > [!NOTE]
     > 유효한 계층 0 액세스 권한으로 만든 사용자 지정 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Tier 1 Admins

     > [!NOTE]
     > 이 그룹은 이전의 1단계에서 만들었습니다.

   * 컴퓨터 구성\정책\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당\서비스로 로그온 거부에서 **이 정책 설정 정의**를 선택하고, 계층 0 및 계층 1 그룹을 추가합니다.
     ```
     Enterprise Admins
     Domain Admins
     Schema Admins
     BUILTIN\Administrators
     Account Operators
     Backup Operators
     Print Operators
     Server Operators
     Domain Controllers
     Read-Only Domain Controllers
     Group Policy Creators Owners
     Cryptographic Operators
     ```

     > [!NOTE]
     > 참고: 기본 제공 계층 0 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Other Delegated Groups

     > [!NOTE]
     > 참고: 유효한 계층 0 액세스 권한으로 만든 사용자 지정 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Tier 1 Admins

     > [!NOTE]
     > 참고: 이 그룹은 이전의 1단계에서 만들었습니다.

2. 새 **Restrict Server Logon** GPO를 만듭니다. 이 설정은 계층 0 관리자 계정이 계층 1 서버에 로그온하지 못하도록 제한합니다.  이 GPO는 최상위 "Tier 1 Servers" OU에 연결되고 다음과 같은 설정을 갖습니다.
   * 컴퓨터 구성\정책\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당\일괄 작업으로 로그온 거부에서 **이 정책 설정 정의**를 선택하고, 계층 0 그룹을 추가합니다.
     ```
     Enterprise Admins
     Domain Admins
     Schema Admins
     BUILTIN\Administrators
     Account Operators
     Backup Operators
     Print Operators
     Server Operators
     Domain Controllers
     Read-Only Domain Controllers
     Group Policy Creators Owners
     Cryptographic Operators
     ```

     > [!NOTE]
     > 기본 제공 계층 0 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Other Delegated Groups

     > [!NOTE]
     > 유효한 계층 0 액세스 권한으로 만든 사용자 지정 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

   * 컴퓨터 구성\정책\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당\서비스로 로그온 거부에서 **이 정책 설정 정의**를 선택하고, 계층 0 그룹을 추가합니다.
     ```
     Enterprise Admins
     Domain Admins
     Schema Admins
     BUILTIN\Administrators
     Account Operators
     Backup Operators
     Print Operators
     Server Operators
     Domain Controllers
     Read-Only Domain Controllers
     Group Policy Creators Owners
     Cryptographic Operators
     ```

     > [!NOTE]
     > 기본 제공 계층 0 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Other Delegated Groups

     > [!NOTE]
     > 유효한 계층 0 액세스 권한으로 만든 사용자 지정 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

   * 컴퓨터 구성\정책\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당\로컬 로그온 거부에서 **이 정책 설정 정의**를 선택하고, 계층 0 그룹을 추가합니다.
     ```
     Enterprise Admins
     Domain Admins
     Schema Admins
     BUILTIN\Administrators
     Account Operators
     Backup Operators
     Print Operators
     Server Operators
     Domain Controllers
     Read-Only Domain Controllers
     Group Policy Creators Owners
     Cryptographic Operators
     ```

     > [!NOTE]
     > 참고: 기본 제공 계층 0 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

         Other Delegated Groups

     > [!NOTE]
     > 참고: 유효한 계층 0 액세스 권한으로 만든 사용자 지정 그룹에 대한 자세한 내용은 계층 0 동일성을 참조하세요.

#### <a name="deploy-your-paws"></a>PAW 배포

   > [!NOTE]
   > 운영 체제 빌드 프로세스 중에 PAW의 네트워크 연결이 끊어졌는지 확인합니다.

1. 이전에 얻은 클린 소스 설치 미디어를 사용하여 Windows 10을 설치합니다.

   > [!NOTE]
   > MDT(Microsoft Deployment Toolkit) 또는 다른 자동화된 이미지 배포 시스템을 사용하여 PAW 배포를 자동화할 수 있지만 빌드 프로세스가 PAW처럼 신뢰할 수 있는지 확인해야 합니다. 특히 악의적 사용자는 회사 이미지 및 배포 시스템(ISO, 배포 패키지 등)을 지속성 메커니즘으로 악용하려고 하므로 기존 배포 시스템 또는 이미지를 사용해서는 안 됩니다.
   >
   > PAW 배포를 자동화하는 경우 다음을 수행해야 합니다.
   >
   > * [설치 미디어에 대한 클린 소스](https://aka.ms/cleansource)의 지침에 따라 유효성을 검사한 설치 미디어를 사용하여 시스템을 구축합니다.
   > * 운영 체제 빌드 프로세스 중에 자동화된 배포 시스템의 네트워크 연결이 끊어졌는지 확인합니다.

2. 로컬 관리자 계정의 고유하고 복잡한 암호를 설정합니다.  환경에서 다른 계정에 사용된 암호를 사용하지 마세요.

   > [!NOTE]
   > [LAPS(Local Administrator Password Solution)](https://www.microsoft.com/download/details.aspx?id=46899)를 사용하여 PAW를 비롯한 모든 워크스테이션의 로컬 관리자 암호를 관리하는 것이 좋습니다.  LAPS를 사용하는 경우 PAW Maintenance 그룹에만 PAW의 LAPS 관리되는 암호를 읽을 수 있는 권한을 부여해야 합니다.

3. 클린 소스 설치 미디어를 사용하여 Windows 10용 원격 서버 관리 도구를 설치합니다.
4. Windows Defender Exploit Guard를 구성합니다.

   > [!NOTE]
   > 따라야 할 구성 지침

5. PAW를 네트워크에 연결합니다.  PAW에서 하나 이상의 DC(도메인 컨트롤러)에 연결할 수 있는지 확인합니다.
6. PAW Maintenance 그룹의 구성원 계정을 통해 새로 만든 PAW에서 PowerShell 명령을 실행하여 적절한 OU의 도메인에 가입합니다.

   `Add-Computer -DomainName Fabrikam -OUPath "OU=Devices,OU=Tier 0,OU=Admin,DC=fabrikam,DC=com"`

   필요한 경우 *Fabrikam*에 대한 참조를 사용자의 도메인 이름으로 바꿉니다.  도메인 이름이 여러 수준(예: child.fabrikam.com)으로 확장되는 경우 도메인의 정규화된 도메인 이름에 표시되는 순서대로 "DC=" 식별자를 사용하여 추가 이름을 추가합니다.

   > [!NOTE]
   > [ESAE 관리 포리스트](https://aka.ms/esae)(1단계의 계층 0 관리자용) 또는 [MIM(Microsoft Identity Manager) PAM(Privileged Access Management)](https://aka.ms/mimpamdeploy)(2단계의 계층 1 및 2 관리자용)을 배포한 경우 프로덕션 도메인 대신 이 환경의 도메인의 PAW를 가입합니다.

7. 다른 소프트웨어(관리 도구, 에이전트 등)를 설치하기 전에 모든 중요한 Windows 업데이트를 적용합니다.
8. 그룹 정책 애플리케이션을 강제 적용합니다.
   1. 관리자 권한 명령 프롬프트를 열고, `Gpupdate /force /sync` 명령을 입력합니다.
   2. 컴퓨터를 다시 시작합니다.

9. (선택 사항) Active Directory 관리자에게 필요한 추가 도구를 설치합니다. 작업을 수행하는 데 필요한 다른 도구 또는 스크립트를 설치합니다. PAW에 추가하기 전에 모두 도구에 대해 대상 컴퓨터에서 자격 증명 노출 위험을 평가해야 합니다. 관리 도구 및 연결 방법에 대해 자격 증명 노출 위험을 평가하는 방법에 대한 자세한 내용은 [이 페이지](https://aka.ms/logontypes)를 참조하세요. [설치 미디어에 대한 클린 소스](https://aka.ms/cleansource)의 지침에 따라 모든 설치 미디어를 가져와야 합니다.

   > [!NOTE]
   > 이러한 도구의 중앙 위치에 점프 서버를 사용하면 보안 경계 역할을 하지 않더라도 복잡성을 줄일 수는 있습니다.

10. (선택 사항) 필요한 원격 액세스 소프트웨어를 다운로드하여 설치합니다. 관리자가 관리를 위해 원격으로 PAW를 사용하는 경우 원격 액세스 솔루션 공급업체의 보안 지침에 따라 원격 액세스 소프트웨어를 설치합니다. 설치 미디어에 대한 클린 소스의 지침에 따라 모든 설치 미디어를 가져와야 합니다.

    > [!NOTE]
    > PAW를 통해 원격 액세스를 허용하는 것과 관련된 모든 위험을 신중히 고려해야 합니다.  모바일 PAW는 재택 근무를 포함하여 중요한 많은 시나리오를 지원하지만 원격 액세스 소프트웨어는 잠재적으로 공격에 취약하고 PAW를 손상시키는 데 사용될 수 있습니다.

11. 아래 단계에 따라 모든 설정이 적절히 완료되었는지 검토 및 확인하여 PAW 시스템의 무결성에 대한 유효성을 검사합니다.
    1. PAW 관련 그룹 정책만 PAW에 적용되는지 확인합니다.
       1. 관리자 권한 명령 프롬프트를 열고, `Gpresult /scope computer /r` 명령을 입력합니다.
       2. 결과 목록을 검토하고 위에서 만든 그룹 정책만 표시되는지 확인합니다.
    2. 아래 단계에 따라 PAW의 권한 있는 그룹에 구성원으로 속한 추가 사용자 계정이 없는지 확인합니다.
       1. **로컬 사용자 및 그룹 편집**(lusrmgr.msc)을 열고 **그룹**을 선택하여 로컬 관리자 계정 및 PAW Maintenance 전역 보안 그룹만 로컬 Administrators 그룹의 구성원인지 확인합니다.

          > [!NOTE]
          > PAW Users 그룹이 로컬 Administrator 그룹의 구성원이어서는 안 됩니다.  로컬 관리자 계정 및 PAW Maintenance 전역 보안 그룹만 구성원이어야 합니다(PAW Users가 전역 그룹의 구성원이어서는 안 됨).

       2. 또한 **로컬 사용자 및 그룹 편집**을 사용하여 다음 그룹에 구성원이 없는지 확인합니다. Backup Operators, Cryptographic Operators Hyper-V Administrators, Network Configuration Operators, Power Users, Remote Desktop Users, Replicators

12. (선택 사항) 조직에서 SIEM(보안 정보 및 이벤트 관리) 솔루션을 사용하는 경우, PAW가 [WEF(Windows 이벤트 전달)를 사용하여 이벤트를 시스템에 전달하도록 구성](https://blogs.technet.com/b/jepayne/archive/2015/11/24/monitoring-what-matters-windows-event-forwarding-for-everyone-even-if-you-already-have-a-siem.aspx)되었거나 SIEM이 PAW로부터 이벤트와 정보를 적극적으로 받을 수 있도록 솔루션에 등록되어 있는지 확인합니다.  이 작업의 세부 정보는 SIEM 솔루션에 따라 크게 다릅니다.

    > [!NOTE]
    > SIEM에 PAW의 시스템 또는 로컬 관리 계정으로 실행되는 에이전트가 필요한 경우 SIEM이 도메인 컨트롤러 및 ID 시스템과 동일한 신뢰 수준으로 관리되는지 확인합니다.

13. (선택 사항) PAW에서 로컬 관리자 계정의 암호를 관리하기 위해 LAPS를 배포하도록 선택한 경우 암호가 성공적으로 등록되었는지 확인합니다.

    * LAPS 관리되는 암호에 대한 읽기 권한이 있는 계정을 사용하여 **Active Directory 사용자 및 컴퓨터**(dsa.msc)를 엽니다.  고급 기능이 사용하도록 설정되어 있는지 확인한 다음 적절한 컴퓨터 개체를 마우스 오른쪽 단추로 클릭합니다.  특성 편집기 탭을 선택하고 msSVSadmPwd 값이 올바른 암호로 채워져 있는지 확인합니다.

### <a name="phase-2-extend-paw-to-all-administrators"></a>2단계: 모든 관리자로 PAW 확장

범위: 중요 업무용 애플리케이션 및 종속성에 대한 관리자 권한이 있는 모든 사용자.  여기에는 최소한 애플리케이션 서버, 작업 상태 및 보안 모니터링 솔루션, 가상화 솔루션, 스토리지 시스템 및 네트워크 디바이스의 관리자가 포함되어야 합니다.

> [!NOTE]
> 이 단계의 지침에서는 1단계가 완전히 완료된 것으로 가정합니다.  1단계의 모든 단계를 완료할 때까지 2단계를 시작하지 마세요.

모든 단계가 완료된 것을 확인했으면 아래 단계를 수행하여 2단계를 완료합니다.

#### <a name="recommended-enable-restrictedadmin-mode"></a>(추천) **RestrictedAdmin**모드 사용

기존 서버와 워크스테이션에서 이 기능을 사용하도록 설정한 다음, 이 기능의 사용을 적용합니다. 이 기능을 사용하려면 대상 서버에서 Windows Server 2008 R2 이상을 실행하고, 워크스테이션에서 Windows 7 이상을 실행해야 합니다.

1. 이 [페이지](https://aka.ms/rdpra)에서 제공되는 지침에 따라 서버 및 워크스테이션에 **RestrictedAdmin** 모드를 사용하도록 설정합니다.

   > [!NOTE]
   > 인터넷 연결 서버에 이 기능을 사용하려면 먼저 악의적 사용자가 이전에 도용한 암호 해시로 이러한 서버에 인증할 수 있는 위험을 고려해야 합니다.

2. "RestrictedAdmin Required - Computer" GPO(그룹 정책 개체)를 만듭니다. 이 섹션에서는 대상 시스템에서 자격 증명 도난으로부터 계정을 보호하기 위해 나가는 원격 데스크톱 연결에 /RestrictedAdmin 스위치 사용을 적용하는 GPO를 만듭니다.
   * 컴퓨터 구성\정책\관리 템플릿\시스템\자격 증명 위임\원격 서버에 대한 자격 증명 위임 제한으로 이동하여 **사용**으로 설정합니다.
3. 아래 정책 옵션을 사용하여 **RestrictedAdmin** Required - Computer를 적절한 계층 1 및/또는 계층 2 디바이스에 연결합니다.
   * PAW Configuration - Computer
      * -> 링크 위치: Admin\Tier 0\Devices (기존)
   * PAW Configuration - User
      * -> 링크 위치: Admin\Tier 0\Accounts
   * RestrictedAdmin Required - Computer
      * ->Admin\Tier1\Devices 또는 -> Admin\Tier2\Devices(둘 다 선택 사항)

   > [!NOTE]
   > 계층 0 시스템은 이미 환경의 모든 자산에 대한 모든 권한이 있으므로 이러한 연결이 필요 없습니다.

#### <a name="move-tier-1-objects-to-the-appropriate-ous"></a>계층 1 개체를 적절한 OU로 이동

1. 계층 1 그룹을 Admin\Tier 1\Groups OU로 이동합니다. 다음 관리 권한을 부여하는 모든 그룹을 찾아서 이 OU로 이동합니다.
   * 둘 이상의 서버에 대한 로컬 관리자
      * 클라우드 서비스에 대한 관리 액세스
      * 엔터프라이즈 애플리케이션에 대한 관리 액세스
2. 계층 1 계정을 Admin\Tier 1\Accounts OU로 이동합니다. 이러한 계층 1 그룹의 구성원인 각 계정(중첩 구성원 포함)을 이 OU로 이동합니다.
3. 관련 그룹에 적절한 구성원 추가
   * **Tier 1 Admins** - 이 그룹은 계층 2 호스트에 로그온하는 것이 제한된 계층 1 관리자를 포함합니다. 서버 또는 인터넷 서비스에 대한 관리자 권한이 있는 모든 계층 1 관리 그룹을 추가합니다.

      > [!NOTE]
      > 관리 직원이 여러 계층의 자산을 관리하는 경우 계층별로 별도의 관리 계정을 만들어야 합니다.

4. Credential Guard를 사용하여 자격 증명 도난 및 재사용 위험 완화  Credential Guard는 애플리케이션에서 자격 증명에 액세스하는 것을 제한하여 자격 증명 도난 공격(Pass-the-Hash 포함)을 방지하는 Windows 10의 새로운 기능입니다.  Credential Guard는 최종 사용자에게 완전히 투명하며, 최소한의 설치 시간 및 노력이 소요됩니다.  배포 단계 및 하드웨어 요구 사항을 포함하여 Credential Guard에 대한 자세한 내용은 [Credential Guard를 사용하여 도메인 자격 증명 보호](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) 문서를 참조하세요.

   > [!NOTE]
   > Credential Guard를 구성하고 사용하려면 Device Guard를 사용하도록 설정해야 합니다.  그러나 Credential Guard를 사용하기 위해 다른 Device Guard 보호를 구성할 필요는 없습니다.

5. (선택 사항) Cloud Services에 대한 연결을 사용하도록 설정합니다. 이 단계에서는 적절한 보안 보증을 지원하는 Azure 및 Office 365와 같은 클라우드 서비스를 관리할 수 있도록 합니다. 이 단계는 Microsoft Intune에서 PAW를 관리하는 데에도 필요합니다.

   > [!NOTE]
   > 클라우드 서비스 관리 또는 Intune의 관리에 클라우드 연결이 필요하지 않은 경우 이 단계를 건너뜁니다.

   * 이러한 단계는 인터넷을 통한 통신을 권한 있는 클라우드 서비스(공개 인터넷은 제한 안 함)로만 제한하며 인터넷 콘텐츠를 처리하는 브라우저 및 기타 애플리케이션에 대한 보호를 강화합니다. 이러한 관리용 PAW는 인터넷 통신 및 생산성과 같은 표준 사용자 작업에 사용해서는 안 됩니다.
   * PAW 서비스에 대한 연결을 설정하려면 아래 단계를 따릅니다.

   1. 권한 있는 인터넷 대상만 허용하도록 PAW를 구성합니다.  클라우드 관리를 사용하도록 PAW 배포를 확장하는 경우 공격자가 관리자를 보다 쉽게 도용할 수 있는 공개 인터넷에서의 액세스를 필터링하면서 권한 있는 서비스에 대한 액세스를 허용해야 합니다.

      1. **Cloud Services Admins** 그룹을 만들고, 인터넷에서 클라우드 서비스에 액세스해야 하는 모든 계정을 이 그룹에 추가합니다.
      2. [TechNet 갤러리](https://aka.ms/pawmedia)에서 PAW *proxy.pac* 파일을 다운로드하여 내부 웹 사이트에 게시합니다.

         > [!NOTE]
         > 다운로드 후 *proxy.pac* 파일을 업데이트해야 완전한 최신 상태로 유지됩니다.  
         > 모든 최신 Office 365 및 Azure URL은 Office [지원 센터](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)에 게시됩니다. 이러한 지침에서는 Office 365, Azure 및 기타 클라우드 서비스의 관리를 위해 Internet Explorer(또는 Microsoft Edge)를 사용하는 것으로 가정합니다. 관리에 필요한 모든 타사 브라우저에 대해서도 유사한 제한을 구성하는 것이 좋습니다. PAW의 웹 브라우저는 클라우드 서비스를 관리하는 데에만 사용해야 합니다. 일반적인 웹 검색에 사용해서는 안 됩니다.
         >
         > 다른 IaaS 공급자를 위해 이 목록에 다른 유효한 인터넷 대상을 추가해야 할 수도 있겠지만 생산성, 엔터테인먼트, 뉴스 또는 검색 사이트는 이 목록에 추가하지 마세요.
         >
         > 유효한 프록시 주소에 사용하기 위해 이러한 주소를 수용하도록 PAC 파일을 조정해야 할 수도 있습니다.
         >
         > 또한 심층 방어를 위해 PAW의 액세스를 제한하고 웹 프록시를 사용한 PAW의 액세스를 제한할 수 있습니다. PAC 파일 없이 이것만 사용할 경우 회사 네트워크 연결되어 있는 동안에만 PAW의 액세스가 제한되므로 이는 권장되지 않습니다.

      3. *proxy.pac* 파일을 구성했으면 PAW Configuration - User GPO를 업데이트합니다.
         1. 사용자 구성\기본 설정\Windows 설정\레지스트리로 이동합니다. 마우스 오른쪽 단추로 [레지스트리]를 클릭하고, **새로 만들기** > **레지스트리 항목**을 차례로 선택하고, 다음 설정을 구성합니다.
            1. 작업: 바꾸기
            2. Hive: HKEY_ CURRENT_USER
            3. 키 경로: Software\Microsoft\Windows\CurrentVersion\Internet Settings
            4. 값 이름: AutoConfigUrl

               > [!NOTE]
               > 값 이름 왼쪽에 있는 **기본값** 상자를 선택하지 마세요.

            5. 값 형식: REG_SZ
            6. 값 데이터: http:// 및 파일 이름을 포함하여 *proxy.pac* 파일에 대한 전체 URL을 입력합니다(예: http://proxy.fabrikam.com/proxy.pac ).  URL은 단일 레이블 URL일 수도 있습니다(예: http://proxy/proxy.pac ).

               > [!NOTE]
               > file://server.fabrikan.com/share/proxy.pac 구문을 사용하여 파일 공유에서 PAC 파일을 호스트할 수도 있지만 그러려면 file:// 프로토콜을 허용해야 합니다. 필요한 레지스트리 값을 구성하는 방법에 대한 자세한 내용은 이 [웹 프록시 구성 이해](https://blogs.msdn.com/b/ieinternals/archive/2013/10/11/web-proxy-configuration-and-ie11-changes.aspx) 블로그의 "참고: File:// 기반 프록시 스크립트 사용 중지" 섹션을 참조하세요.

            7. **일반** 탭을 클릭하고 **이 항목을 더 이상 적용하지 않을 때 제거**를 선택합니다.
            8. **일반** 탭에서 **항목 수준 대상**을 선택하고 **대상**을 클릭합니다.
            9. **새 항목**을 클릭하고 **보안 그룹**을 선택합니다.
            10. "..." 단추를 선택하고 **Cloud Services Admins** 그룹을 찾습니다.
            11. **새 항목**을 클릭하고 **보안 그룹**을 선택합니다.
            12. "..." 단추를 선택하고 **PAW Users** 그룹을 찾습니다.
            13. **PAW Users** 항목을 클릭하고 **항목 옵션**을 클릭합니다.
            14. **아님**을 선택합니다.
            15. 대상 창에서 **확인**을 클릭합니다.
            16. **확인**을 클릭하여 **AutoConfigUrl** 그룹 정책 설정을 완료합니다.
   2. Windows 10 보안 기준 및 클라우드 서비스 액세스를 적용합니다. 아래 단계를 사용하여 Windows 및 클라우드 서비스(필요한 경우)에 대한 보안 기준을 올바른 OU에 연결합니다.
      1. Windows 10 보안 기준 ZIP 파일의 압축을 풉니다.
      2. 이러한 GPO를 만들고 [정책 설정을 가져온](https://technet.microsoft.com/library/cc753786.aspx) 다음 아래 표에 따라 [연결](https://technet.microsoft.com/library/cc732979.aspx)합니다. 각 정책을 각 위치에 연결하고 순서가 표에 따르는지 확인합니다(표의 아래쪽에 있는 항목이 나중에 적용되고 우선 순위가 더 높음).

         **정책:**

         |||
         |-|-|
         |CM Windows 10 - Domain Security|해당 없음 - 지금은 연결하지 않음|
         |SCM Windows 10 TH2 - Computer|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 TH2- BitLocker|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 - Credential Guard|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Internet Explorer - Computer|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |PAW Configuration - Computer|Admin\Tier 0\Devices (기존)|
         ||Admin\Tier 1\Devices (새 링크)|
         ||Admin\Tier 2\Devices (새 링크)|
         |RestrictedAdmin Required - Computer|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 - User|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Internet Explorer - User|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |PAW Configuration - User|Admin\Tier 0\Devices (기존)|
         ||Admin\Tier 1\Devices (새 링크)|
         ||Admin\Tier 2\Devices (새 링크)|

         > [!NOTE]
         > "SCM Windows 10 - Domain Security" GPO는 PAW와 독립적으로 도메인에 연결할 수 있지만 전체 도메인에 영향을 줍니다.

6. (선택 사항) Tier 1 Admins에 필요한 추가 도구를 설치합니다. 작업을 수행하는 데 필요한 다른 도구 또는 스크립트를 설치합니다. PAW에 추가하기 전에 모두 도구에 대해 대상 컴퓨터에서 자격 증명 노출 위험을 평가해야 합니다. 관리 도구 및 연결 방법에 대해 자격 증명 노출 위험을 평가하는 방법에 대한 자세한 내용은 [이 페이지](https://aka.ms/logontypes)를 참조하세요. 설치 미디어에 대한 클린 소스의 지침에 따라 모든 설치 미디어를 가져와야 합니다.
7. 관리에 필요한 소프트웨어 및 애플리케이션을 식별하고 안전하게 가져오기.  이는 1단계에서 수행한 작업과 유사하지만 보안을 유지해야 하는 애플리케이션, 서비스 및 시스템 수가 증가했기 때문에 범위가 더 넓습니다.

   > [!NOTE]
   > Windows Defender Exploit Guard에서 제공하는 보호로 옵트인하여 이러한 새 애플리케이션(웹 브라우저 포함)을 보호해야 합니다.

   추가 소프트웨어 및 애플리케이션의 예:

      * Microsoft Azure PowerShell
      * Office 365 PowerShell(Microsoft Online Services 모듈이라고도 함)
      * Microsoft Management Console을 기반으로 하는 애플리케이션 또는 서비스 관리 소프트웨어
      * 독점(비 MMC 기반) 애플리케이션 또는 서비스 관리 소프트웨어

         > [!NOTE]
         > 현재 다양한 클라우드 서비스를 포함하여 많은 애플리케이션이 웹 브라우저를 통해 단독으로 관리됩니다.  따라서 PAW에 설치해야 하는 애플리케이션 수는 감소하지만 브라우저 상호 운용성 문제의 위험이 발생합니다.  특정 서비스를 관리하기 위해 특정 PAW 인스턴스에 타사 웹 브라우저를 배포해야 할 수도 있습니다.  추가 웹 브라우저를 배포하는 경우 모든 클린 소스 원칙을 준수하고 공급업체의 보안 지침에 따라 브라우저의 보안을 유지해야 합니다.

8. (선택 사항) 필요한 관리 에이전트를 다운로드하여 설치합니다.

   > [!NOTE]
   > 추가 관리 에이전트(모니터링, 보안, 구성 관리 등)를 설치할 경우 관리 시스템을 도메인 컨트롤러 및 ID 시스템과 동일한 수준으로 신뢰할 수 있는지 확인해야 합니다. 추가 지침은 PAW 관리 및 업데이트를 참조하세요.

9. PAW에서 제공하는 추가 보안 보호가 필요한 시스템을 식별하기 위해 인프라 평가.  보호해야 하는 시스템을 정확히 알아야 합니다.  리소스 자체에 대해 다음과 같은 중요한 질문을 합니다.

   * 관리해야 하는 대상 시스템은 어디에 있습니까?  단일 물리적 위치에서 수집됩니까, 아니면 잘 정의된 단일 서브넷에 연결되어 있습니까?
   * 몇 개의 시스템이 있습니까?
   * 이러한 시스템이 다른 시스템(가상화, 스토리지 등)에 종속되어 있습니까? 그렇다면 그러한 시스템은 어떻게 관리되고 있습니까?  중요한 시스템이 이러한 종속성에 어떻게 노출되어 있으며, 이러한 종속성과 관련된 추가적인 위험은 무엇입니까?
   * 관리되는 서비스가 얼마나 중요하며, 이러한 서비스가 손상된 경우 예상되는 손실은 어느 정도입니까?

      > [!NOTE]
      > 이 평가에 클라우드 서비스를 포함합니다. 보안되지 않은 클라우드 배포를 대상으로 하는 공격자가 점점 늘어나고 있으므로 업무에 중요한 온-프레미스 애플리케이션처럼 이러한 서비스를 안전하게 관리하는 것이 매우 중요합니다.

        이 평가를 사용하여 추가 보호가 필요한 특정 시스템을 식별한 다음 해당 시스템의 관리자로 PAW 프로그램을 확장합니다.  PAW 기반 관리의 이점을 크게 활용할 수 있는 시스템의 일반적인 예로는 SQL Server(온-프레미스와 SQL Azure 모두), HR 애플리케이션, 재무 소프트웨어 등이 있습니다.

        > [!NOTE]
        > 리소스가 Windows 시스템에서 관리되는 경우 PAW로 관리할 수 있으며, 이는 애플리케이션 자체가 Windows가 아닌 다른 운영 체제 또는 타사 클라우드 플랫폼에서 실행되는 경우에도 마찬가지입니다.  예를 들어 Amazon Web Services 구독 소유자는 PAW만 사용하여 해당 계정을 관리해야 합니다.

10. 조직의 규모에 맞게 PAW를 배포하기 위한 요청 배포 방법 개발.  2단계에서 배포하려고 선택한 PAW 수에 따라 프로세스를 자동화해야 할 수도 있습니다.

    * 관리자가 PAW를 얻는 데 사용할 수 있는 공식적인 요청 및 승인 프로세스를 개발하는 것이 좋습니다.  이 프로세스는 배포 프로세스를 표준화하고, PAW 디바이스에 대한 책임을 보장하며, PAW 배포의 차이를 식별하는 데 도움이 됩니다.
    * 앞서 설명한 바와 같이 이 배포 솔루션은 기존 자동화 방법(이미 손상되었을 수 있음)과 분리되어야 하며, 1단계에 설명된 원칙을 따라야 합니다.

        > [!NOTE]
        > 리소스를 관리하는 모든 시스템은 동일하거나 그보다 높은 신뢰 수준에서 관리되어야 합니다.

11. 추가 PAW 하드웨어 프로필 검토 및 필요한 경우 배포.  1단계 배포에서 선택한 하드웨어 프로필이 일부 관리자에게 적합하지 않을 수 있습니다.  하드웨어 프로필을 검토하고 필요한 경우 관리자의 요구에 맞게 추가 PAW 하드웨어 프로필을 선택합니다.  예를 들어 전용 하드웨어 프로필(별도의 PAW와 일상적으로 사용되는 워크스테이션)은 출장이 잦은 관리자에게 적합할 수 있습니다. 이 경우 해당 관리자에 대해 동시 사용 프로필(PAW와 사용자 VM)을 배포할 수도 있습니다.
12. 확장된 PAW 배포를 수반하는 문화권, 운영, 통신 및 교육 요구 사항 고려.   이러한 관리 모델의 상당한 변화는 자연스럽게 어느 정도의 변경 관리를 필요로 하며, 배포 프로젝트 자체에 기본 제공되어야 합니다.  적어도 다음을 고려해야 합니다.

    * 경영진의 지원을 보장하기 위해 이들에게 변경 내용을 전달할 방법  경영진의 지원 없는 프로젝트는 실패할 가능성이 높거나 자금 조달 및 광범위한 수용 면에서 큰 어려움을 겪을 수 있습니다.
    * 관리자를 위해 새 프로세스를 문서화할 방법  이러한 변경 내용은 문서화하여 기존 관리자(습관을 바꾸고 다른 방식으로 리소스를 관리해야 하는 사람)뿐만 아니라 새 관리자(조직 내부에서 승진하거나 외부에서 고용된 사람)에게도 전달해야 합니다.  위협의 중요성, 관리 보호에 대한 PAW의 역할 및 PAW를 올바르게 사용하는 방법이 문서에 명확하고 자세하게 기록되어야 합니다.

      > [!NOTE]
      > 이는 지원 센터 담당자를 포함하여 이직률이 높은 역할에 특히 중요합니다.

    * 새 프로세스의 준수를 보장할 방법  PAW 모델에는 권한 있는 자격 증명의 노출을 방지하는 여러 기술적 제어가 포함되어 있지만, 이러한 기술적 제어만을 사용하여 가능한 모든 노출을 완벽히 방지할 수는 없습니다.  예를 들어 관리자가 권한 있는 자격 증명으로 사용자 데스크톱에 로그온하지 못하도록 할 수 있지만 로그온을 시도하는 것만으로도 해당 사용자 데스크톱에 설치된 맬웨어에 자격 증명이 노출될 수 있습니다.  따라서 PAW 모델의 이점뿐 아니라 준수하지 않을 경우의 위험도 명시해야 합니다.  이를 감사 및 경고로 보완하여 자격 증명 노출을 신속하게 감지하고 해결할 수 있도록 해야 합니다.

### <a name="phase-3-extend-and-enhance-protection"></a>3단계: 보호 확장 및 향상

범위: 이러한 보호는 1단계에서 구축한 시스템을 향상시켜 다단계 인증과 네트워크 액세스 규칙을 포함한 고급 기능으로 기본 보호를 강화합니다.

> [!NOTE]
> 1단계를 완료한 후 언제든지 이 단계를 수행할 수 있습니다.  2단계의 완료에는 종속되지 않으므로 2단계 이전, 도중 또는 이후에 수행할 수 있습니다.

이 단계를 구성하려면 아래 단계를 따르세요.

1. **권한 있는 계정에서 다단계 인증을 사용하도록 설정합니다**.  다단계 인증은 사용자에게 자격 증명 외에 물리적 토큰을 제공하도록 하여 계정 보안을 강화합니다.  다단계 인증은 인증 정책을 보완할 뿐만 아니라 배포용 인증 정책에 종속되지도 않습니다(마찬가지로 인증 정책에서는 다단계 인증을 요구하지 않음).  다음 형태 중 하나의 다단계 인증을 사용하는 것이 좋습니다.

   * **스마트 카드**: 스마트 카드는 Windows 로그온 프로세스 중에 두 번째 확인을 제공하는 변조 방지된 휴대용 물리적 디바이스입니다.  로그온하려면 개인이 카드를 소지해야 하므로 도난된 자격 증명이 원격으로 재사용되는 위험을 줄일 수 있습니다.  Windows에서의 스마트 카드 로그온에 대한 자세한 내용은 [스마트 카드 개요](https://technet.microsoft.com/library/hh831433.aspx) 문서를 참조하세요.
   * **가상 스마트 카드**:  가상 스마트 카드는 물리적 스마트 카드와 동일한 보안 이점을 제공하며, 특정 하드웨어에 연결되는 추가적인 이점도 있습니다.  배포 및 하드웨어 요구 사항에 대한 자세한 내용은 [가상 스마트 카드 개요](https://technet.microsoft.com/library/dn593708.aspx) 및 [가상 스마트 카드 시작: 연습 가이드](https://technet.microsoft.com/library/dn579260.aspx)를 참조하세요.
   * **비즈니스용 Windows Hello**: 비즈니스용 Windows Hello를 사용하면 사용자가 Microsoft 계정, Active Directory 계정, Microsoft Azure AD(Azure Active Directory) 계정 또는 FIDO(Fast ID Online) 인증을 지원하는 타사 서비스를 인증할 수 있습니다. 비즈니스용 Windows Hello 등록 중에 초기 2단계 인증을 수행하면 비즈니스용 Windows Hello가 사용자의 디바이스에 설정되고, 사용자는 Windows Hello 또는 PIN이 될 수 있는 제스처를 설정합니다. 비즈니스용 Windows Hello 자격 증명은 TPM(신뢰할 수 있는 플랫폼 모듈)의 격리된 환경 내에서 생성될 수 있는 비대칭 키 쌍입니다.
      비즈니스용 Windows Hello에 대한 자세한 내용은 [비즈니스용 Windows Hello](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification) 문서를 참조하세요.
   * **Azure 다단계 인증**:  Azure MFA(다단계 인증)는 두 번째 확인 요소의 보안을 제공할 뿐만 아니라 모니터링 및 기계 학습 기반 분석을 통해 향상된 보호도 제공합니다.  Azure MFA는 Azure 관리자는 물론, 웹 애플리케이션, Azure Active Directory, 온-프레미스 솔루션(예: 원격 액세스 및 원격 데스크톱) 등 다른 많은 솔루션의 보안도 유지할 수 있습니다.  Azure 다단계 인증에 대한 자세한 내용은 [다단계 인증](https://azure.microsoft.com/services/multi-factor-authentication)을 참조하세요.

2. **Windows Defender Application Control 및/또는 AppLocker를 사용하여 신뢰할 수 있는 애플리케이션을 허용 목록에 추가합니다**.  신뢰할 수 없거나 서명되지 않은 코드를 PAW에서 실행할 수 있는 권한을 제한하면 악의적인 활동 및 손상의 가능성을 더욱 줄일 수 있습니다.  Windows에서는 애플리케이션 제어에 대한 두 가지 기본 옵션을 제공합니다.

   * **AppLocker**:  AppLocker를 사용하면 관리자가 지정된 시스템에서 실행될 수 있는 애플리케이션을 제어할 수 있습니다.  AppLocker는 그룹 정책을 통해 중앙에서 제어하고 특정 사용자 또는 그룹(PAW 사용자를 대상으로 하는 애플리케이션의 경우)에 적용할 수 있습니다.  AppLocker에 대한 자세한 내용은 [AppLocker 개요](https://technet.microsoft.com/library/hh831440.aspx) TechNet 문서를 참조하세요.
   * **Windows Defender Application Control**: 새 Windows Defender Application Control 기능은 AppLocker와 달리 영향을 받는 디바이스에서 재정의할 수 없는 향상된 하드웨어 기반 애플리케이션 제어를 제공합니다.  AppLocker와 마찬가지로 Windows Defender Application Control은 그룹 정책을 통해 제어하고 특정 사용자를 대상으로 할 수 있습니다.  Windows Defender Application Control을 사용하여 애플리케이션 사용을 제한하는 방법에 대한 자세한 내용은 [Windows Defender Application Control 배포 가이드](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)를 참조하세요.

3. **보호된 사용자, 인증 정책 및 인증 사일로를 사용하여 권한 있는 계정을 추가로 보호합니다**.  보호된 사용자의 구성원에게는 LSA(로컬 보안 에이전트)에 저장된 자격 증명을 보호하고 자격 증명 도난 및 재사용의 위험을 최소화하는 추가적인 보안 정책이 적용됩니다.  인증 정책 및 사일로는 권한 있는 사용자가 도메인의 리소스에 액세스할 수 있는 방법을 제어합니다.  종합적으로 이러한 보호는 권한 있는 사용자의 계정 보안을 크게 강화합니다.  이러한 기능에 대한 자세한 내용은 [보호된 계정을 구성하는 방법](https://technet.microsoft.com/library/dn518179.aspx) 웹 문서를 참조하세요.

   > [!NOTE]
   > 이러한 보호는 1단계의 기존 보안 조치를 대체하는 것이 아니라 보완합니다.  관리자는 여전히 관리 및 일반적인 용도에 별도의 계정을 사용해야 합니다.

## <a name="managing-and-updating"></a>관리 및 업데이트

PAW에는 맬웨어 방지 기능이 있어야 하며, 이러한 워크스테이션의 무결성을 유지하기 위해 소프트웨어 업데이트를 신속하게 적용해야 합니다.

PAW에서 추가적인 구성 관리, 운영 모니터링 및 보안 관리를 사용할 수도 있지만 각 관리 기능에는 해당 도구를 통한 PAW 손상 위험도 따르므로 이러한 기능을 통합할 때는 신중히 고려해야 합니다. 고급 관리 기능을 도입하는 것이 적절한지 여부는 다음과 같은 몇 가지 요인에 따라 달라집니다.

* 관리 기능의 보안 상태 및 방식(도구, 관리 역할 및 이러한 역할의 계정, 도구가 호스트되거나 관리되는 운영 체제, 기타 해당 도구의 모든 하드웨어 또는 소프트웨어 종속성에 대한 소프트웨어 업데이트 방식 포함)
* PAW에서 소프트웨어 배포 및 업데이트의 주기 및 수량
* 세부적인 인벤토리 및 구성 정보에 대한 요구 사항
* 보안 요구 사항 모니터링
* 조직의 표준 및 기타 조직 관련 요소

클린 소스 원칙에 따라 PAW를 관리하거나 모니터링하는 데 사용되는 모든 도구는 PAW 이상의 수준으로 신뢰할 수 있어야 합니다. 그러려면 일반적으로 PAW에서 이러한 도구를 관리하여 하위 권한 워크스테이션의 보안 종속성이 없도록 해야 합니다.

다음 표에서는 PAW를 관리하고 모니터링하는 데 사용할 수 있는 여러 가지 접근 방식을 설명합니다.

|접근 방식|고려 사항|
|------|---------|
|기본적으로 PAW<p>-   Windows Server Update Services<br />-   Windows Defender|-   추가 비용 없음<br />-   기본적인 필수 보안 기능 수행<br />-   이 지침에 포함된 설명|
|[Intune](https://technet.microsoft.com/library/jj676587.aspx)으로 관리|<ul><li>클라우드 기반 가시성 및 제어 제공<p><ul><li>소프트웨어 배포</li><li>o   소프트웨어 업데이트 관리</li><li>Windows 방화벽 정책 관리</li><li>맬웨어 방지 보호</li><li>원격 지원</li><li>소프트웨어 라이선스 관리.</li></ul></li><li>필요한 서버 인프라 없음</li><li>2단계의 "클라우드 서비스 연결 사용" 단계를 따라야 함</li><li>PAW 컴퓨터가 도메인에 가입되지 않은 경우 보안 기준 다운로드에 제공된 도구를 사용하여 로컬 이미지에 SCM 기준을 적용해야 함</li></ul>|
|PAW 관리를 위한 새 System Center 인스턴스|-   구성, 소프트웨어 배포 및 보안 업데이트에 대한 가시성 및 제어 제공<br />-   PAW 수준으로 보호하고 높은 권한을 가진 직원을 위한 기술을 제공하도록 별도의 서버 인프라 필요|
|기존 관리 도구로 PAW 관리|-   기존 관리 인프라를 PAW의 보안 수준으로 설정하지 않은 경우 PAW가 손상될 위험이 매우 높아집니다. **참고:**     조직에서 이 접근 방식을 사용해야 하는 특별한 이유가 없으면 Microsoft는 일반적으로 이를 추천하지 않습니다. 경험상 이러한 모든 도구(및 해당 보안 종속성)를 PAW의 보안 수준으로 강화하는 데는 일반적으로 매우 많은 비용이 듭니다.<br />-   이러한 도구는 대부분 구성, 소프트웨어 배포 및 보안 업데이트에 대한 가시성 및 제어를 제공함|
|관리 액세스가 필요한 보안 검사 또는 모니터링 도구|에이전트를 설치하는 도구를 포함하거나 로컬 관리 액세스 계정이 필요함<p>-   도구 보안 보증을 PAW 수준까지 강화해야 함<br />-   도구 기능(포트 열기, Java 또는 기타 미들웨어 설치 등)을 지원하기 위해 PAW의 보안 상태를 낮추거나 보안 위험 감수에 대한 의사 결정이 필요함|
|SIEM(보안 정보 및 이벤트 관리)|<ul><li>SIEM에 에이전트가 없는 경우<p><ul><li>**Event Log Readers** 그룹의 계정을 사용하여 관리 액세스 없이 PAW에서 이벤트에 액세스할 수 있음</li><li>SIEM 서버의 인바운드 트래픽을 허용하도록 네트워크 포트를 열어야 함</li></ul></li><li>SIEM에 에이전트가 필요로 하는 경우에는 **관리 액세스가 필요한 보안 검사 또는 모니터링 도구** 행 참조</li></ul>|
|Windows 이벤트 전달|-   PAW에서 외부 수집기 또는 SIEM으로 보안 이벤트를 전달할 에이전트 없는 방법 제공<br />-   관리 액세스 없이 PAW에서 이벤트에 액세스할 수 있음<br />-   SIEM 서버의 인바운드 트래픽을 허용하도록 네트워크 포트를 열지 않아도 됨|

## <a name="operating-paws"></a>PAW 운영

클린 소스 원칙을 기반으로 하는 [운영 표준](https://aka.ms/securitystandards)의 표준에 따라 PAW 솔루션을 운영해야 합니다.

## <a name="deploy-paws-using-a-guarded-fabric"></a>보호된 패브릭을 사용하여 PAW 배포

[보호된 패브릭](https://aka.ms/shieldedvms)을 사용하여 랩톱 또는 점프 서버의 보호된 가상 머신에서 PAW 작업을 실행할 수 있습니다.
이 접근 방식을 채택하려면 추가 인프라 및 운영 단계가 필요하지만, PAW 이미지를 정기적으로 더 쉽게 배포할 수 있으며 여러 계층으로 계층화(또는 분류)된 PAW를 단일 디바이스에서 병렬로 실행하는 가상 머신에 통합할 수 있습니다.
보호된 패브릭 토폴로지 및 보안 약속에 대한 자세한 설명은 [보호된 패브릭 설명서](https://aka.ms/shieldedvms)를 참조하세요.

### <a name="changes-to-the-paw-gpos"></a>PAW GPO에 대한 변경

보호된 VM 기반 PAW를 사용하는 경우 가상 머신의 사용을 지원하도록 위에서 정의한 [추천 GPO 설정](#create-paw-configuration---computer-group-policy-object-gpo)을 수정해야 합니다.

1. 물리적 PAW 호스트에 대한 새 OU를 만듭니다. 물리적 PAW와 가상 PAW는 보안 요구 사항이 다르므로 이에 따라 Active Directory에서 구분해야 합니다.
2. PAW 컴퓨터 GPO는 물리적 PAW OU와 가상 PAW OU 모두에 연결되어야 합니다.
3. 물리적 PAW에 대한 새 GPO를 만들어 PAW 사용자를 Hyper-V Admins 그룹에 추가합니다. 이는 관리자가 관리 VM에 연결하고, 필요에 따라 해당 VM을 설정/해제할 수 있어야 합니다. 물리적 PAW에 로그인하는 사용자에게는 관리자 권한, 인터넷 액세스 권한 또는 네트워크 공유 디바이스나 외부 스토리지 디바이스에서 물리적 PAW로 악성 가상 머신 데이터를 복사하는 기능이 없어야 합니다.
4. 관리 VM에 대한 새 GPO를 만들어 PAW 사용자를 Remote Desktop Users 그룹에 추가합니다. 이렇게 하면 사용자가 더 나은 사용자 환경을 제공하고 스마트 카드를 VM으로 통과시킬 수 있게 하는 Hyper-V 고급 콘솔 세션을 사용할 수 있습니다.

### <a name="set-up-the-host-guardian-service"></a>호스트 보호 서비스 설정

호스트 보호 서비스는 물리적 PAW 디바이스의 ID와 상태를 증명하는 역할을 수행합니다.
HGS에 알려져 있고 신뢰할 수 있는 [코드 무결성 정책](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)을 실행하는 머신만 보호된 VM을 시작할 수 있습니다.
이렇게 하면 신뢰할 수 있는 작업을 실행하여 계층화된 리소스를 관리하는 보호된 VM을 사용자 데스크톱 환경 위협으로부터 보호할 수 있습니다.

HGS는 PAW VM을 실행할 수 있는 디바이스를 결정해야 하므로 계층 0 리소스로 간주됩니다.
다른 계층 0 리소스와 함께 배포하고, 권한이 없는 물리적/논리적 액세스로부터 보호해야 합니다.
HGS는 클러스터된 역할이므로 모든 규모의 배포에 맞게 쉽게 확장할 수 있습니다.
일반적으로 세 개 이상의 노드를 사용하여 1,000개의 디바이스마다 하나의 HGS 서버를 계획합니다.

1. 첫 번째 HGS 서버를 설치하려면 [HGS 설치 - 요새 포리스트](../../security/guarded-fabric-shielded-vm/guarded-fabric-install-hgs-in-a-bastion-forest.md) 문서로 시작하여 HGS를 계층 0 도메인에 조인합니다.

2. 그런 다음, 엔터프라이즈 인증 기관을 사용하여 [HGS에 대한 인증서를 만듭니다](../../security/guarded-fabric-shielded-vm/guarded-fabric-obtain-certs.md).
HGS 암호화 및 서명 인증서를 소유한 사용자는 보호된 VM의 암호를 해독할 수 있으므로, 프라이빗 키를 보호하기 위해 하드웨어 보안 모듈에 액세스할 수 있는 경우 HSM을 사용하여 이러한 인증서를 생성하는 것이 좋습니다.
더 강력한 보안을 위해 4,096비트 이상의 키 크기를 선택합니다.

3. 마지막으로, **TPM 모드**에서 [HGS 서버 초기화](../../security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode-bastion.md) 단계를 수행합니다.
초기화는 PAW에서 사용하는 증명 및 키 보호 웹 서비스를 설정합니다.
이러한 통신을 보호하기 위해 [TLS 인증서를 사용하여 HGS를 구성](../../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https.md)하고, 443 포트만 신뢰할 수 없는 네트워크에서 HGS로 열어야 합니다.

4. 두 번째, 세 번째 및 추가 HGS 노드에 대해 [추가 노드를 추가](../../security/guarded-fabric-shielded-vm/guarded-fabric-configure-additional-hgs-nodes.md)하는 단계를 수행합니다.

5. HGS 서버에서 Windows 서버 2019 이상을 실행하는 경우 선택적 기능을 사용하도록 설정하여 오프라인에서 사용할 수 있도록 PAW에서 보호된 VM의 키를 캐시할 수 있습니다. 키는 시스템의 현재 보안 구성으로 봉인되어 안전하지 않은 다른 머신 또는 동일한 머신에서 캐시된 키를 사용하지 못하도록 방지합니다. 이 해결 방법은 PAW 사용자가 인터넷에 액세스하지 않고 이동하지만 여전히 PAW VM에 로그인할 수 있어야 하는 경우에 유용할 수 있습니다. 이 기능을 사용하려면 HGS 서버에서 다음 명령을 실행합니다.

      ```powershell
      Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
      ```

### <a name="set-up-the-physical-paw-device"></a>물리적 PAW 디바이스 설정

물리적 PAW 디바이스는 보호된 패브릭 솔루션에서 기본적으로 신뢰할 수 없는 것으로 간주됩니다.
증명 프로세스 중에 신뢰할 수 있음을 증명할 수 있으며, 그 후에는 보호된 관리 VM을 시작하는 데 필요한 키를 가져올 수 있습니다.
디바이스는 Hyper-V를 실행할 수 있어야 하며, 보안 부팅 및 TPM 2.0을 사용하도록 설정하여 [보호된 호스트 필수 구성 요소](../../security/guarded-fabric-shielded-vm/guarded-fabric-guarded-host-prerequisites.md)를 충족해야 합니다.
모든 PAW 기능을 지원하는 최소 운영 체제 버전은 **Windows 10 버전 1803**입니다.

물리적 PAW는 다른 PAW와 마찬가지로 설정해야 합니다. 단, 관리 VM을 켜고 연결할 수 있으려면 모든 PAW 사용자가 Hyper-V Administrators여야 합니다.
깨끗한 환경에서는 관리 VM의 보호된 호스트로 배포하는 각각의 고유한 하드웨어/소프트웨어 조합에 대해 골든 구성을 만들어야 합니다.
각 골든 구성에서 다음 작업을 완료합니다.

1. Windows, 드라이버 및 펌웨어에 대한 최신 업데이트 및 타사 관리 또는 모니터링 에이전트를 머신에 설치합니다.
2. 고유한 TPM 식별자(인증 키), 부팅 측정(TCG 로그) 및 머신에 대한 코드 무결성 정책을 포함하여 [필요한 기준 정보를 캡처](../../security/guarded-fabric-shielded-vm/guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)합니다.
3. 이러한 아티팩트를 HGS 서버에 복사하고, 이전 문서의 HGS 증명 명령을 실행하여 호스트를 등록합니다. 모든 호스트가 동일한 코드 무결성 정책을 사용하거나 동일한 하드웨어 구성을 사용하는 경우 코드 무결성 정책/TCG 로그를 한 번만 등록해야 합니다.

### <a name="create-the-signed-template-disk"></a>서명된 템플릿 디스크 만들기

보호된 VM은 서명된 템플릿 디스크를 사용하여 만들어집니다.
배포 시 서명을 확인하여 관리자 암호와 같은 비밀을 VM에 공개하기 전에 디스크 무결성 및 신뢰성을 확인합니다.

서명된 템플릿 디스크를 만들려면 일반적인 2세대 가상 머신에서 배포 프로세스의 1단계를 수행합니다.
이 머신은 관리 VM의 골든 이미지가 됩니다.
여러 컨텍스트에서 특수한 도구를 사용할 수 있도록 둘 이상의 템플릿 디스크를 만들 수 있습니다.

VM이 원하는 대로 구성되면 `C:\Windows\System32\sysprep\sysprep.exe`를 실행하고, 디스크를 **일반화**하도록 선택합니다. 일반화가 완료되면 OS를 **종료**합니다.

마지막으로, VM의 VHDX 파일에서 [템플릿 디스크 마법사](../../security/guarded-fabric-shielded-vm/guarded-fabric-create-a-shielded-vm-template.md)를 실행하여 BitLocker 구성 요소를 설치하고 디스크 서명을 생성합니다.

#### <a name="create-the-shielding-data-file"></a>보호 데이터 파일 만들기

일반화된 템플릿 디스크는 보호된 VM을 프로비저닝하는 데 필요한 비밀을 포함하는 보호 데이터 파일과 쌍을 이룹니다.
보호 데이터 파일에 포함되는 항목은 다음과 같습니다.
   - VM을 실행할 수 있는 패브릭을 정의하는 보호자의 목록. 각 HGS 클러스터는 PAW 디바이스를 보호하는 보호자입니다.
   - 배포용으로 신뢰할 수 있는 디스크 서명의 목록. 보호 데이터 파일은 인증된 원본 미디어를 사용하여 만든 VM에만 해당 비밀을 공개합니다.
   - 호스트로부터 VM을 보호하기 위해 추가 보호를 설정해야 하는지와 VM을 다른 머신으로 이동할 수 있는지를 결정하는 보안 정책. PAW 관리 VM은 항상 완전히 보호되어야 합니다.
   - unattend.xml 특수화 파일 - 이를 통해 Windows에서 자동으로 설치를 완료하고 로컬 관리자의 암호와 같은 비밀을 포함할 수 있습니다.
   - 추가 파일(예: RDP 또는 VPN 인증서)

보호 데이터 파일을 만드는 방법에 대한 단계는 [보호 데이터 파일 문서](../../security/guarded-fabric-shielded-vm/guarded-fabric-tenant-creates-shielding-data.md)를 참조하세요.

보호된 VM의 소유자 키는 매우 중요하므로 HSM에 유지하거나 안전한 위치에 오프라인으로 저장해야 합니다.
이러한 키는 응급 비상 시나리오에서 HGS 없이 보호된 VM을 부팅하는 데 사용할 수 있습니다.

PAW 관리 VM의 보호 데이터에는 VM을 잠그는 설정이 VM이 부팅되는 첫 번째 물리적 호스트에 포함되어 있는 것이 좋습니다.
이렇게 하면 다른 사용자가 동일한 환경에서 관리 VM을 한 PAW에서 다른 PAW로 이동시킬 수 없습니다.
이 기능을 사용하려면 PowerShell을 사용하여 보호 데이터 파일을 만들고, **BindToHostTpm** 매개 변수를 포함합니다.

```powershell
New-ShieldingDataFile -Policy Shielded -BindToHostTpm [...]
```

#### <a name="deploy-an-admin-vm"></a>관리 VM 배포

템플릿 디스크와 보호 데이터 파일이 준비되면 관리 VM을 HGS에 등록된 모든 PAW에 배포할 수 있습니다.

1. 템플릿 디스크(.vhdx) 및 보호 데이터 파일(.pdk)을 신뢰할 수 있는 PAW 디바이스에 복사합니다.
2. 지침에 따라 [PowerShell을 사용하여 새 보호된 VM을 배포](../../security/guarded-fabric-shielded-vm/guarded-fabric-create-a-shielded-vm-using-powershell.md)합니다.
3. 배포 프로세스의 1단계에서 나머지 단계를 완료하여 VM 운영 체제를 보호하고 원하는 역할에 맞게 구성합니다.


## <a name="related-topics"></a>관련 항목

[Microsoft Cybersecurity Services 참여](https://www.microsoft.com/microsoftservices/campaigns/cybersecurity-protection.aspx)

[Taste of Premier: Pass-the-Hash 및 기타 형태의 자격 증명 탈취를 완화하는 방법](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced Threat Analytics](https://aka.ms/ata)

[Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx)

[Device Guard 개요](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx)

[보안 관리 워크스테이션을 사용하여 고부가가치 자산 보호](https://msdn.microsoft.com/library/mt186538.aspx)

[Windows 10의 격리된 사용자 모드 - Dave Probert(채널 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[Windows 10의 격리된 사용자 모드 프로세스 및 기능 - Logan Gabriel(채널 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[Windows 10 격리된 사용자 모드의 프로세스와 기능에 대한 자세한 내용 - Dave Probert(채널 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Windows 10 격리된 사용자 모드를 사용하여 자격 증명 탈취 완화(채널 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Windows Kerberos에서 엄격한 KDC 유효성 검사 사용](https://www.microsoft.com/download/details.aspx?id=6382)

[Windows Server 2012용 Kerberos 인증의 새로운 기능](https://technet.microsoft.com/library/hh831747.aspx)

[Windows Server 2008 R2의 AD DS에 대한 인증 메커니즘 보증 단계별 가이드](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[신뢰할 수 있는 플랫폼 모듈](C:/sd/docs/p_ent_keep_secure/p_ent_keep_secure/trusted_platform_module_technology_overview.xml)
