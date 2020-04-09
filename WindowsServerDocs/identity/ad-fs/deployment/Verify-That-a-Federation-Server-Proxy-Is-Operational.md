---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: 페더레이션 서버 프록시 작동 여부 확인
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3e74af4a63476040ca44522ceb7c0ae22e914fec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855856"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>페더레이션 서버 프록시 작동 여부 확인


다음 절차를 사용 하 여 페더레이션 서버 프록시가 Active Directory Federation Services \(AD FS\)페더레이션 서비스와 통신할 수 있는지 확인할 수 있습니다. **AD FS 페더레이션 서버 프록시 구성 마법사** 를 실행 하 여 페더레이션 서버 프록시 역할에서 실행 되도록 컴퓨터를 구성한 후이 절차를 실행 합니다. 이 마법사를 실행 하는 방법에 대 한 자세한 내용은 [페더레이션 서버 프록시 역할에 대 한 컴퓨터 구성](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)을 참조 하세요.  
  
> [!IMPORTANT]  
> 이 테스트에 성공하면 이벤트 뷰어에 페더레이션 서버 프록시 컴퓨터에 대한 특정 이벤트가 생성됩니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터의 **Administrators** 구성원 자격 또는 동급의 권한이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>페더레이션 서버 프록시가 작동 하는지 확인 하려면  
  
1.  페더레이션 서버 프록시에 관리자로 로그온 합니다.  
  
2.  **시작** 화면에서**이벤트 뷰어**를 입력 한 다음 enter 키를 누릅니다.  
  
3.  세부 정보 창에서 **응용 프로그램 및 서비스 로그**를 두 번 클릭 하\-\-**AD FS 이벤트**를 두 번 클릭 한 다음 **관리자**를 클릭 합니다.  
  
4.  **이벤트 ID** 열에서 이벤트 ID 198을 확인합니다.  
  
    페더레이션 서버 프록시가 올바르게 구성 된 경우 이벤트 뷰어의 응용 프로그램 로그에 이벤트 ID가 198 인 새 이벤트가 표시 됩니다. 이 이벤트는 페더레이션 서버 프록시 서비스가 성공적으로 시작 되었으며 현재 온라인 상태 인지 확인 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

