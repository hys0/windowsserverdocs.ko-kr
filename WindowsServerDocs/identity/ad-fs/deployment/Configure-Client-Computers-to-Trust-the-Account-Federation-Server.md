---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: "계정 Federation 서버 신뢰 하는 클라이언트 컴퓨터 구성"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdfb086c8177e72c074ac5b5b1a38aac49c4082c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>계정 Federation 서버 신뢰 하는 클라이언트 컴퓨터 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

클라이언트 컴퓨터 \(AD FS\) Active Directory Federation Services를 사용 하 여 연결 된 응용 프로그램에 액세스할 수 있는, 되도록 먼저 구성 해야 Internet Explorer 설정을 클라이언트 각 컴퓨터에서 브라우저 신뢰 계정 federation 서버를 합니다. 이렇게 하려면 수동으로 또는 그룹 정책을 통해 관리 기본 설정에 따라 다음 중 하나를 수행 하 여 합니다.  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Internet Explorer 설정 구성 중 수동으로  
다음 절차 각 사용자를 통해 ADFS federation 지원 하기 위해 Internet Explorer 설정을 수동으로 구성에 사용할 수 있습니다. 여러 사용자는 한 대의 컴퓨터를 사용 하는 경우이 절차 여러 번을 완료 등 각 사용자 프로필에 대해 한 번만 합니다.  
  
이 절차를 수행 하는 연결 된 응용 프로그램에 액세스할 수 있는 사용자로 로그온 합니다. 특정 profile\ 설정입니다. 그러므로 특정 컴퓨터에 존재 하는 각 프로필에 대해이 설정을 수동으로 추가 해야 합니다.  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>계정 federation 서버 신뢰 하는 클라이언트 컴퓨터 수동으로 구성 하려면  
  
1.  클라이언트 컴퓨터에서 Internet Explorer를 시작 합니다.  
  
2.  에 **도구** 메뉴를 클릭 **인터넷 옵션**합니다.  
  
3.  에 **보안** 탭을 클릭는 **로컬 인트라넷** 아이콘을 클릭 하 고 **사이트**합니다.  
  
4.  클릭 **고급**의 **영역에 웹 사이트를 추가**, 계정 federation 서버의 전체 Domain Name System \(DNS\) 이름을 입력 \ (예: https:\/\/fs1.fabrikam.com\)를 클릭 한 다음 **추가**합니다.  
  
5.  클릭 **확인** 세 번 합니다.  
  
## <a name="configuring-internet-explorer-settings-by-using-group-policy"></a>그룹 정책을 사용 하 여 Internet Explorer 설정 구성  
대부분의 배포에 대 한 그룹 정책에 적절 한 Internet Explorer 설정을 각 클라이언트 컴퓨터를 사용 하는 것이 좋습니다.  
  
회원 **도메인 관리자** 또는 **엔터프라이즈 관리자**, Active Directory 도메인 서비스에 해당 하는 \(AD DS\)는 최소가이 절차를 수행 하는 데 필요한 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-group-policy"></a>그룹 정책을 사용 하 여 계정 federation 서버 신뢰 하는 클라이언트 컴퓨터 구성 하려면  
  
1.  계정 파트너 회사의 숲 속의 도메인 컨트롤러에서 시작의 **그룹 정책 관리** snap\에 있습니다.  
  
2.  적절 한 그룹 정책 개체 \(GPO\) 찾기 right\ 클릭을 누른 다음 **편집**합니다.  
  
3.  콘솔 트리에서 열고 **사용자 Configuration\\Preferences\\Windows Settings\\Internet 탐색기 유지 관리**을 차례로 클릭 하 고 **보안**합니다.  
  
4.  세부 정보 창에서 double\ 클릭 **보안 영역 및 콘텐츠 등급**합니다.  
  
5.  아래에서 **보안 영역 및 개인 정보 보호**, 클릭 **현재 보안 영역 및 개인 정보 설정을 가져오기**을 차례로 클릭 하 고 **설정 수정**합니다.  
  
6.  클릭 **로컬 인트라넷**을 차례로 클릭 하 고 **사이트**합니다.  
  
7.  **영역에 웹 사이트를 추가**, 계정 federation 서버 DNS 전체 이름을 입력 \ (예: https:\/\/fs1.fabrikam.com\)를 클릭 **추가**을 차례로 클릭 하 고 **닫기**합니다.  
  
8.  클릭 **확인** 그룹 정책에 이러한 변경 내용을 적용 하려면 두 번 합니다.  
  
