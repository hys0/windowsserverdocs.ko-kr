---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: 기본 웹 사이트로 서버 인증 인증서 가져오기
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: da91a3e8c34c86f7fd03ca875b3800fdb6001750
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192122"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>기본 웹 사이트로 서버 인증 인증서 가져오기

인증 기관에서 서버 인증 인증서 가져온 후 \(CA\)를 수동으로 설치 해야 해당 인증서를 기본 웹 사이트에서 각 페더레이션 서버 또는 서버 팜에 페더레이션 서버 프록시에 대 한 합니다.  
  
웹 서버의 경우 해당 웹 사이트 또는 페더레이션된 응용 프로그램이 있는 가상 디렉터리에 서버 인증 인증서를 수동으로 설치해야 합니다.  
  
팜을 설정하는 경우 팜의 각 서버에서 정확히 동일한 설정을 사용하여 이 절차를 동일하게 수행해야 합니다.  
  
> [!NOTE]  
> AD FS 관리 스냅인\-에서 서버 인증 인증서를 서비스 통신 인증서로 페더레이션 서버에 대 한 참조입니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>서버 인증 인증서를 기본 웹 사이트로 가져오려면  
  
1.  에 **시작** 화면에서 입력**인터넷 정보 서비스 \(IIS\) Manager**, 한 다음 ENTER를 누릅니다.  
  
2.  콘솔 트리에서 **ComputerName**을 클릭합니다.  
  
3.  가운데 창에서 두 번\-클릭 **서버 인증서**합니다.  
  
4.  **작업** 창에서 **가져오기**를 클릭합니다.  
  
5.  에 **인증서 가져오기** 대화 상자에서 클릭 된 **...** 단추를 선택합니다.  
  
6.  pfx 인증서 파일의 위치를 찾아서 강조 표시한 후 **열기**를 클릭합니다.  
  
7.  인증서 암호를 입력하고 **확인**을 클릭합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)  
  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[페더레이션 서버에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)  
  
[페더레이션 서버 프록시에 대한 인증서 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

