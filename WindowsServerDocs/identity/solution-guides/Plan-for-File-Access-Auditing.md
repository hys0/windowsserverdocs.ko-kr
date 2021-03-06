---
ms.assetid: 3ea48a72-20a2-4da4-84e4-26b5728513ce
title: 파일 액세스 감사 계획
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ffe8843f9ace604bc0904ba2d1eaef78d2872b99
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861166"
---
# <a name="plan-for-file-access-auditing"></a>파일 액세스 감사 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목의 정보는 Windows Server 2012에 도입 된 보안 감사 향상 기능 및 엔터프라이즈에 동적 Access Control를 배포할 때 고려해 야 하는 새로운 감사 설정에 대해 설명 합니다. 배포하는 실제 감사 정책 설정은 목표에 따라 다르며 목표에는 규정 준수, 모니터링, 법정 분석 및 문제 해결 등이 포함될 수 있습니다.  
  
> [!NOTE]  
> 회사에 대해 전반적인 보안 감사 전략을 계획하고 배포하는 방법에 대한 자세한 내용은 [고급 보안 감사 정책 계획 및 배포](https://go.microsoft.com/fwlink/?LinkID=191139)에 설명되어 있습니다. 보안 감사 정책을 구성하고 배포하는 방법에 대한 자세한 내용은 [고급 보안 감사 정책 단계별 가이드](https://go.microsoft.com/fwlink/?LinkID=191141)를 참조하세요.  
  
Windows Server 2012의 다음과 같은 보안 감사 기능을 동적 Access Control와 함께 사용 하 여 전반적인 보안 감사 전략을 확장할 수 있습니다.  
  
-   **식 기반 감사 정책**. 동적 액세스 제어를 사용하면 사용자, 컴퓨터 및 리소스 클레임을 기반으로 하는 식을 사용하여 대상이 지정된 감사 정책을 만들 수 있습니다. 예를 들어 감사 정책을 만들어 높은 수준의 보안이 허가되지 않은 직원이 업무에 많은 영향을 주는 것으로 분류한 파일에 대해 모든 읽기 및 쓰기 작업을 추적할 수 있습니다. 식 기반 감사 정책은 그룹 정책을 통해 중앙에서 적용할 수도 있고, 특정 파일이나 폴더에 직접 작성할 수도 있습니다. 자세한 내용은 [전역 개체 액세스 감사를 사용한 그룹 정책](https://go.microsoft.com/fwlink/?LinkId=241498)(영문)을 참조하세요.  
  
-   **개체 액세스 감사의 추가 정보**. 파일 액세스 감사는 Windows Server 2012의 새로운 기능은 아닙니다. 적절한 감사 정책이 적용되어 있는 경우 Windows 및 Windows Server 운영 체제에서는 사용자가 파일에 액세스할 때마다 감사 이벤트를 생성합니다. 기존 파일 액세스 이벤트(4656, 4663)에는 액세스한 파일의 특성에 대한 정보가 포함됩니다. 이벤트 로그 필터링 도구에서는 이 추가 정보를 사용하여 가장 관련성 높은 감사 이벤트를 식별할 수 있습니다. 자세한 내용은 [핸들 조작 감사](https://technet.microsoft.com//library/dd772626(WS.10).aspx) (영문) 및 [보안 계정 관리자 감사](https://go.microsoft.com/fwlink/?LinkId=241501)(영문)를 참조하세요.  
  
-   **사용자 로그온 이벤트의 자세한 정보**. 적절한 감사 정책이 적용되어 있는 경우 Windows 운영 체제에서는 사용자가 로컬로 또는 원격으로 컴퓨터에 로그인할 때마다 감사 이벤트를 생성합니다. Windows Server 2012 또는 Windows 8에서는 사용자의 보안 토큰과 연결 된 사용자 및 장치 클레임을 모니터링할 수도 있습니다. 이벤트 4626에는 이러한 사용자 클레임 및 디바이스 클레임에 대한 정보가 포함되며, 감사 로그 관리 도구에서는 이 정보를 활용하여 사용자 로그온 이벤트와 개체 액세스 이벤트를 상호 연결하여 파일 특성 및 사용자 특성을 기반으로 하는 이벤트 필터링을 사용하도록 설정할 수 있습니다. 사용자 로그온 감사에 대한 자세한 내용은 [로그온 감사](https://go.microsoft.com/fwlink/?LinkId=241502)(영문)를 참조하세요.  
  
-   **새 유형의 보안 개체에 대한 변경 추적**. 다음 시나리오에서는 보안 개체에 대한 변경 추적이 중요할 수 있습니다.  
  
    -   **중앙 액세스 정책 및 중앙 액세스 규칙에 대한 변경 추적**. 중앙 액세스 정책 및 중앙 액세스 규칙은 중요한 리소스에 대한 액세스를 제어하는 데 사용할 수 있는 중앙 정책을 정의합니다. 이러한 정책 및 규칙에 대한 변경 내용은 여러 컴퓨터에서 사용자에게 부여되는 파일 액세스 권한에 직접적으로 영향을 미칠 수 있습니다. 따라서 조직 입장에서 중앙 액세스 정책 및 중앙 액세스 규칙에 대한 변경 추적은 중요할 수 있습니다. 중앙 액세스 정책 및 중앙 액세스 규칙은 AD DS(Active Directory 도메인 서비스)에 저장되므로 AD DS의 기타 보안 개체에 대한 감사 변경 내용과 같이 이러한 정책 및 규칙을 수정하려는 시도를 감사할 수 있습니다. 자세한 내용은 [디렉터리 서비스 액세스 감사](https://technet.microsoft.com/library/dd941618(WS.10).aspx)(영문)를 참조하세요.  
  
    -   **클레임 사전의 정의에 대한 변경 추적**. 클레임 정의에는 클레임 이름, 설명 및 사용 가능한 값이 포함됩니다. 클레임 정의에 대한 변경 내용은 중요한 리소스에 대한 액세스 권한에 영향을 미칠 수 있습니다. 따라서 조직 입장에서 클레임 정의에 대한 변경 추적은 중요할 수 있습니다. 중앙 액세스 정책 및 중앙 액세스 규칙과 같이 클레임도 AD DS에 저장되므로 AD DS의 다른 보안 개체와 같이 감사할 수 있습니다. 자세한 내용은 [디렉터리 서비스 액세스 감사](https://technet.microsoft.com/library/dd941618(WS.10).aspx)(영문)를 참조하세요.  
  
    -   **파일 특성에 대한 변경 추적**. 파일 특성은 파일에 적용되는 중앙 액세스 규칙을 결정합니다. 파일 특성에 대한 변경 내용은 잠재적으로 파일에 대한 액세스 제한에 영향을 미칠 수 있습니다. 따라서 파일 특성에 대한 변경 내용을 추적하는 것은 중요할 수 있습니다. 권한 부여 정책 변경 감사 정책을 구성하여 모든 컴퓨터에서 파일 특성에 대한 변경 내용을 추적할 수 있습니다. 자세한 내용은 [권한 부여 정책 변경 감사](https://go.microsoft.com/fwlink/?LinkId=241504) (영문) 및 [파일 시스템에 대한 개체 액세스 감사](https://go.microsoft.com/fwlink/?LinkId=241505)(영문)를 참조하세요. Windows Server 2012에서 이벤트 4911은 다른 권한 부여 정책 변경 이벤트의 파일 특성 정책 변경 내용을 구별 합니다.  
  
    -   **파일과 관련된 중앙 액세스 정책에 대한 변경 추적.** 이벤트 4913에는 이전 및 신규 중앙 액세스 정책의 SID(보안 식별자)가 표시됩니다. 각 중앙 액세스 정책에는 이 보안 식별자를 사용하여 검색할 수 있는 사용자 이름도 포함됩니다. 자세한 내용은 [권한 부여 정책 변경 감사](https://go.microsoft.com/fwlink/?LinkId=241504)(영문)를 참조하세요.  
  
    -   **사용자 및 컴퓨터 특성에 대한 변경 추적**. 파일과 마찬가지로, 사용자 및 컴퓨터 개체는 특성을 가질 수 있으며 이러한 특성을 변경 하면 사용자가 파일에 액세스 하는 기능에 영향을 줄 수 있습니다. 따라서 사용자나 컴퓨터 특성에 대한 변경 내용을 추적하는 것은 중요할 수 있습니다. 사용자 및 컴퓨터 개체는 AD DS에 저장되므로 이러한 개체의 특성에 대한 변경 내용을 감사할 수 있습니다. 자세한 내용은 [DS 액세스](https://go.microsoft.com/fwlink/?LinkId=241508)(영문)를 참조하세요.  
  
-   **정책 변경 준비**. 중앙 액세스 정책에 대한 변경 내용은 정책이 적용된 모든 컴퓨터에 대한 액세스 제어 결정에 영향을 미칠 수 있습니다. 완화된 정책은 원하는 수준보다 높은 수준의 액세스를 부여할 수 있으며, 지나치게 제한된 정책은 과도한 지원 센터 문의를 야기할 수 있습니다. 따라서 변경을 적용하기 전에 중앙 액세스 정책에 대한 변경 내용을 확인하는 것은 매우 효과적일 수 있습니다. 이러한 목적을 위해 Windows Server 2012에는 "준비" 라는 개념이 도입 되었습니다. 준비를 통해 사용자는 제안된 정책 변경 내용을 적용하기 전에 확인해볼 수 있습니다. 정책 준비를 사용하기 위해 적용된 정책과 함께 제안된 정책이 배포됩니다. 하지만 준비된 정책은 실제로 사용 권한을 부여하거나 거부하지 않습니다. 대신, Windows Server 2012은 준비 된 정책을 사용 하는 액세스 검사 결과가 적용 된 정책을 사용 하는 액세스 검사 결과와 다를 때 언제 든 지 감사 이벤트 (4818)를 기록 합니다.  
  


