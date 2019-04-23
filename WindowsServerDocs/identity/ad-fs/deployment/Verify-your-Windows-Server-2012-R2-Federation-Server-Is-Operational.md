---
ms.assetid: 1115d276-00f6-4c23-9278-eedcc31295d8
title: Windows Server 2012 R2 페더레이션 서버 작동 중인지 확인 합니다
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2df8a00a953196d7ca19ea0d164abbbf6eefd829
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840744"
---
# <a name="verify-your-windows-server-2012-r2-federation-server-is-operational"></a>Windows Server 2012 R2 페더레이션 서버 작동 중인지 확인 합니다

>적용 대상: Windows Server 2016, Windows Server 2012 R2

다음 절차를 사용하여 페더레이션 서버가 작동하는지, 즉 같은 네트워크의 클라이언트에서 새 페더레이션 서버에 연결할 수 있는지 확인할 수 있습니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터에 대한 **Users**, **Backup Operators**, **Power Users**, **Administrators** 또는 이에 상응하는 구성원 자격이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>절차 1: 페더레이션 서버가 작동하는지 확인하려면  
  
1.  인터넷 정보 서비스를 확인 하려면 \(IIS\) 페더레이션 서버에 페더레이션 서버와 동일한 포리스트에 있는 클라이언트 컴퓨터에 로그온에서 올바르게 구성 되어 있습니다.  
  
2.  브라우저 창을 열고 주소 표시줄에 페더레이션 서버의 DNS 호스트 이름, 입력 추가 \/adfs\/fs\/federationserverservice.asmx를 예를 들어 새 페더레이션 서버에 대 한 합니다.  
  
    **https:\/\/fs1.fabrikam.com\/adfs\/fs\/federationserverservice.asmx**  
  
3.  Enter 키를 누른 후 페더레이션 서버 컴퓨터에서 다음 절차를 완료합니다. **이 웹 사이트의 보안 인증서에 문제가 있습니다.** 라는 메시지가 표시되면 **이 웹 사이트를 계속 탐색합니다.** 를 클릭합니다.  
  
    그러면 XML로 표시된 서비스 설명 문서가 출력되어야 합니다. 이 페이지가 나타나면 페더레이션 서버에서 IIS가 정상적으로 작동하고 페이지를 제공하는 것입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>절차 2: 페더레이션 서버가 작동하는지 확인하려면  
  
1.  새 페더레이션 서버에 관리자로 로그온 합니다.  
  
2.  에 **시작** 화면에서 입력**이벤트 뷰어**, 한 다음 ENTER를 누릅니다.  
  
3.  세부 정보 창에서 두 번\-클릭 **Applications and Services Logs**, 이중\-클릭 **AD FS 이벤트**를 클릭 하 고 **관리자**합니다.  
  
4.  에 **이벤트 ID** 열에서 이벤트 ID 100입니다. 새 이벤트가 표시 하는 페더레이션 서버를 올바르게 구성 되어-이벤트 뷰어의 응용 프로그램 로그, 이벤트 ID 100을 사용 하 여 합니다. 이 이벤트는 페더레이션 서버가 페더레이션 서비스와 성공적으로 통신할 수 있음을 확인 합니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
   
  

