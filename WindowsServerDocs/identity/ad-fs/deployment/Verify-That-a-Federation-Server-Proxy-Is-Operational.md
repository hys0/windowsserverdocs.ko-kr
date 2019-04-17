---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: "Federation 서버 프록시가 작동 하는지 확인"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4900d8621b94a514a07bba55b2f7f3df5dd36353
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>Federation 서버 프록시가 작동 하는지 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 절차 federation 서버 프록시 Active Directory Federation Services \(AD FS\)에 통신할 수 있는지 확인 하기 위해 사용할 수 있습니다. 실행 한 후이 절차를 실행 하면는 **광고 FS Federation 서버 프록시 구성을 마법사** federation 서버 프록시 역할에서 실행 하려면 컴퓨터를 구성할 수 있습니다. 이 마법사를 실행 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 프록시 역할 컴퓨터 구성](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)합니다.  
  
> [!IMPORTANT]  
> 이 테스트 결과 해당 federation 서버 프록시 컴퓨터에서 특정 이벤트 이벤트 뷰어에서 성공 생성 합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>Federation 서버 프록시가 작동 하는지 확인 하려면  
  
1.  Federation 서버 프록시 관리자 권한으로 로그온 합니다.  
  
2.  에 **시작** 화면에서 입력**이벤트 뷰어**, ENTER 키를 누릅니다.  
  
3.  세부 정보 창에서 double\ 클릭 **응용 프로그램 및 서비스 로그**, double\ 클릭 **광고 FS 이벤트**을 차례로 클릭 하 고 **관리자**합니다.  
  
4.  에 **이벤트 ID** 열 이벤트 ID 198 찾습니다.  
  
    Federation 서버 프록시 올바르게 구성 되었는지, 이벤트 뷰어 이벤트 ID 198와의 응용 프로그램 로그 새 이벤트를 표시 합니다. 이 이벤트 federation 서버 프록시 서비스 성공적으로 시작 하 고 있는 이제 온라인 확인 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

