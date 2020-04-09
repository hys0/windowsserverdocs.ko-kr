---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: WID를 사용하는 독립 실행형 페더레이션 서버
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7253691cff4cc83032e4a345682ca1e43bafddc4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858776"
---
# <a name="stand-alone-federation-server-using-wid"></a>WID를 사용하는 독립 실행형 페더레이션 서버

Active Directory Federation Services \(AD FS\)의 독립\-단독 페더레이션 서버는 Windows 내부 데이터베이스 페더레이션 서비스 WID \(를 사용 하도록 구성 된\)를 호스팅하는 단일 서버로 구성 됩니다. 이 AD FS 토폴로지는 테스트 환경입니다. 바람직하지 않습니다 것 프로덕션 환경에 대 한 않기 때문에 최대 하나의 페더레이션 서버를 더 많은 서버 크기를 사용할 수 없습니다.  
  
테스트 랩에 추가 페더레이션 서버를 추가 하려는 경우 페더레이션 서비스를 처음부터이 단원의 뒷부분에서 언급 하는 다른 토폴로지 중 하나를 배포 하 여 다시 작성 해야 합니다. 이 토폴로지를 사용하여 테스트 환경 또는 증명에 대한 권장 따라서\-의\-단일 페더레이션 서버의 부족한 경우 다음 그림에 나와 있는 것처럼 프라이빗 테스트 네트워크 환경 개념입니다.  
  
![WID를 사용 하 여 서버](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>테스트 랩 고려 사항  
이 섹션에서는 대상, 이점 및 연결 된 테스트 랩 환경에이 토폴로지는 제한 사항에 대 한 다양 한 고려 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지를 사용 해야 합니까?  
  
-   정보 기술 \(IT\) 전문가 나 평가 하거나이 기술에 대 한 개념 증명을 개발 하는 IT 설계자  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 장점은 무엇입니까?  
  
-   테스트 랩 환경에서 설정할 수  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 제한 사항은 무엇입니까?  
  
-   페더레이션 서비스 당 페더레이션 서버는 하나만 \(팜을 확장할 수 있는 기능은 없습니다\)  
  
-   중복 되지 \(AD FS 구성 데이터베이스의 단일 인스턴스만 존재\)  
  

## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
