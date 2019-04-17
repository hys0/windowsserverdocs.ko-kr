---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: "Federation 서버를 배포"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f80425b6f062040c51357353038fd07ff0a79ae6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="interoperating-with-ad-fs-1x"></a>Adfs와 상호 작용 1.x

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

® Windows Server 2012에 대 한 Active Directory Federation Services \(AD FS\) ADFS 1과 상호 운용성 합니다. *x*, 조직의 요구에 따라 다음 작업 중 하나 이상을 수행 합니다.  
  
-   Windows Server 2012에서 ADFS 및 이전 버전의 ADFS, 간의 상호 운용성 계획 하 고 클레임 유형 이름 ID 대 한 자세한 내용을 알아보세요. 자세한 내용은 참조 [ADFS 상호 운용성 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)합니다.  
  
-   클레임은 ADFS Federation 서비스에서 ADFS 1 사용할 수 있는 Windows Server 2012에서 전송 됩니다. *x* Federation 서비스 참조 [검사: 클레임 ADFS 전송 ADFS 구성 1.x Federation 서비스](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)합니다.  
  
-   클레임은 ADFS Federation 서비스 ADFS 1 실행 하는 웹 서버에서 호스트 하는 응용 프로그램에 의해 소모 될 수 있는 Windows Server 2012에서 전송 됩니다. *x* claims\ 인식 웹 에이전트 참조 [검사: 클레임 ADFS 전송 ADFS 구성 1.x 클레임 인식 웹 에이전트](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)합니다.  
  
-   클레임 ADFS 1에서에서 전송 됩니다. *x* Federation 서비스를 사용할 수 있는 ADFS Federation 서비스 Windows Server 2012에서 참조 [검사: Adfs의 소모 청구 발생 시에도 ADFS 구성 1.x](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)합니다.  
  
## <a name="differences-between-federation-service-settings"></a>설정 Federation 서비스 간의 차이점  
있지만 대부분은 Adfs의 1입니다. *x* Windows Server 2012 설정에서 ADFS Federation 서비스와 유사한 방식에서 Federation 서비스 설정 작업을 일부 설정을 이름이 변경 되었습니다. 다음 표에서 ADFS 1에 대 한 설정 이름입니다. *x* Federation 서비스와는 ADFS Federation 서비스에서 Windows Server 2012에 대 한 해당 하는 이름입니다.  
  
|광고 FS 1.x Federation 서비스 설정|해당 하는 ADFS Federation 서비스 Windows Server 2012 설정에서  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|계정 파트너|청구 공급자 보안  
|리소스 파트너|파티 신뢰 사용 
|응용 프로그램|파티 신뢰 사용  
|응용 프로그램 속성|파티 신뢰 속성 사용  
|응용 프로그램 URL|신뢰 파티 식별자와 WS\ Federation 수동 끝점 URL  
|URI federation 서비스|Federation 서비스 id  
|Federation 서비스 endpoint URL|WS\ Federation 수동 끝점 URL  
  
## <a name="see-also"></a>참조 하십시오  
[ADFS 및 광고 FS 1.x 상호 운용성](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

