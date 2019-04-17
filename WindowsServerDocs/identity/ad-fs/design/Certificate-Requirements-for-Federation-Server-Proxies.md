---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: "인증서 Federation 서버 프록시 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7fb8e71afed1c0eb6b55857835d95f2dd0ec9d5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>인증서 Federation 서버 프록시 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 프록시 역할 Active Directory Federation Services \(AD FS\)에 실행 하는 서버 주소 \(SSL\) 서버 인증 인증서를 사용 해야 합니다. Federation 서버 프록시 SSL 서버 인증 인증서를 사용 하 여 웹 고객과 웹 서버 교통 통신 보호를 위해 합니다.  
  
엔터프라이즈 공개 키 인프라에 포함 되어 있지 않은 인터넷에서 컴퓨터에 federation 서버 프록시 노출 일반적으로 \(PKI\) 합니다. 따라서 공개 \(third\-party\) 인증 기관에서 발급 한 서버 인증 인증서를 사용 하 여 \(CA\) VeriSign 예를 들어 합니다.  
  
Federation 서버 프록시 농장을 사용 하는 경우 모든 federation 서버 프록시 컴퓨터 동일한 서버 인증 인증서를 사용 해야 합니다. 자세한 내용은 참조 [Federation 서버 프록시 팜 만들어야 하는 경우](When-to-Create-a-Federation-Server-Proxy-Farm.md)합니다.  
  
서버 인증 인증서의 제목 이름에 snap\ AD FS 관리에 지정 된 Federation 서비스 이름 값와 일치 하는지 확인을 고려해 야 합니다. 이 값을 찾으려면 snap\에 right\-클릭 열고 **서비스**, 클릭 **Federation 서비스 속성 편집**를 선택한 다음에 값을 찾습니다 **Federation 서비스 이름** 텍스트 상자 합니다.  
  
SSL 인증서 사용에 대 한 일반 정보에 대 한 구성 주소 IIS 7.0에서 참조 \ ([http:///\/go.microsoft.com\/fwlink\/ 있나요? LinkID\ 108544 =](https://go.microsoft.com/fwlink/?LinkID=108544)\) 및 서버 인증서 iis 7.0 구성 \ ([http:///\/go.microsoft.com\/fwlink\/ 있나요? LinkID\ 108545 =](https://go.microsoft.com/fwlink/?LinkID=108545)\).  
  
> [!NOTE]  
> 클라이언트 인증 인증서 ADFS federation 서버 프록시 필요 하지 않습니다.  
  
모든 인증서를 사용 하는 인증서 해지 \(CRLs\) 목록, 구성 된 인증서를 사용 하 여 서버 Crl 배포 하는 서버에 연결할 수 있어야 합니다. CRL 유형의 사용 되는 어떤 포트 결정 합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
