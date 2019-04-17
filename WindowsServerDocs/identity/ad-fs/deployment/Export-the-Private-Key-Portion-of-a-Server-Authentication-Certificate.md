---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: "서버 인증 인증서의 개인 키 부분을 내보내기"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c968f0702d56b56d0a80459e5cf0c9e658c56741
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>서버 인증 인증서의 개인 키 부분을 내보내기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 federation 서버에 Active Directory Federation Services \(AD FS\) 농장 개인 키 서버 인증 인증서의에 액세스할 수 있어야 합니다. 서버 팜 federation 또는 웹 서버를 구현 하는 경우 단일 인증 인증서가 있어야 합니다. 이 인증서를 발행 해야 엔터프라이즈 인증 기관에서 \(CA\), 있으며 키가 있어야를 내보낼 수 있는 개인 합니다. 그룹의 모든 서버를 사용할 수 있게 될 수 있도록 서버 인증 인증서의 개인 키 내보낼 수 있어야 합니다.  
  
이 같은 개념이 농장에 있는 모든 federation 서버 프록시 동일한 서버 인증 인증서의 키 개인 부분을 공유 해야 센스에서 federation 서버 프록시 농장의 그렇습니다.  
  
> [!NOTE]  
> snap\ AD FS 관리 서버 인증 인증서 federation 서버에 대 한 서비스 통신 인증서도 참조합니다.  
  
이 컴퓨터에서 재생 됩니다 역할을에 따라 사용이 절차 federation 서버 컴퓨터 또는 federation 서버 프록시 컴퓨터에서 개인 키와 함께 서버 인증 인증서를 설치한 합니다. 절차 완료 되 면이 인증서 팜의 각 서버 기본 웹 사이트에서 가져올 수 있습니다. 자세한 내용은 참조 [서버 인증 인증서를 기본 웹 사이트를 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>서버 인증 인증서의 키 개인 부분을 내보내려면  
  
1.  에 **시작** 화면에서 입력**인터넷 정보 서비스 \(IIS\) 관리자**, ENTER 키를 누릅니다.  
  
2.  콘솔 트리에서 클릭 **ComputerName**합니다.  
  
3.  가운데 창에서 double\ 클릭 **서버 인증서**합니다.  
  
4.  가운데 창에서 right\ 클릭을 내보내고, 클릭 한 다음 원하는 인증서 **내보내려면**합니다.  
  
5.  **내보내려면 인증서** 대화 상자에서 클릭는 **...** 단추입니다.  
  
6.  **파일 이름**, 입력 **C:\\***NameofCertificate*을 차례로 클릭 하 고 **열기**합니다.  
  
7.  인증서에 대 한 암호를 입력을 확인을 클릭 한 다음 **확인**합니다.  
  
8.  지정한 파일을 지정된 위치에 만들어집니다 있는지 확인 하 여 사용자 내보내기의 성공 여부를 확인 합니다.  
  
    > [!IMPORTANT]  
    > 새 서버에 로컬 인증서 스토어에이 인증서를 가져올 수 있으며 되도록 물리적 미디어 파일을 전송 하 고 새 서버에 전송 하는 동안 보안이 보호 합니다. 매우 중요 한 개인 키의 보안을 보호 하기 위해입니다. 이 키는 손상 될 경우 전체 ADFS 배포 보안 \ (리소스와 파트너 organizations\ 리소스 조직 내에 포함)는 손상 합니다.  
  
9. Federation 서비스 설치 하기 전에 내보낸된 서버 인증 인증서를 새로운 서버의 인증서 스토어로 가져옵니다. 인증서를 가져오는 방법에 대 한 정보 가져오기 서버 인증서 참조 \ ([http:///\/go.microsoft.com\/fwlink\/ 있나요? LinkId\ 108283 =](https://go.microsoft.com/fwlink/?LinkId=108283)\).  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Federation 서버의 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  
[인증서 Federation 서버 프록시 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)  
  

