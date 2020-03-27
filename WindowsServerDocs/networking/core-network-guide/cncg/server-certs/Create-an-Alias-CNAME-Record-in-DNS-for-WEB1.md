---
title: DNS에 WEB1에 대한 별칭(CNAME) 레코드 만들기
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0ac6ef7da3c9e604d9fa3c029f1afa2861a56741
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318333"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>별칭을 만들 \(CNAME\) w e b 1에 대 한 dns 레코드

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 절차를 사용 하 여 별칭 정식 이름을 추가 하려면 \(CNAME\) 도메인 컨트롤러에서 dns에서 영역에 웹 서버에 대 한 리소스 레코드입니다. CNAME 레코드를 통해 파일 전송 프로토콜 모두 호스트 하는 등의 작업을 수행 하기 쉽고, 단일 호스트를 가리키도록 이름을 여러 개를 사용할 수 있습니다 \(FTP\) 서버와 동일한 컴퓨터에 웹 서버입니다.   
  
웹 서버를 사용 하 여 인증서 해지 목록에 호스트를 위해 사용할 수 있는이 인해 \(CRL\) 인증 기관에 대 한 \(CA\) 뿐만 아니라 FTP 또는 웹 서버 등의 서비스를 수행 합니다.  
  
이 절차를 수행 하는 경우 대체 **별칭 이름을** 및 배포에 대 한 적절 한 값을 사용 하 여 다른 변수입니다.  
  
이 절차를 수행 하려면의 구성원 이어야 **Domain Admins**합니다.  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>별칭을 추가 하려면 \(CNAME\) 영역에 리소스 레코드  
  
>[!NOTE]  
>Windows PowerShell을 사용 하 여이 절차를 수행 하려면 참조 [추가 DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx)합니다.  
  
1.  서버 관리자에서 d c 1 **도구** 클릭 하 고 **DNS**합니다. DNS 관리자 Microsoft Management Console (MMC)가 열립니다.  
  
2.  콘솔 트리에서 **정방향 조회 영역**, 별칭 리소스 레코드를 추가 하 고 클릭 한 다음 원하는 정방향 조회 영역을 마우스 오른쪽 단추로 클릭 **새 별칭 \(CNAME\)** 합니다. **새 리소스 레코드** 대화 상자가 열립니다.  
  
3.  **별칭 이름을**, 별칭 이름을 입력 **pki**합니다.  
  
4.  에 대 한 값을 입력 하면 **별칭 이름을**,  **정규화 된 도메인 이름 \(FQDN\)** 대화 상자에서 자동 채우기입니다. 예를 들어 별칭 이름을 "pki" 이며 도메인 경우 corp.contoso.com 인 경우 값 **pki.corp.contoso.com** 자동으로 채워지므로 드립니다.  
  
5.  **정규화 된 도메인 이름 \(FQDN\) 대상 호스트에 대해**, 웹 서버의 FQDN을 입력 합니다. 웹 서버 이름이 w e b 1이 고 도메인이 corp.contoso.com을 입력 하는 예를 들어 **WEB1.corp.contoso.com**합니다.  
  
6.  클릭 **확인** 영역에 새 레코드를 추가 합니다.  
  

