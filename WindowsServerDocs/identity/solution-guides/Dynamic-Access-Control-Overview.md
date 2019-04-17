---
ms.assetid: 9ee8a6cb-7550-46e2-9c11-78d0545c3a97
title: "동적 액세스 제어 개요"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5cf74042c9b511abb1fbeb88224dea0c7f2c8706
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="dynamic-access-control-overview"></a>동적 액세스 제어 개요

>적용 대상: Windows Server 2012 R2, Windows Server 2012

IT 전문가 위한이 개요 항목 동적 액세스 제어를 설명 하 고 요소를 Windows 8 및 Windows Server 2012에서 도입 된에 연결 합니다.  
  
동적 액세스 제어 도메인 기반 관리자를 액세스 권한 및 리소스는 작업이 또는 이러한 리소스에 액세스 하는 데 사용 하는 디바이스의 구성과 역할은 사용자의의 민감도 포함할 수 있는 윤곽이 규칙에 따라 제한을 적용할 수 있습니다.  
  
예를 들어, 사용자 가상 개인 네트워크를 통해 노트북을 사용 하 고 있을 때와 office 컴퓨터에서 리소스에 액세스할 때 다른 권한이 있을 수 있습니다. 또는 디바이스 한 경우에만 네트워크 관리자가 정의 보안 요구 사항을 충족 액세스를 허용 수 있습니다. 동적 액세스 제어를 사용 하면 사용자의 권한을 동적으로 변경 관리자 추가 작업 없이 (사용자의 계정 특성 AD DS 변경 되) 사용자의 작업 이나 역할 변경 합니다.  
  
동적 액세스 제어 Windows 8 및 Windows Server 2012 하기 전에 Windows 운영 체제의 지원 되지 않습니다. 동적 액세스 제어 및 지원 되는 지원 되지 않는 버전의 Windows 환경에서 구성한 경우 지원 되는 버전 변경 내용을 적용 됩니다.  
  
기능과 관련 된 동적 액세스 제어 개념 다음과 같습니다.  
  
-   [중앙 액세스 규칙](#BKMK_Rules)  
  
-   [중앙 액세스 정책](#BKMK_Policies)  
  
-   [클레임](#BKMK_Claims)  
  
-   [표현](#BKMK_Expressions2)  
  
-   [제안 된 권한](#BKMK_Permissions2)  
  
### <a name="BKMK_Rules"></a>중앙 액세스 규칙  
중앙 액세스 규칙의 사용자 그룹, 사용자 청구, 장치 청구 및 리소스 속성 하나 이상의 상황을 포함할 수 있는 승인 규칙 식입니다. 여러 중앙 액세스 규칙 중앙 액세스 정책으로 결합할 수 있습니다.  
  
하나 이상의 중앙 액세스 규칙 도메인에 정의 된, 파일 공유 관리자 특정 리소스와 이래 특정 규칙 일치 수 있습니다.  
  
### <a name="BKMK_Policies"></a>중앙 액세스 정책  
중앙 액세스 정책은 승인 하는 정책이 조건부 식을 포함 합니다. 예를 들어, 파일 소유자와 pii 개인 정보를 볼 수 있는 인사 (인사) 부서의 회원 파일에서에 액세스 (PII) 개인 식별 정보를 제한 하는 비즈니스 요구 사항이 조직 말 봅시다. 조직에서 파일 서버에 있는 어디에서 든 PII 파일에 적용 되는 조직 전체 정책을 나타냅니다. 이 정책을 구현 조직을 할 수 있어야 합니다.  
  
-   사용자의 신원을 확인 하 고 있는 PII 포함 된 파일을 표시 합니다.  
  
-   그룹 pii 개인 정보를 볼 수 있는 시간 구성원을 확인 합니다.  
  
-   중앙 액세스 정책 중앙 액세스 규칙에 추가 하 고는 조직에서 간에 파일 서버 있는 어디에서 든 PII을 포함 하는 모든 파일에 액세스 중앙 규칙을 적용할 합니다.  
  
중앙 액세스 정책을 서버에서 조직 적용 되는 보안 umbrellas로 작동 합니다. 이러한 정책을 이외에 되지만 대체 하지는 않습니다 로컬 액세스 정책 또는 파일 및 폴더에 적용 되는 임의 액세스 제어 목록 (Dacl).  
  
### <a name="BKMK_Claims"></a>클레임  
클레임은 고유한 부분의 사용자, 디바이스 또는 도메인 컨트롤러에 의해 게시 된 리소스에 대 한 정보입니다. 사용자의 제목, 파일 또는 컴퓨터의 상태의 부서 분류는 클레임 유효한 예입니다. 엔터티 개 이상의 클레임 포함 될 수 있습니다 및 클레임 조합 리소스에 대 한 액세스 권한을 부여 데 사용할 수 있습니다. 다음과 같은 유형의 클레임 지원 되는 버전의 Windows에서 사용할 수 있습니다.  
  
-   **사용자 클레임** 특정 사용자와 관련 된 Active Directory 특성 합니다.  
  
-   **장치 클레임** 특정 컴퓨터 개체와 관련 된 Active Directory 특성 합니다.  
  
-   **리소스 특성** 인증 결정에 사용 된 것으로 표시 되어 있고 Active Directory에 게시 되는 전 세계 리소스 속성 합니다.  
  
클레임 식, 규칙 및 정책에 사용자가, 디바이스 및 포함 될 수 있는 리소스에 대 한 정확한 조직 또는 엔터프라이즈 전체 취급 하는 관리자 수 있게 합니다.  
  
### <a name="BKMK_Expressions2"></a>표현  
조건부 식 허용 하거나, 그룹 구성원, 위치, 나 디바이스의 보안 상태 같은 특정 조건에 하는 경우에 리소스에 액세스 거부 있는 액세스 제어 관리를 향상 됩니다. 중앙 액세스 규칙 편집기의의 Active Directory 관리 센터 (ADAC) 또는 ACL 편집기의 고급 보안 설정 대화 상자를 통해 식 관리 합니다.  
  
식 관리자 점점 더 복잡 업무 환경에 유연한 조건으로 중요 한 리소스에 대 한 액세스를 관리 하는 데 도움이 됩니다.  
  
### <a name="BKMK_Permissions2"></a>제안 된 권한  
제안 된 권한 관리자가 설정에 액세스 하려면 제어 실제로 변경 없이 변경 될의 영향을 더 정확 하 게 모델을 사용 하도록 설정 합니다.  
  
리소스에 유효한 액세스 하는 데 도움이 예측 계획 하 고 변경 내용을 구현 하기 전에 리소스에 대 한 권한 구성 합니다.  
  
## <a name="additional-changes"></a>추가 변경 사항과  
지원 되는 버전의 Windows 지원 동적 액세스 제어 하는 향상 된 기능 추가 다음과 같습니다.  
  
### <a name="support-in-the-kerberos-authentication-protocol-to-reliably-provide-user-claims-device-claims-and-device-groups"></a>사용자 청구, 장치 청구 및 디바이스 그룹 안정적으로 제공 하기 위해 Kerberos 인증 프로토콜을 지원 합니다.  
기본적으로 지원 되는 버전의 Windows 중 하나를 실행 하는 디바이스 복합 인증을 위해 필요한 데이터를 포함 하는 Kerberos 동적 액세스 제어 관련 티켓을 처리할 수 있습니다. 도메인 컨트롤러 발급 및 인증 관련 정보 복합 티켓 Kerberos에 응답할 수 있습니다. 도메인을 동적 액세스 제어 인식 하도록 구성 장치 클레임 도메인 컨트롤러에서 초기 인증 하는 동안 나타나고 서비스 티켓 제출할 때 인증 복합 티켓을 받게 됩니다. 액세스 하 고 동적 액세스 제어 인식 리소스에 디바이스 사용자의 신원을 포함 된 토큰 복합 인증 하면 됩니다.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>도메인에 대 한 동적 액세스 제어를 사용 하도록 키 메일 센터 KDC () 그룹 정책 설정을 사용할 수 있도록 지원 합니다.  
모든 도메인 컨트롤러에 위치한 같은 관리 템플릿 정책 설정이 필요한 **컴퓨터 구성 Templates\System\KDC\Support 동적 액세스 제어 및 Kerberos armoring**합니다.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>도메인에 대 한 동적 액세스 제어를 사용 하도록 키 메일 센터 KDC () 그룹 정책 설정을 사용할 수 있도록 지원 합니다.  
모든 도메인 컨트롤러에 위치한 같은 관리 템플릿 정책 설정이 필요한 **컴퓨터 구성 Templates\System\KDC\Support 동적 액세스 제어 및 Kerberos armoring**합니다.  
  
### <a name="support-in-active-directory-to-store-user-and-device-claims-resource-properties-and-central-access-policy-objects"></a>사용자와 디바이스가 클레임, 리소스 속성 및 중앙 액세스 정책 개체 저장 하기 위해 Active Directory를 지원 합니다.  
  
### <a name="support-for-using-group-policy-to-deploy-central-access-policy-objects"></a>그룹 정책을 사용 하 여 중앙 배포 하는 지원 정책 개체 액세스 합니다.  
다음 그룹 정책 설정을 중앙 액세스 정책 개체 조직에서 파일 서버에 배포할 수 있습니다: **컴퓨터 Configuration\Policies\ Windows 보안 Settings\File System\Central 액세스 정책**합니다.  
  
### <a name="support-for-claims-based-file-authorization-and-auditing-for-file-systems-by-using-group-policy-and-global-object-access-auditing"></a>클레임 기반 파일 인증과 글로벌 개체 액세스 감사 및 그룹 정책을 사용 하 여 파일 시스템에 대 한 감사에 대 한 지원  
준비 된 중앙 액세스 정책 제안된 권한을 사용 하 여 중앙 액세스 정책 유효한 액세스 감사할 감사 사용 하도록 설정 해야 합니다. 이 설정을 사용 하면 컴퓨터에 대 한 **감사 정책 구성 고급** 에 **보안 설정** 한 그룹 정책 개체 (GPO). 보안 설정 gpo에서 구성 하면 사용자의 네트워크 안에 GPO 컴퓨터에 배포할 수 있습니다.  
  
### <a name="support-for-transforming-or-filtering-claim-policy-objects-that-traverse-active-directory-forest-trusts"></a>필터링 Active Directory 숲 신뢰를 탐색 하는 클레임 정책 개체 또는 변환에 대 한 지원  
필터링 하거나 이동 숲 신뢰 하는 송수신 클레임 변환 수 있습니다. 필터링 및 청구 변환에 대 한 기본 시나리오 세 가지가 있습니다.  
  
-   **필터링 값 기반** 필터 클레임 값에 따라 될 수 있습니다. 이렇게 하면 특정 값으로 클레임 신뢰 숲으로 전송 되지 않도록 방지 신뢰할 수 있는 숲입니다. 숲 신뢰 하는 도메인 컨트롤러 신뢰할 수 있는 숲 속의 특정 값으로 수신 클레임 필터링 하 여-상승 공격 으로부터 보호 하기 위해 값 기반 필터링 사용할 수 있습니다.  
  
-   **타이핑 기반 필터링 주장** 필터 클레임 값 것이 아니라 유형의 클레임을 기반으로 합니다. 클레임의 이름으로 클레임 유형을 식별 합니다. 클레임 형식 기반 신뢰할 수 있는 숲 속의 필터링을 사용 하 고 Windows 보내는 정보를 신뢰 숲 공개 클레임 못하도록 합니다.  
  
-   **타이핑 기반 변환 주장** 의도 대상에 게 보내기 전에 클레임 조작 합니다. 신뢰할 수 있는 숲 속의 클레임 형식 기반 변환을 사용 하 여 특정 정보를 포함 하는 알려진된 클레임 generalize 합니다. Generalize 클레임 형식이 나 클레임 값을 변환 사용할 수 있습니다.  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
클레임 및 동적 액세스 제어 복합 인증 요구 Kerberos 인증 확장을 하기 때문에 충분 한 도메인 컨트롤러에서 지원 되는 Windows 버전을 실행 인증 동적 액세스 제어 인식 Kerberos 클라이언트를 지원 하기 위해 동적 액세스 제어를 지 원하는 모든 도메인 있어야 합니다. 기본적으로 장치에서 다른 사이트 도메인 컨트롤러를 사용 해야 합니다. 이러한 도메인 컨트롤러를 사용할 수 있는 인증 되지 것입니다. 따라서 다음 중 하나를 지원 해야 합니다.  
  
-   동적 액세스 제어를 지 원하는 모든 도메인 도메인 컨트롤러를 실행 하는 지원 되는 버전의 Windows 또는 Windows Server의 지원 되는 버전을 실행 하는 모든 디바이스에서 인증이 지원 하기 위해 Windows Server 충분히 있어야 합니다.  
  
-   지원 되는 버전의 Windows 또는 실행 하는 디바이스 클레임 또는 복합 id를 사용 하 여 리소스를 보호 하지 않으면, 동적 액세스 제어에 대 한 프로토콜 지원 Kerberos 사용 하지 않도록 설정 해야 합니다.  
  
도메인 사용자 청구를 지 원하는 대 한 적절 한 설정을 클레임 및 복합 인증을 지원 하 고 Kerberos armoring 제공 하기 위해 사용 하 여 Windows server의 지원 되는 버전을 실행 중인 모든 도메인 컨트롤러를 구성 합니다. 다음과 같이 설정을 관리 템플릿 KDC 정책에서 구성 합니다.  
  
-   **항상 클레임 제공** 모든 도메인 컨트롤러에서 지원 되는 버전의 Windows Server를 실행 하는 경우이 설정을 사용 합니다. 또한 Windows Server 2012 이상 도메인 기능 수준을 설정 합니다.  
  
-   **지원 되는** 이 설정을 사용 하면 모니터링 도메인 컨트롤러 Windows Server의 지원 되는 버전을 실행 하는 도메인 컨트롤러 수가 동적 액세스 제어에 의해 보호 리소스에 액세스 해야 하는 컴퓨터의 수에 대 한 충분 한지 확인 합니다.  
  
사용자 도메인 및 파일 서버 도메인 중인 경우 다른 숲, Windows Server 2012 또는 높은 기능 수준 파일 서버 숲 루트 모든 도메인 컨트롤러를 설정 해야 합니다.  
  
클라이언트 동적 액세스 제어를 인식 하지 두 숲 사이 양방향 보안 관계 여야 합니다.  
  
숲을 떠날 때 클레임 변환 하는 경우 Windows Server 2012 또는 높은 기능 수준 모든 사용자의 숲 루트 도메인 컨트롤러를 설정 해야 합니다.  
  
Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 파일 서버 여부를 하는 데 필요한 클레임 수행 하지 않으면 사용자 토큰에 대 한 주장 사용자 지정 하는 그룹 정책 설정이 있어야 합니다. 이 설정에 기본적으로 설정 되어 **자동**를 설정 하려면 그룹 정책 설정을이 발생 하는 **에** 해당 파일 서버에 대 한 주장 사용자 또는 장치를 포함 하는 중앙 정책을 인지 합니다. 이 그룹 정책을으로 설정 해야 하는 파일 서버에 사용자 클레임 포함 하는 임의 Acl 포함 된 경우 **에** 서버 클레임 서버에 액세스할 때 클레임 제공 하지 않는 사용자를 대신 하 여 요청을 알 수 있도록 합니다.  
  
## <a name="additional-resource"></a>추가 리소스  
이 기술을 기반 솔루션을 구현에 대 한 정보를 참조 하세요. [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)합니다.  
  


