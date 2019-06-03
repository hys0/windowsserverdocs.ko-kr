---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: 서버 인증 인증서의 프라이빗 키 부분 내보내기
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c3a39f9d51ed8243118522ae37bc7d205a7ea416
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192144"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>서버 인증 인증서의 프라이빗 키 부분 내보내기

모든 페더레이션 서버에는 Active Directory Federation Services \(AD FS\) 팜에는 서버 인증 인증서의 개인 키에 액세스할 수 있어야 합니다. 서버 팜에 페더레이션 서버 또는 웹 서버를 구현 하는 경우 단일 인증 인증서를 해야 합니다. 이 인증서를 엔터프라이즈 인증 기관에서 발급 해야 \(CA\), 되며 내보낼 수 있는 개인 키가 있어야 합니다. 서버 인증 인증서의 프라이빗 키는 팜의 모든 서버에서 사용할 수 있도록 내보낼 수 있어야 합니다.  
  
이 동일한 개념은 팜의 모든 페더레이션 서버 프록시 동일한 서버 인증 인증서의 개인 키 부분을 공유 해야 하는 의미에서 페더레이션 서버 프록시 팜 true입니다.  
  
> [!NOTE]  
> AD FS 관리 스냅인\-에서 서버 인증 인증서를 서비스 통신 인증서로 페더레이션 서버에 대 한 참조입니다.  
  
역할에 따라이 컴퓨터 재생을 개인 키를 사용 하 여 설치한 서버 인증 인증서를 페더레이션 서버 프록시 컴퓨터를 페더레이션 서버 컴퓨터에서이 절차를 사용 합니다. 절차를 마치면 팜의 각 서버에 대한 기본 웹 사이트에서 이 인증서를 가져올 수 있습니다. 자세한 내용은 참조 [기본 웹 사이트로 서버 인증 인증서 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>서버 인증 인증서의 프라이빗 키 부분을 내보내려면  
  
1.  에 **시작** 화면에서 입력**인터넷 정보 서비스 \(IIS\) Manager**, 한 다음 ENTER를 누릅니다.  
  
2.  콘솔 트리에서 **ComputerName**을 클릭합니다.  
  
3.  가운데 창에서 두 번\-클릭 **서버 인증서**합니다.  
  
4.  가운데 창에서 마우스 오른쪽\-인증서를 내보내고, 클릭 하려는 클릭 **내보내기**합니다.  
  
5.  에 **인증서 내보내기** 대화 상자에서 클릭 된 **...** 단추를 선택합니다.  
  
6.  **파일 이름**, 형식 **c:\\* * * NameofCertificate*를 클릭 하 고 **열기**합니다.  
  
7.  인증서 암호를 입력하고 확인한 다음 **확인**을 클릭합니다.  
  
8.  지정한 파일이 지정한 위치에 만들어졌는지 확인하여 내보내기 성공을 확인합니다.  
  
    > [!IMPORTANT]  
    > 이 인증서를 새 서버의 로컬 인증서 저장소로 가져올 수 있도록 파일을 실제 미디어로 전송하고 새 서버로 전송하는 동안 보안을 유지해야 합니다. 프라이빗 키의 보안을 유지하는 것이 매우 중요합니다. 이 키가 손상 되 면 전체 AD FS 배포의 보안 \(리소스 파트너 조직 및 조직 내의 리소스를 포함 하 여\) 손상 됩니다.  
  
9. 페더레이션 서비스를 설치하기 전에 내보낸 서버 인증 인증서를 새 서버의 인증서 저장소로 가져옵니다. 인증서를 가져오는 방법에 대 한 자세한 내용은 참조 서버 인증서 가져오기 \( [http:\/\/이 포트는 go.microsoft.com\/fwlink\/? LinkId\=108283](https://go.microsoft.com/fwlink/?LinkId=108283)\)합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[페더레이션 서버에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  
[페더레이션 서버 프록시에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)  
  

