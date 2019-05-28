---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: 페더레이션 서버 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0eb9265513d5ca18da1150d3be6752d364b7cd1a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192084"
---
# <a name="interoperating-with-ad-fs-1x"></a>AD FS 1.x와 상호 운용

Active Directory Federation Services 간의 상호 운용성 \(AD FS\) Windows Server® 2012에 AD FS 1. *x*, 하나 이상을 조직의 요구에 따라 다음 작업을 완료 합니다.  
  
-   Windows Server 2012의 AD FS 및 AD FS의 이전 버전 간의 상호 운용성 계획 하 고 클레임 유형 이름이 ID에 대 한 자세히 알아봅니다. 자세한 내용은 [AD FS와의 상호 운용성에 대 한 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)합니다.  
  
-   AD FS 1에서 사용할 수 있는 Windows Server 2012의 AD FS 페더레이션 서비스에서 클레임 전송 됩니다. *x* 페더레이션 서비스 표시 [검사 목록: AD FS 1.x 페더레이션 서비스에 클레임을 보내도록 AD FS 구성](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)합니다.  
  
-   AD FS 1을 실행 하는 웹 서버에서 호스트 되는 응용 프로그램에서 사용할 수 있는 Windows Server 2012의 AD FS 페더레이션 서비스에서 클레임 전송 됩니다. *x* 클레임\-인식 웹 에이전트 참조 [검사 목록: AD FS 1.x 클레임 인식 웹 에이전트에 대 한 클레임을 보내도록 AD FS 구성](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)합니다.  
  
-   AD FS 1에서에서 클레임 전송 됩니다. *x* Windows Server 2012에서 AD FS 페더레이션 서비스에서 사용할 수 있도록 페더레이션 서비스 표시 [검사 목록: AD FS에서 클레임을 사용 하도록 AD FS 구성 1.x](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)합니다.  
  
## <a name="differences-between-federation-service-settings"></a>페더레이션 서비스 설정의 차이점  
하지만 대부분의 AD FS 1. *x* 유사한 방식으로 Windows Server 2012 설정에서 AD FS 페더레이션 서비스에서 페더레이션 서비스 설정 작업을 몇 가지 설정 이름이 변경 되었습니다. 다음 표에서 AD FS 1에 대 한 설정의 이름을 나열합니다. *x* 페더레이션 서비스와 Windows Server 2012의 AD FS 페더레이션 서비스에 대 한 해당 이름입니다.  
  
|AD FS 1.x 페더레이션 서비스 설정|Windows Server 2012 설정에서 해당 하는 AD FS 페더레이션 서비스  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|계정 파트너|클레임 공급자 트러스트  
|리소스 파트너|신뢰 당사자 트러스트 
|애플리케이션|신뢰 당사자 트러스트  
|응용 프로그램 속성|신뢰 당사자 트러스트 속성  
|응용 프로그램 URL|신뢰 당사자 식별자 및 WS\-페더레이션 수동 끝점 URL  
|페더레이션 서비스 URI|페더레이션 서비스 식별자  
|페더레이션 서비스 끝점 URL|WS\-페더레이션 수동 끝점 URL  
  
## <a name="see-also"></a>관련 항목  
[AD FS 및 AD FS 1.x 상호 운용성](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

