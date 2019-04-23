---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: 페더레이션 서버 프록시에 대한 인증서 요구 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7fb8e71afed1c0eb6b55857835d95f2dd0ec9d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875724"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>페더레이션 서버 프록시에 대한 인증서 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 페더레이션 서버 프록시 역할에서 실행 되는 서버 \(AD FS\) Secure Sockets Layer를 사용 하는 데 필요한 \(SSL\) 서버 인증 인증서. 페더레이션 서버 프록시는 SSL 서버 인증 인증서를 사용하여 웹 클라이언트와 웹 서버의 트래픽 통신을 보호합니다.  
  
페더레이션 서버 프록시는 일반적으로 엔터프라이즈 공개 키 인프라에 포함 되지 않은 컴퓨터에서 인터넷에 노출 \(PKI\)합니다. 따라서 공용에서 발급 한 서버 인증 인증서를 사용 하 여 \(세 번째\-파티\) 인증 기관 \(CA\), 예를 들어, VeriSign 합니다.  
  
페더레이션 서버 프록시 팜을 경우 모든 페더레이션 서버 프록시 컴퓨터는 동일한 서버 인증 인증서를 사용 해야 합니다. 자세한 내용은 [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md)를 참조하세요.  
  
AD FS 관리 스냅인에 페더레이션 서비스 이름 값이 서버 인증 인증서 일치의 주체 이름을 지정 있는지 확인 해야\-에서 합니다. 이 값을 찾으려면 스냅인을 엽니다\-에서는 오른쪽\-클릭 **서비스**, 클릭 **페더레이션 서비스 속성 편집**를 다음에서 값을 확인 하 고 **페더레이션 서비스 이름** 입력란입니다.  
  
SSL 인증서를 사용 하는 방법에 대 한 일반적인 내용은 IIS 7.0에서 Secure Sockets Layer 구성을 참조 하세요 \( [http:\/\/이 포트는 go.microsoft.com\/fwlink\/? LinkID\=108544](https://go.microsoft.com/fwlink/?LinkID=108544) \) 및 IIS 7.0에서 서버 인증서 구성 \( [http:\/\/go.microsoft.com\/fwlink\/? LinkID\=108545](https://go.microsoft.com/fwlink/?LinkID=108545)\)합니다.  
  
> [!NOTE]  
> 클라이언트 인증 인증서는 AD FS 페더레이션 서버 프록시 필요 하지 않습니다.  
  
사용 하 여 인증서 해지 목록에는 모든 인증서 \(Crl\), 구성 된 인증서를 사용 하 여 서버 Crl을 배포 하는 서버에 연결할 수 있어야 합니다. CRL 유형에 따라 사용되는 포트가 결정됩니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
