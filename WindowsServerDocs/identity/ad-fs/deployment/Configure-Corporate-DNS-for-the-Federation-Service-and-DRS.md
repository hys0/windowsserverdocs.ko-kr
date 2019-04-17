---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: "회사 DNS Federation 서비스 및 DRS 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9b66bed99cbc2ac2cdf116579adaea282c45fabe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>회사 DNS Federation 서비스 및 DRS 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>6 단계: 호스트 추가 Federation 서비스 및 DRS 회사 dns \(A\) 및 별칭 \(CNAME\) 리소스 기록  
다음 리소스 레코드 federation 서비스에 대 한 회사 Domain Name System \(DNS\) 및 이전 단계에서 구성 디바이스 등록 서비스에 추가 해야 합니다.  
  
|항목|입력|주소|  
|---------|--------|-----------|  
|federation\_service\_name|\(A\) 개최|ADFS 서버 또는 ADFS 팜 앞으로 구성 된 부하 분산의 IP 주소의 IP 주소|  
|enterpriseregistration|별칭 \(CNAME\)|federation\_server\_name.contoso.com|  
  
호스트 \(A\) 및 별칭 \(CNAME\) 리소스 레코드 federation 서버에 대 한 회사 DNS와 디바이스 등록 서비스에 추가 하려면 다음 절차에 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 최소 요구 사항을 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>해당 federation 서버에 대 한 호스트 \(A\) 및 별칭 \(CNAME\) 리소스 레코드 DNS에 추가 하려면  
  
1.  사용자 도메인 컨트롤러 서버 관리자에서에 **도구** 메뉴를 클릭 **DNS** snap\에서 DNS 열려면 합니다.  
  
2.  콘솔 트리에서 확장는 **domain\_controller\_name** 노드를 확장 **앞 조회 영역이**, right\ 클릭 **domain\_name**을 차례로 클릭 하 고 **새 호스트 \(A or AAAA\)**합니다.  
  
3.  에 **이름** 상자 ADFS 농장 사용할 이름을 입력 합니다.  
  
4.  에 **IP 주소** 상자에 IP 주소 해당 federation 서버를 입력 합니다. 클릭 **호스트 추가**합니다.  
  
5.  Right\ 클릭은 **domain\_name** 노드와 클릭 **새 별칭 \(CNAME\)**합니다.  
  
6.  에 **새 리소스 레코드** 대화 상자, 입력 **enterpriseregistration** 에 **별칭 이름** 상자 합니다.  
  
7.  정식된 도메인에 표시 된 이름 입력 대상 호스트 상자의 \(FQDN\) **federation\_service\_farm\_name.domain\_name.com**을 차례로 클릭 하 고 **확인**합니다.  
  
    > [!IMPORTANT]  
    > 실제 배포에서 회사에 여러 사용자 이름 \(UPN\) 접미사 경우 만들어야 여러 CNAME 레코드 각 DNS에 이러한 UPN 접미사 합니다.  
  
## <a name="see-also"></a>참조 하십시오 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[지침에 따라 Windows Server 2012 r 2 광고 FS 배포](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Federation 서버 농장 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

