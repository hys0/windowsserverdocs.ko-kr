---
ms.assetid: 1115d276-00f6-4c23-9278-eedcc31295d8
title: Windows Server 2012 R2 페더레이션 서버가 작동 하는지 확인
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d32338d0e9242d12ab18fd30192736ea3b44fdb4
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868062"
---
# <a name="verify-your-windows-server-2012-r2-federation-server-is-operational"></a>Windows Server 2012 R2 페더레이션 서버가 작동 하는지 확인



다음 절차를 사용하여 페더레이션 서버가 작동하는지, 즉 같은 네트워크의 클라이언트에서 새 페더레이션 서버에 연결할 수 있는지 확인할 수 있습니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터에 대한 **Users**, **Backup Operators**, **Power Users**, **Administrators** 또는 이에 상응하는 구성원 자격이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>절차 1: 페더레이션 서버가 작동하는지 확인하려면  
  
1.  페더레이션 서버에 인터넷 정보 서비스 \(IIS\) 가 올바르게 구성 되어 있는지 확인 하려면 페더레이션 서버와 같은 포리스트에 있는 클라이언트 컴퓨터에 로그온 합니다.  
  
2.  브라우저 창을 열고 주소 표시줄에 페더레이션 서버의 DNS 호스트 이름을 입력 한 다음 새 페더레이션 서버에 대해 adfs \/\/fs\/federationserverservice를 추가 합니다. 예를 들면 다음과 같습니다.  
  
    **https:\/\/fs1.fabrikam.comadfs\/fs\/federationserverservice\/**  
  
3.  Enter 키를 누른 후 페더레이션 서버 컴퓨터에서 다음 절차를 완료합니다. **이 웹 사이트의 보안 인증서에 문제가 있습니다**. 메시지가 표시 되 면 **이 웹 사이트를 계속**탐색 합니다 .를 클릭 합니다.  
  
    그러면 XML로 표시된 서비스 설명 문서가 출력되어야 합니다. 이 페이지가 나타나면 페더레이션 서버에서 IIS가 정상적으로 작동하고 페이지를 제공하는 것입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>절차 2: 페더레이션 서버가 작동하는지 확인하려면  
  
1.  새 페더레이션 서버에 관리자로 로그온 합니다.  
  
2.  **시작** 화면에서**이벤트 뷰어**를 입력 한 다음 enter 키를 누릅니다.  
  
3.  세부 정보 창에서 **응용 프로그램 및 서비스 로그**를 두 번\-클릭\-하 고 **AD FS 이벤트**를 두 번 클릭 한 다음 **관리자**를 클릭 합니다.  
  
4.  **이벤트 id** 열에서 이벤트 id 100를 찾습니다. 페더레이션 서버가 올바르게 구성 된 경우 이벤트 뷰어의 응용 프로그램 로그에 이벤트 ID가 100 인 새 이벤트가 표시 됩니다. 이 이벤트는 페더레이션 서버가 페더레이션 서비스와 성공적으로 통신할 수 있는지 확인 합니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
   
  

