---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: 페더레이션 서버 프록시에 대한 인증서 요구 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: dab77c3e3226e89eb3ac9b74e7db9b6df8f181bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408142"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>페더레이션 서버 프록시에 대한 인증서 요구 사항

Active Directory Federation Services \(AD FS\)에서 페더레이션 서버 프록시 역할을 실행 하는 서버는 SSL(Secure Sockets Layer) \(SSL\) 서버 인증 인증서를 사용 하는 데 필요 합니다. 페더레이션 서버 프록시는 SSL 서버 인증 인증서를 사용하여 웹 클라이언트와 웹 서버의 트래픽 통신을 보호합니다.  
  
일반적으로 페더레이션 서버 프록시는 PKI\)\(엔터프라이즈 공개 키 인프라에 포함 되지 않은 인터넷 상의 컴퓨터에 노출 됩니다. 따라서 인증 기관 \(인증 기관 CA\)(예: VeriSign)\)\-\(에서 발급 한 서버 인증 인증서를 사용 합니다.  
  
페더레이션 서버 프록시 팜이 있는 경우 모든 페더레이션 서버 프록시 컴퓨터에서 동일한 서버 인증 인증서를 사용 해야 합니다. 자세한 내용은 참조 [페더레이션 서버 프록시 배치 위치](When-to-Create-a-Federation-Server-Proxy-Farm.md)합니다.  
  
서버 인증 인증서의 주체 이름이의 AD FS Management snap\-에 지정 된 페더레이션 서비스 이름 값과 일치 하는지 확인 하는 것이 중요 합니다. 이 값을 찾으려면에서 snap\-를 열고\-**서비스**를 클릭 한 다음 **페더레이션 서비스 속성 편집**을 클릭 하 고 **페더레이션 서비스 이름** 입력란에서 값을 찾습니다.  
  
SSL 인증서를 사용 하는 방법에 대 한 일반적인 내용은 IIS 7.0 \(SSL(Secure Sockets Layer) 구성 ( [http:\/\/go.microsoft.com\/fwlink\/을 참조 하세요. LinkID\=108544](https://go.microsoft.com/fwlink/?LinkID=108544)\) 및 IIS 7.0에서 서버 인증서 구성 \([http:\/\/go.microsoft.com\/fwlink\/? LinkID\=108545](https://go.microsoft.com/fwlink/?LinkID=108545)\).  
  
> [!NOTE]  
> AD FS 페더레이션 서버 프록시에는 클라이언트 인증 인증서가 필요 하지 않습니다.  
  
사용 하는 인증서에 Crl\)\(인증서 해지 목록이 있는 경우 구성 된 인증서가 있는 서버는 Crl을 배포 하는 서버에 연결할 수 있어야 합니다. CRL 유형에 따라 사용되는 포트가 결정됩니다.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
