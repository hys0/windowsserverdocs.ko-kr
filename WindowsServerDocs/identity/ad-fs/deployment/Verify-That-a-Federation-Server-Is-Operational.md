---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: "Federation 서버가 제대로 작동 하는지 확인"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2034b4c35061879a64004486395d0887c59087b2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="verify-that-a-federation-server-is-operational"></a>Federation 서버가 제대로 작동 하는지 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 절차를 사용 하 여 federation 서버 운영; 인지 확인 하려면 즉, 모든 클라이언트 동일한 네트워크에 새 federation 서버에 연결할 수 있습니다.  
  
회원 **사용자**, **백업 운영자**, **고급 사용자**, **관리자** 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>절차 1: federation 서버가 작동 하는지 확인 하려면  
  
1.  인터넷 정보 서비스 \(IIS\) federation 서버에 올바르게 구성 되어 있는지를 확인 하려면 federation 서버와 같은 숲 속에 있는 클라이언트 컴퓨터에 로그온 합니다.  
  
2.  브라우저 창 열기, 주소 표시줄 글꼴로 연합 DNS 서버의 이름, 개최 된와 후 추가 /adfs/fs/federationserverservice.asmx에 새 federation 서버에 대 한 예를 들어 다음과 같습니다.  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Enter 키를 하 고 해당 federation 서버 컴퓨터에서 다음 절차를 수행 합니다. 메시지가 표시 되는 경우 **이 웹 사이트의 보안 인증서에 문제가**, 클릭 **이 웹 사이트를 계속**합니다.  
  
    출력 예상 되는 서비스 설명 문서와 xml 표시 됩니다. 이 페이지에 표시 되 면 IIS federation 서버에 성공적으로 작동 하 고 제공 페이지를는 합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>절차 2: federation 서버가 작동 하는지 확인 하려면  
  
1.  새 federation 서버에 관리자 권한으로 로그온 합니다.  
  
2.  에 **시작** 화면에서 입력 **이벤트 뷰어**, ENTER 키를 누릅니다.  
  
3.  세부 정보 창에서 double\ 클릭 **응용 프로그램 및 서비스 로그**, double\ 클릭 **광고 FS 이벤트**을 차례로 클릭 하 고 **관리자**합니다.  
  
4.  에 **이벤트 ID** 열 이벤트 ID 100 찾습니다. 새 이벤트를 표시 federation 서버를 올바르게 구성 되어-이벤트 뷰어의 응용 프로그램 로그에서-ID 100 이벤트와 함께 합니다. 이 이벤트 federation 서버에서 해당 Federation 서비스와 통신 수 있는지 확인 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  

