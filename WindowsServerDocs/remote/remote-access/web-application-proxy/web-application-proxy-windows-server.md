---
ms.assetid: d8adcb68-18e0-41bf-a817-d57344bf2e7d
title: Windows Server 2016에서 웹 응용 프로그램 프록시
description: ''
author: kgremban
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: c4e4eb73b7d50c7618ad2c998ee484e660bcfef1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446758"
---
# <a name="web-application-proxy-in-windows-server-2016"></a>Windows Server 2016에서 웹 응용 프로그램 프록시

>적용 대상: Windows Server 2016

**이 콘텐츠는 웹 응용 프로그램 프록시의 온-프레미스 버전에 적합 합니다. 클라우드를 통해 온-프레미스 응용 프로그램에 대 한 보안 액세스를 사용 합니다 [Azure AD 응용 프로그램 프록시 콘텐츠](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)합니다.**  
  
이 섹션에는 웹 응용 프로그램 프록시에 대 한 Windows Server 2016의 새로운 기능과 변경 이란 설명 합니다. 새로운 기능과 변경 내용이 여기에 나열 된에이 미리 보기를 사용 하 여 작업할 때 가장 큰 영향을 있을 가능성이 높은 원인입니다.  
  
## <a name="web-application-proxy-new-features-in-windows-server-2016"></a>웹 응용 프로그램 프록시 Windows Server 2016의 새로운 기능
  
- HTTP 기본 응용 프로그램 게시에 대 한 사전 인증  
  
  HTTP 기본은 Exchange 사서함이 있는 스마트폰을 포함 한 풍부한 클라이언트에 연결 하려면 ActiveSync를 등의 여러 프로토콜에서 사용 하는 권한 부여 프로토콜입니다. 웹 응용 프로그램 프록시는 전통적으로 ActiveSync 클라이언트에서 지원 되지 않는 AD FS 리디렉션 수를 사용 하 여 상호 작용 합니다. 이 새 버전의 웹 응용 프로그램 프록시에서는 HTTP 응용 프로그램에서 수신 비 클레임을 사용 하 여 기본 HTTP를 사용 하 여 응용 프로그램 게시를 페더레이션 서비스에 응용 프로그램에 대 한 신뢰 당사자 트러스트 합니다.  
  
  HTTP 기본 게시에 대 한 자세한 내용은 참조 하십시오. [AD FS 사전 인증을 사용 하 여 응용 프로그램 게시](Publishing-Applications-using-AD-FS-Preauthentication.md#publish-an-application-that-uses-http-basic)  
  
- 응용 프로그램의 와일드 카드 도메인 게시  
  
  SharePoint 2013과 같은 시나리오를 지원 하기 위해 응용 프로그램에 대 한 외부 URL 이제 https://*.sp-apps.contoso.com 예를 들어 특정 도메인 내에서 여러 응용 프로그램을 게시할 수 있도록 와일드 카드를 포함할 수 있습니다. SharePoint 응용 프로그램을 게시를 하면 간단해 집니다.  
  
- HTTP를 HTTPS 리디렉션  
  
  URL에 HTTPS를 입력 하 여 절차를 무시 하는 경우에 사용자가 응용 프로그램을 액세스할 수 있는지를 확인 하 고, 하기 위해 웹 응용 프로그램 프록시를 HTTPS로 리디렉션하 HTTP 이제 지원 합니다.  
  
- HTTP 게시  
  
  통과 사전 인증을 사용 하 여 HTTP 응용 프로그램을 게시할 수 있게 되었습니다.  
  
- 원격 데스크톱 게이트웨이 응용 프로그램 게시  
  
  RDG 웹 응용 프로그램 프록시에 대 한 자세한 내용은 참조 하십시오. [RDG, SharePoint 및 Exchange와 응용 프로그램 게시](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)  
  
- 더 나은 문제 해결을 위한 새 디버그 로그 및 완전 한 감사 추적 및 향상 된 오류 처리에 대 한 향상 된 서비스 로그  
  
  문제 해결에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 프록시 문제 해결](https://technet.microsoft.com/library/dn770156.aspx)  
  
- 향상 된 관리자 콘솔 UI  
  
- 백 엔드 응용 프로그램에 대 한 클라이언트 IP 주소의 전파  
  
## <a name="see-also"></a>관련 항목  
  
-   [Windows Server 2016의 새로운 기능](https://technet.microsoft.com/library/dn765472.aspx)  
  
-   [AD FS 사전 인증을 사용하는 애플리케이션 게시](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)  
  
-   [웹 애플리케이션 프록시 문제 해결](https://technet.microsoft.com/library/dn770156.aspx)  
  


