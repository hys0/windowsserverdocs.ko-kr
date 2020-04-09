---
ms.assetid: 9ee8a6cb-7550-46e2-9c11-78d0545c3a97
title: 동적 액세스 제어 개요
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2374e2c8a1efb204dbae1ee633bc5ee41d049d57
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861176"
---
# <a name="dynamic-access-control-overview"></a>동적 액세스 제어 개요

>적용 대상: Windows Server 2012 R2, Windows Server 2012

IT 전문가를 위한 이 개요 항목에서는 Windows Server 2012 및 Windows 8에 도입된 동적 액세스 제어 및 해당 관련 요소에 대해 설명합니다.  
  
도메인 기반 동적 Access Control을 통해 관리자는 리소스 민감도, 사용자 작업이나 역할, 이러한 리소스에 액세스하는 데 사용되는 디바이스 구성 등을 포함할 수 있는 올바르게 정의된 규칙을 바탕으로 Access Control 권한 및 제한을 적용할 수 있습니다.  
  
예를 들어 사용자가 사무실 컴퓨터에서 리소스에 액세스하는 경우와 가상 사설망을 통해 휴대용 컴퓨터를 사용하는 경우의 사용 권한이 다를 수 있습니다. 또는 디바이스에서 네트워크 관리자가 정의한 보안 요구 사항을 충족하는 경우에만 액세스가 허용될 수 있습니다. 동적 Access Control를 사용 하는 경우 사용자의 작업이 나 역할이 변경 되 면 (AD DS에서 사용자 계정 특성이 변경 되는 경우) 추가 관리자 개입 없이 사용자의 사용 권한이 동적으로 변경 됩니다.  
  
동적 Access Control은 Windows Server 2012 및 Windows 8 이전의 Windows 운영 체제에서 지원되지 않습니다. 지원되거나 지원되지 않는 Windows 버전의 환경에서 동적 Access Control이 구성된 경우 지원되는 버전만 변경 내용을 구현합니다.  
  
동적 Access Control과 연관된 기능 및 개념은 다음과 같습니다.  
  
-   [중앙 액세스 규칙](#BKMK_Rules)  
  
-   [중앙 액세스 정책](#BKMK_Policies)  
  
-   [요청이](#BKMK_Claims)  
  
-   [산술식](#BKMK_Expressions2)  
  
-   [제안 된 사용 권한](#BKMK_Permissions2)  
  
### <a name="central-access-rules"></a><a name="BKMK_Rules"></a>중앙 액세스 규칙  
중앙 액세스 규칙은 사용자 그룹, 사용자 클레임, 디바이스 클레임 및 리소스 속성과 관련된 하나 이상의 조건을 포함할 수 있는 권한 부여 규칙 식입니다. 여러 중앙 액세스 규칙을 중앙 액세스 정책으로 결합할 수 있습니다.  
  
도메인에 대해 하나 이상의 중앙 액세스 규칙이 정의된 경우 파일 공유 관리자는 특정 규칙을 특정 리소스 및 비즈니스 요구 사항에 맞출 수 있습니다.  
  
### <a name="central-access-policies"></a><a name="BKMK_Policies"></a>중앙 액세스 정책  
중앙 액세스 정책은 조건식을 포함하는 권한 부여 정책입니다. 예를 들어 PII (개인 식별이 가능한 정보)에 대 한 액세스를 파일 소유자 및 PII (인적 자원) 부서의 구성원 에게만 허용 하는 비즈니스 요구 사항이 조직에 있다고 가정해 보겠습니다. 이는 조직 전체의 파일 서버에 있는 PII 파일에 적용되는 조직 전체의 정책을 나타냅니다. 이 정책을 구현하려면 조직에서 다음을 수행할 수 있어야 합니다.  
  
-   PII가 포함된 파일 식별 및 표시  
  
-   PII 정보를 볼 수 있도록 허용된 HR 구성원 그룹 식별  
  
-   중앙 액세스 규칙에 중앙 액세스 정책을 추가하고 조직의 파일 서버 모든 위치에서 PII를 포함하는 모든 파일에 중앙 액세스 규칙 적용  
  
중앙 액세스 정책은 조직에서 서버 전체에 적용하는 보안 방어막과 같은 역할을 합니다. 이러한 정책은 파일 및 폴더에 적용된 로컬 액세스 정책 및 DACL(임의 액세스 제어 목록)에 추가됩니다(로컬 액세스 정책 및 DACL을 대체하는 것이 아님).  
  
### <a name="claims"></a><a name="BKMK_Claims"></a>요청이  
클레임은 도메인 컨트롤러에서 게시한 사용자, 디바이스 또는 리소스에 대한 일련의 고유한 정보입니다. 사용자의 제목, 파일의 부서 분류 또는 컴퓨터의 상태는 클레임의 유효한 예입니다. 엔터티는 둘 이상의 클레임을 포함할 수 있으며, 클레임 결합을 통해 리소스에 대한 액세스 권한을 부여할 수 있습니다. 다음 클레임 유형은 지원되는 Windows 버전에서 사용할 수 있습니다.  
  
-   **사용자 클레임** 특정 사용자와 연관된 Active Directory 특성입니다.  
  
-   **장치 클레임** 특정 컴퓨터 개체와 연관된 Active Directory 특성입니다.  
  
-   **리소스 특성** 권한 부여 결정에 사용하도록 표시되고 Active Directory에 게시된 전역 리소스 속성입니다.  
  
클레임을 통해 관리자는 식, 규칙 및 정책에 통합할 수 있는, 사용자, 디바이스 및 리소스에 대한 조직 또는 기업 차원의 정확한 문을 작성할 수 있습니다.  
  
### <a name="expressions"></a><a name="BKMK_Expressions2"></a>산술식  
조건식은 특정 조건이 충족하는 경우에만(예: 디바이스의 보안 상태, 위치, 그룹 구성원 등) 리소스에 대한 액세스 권한을 허용하거나 거부하는 향상된 액세스 제어 관리 기능입니다. 식은 ADAC(Active Directory Administrative Center)의 중앙 액세스 규칙 편집기나 ACL 편집기의 고급 보안 설정 대화 상자를 통해 관리됩니다.  
  
식을 통해 관리자는 나날이 복잡해지는 비즈니스 환경에서 유연한 조건으로 민감한 리소스에 대한 액세스를 관리할 수 있습니다.  
  
### <a name="proposed-permissions"></a><a name="BKMK_Permissions2"></a>제안 된 사용 권한  
제안된 사용 권한을 통해 관리자는 실제로 액세스 제어 설정을 변경하지 않고도 액세스 제어 설정에 대한 잠재적인 변경 영향을 보다 정확하게 모델링할 수 있습니다.  
  
리소스에 대해 유효한 액세스를 예측함으로써 변경 사항을 구현하기 전에 해당 리소스의 사용 권한을 계획하고 구성할 수 있습니다.  
  
## <a name="additional-changes"></a>추가 변경 사항  
동적 Access Control을 지원하는 Windows 버전의 추가 개선 사항은 다음과 같습니다.  
  
### <a name="support-in-the-kerberos-authentication-protocol-to-reliably-provide-user-claims-device-claims-and-device-groups"></a>안정적으로 사용자 클레임, 디바이스 클레임 및 디바이스 그룹을 제공하도록 Kerberos 인증 프로토콜 지원  
기본적으로 지원되는 Windows 버전을 실행하는 디바이스는 동적 Access Control 관련 Kerberos 티켓을 처리할 수 있으며, 이 티켓에는 복합 인증에 필요한 데이터가 포함됩니다. 도메인 컨트롤러는 복합 인증 관련 정보가 포함된 Kerberos 티켓을 발급하고 이 티켓에 응답할 수 있습니다. 동적 Access Control을 인식하도록 도메인이 구성된 경우 디바이스는 초기 인증 동안 도메인 컨트롤러에서 클레임을 수신하며, 서비스 티켓 요청 제출 시 복합 인증 티켓을 수신합니다. 복합 인증으로 동적 Access Control을 인식하는 리소스에 대한 사용자 및 디바이스 ID를 포함하는 액세스 토큰이 발급됩니다.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>KDC(키 배포 센터) 그룹 정책 설정을 사용하여 도메인에 대해 동적 Access Control을 사용할 수 있도록 지원  
모든 도메인 컨트롤러에는 동일한 관리 템플릿 정책 설정이 있어야 하며, 이 설정은 **컴퓨터 구성\정책\관리 템플릿\시스템\KDC\동적 Access Control 및 Kerberos 아머링 지원**에 있습니다.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>KDC(키 배포 센터) 그룹 정책 설정을 사용하여 도메인에 대해 동적 Access Control을 사용할 수 있도록 지원  
모든 도메인 컨트롤러에는 동일한 관리 템플릿 정책 설정이 있어야 하며, 이 설정은 **컴퓨터 구성\정책\관리 템플릿\시스템\KDC\동적 Access Control 및 Kerberos 아머링 지원**에 있습니다.  
  
### <a name="support-in-active-directory-to-store-user-and-device-claims-resource-properties-and-central-access-policy-objects"></a>Active Directory에 사용자 및 디바이스 클레임, 리소스 속성 및 중앙 액세스 정책 개체를 저장하도록 지원  
  
### <a name="support-for-using-group-policy-to-deploy-central-access-policy-objects"></a>그룹 정책을 사용하여 중앙 액세스 정책 개체를 배포하도록 지원  
그룹 정책 설정, **컴퓨터 구성\정책\Windows 설정\보안 설정\파일 시스템\중앙 액세스 정책**을 통해 조직의 파일 서버에 중앙 액세스 정책 개체를 배포할 수 있습니다.  
  
### <a name="support-for-claims-based-file-authorization-and-auditing-for-file-systems-by-using-group-policy-and-global-object-access-auditing"></a>그룹 정책 및 전역 개체 액세스 감사를 사용하여 파일 시스템에 대한 클레임 기반 파일 권한 부여 및 감사 지원  
제안된 사용 권한을 사용하여 중앙 액세스 정책에 대한 유효한 액세스를 감사하려면 준비된 중앙 액세스 정책 감사를 사용하도록 설정해야 합니다. 컴퓨터에 대한 이 설정은 GPO(그룹 정책 개체)의 **보안 설정**에 있는 **고급 감사 정책 구성** 아래에서 구성할 수 있습니다. GPO의 보안 설정을 구성한 후 네트워크의 컴퓨터에 GPO를 배포할 수 있습니다.  
  
### <a name="support-for-transforming-or-filtering-claim-policy-objects-that-traverse-active-directory-forest-trusts"></a>Active Directory 포리스트 트러스트를 트래버스하는 클레임 정책 개체의 변환 또는 필터링에 대한 지원  
포리스트 트러스트를 트래버스하는, 들어오고 나가는 클레임을 필터링하거나 변환할 수 있습니다. 클레임 필터링 및 변환과 관련하여 다음과 같은 세 개의 기본 시나리오가 있습니다.  
  
-   **값 기반 필터링** 클레임 값을 바탕으로 필터링을 수행할 수 있습니다. 이를 통해 트러스트된 포리스트에서 특정 값을 포함한 클레임이 트러스팅 포리스트에 전송되지 않도록 할 수 있습니다. 트러스팅 포리스트의 도메인 컨트롤러는 값 기반 필터링을 사용하여 트러스트된 포리스트에서 특정 값이 있는 들어오는 클레임을 필터링함으로써 권한 상승 공격을 방지할 수 있습니다.  
  
-   **클레임 유형 기반 필터링** 클레임 값이 아닌 클레임 유형을 바탕으로 필터링을 수행합니다. 클레임 이름으로 클레임 유형을 식별합니다. 트러스트된 포리스트에서 클레임 유형 기반 필터링을 사용하면 Windows가 트러스팅 포리스트에 정보를 공개하는 클레임을 보내지 않습니다.  
  
-   **클레임 유형 기반 변환** 클레임을 의도한 대상에 보내기 전에 조작합니다. 트러스트 포리스트에서 클레임 유형 기반 변환을 사용하여 특정 정보를 포함하는 알려진 클레임을 일반화할 수 있습니다. 변환을 통해 클레임 유형이나 클레임 값 또는 둘 다를 일반화할 수 있습니다.  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
동적 Access Control에 대한 클레임 및 복합 인증에는 Kerberos 인증 확장 프로그램이 필요하므로 동적 Access Control을 지원하는 모든 도메인에는 동적 Access Control 인식 Kerberos 클라이언트의 인증을 지원하도록, 지원되는 Windows 버전을 실행하는 도메인 컨트롤러가 충분히 있어야 합니다. 기본적으로 디바이스는 다른 사이트의 도메인 컨트롤러를 사용해야 합니다. 이러한 도메인 컨트롤러를 사용할 수 없는 경우 인증에 실패하게 됩니다. 따라서 다음 조건 중 하나를 지원해야 합니다.  
  
-   지원되는 Windows 또는 Windows Server 버전을 실행하는 모든 디바이스로부터의 인증을 지원하려면, 동적 Access Control을 지원하는 모든 도메인에 지원되는 Windows Server 버전을 실행하는 도메인 컨트롤러가 충분히 있어야 합니다.  
  
-   클레임이나 복합 ID를 사용하여 리소스를 보호하지 않는, 지원되는 Windows 버전을 실행하는 장치에서는 동적 Access Control에 대해 Kerberos 프로토콜 지원을 사용하지 않도록 설정해야 합니다.  
  
사용자 클레임을 지원하는 도메인의 경우 클레임과 복합 인증을 지원하고 Kerberos 아머링을 제공하려면, 지원되는 Windows Server 버전을 실행하는 모든 도메인 컨트롤러를 적절한 설정으로 구성해야 합니다. 다음과 같이 KDC 관리 템플릿 정책의 설정을 구성합니다.  
  
-   **항상 클레임 제공** 지원되는 Windows Server 버전을 모든 도메인 컨트롤러에서 실행하는 경우 이 설정을 사용합니다. 또한 도메인 기능 수준을 Windows Server 2012 이상으로 설정합니다.  
  
-   **지원됨** 이 설정을 사용할 경우 동적 Access Control에서 보호되는 리소스에 액세스하는 데 필요한 클라이언트 컴퓨터 수만큼, 지원되는 Windows Server 버전을 실행하는 도메인 컨트롤러 수가 확보되도록 도메인 컨트롤러를 모니터링합니다.  
  
사용자 도메인과 파일 서버 도메인이 서로 다른 포리스트에 있는 경우 파일 서버 포리스트 루트의 모든 도메인 컨트롤러는 Windows Server 2012 이상 기능 수준에서 설정 해야 합니다.  
  
클라이언트에서 동적 Access Control을 인식하지 못하는 경우 두 포리스트 간 양방향 트러스트 관계가 설정되어야 합니다.  
  
포리스트를 벗어날 때 클레임이 변환 되 면 사용자 포리스트 루트의 모든 도메인 컨트롤러가 Windows Server 2012 이상 기능 수준에서 설정 되어야 합니다.  
  
Windows Server 2012 또는 Windows Server 2012 R2를 실행하는 파일 서버에는 클레임을 포함하지 않는 사용자 토큰에 대해 사용자 클레임을 가져와야 하는지 여부를 지정하는 그룹 정책 설정이 포함됩니다. 이 설정은 기본적으로 **자동**으로 설정됩니다. 따라서 해당 파일 서버에 대해 사용자 또는 장치 클레임을 포함하는 중앙 정책이 있는 경우 이 그룹 정책 설정이 **켜짐**으로 설정됩니다. 파일 서버에 사용자 클레임을 포함하는 임의의 ACL이 포함된 경우, 서버를 액세스할 때 클레임을 제공하지 않는 사용자 대신 서버에서 클레임을 요청해야 한다는 것을 알 수 있도록 이 그룹 정책을 **켜짐**으로 설정해야 합니다.  
  
## <a name="additional-resource"></a>추가 리소스  
이 기술을 기반으로 솔루션을 구현 하는 방법에 대 한 자세한 내용은 [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)를 참조 하세요.  
  


