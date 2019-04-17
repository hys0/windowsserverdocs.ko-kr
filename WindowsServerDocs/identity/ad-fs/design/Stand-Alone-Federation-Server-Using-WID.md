---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: "WID 사용 하 여 독립 실행형 Federation 서버"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9ec4150a7d3adfaac786219d253e1d0898c18204
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="stand-alone-federation-server-using-wid"></a>WID 사용 하 여 독립 실행형 Federation 서버

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stand\만 federation 서버 Active Directory Federation Services \(AD FS\)에서 단일 Windows 내부 데이터베이스 \(WID\) 사용 하도록 구성 된 Federation 서비스 호스트 하는 서버 구성 되어 있습니다. 이 ADFS 토폴로지를 테스트 랩에 대 한 않습니다. 권장 되지 않습니다 것 생산 환경에 대 한 때문에 하나의 federation 서버를 제한 하 고 더 많은 서버로 확장을 사용할 수 없습니다.  
  
추가 federation 서버를 테스트 랩에 추가 하려는 경우 나중에이 섹션에 언급 된 다른 토폴로지에서 배포 하 여 Federation 서비스 처음부터 다시 만들어야 합니다. 따라서이 토폴로지 테스트 랩 또는 proof\ of\ 개념 환경에 대 한 단일 federation 서버 인, 적절 한 다음 그림에서 표시 된 대로 개인 테스트 네트워크에서 사용 하는 것이 좋습니다.  
  
![사용 하 여 WID 서버](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>고려 랩 테스트  
이 여기서 대상, 혜택을 테스트 랩 환경에 대 한이 토폴로지와 관련 된 제한 사항에 대 한 다양 한 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지 사용 해야 하나요?  
  
-   정보 기술 \(IT\) 전문가 또는 계산 하거나이 기술에 대 한를 검증 개발 하려는 IT 설계자  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지에 사용 하는 어떤 혜택이 있나요?  
  
-   쉽게 테스트 랩 환경에서를 설정 하려면  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여 제한 이란 무엇 인가요?  
  
-   하나의 federation 서버 Federation 서비스 별로 \ (한 farm\로 확장 기능이)  
  
-   하지 중복 \ (ADFS 구성 데이터베이스 exists\ 단일 인스턴스만)  
  

## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
