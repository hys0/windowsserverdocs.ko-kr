---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: 서버 인증 인증서의 프라이빗 키 부분 내보내기
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8e1bbeddc4bae1c420b6cc78b52d6b873320ae8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359583"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>서버 인증 인증서의 프라이빗 키 부분 내보내기

Active Directory Federation Services \(AD FS\) 팜의 모든 페더레이션 서버에는 서버 인증 인증서의 개인 키에 대 한 액세스 권한이 있어야 합니다. 페더레이션 서버 또는 웹 서버의 서버 팜을 구현 하는 경우 단일 인증 인증서가 있어야 합니다. 이 인증서는 엔터프라이즈 인증 기관 \(CA\)발급 해야 하며, 내보내기 가능한 개인 키가 있어야 합니다. 서버 인증 인증서의 프라이빗 키는 팜의 모든 서버에서 사용할 수 있도록 내보낼 수 있어야 합니다.  
  
이와 동일한 개념은 팜의 모든 페더레이션 서버 프록시가 동일한 서버 인증 인증서의 개인 키 부분을 공유 해야 한다는 점에서 페더레이션 서버 프록시 팜에 있습니다.  
  
> [!NOTE]  
> 의 AD FS Management snap\-는 페더레이션 서버에 대 한 서버 인증 인증서를 서비스 통신 인증서로 참조 합니다.  
  
이 컴퓨터의 역할에 따라 개인 키와 함께 서버 인증 인증서를 설치한 페더레이션 서버 컴퓨터 또는 페더레이션 서버 프록시 컴퓨터에서이 절차를 사용 합니다. 절차를 마치면 팜의 각 서버에 대한 기본 웹 사이트에서 이 인증서를 가져올 수 있습니다. 자세한 내용은 참조 [기본 웹 사이트로 서버 인증 인증서 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>서버 인증 인증서의 프라이빗 키 부분을 내보내려면  
  
1. **시작** 화면에서**인터넷 정보 서비스 \(IIS\) Manager**를 입력 한 다음 enter 키를 누릅니다.  
  
2. 콘솔 트리에서 **ComputerName**을 클릭합니다.  
  
3. 가운데 창에서 **서버 인증서**를 두 번 클릭\-합니다.  
  
4. 가운데 창에서 내보낼 인증서를 마우스 오른쪽 단추로\-클릭 한 다음 **내보내기**를 클릭 합니다.  
  
5. **인증서 내보내기** 대화 상자 **에서 ...** 단추를 선택합니다.  
  
6. **파일 이름**에 **C:\\** <em>NameofCertificate</em>를 입력 한 다음 **열기**를 클릭 합니다.  
  
7. 인증서 암호를 입력하고 확인한 다음 **확인**을 클릭합니다.  
  
8. 지정한 파일이 지정한 위치에 만들어졌는지 확인하여 내보내기 성공을 확인합니다.  
  
   > [!IMPORTANT]  
   > 이 인증서를 새 서버의 로컬 인증서 저장소로 가져올 수 있도록 파일을 실제 미디어로 전송하고 새 서버로 전송하는 동안 보안을 유지해야 합니다. 프라이빗 키의 보안을 유지하는 것이 매우 중요합니다. 이 키가 손상 되 면 조직 내 및 리소스 파트너\) 조직 내 리소스를 포함 하 여 전체 AD FS 배포 \(의 보안이 손상 됩니다.  
  
9. 페더레이션 서비스를 설치하기 전에 내보낸 서버 인증 인증서를 새 서버의 인증서 저장소로 가져옵니다. 인증서를 가져오는 방법에 대 한 자세한 내용은 서버 인증서 가져오기 \([http:\/\/go.microsoft.com\/fwlink\/을 참조 하세요. LinkId\=108283](https://go.microsoft.com/fwlink/?LinkId=108283)\).  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[페더레이션 서버에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  
[페더레이션 서버 프록시에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)  
  

