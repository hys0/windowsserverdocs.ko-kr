---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: 계정 페더레이션 서버를 신뢰 하도록 클라이언트 컴퓨터를 구성 합니다.
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e28d050a9aa40c015af16a665e90535cb810b4ff
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192333"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>계정 페더레이션 서버를 신뢰 하도록 클라이언트 컴퓨터를 구성 합니다.

클라이언트 컴퓨터는 Active Directory Federation Services를 사용 하 여 페더레이션된 응용 프로그램은 성공적으로 액세스할 수 있도록 \(AD FS\)를 먼저 구성 해야 Internet Explorer 설정은 각 클라이언트 컴퓨터에서 브라우저 트러스트 되도록 계정 페더레이션 서버입니다. 하면이 수동으로 또는 그룹 정책을 통해 관리 사용자의 기본 설정에 따라 다음 절차 중 하나를 완료 합니다.  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Internet Explorer 설정 구성 수동으로  
다음 절차를 사용 하 여 AD FS 통해 페더레이션을 지원 하도록 각 사용자의 Internet Explorer 설정을 수동으로 구성 하 수 있습니다. 여러 사용자가 단일 컴퓨터를 사용 하는 경우 절차이 여러 번-각 사용자 프로필에 한 번씩입니다.  
  
이 절차를 수행 하려면 페더레이션된 응용 프로그램에 액세스 하는 사용자로 로그온 합니다. 이 프로필을\-특정 설정 합니다. 따라서 특정 컴퓨터에 있는 각 프로필에 대해이 설정을 수동으로 추가 해야 합니다.  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>수동으로 계정 페더레이션 서버를 신뢰 하도록 클라이언트 컴퓨터를 구성 하려면  
  
1.  클라이언트 컴퓨터에서 Internet Explorer를 시작 합니다.  
  
2.  에 **도구** 메뉴에서 클릭 **인터넷 옵션**합니다.  
  
3.  에 **보안** 탭을 클릭 합니다 **로컬 인트라넷** 아이콘을 클릭 하 고 **사이트**합니다.  
  
4.  클릭 **고급**, 및 **웹 사이트 영역에 추가**, 전체 도메인 이름 시스템 입력 \(DNS\) 계정 페더레이션 서버 이름 \(예를 들어, https :\/\/fs1.fabrikam.com\)를 클릭 하 고 **추가**합니다.  
  
5.  **확인**을 세 번 클릭합니다.  
  
## <a name="configuring-internet-explorer-settings-by-using-grouppolicy"></a>그룹 정책을 사용 하 여 Internet Explorer 설정 구성  
대부분의 배포에 대 한 그룹 정책을 사용 하 여 각 클라이언트 컴퓨터에 적절 한 Internet Explorer 설정을 푸시하는 것이 좋습니다.  
  
멤버 자격이 **Domain Admins** 또는 **Enterprise Admins**, 또는 Active Directory Domain Services에서 그와 동등한 \(AD DS\) 이 절차를 완료 하려면 최소한 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-grouppolicy"></a>그룹 정책을 사용 하 여 계정 페더레이션 서버를 신뢰 하도록 클라이언트 컴퓨터를 구성 하려면  
  
1.  계정 파트너 조직의 포리스트의 도메인 컨트롤러에서를 시작 합니다 **그룹 정책 관리** 맞춤\-에서 합니다.  
  
2.  적절 한 그룹 정책 개체를 찾을 \(GPO\)그렇죠\-를 클릭 한 다음 클릭 **편집**합니다.  
  
3.  콘솔 트리에서 엽니다 **사용자 구성\\기본 설정\\Windows 설정\\Internet Explorer 유지 관리**를 클릭 하 고 **보안**합니다.  
  
4.  세부 정보 창에서 두 번\-클릭 **보안 영역 및 콘텐츠 등급**합니다.  
  
5.  아래 **보안 영역 및 개인 정보**, 클릭 **현재 보안 영역 및 개인 정보 설정 가져오기**를 클릭 하 고 **설정 수정**합니다.  
  
6.  클릭 **로컬 인트라넷**를 클릭 하 고 **사이트**합니다.  
  
7.  **영역에 웹 사이트를 추가**, 계정 페더레이션 서버를의 전체 DNS 이름을 입력 \(예를 들어, https:\/\/fs1.fabrikam.com\), 클릭 **추가**를 클릭 하 고 **닫기**합니다.  
  
8.  클릭 **확인** 그룹 정책에 이러한 변경 내용을 적용할 두 배입니다.  
  
