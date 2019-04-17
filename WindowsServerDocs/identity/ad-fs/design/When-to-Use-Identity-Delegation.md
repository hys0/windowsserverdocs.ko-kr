---
ms.assetid: 6e711a96-9055-4508-b6d4-318d6aa95fd1
title: "신원을 위임 사용 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: af227d9e87ddb73f194dd46c8ce45fcdf12a34cf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-use-identity-delegation"></a>신원을 위임 사용 하는 경우

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="what-is-identity-delegation"></a>신원을 위임은 무엇 인가요?  
신원을 위임 administrator\ 지정 된 계정을 사용자에 게 가장 수 있도록 Active Directory Federation Services \(AD FS\)의 기능입니다. 사용자가 가장 계정 이라고는 *위임*합니다. 이 위임 기능은 있는 일련의 액세스를 제어 검사 각 응용 프로그램, 데이터베이스 또는 원래 요청에 대 한 권한 체인에 서비스에 대 한 순서 대로 수행 해야 하는 많은 분산된 응용 프로그램에 대 한 중요 합니다. 많은 real\ 세계 시나리오 존재 웹 응용 프로그램 "전면 엔드"를 더 안전 "백 엔드"을 등 Microsoft SQL Server 데이터베이스에 연결 하는 웹 서비스의에서 데이터는 검색 해야 합니다.  
  
예를 들어, 기존 parts\ 주문 웹 사이트 향상 시킬 수 있습니다 프로그래밍 방식으로 되도록 파트너 조직 자신의 구매 내역 및 계정 상태를 볼 수 있습니다. 모든 파트너 금융 데이터는 보안상의 이유로 전용된 구조적 쿼리 언어 \(SQL\) 서버에 안전 하 게 데이터베이스에 저장 됩니다. 이 경우 front\ 종료 응용 프로그램의 코드를 파트너 회사의 금융 데이터에 대해 알고 있습니다. 따라서이 데이터를 호스트 하는 네트워크의 다른 위치에서 다른 컴퓨터에서 검색 해야 \ (이 case\)에서 일부 데이터베이스에 대 한 웹 서비스 \(the back end\) 합니다.  
  
성공 하려면이 data\ 검색 프로세스에 대 한 몇 가지 수행 해야 합니다 "hand\ 흔들기" 인증 연달아는 예시와 같이 웹 응용 프로그램과 부품 데이터베이스에 대 한 웹 서비스 간의 놓습니다.  
  
![신원 위임](media/adfs2_identitydelegationconcept.gif)  
  
원래 요청이 가능성이 웹 서버에 액세스 하려고 사용자의 조직에서 다른 완전히 조직에는 자체 웹 서버에 때문에 전보다 전송 된 보안 토큰 웹 서버 외에도 다른 컴퓨터에 액세스 하는 데 필요한 인증 조건을 충족 하지 않습니다. 따라서 사용자 요청을 원래를 수행할 수 있는 유일한 방법은 중간 federation 서버를 위해 다시 실행 보안 토큰 적절 한 액세스 권한이 있는 리소스 파트너 조직에 삽입 하 여입니다.  
  
## <a name="how-does-identity-delegation-work"></a>신원을 위임은 어떻게 작동 하나요?  
웹 응용 프로그램 계층 응용 프로그램 아키텍처에 자주 일반적인 데이터 나 기능에 액세스 하려면 웹 서비스에 문의 합니다. 이러한 서비스 인증 결정 하 고 감사 쉽게 수 있도록 원래 사용자의 신원을 확인 하려면 웹 서비스에 대 한 중요 한입니다. 이 경우 front\ 종료 웹 응용 프로그램으로 대리인이 웹 서비스에 사용자를 나타냅니다. Adfs이이 시나리오 Active Directory 계정 당사자에 다른 사용자와 작동 하도록 함으로써 수 있습니다. 다음 그림에서 신원을 위임 시나리오 표시 됩니다.  
  
![신원 위임](media/adfs2_identitydelegationsteps.gif)  
  
1.  프랭크 웹 응용 프로그램을 다른 조직에서 part\ 주문 기록에 액세스 하려고 했습니다. 그의 가지의 요청 하 고 ADFS front\ 종료 part\ 주문 웹 응용 프로그램에서 토큰 받습니다.  
  
2.  클라이언트 컴퓨터 클라이언트의 id 증명 1 단계에서 얻은 토큰을 포함 하 여 웹 응용 프로그램에는 요청을 보냅니다.  
  
3.  웹 응용 프로그램에 대 한 클라이언트는 거래를 완료 하기 위해 웹 서비스와 통신 하도록 해야 합니다. 웹 응용 프로그램 연락처 ADFS 위임 토큰 웹 서비스와 상호 작용을 얻을 수 있습니다. 위임 토큰은 대리인이 역할을 사용자에 게 발급 보안 토큰 합니다. ADFS 대상 웹 서비스에 대 한 클라이언트에 대 한 클레임 위임 토큰을 반환 합니다.  
  
4.  웹 응용 프로그램 토큰은 클라이언트와 작동 하는 웹 서비스에 액세스할 3 단계에서 Adfs에서 얻은 사용 합니다. 위임 토큰 검사를 웹 서비스는 웹 응용 프로그램 역할을 하는 클라이언트 확인할 수 있습니다. 웹 서비스의 승인 정책 실행 요청을 기록 하 고 필요한 부품 웹 응용 프로그램에서 프랭크 원래 요청한 기록 데이터를 제공 되므로 프랭크에 있습니다.  
  
특정 대리인이 대 한 ADFS 웹 응용 프로그램 위임 토큰을 요청할 수 있는 웹 서비스를 제한할 수 있습니다. 클라이언트 컴퓨터가이 작업을 수행 하려면에 대 한 Active Directory 계정이 필요가 없습니다. 마지막으로,에서 설명한 대로 웹 서비스의 역할은 사용자를 대리인이 id을 쉽게 확인할 수 있습니다. 이 통해 웹 서비스 여부 자녀가 말하는 클라이언트 컴퓨터에 직접 또는 대리인이 통해에 따라 다른 문제가 발생할 수 있습니다.  
  
## <a name="configuring-ad-fs-for-identity-delegation"></a>신원 위임 ADFS 구성  
신원 위임 ADFS 데이터 검색 프로세스 쉽게 해야 할 때마다 구성 하려면 snap\에 AD FS 관리를 사용할 수 있습니다. ADFS back\ 종료 서비스 필요할 수 있는 승인 컨텍스트를 포함 하는 새로운 보안 토큰 생성할 수를 구성 전에 보호 되는 데이터에 액세스할 수 있습니다.  
  
ADFS 가장 수 있는 사용자를 제한 하지 않습니다. 신원 위임 ADFS 구성 하 고 나면 다음 작업을 수행 합니다.  
  
-   서버 위임 될 수 있는지 여부를 결정 사용자 가장 수 있는 권한을 요청 토큰 합니다.  
  
-   설정 하 고 위임 되는 클라이언트 계정과 대리인이 처럼 작동 하는 서버에 대 한 신원을 컨텍스트 별도로 유지 합니다.  
  
위임 인증 규칙의 snap\ AD FS 관리에 신뢰 파티 신뢰를 추가 하 여 신원을 위임을 구성할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [검사: 필요로 하는 타사 신뢰할에 대 한 청구 규칙 만들기](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)합니다.  
  
## <a name="configuring-the-front-end-web-application-for-identity-delegation"></a>신원 위임 front\ 종료 웹 응용 프로그램을 구성  
개발자 적절 하 게 웹 front\ 종료 응용 프로그램 또는 서비스를 ADFS 컴퓨터에 위임 요청 리디렉션하여 프로그램을 사용할 수 있는 몇 가지 옵션이 있습니다. 신원 위임 연동 웹 응용 프로그램을 사용자 지정 하는 방법에 대 한 자세한 내용은 참조는 [Windows 신원을 Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
