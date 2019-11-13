---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: 페더레이션 서버 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f2aaca5ffc846c41af82c276750c564db38b5020
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359515"
---
# <a name="interoperating-with-ad-fs-1x"></a>AD FS 1.x와 상호 운용

Active Directory Federation Services \(AD FS\) Windows Server® 2012 및 AD FS 1의 상호 운용성을 위해. *x*에서 조직의 요구에 따라 다음 작업 중 하나 이상을 완료 합니다.  
  
-   Windows Server 2012의 AD FS와 이전 버전의 AD FS에 대 한 상호 운용성을 계획 하 고 이름 ID 클레임 유형에 대해 자세히 알아보세요. 자세한 내용은 [AD FS 1.x와의 상호 운용성 계획](https://technet.microsoft.com/library/ff678040.aspx)을 참조 하세요.  
  
-   AD FS 1에서 사용할 수 있는 Windows Server 2012의 AD FS 페더레이션 서비스에서 클레임을 보내려는 경우 *x* 페더레이션 서비스 [검사 목록: AD FS 1.X 페더레이션 서비스에 클레임을 보내도록 AD FS 구성](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)을 참조 하세요.  
  
-   AD FS 1을 실행 하는 웹 서버에서 호스트 되는 응용 프로그램에서 사용 될 수 있는 Windows Server 2012의 AD FS 페더레이션 서비스에서 클레임을 전송 하려는 경우 *x* 클레임\-인식 웹 에이전트 [는 검사 목록: AD FS 1.X 클레임 인식 웹 에이전트로 클레임을 보내도록 AD FS 구성](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)을 참조 하세요.  
  
-   AD FS 1에서 클레임을 보내려는 경우 *x* 페더레이션 서비스 Windows Server 2012에서 AD FS 페더레이션 서비스에서 사용할 수 있습니다. [검사 목록: AD FS 1.x에서 클레임을 사용 하도록 AD FS 구성](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)을 참조 하세요.  
  
## <a name="differences-between-federation-service-settings"></a>페더레이션 서비스 설정 간의 차이점  
대부분의 AD FS 1입니다. *x* 페더레이션 서비스 설정은 Windows Server 2012 설정에서 AD FS 페더레이션 서비스와 비슷한 방식으로 작동 합니다. 일부 설정 이름이 변경 되었습니다. 다음 표에서는 AD FS 1에 대 한 설정의 이름을 나열 합니다. *x* 페더레이션 서비스 Windows Server 2012에서 AD FS 페더레이션 서비스에 해당 하는 이름입니다.  
  
|AD FS 1.x 페더레이션 서비스 설정|Windows Server 2012 설정에 해당 하는 AD FS 페더레이션 서비스  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|계정 파트너|클레임 공급자 트러스트  
|리소스 파트너|신뢰 당사자 트러스트 
|애플리케이션|신뢰 당사자 트러스트  
|응용 프로그램 속성|신뢰 당사자 트러스트 속성  
|응용 프로그램 URL|신뢰 당사자 식별자 및 WS\-페더레이션 수동 끝점 URL  
|페더레이션 서비스 URI|페더레이션 서비스 식별자  
|페더레이션 서비스 끝점 URL|WS\-페더레이션 수동 끝점 URL  
  
## <a name="see-also"></a>참고 항목  
[AD FS 및 AD FS 1.x 상호 운용성](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

