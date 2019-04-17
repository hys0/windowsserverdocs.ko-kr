---
title: Dns에서 (CNAME) 별칭 기록 WEB1 만들려면
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 65f10efe1cfd2866fb99406bf031197f6268b05b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>Dns에서 WEB1 별칭 \(CNAME\) 기록 만들기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차를 사용 하 여 별칭 정식 이름 \(CNAME\) 리소스 레코드 도메인 컨트롤러에서 DNS에 영역에 웹 서버에 대 한 추가 수 있습니다. CNAME 레코드를 통해 쉽게 파일을 전송 프로토콜 \(FTP\) 서버와 동일한 컴퓨터에는 웹 서버 호스트 하는 등의 작업을 수행할 수 있도록 단일 호스트 가리키도록 개 이상의 이름을 사용할 수 있습니다.   
  
자유롭게 사용 하면서 웹 서버의 인증서가 해지 호스트 하는이 때문 인증 기관에 대 한 \(CRL\) 목록 \(CA\)도 FTP 나 웹 서버의 같은 추가 서비스를 수행 합니다.  
  
이 절차를 수행 하면 교체 **별칭 이름** 및 기타 변수 배포에 대 한 적절 한 값으로 합니다.  
  
이 절차를 수행 하려면의 회원 있어야 **도메인 관리자**합니다.  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>별칭 \(CNAME\) 리소스 레코드 영역에 추가 하려면  
  
>[!NOTE]  
>이 절차를 Windows PowerShell를 사용 하 여 수행 참조 [추가 DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx)합니다.  
  
1.  서버 관리자 d c 1 클릭 **도구** 차례로 클릭 하 고 **DNS**합니다. (MMC) DNS 관리자 Microsoft Management Console을 엽니다.  
  
2.  두 번 클릭 콘솔 트리에서 **앞 조회 영역이**, 별칭 리소스 레코드 추가를 클릭 한 다음 원하는 앞으로 조회 영역이 마우스 오른쪽 단추로 클릭 **새 별칭 \(CNAME\)**합니다. **새 리소스 레코드** 대화 상자를 엽니다.  
  
3.  **별칭 이름**, 이름을 입력 하 고 별칭 **pki**합니다.  
  
4.  에 대 한 값을 입력 하면 **별칭 이름**, **정식된 도메인 \(FQDN\) 이름을** 대화 상자에서 자동 채우기 합니다. 예를 들어 별칭 이름은 "pki"과 도메인 것은 corp.contoso.com 값 **pki.corp.contoso.com** 를 자동으로 채워집니다입니다.  
  
5.  **정식된 도메인 이름 \(FQDN\) 대상 호스트**, FQDN 웹 서버를 입력 합니다. 예를 들어 웹 서버 WEB1 라고 하는 경우 도메인이 corp.contoso.com 입력 **WEB1.corp.contoso.com**합니다.  
  
6.  클릭 **확인** 새 레코드 영역에 추가 합니다.  
  

