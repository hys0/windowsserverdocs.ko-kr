---
title: 인증서 해지 목록 (Crl)를 배포 하도록 WEB1 구성
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: fa4a8c41-8c2a-425c-8511-736fe5d196ac
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3319715e70c1e68739a10a4c67a9fa404d5ad80e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318411"
---
# <a name="configure-web1-to-distribute-certificate-revocation-lists-crls"></a>인증서 해지 목록 (Crl)를 배포 하도록 WEB1 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

W e b 1 Crl을 배포 하려면 웹 서버를 구성 하려면이 절차를 사용할 수 있습니다.  
  
루트 CA의 확장에서는 루트 CA의 CRL을 https://pki.corp.contoso.com/pki를 통해 사용할 수 있음을 언급 했습니다. 현재 있는 아니므로 PKI 가상 디렉터리에 w e b 1을 만들어야 합니다.  
  
이 절차를 수행 하려면의 구성원 이어야 **Domain Admins**합니다.  
  
> [!NOTE]  
> 아래 절차에 관련 된 배포에 적합 한 사용자 계정 이름, 웹 서버 이름, 폴더 이름 및 위치와 다른 값을 바꿉니다.  
  
#### <a name="to-configure-web1-to-distribute-certificates-and-crls"></a>인증서를 배포할 w e b 1 및 Crl을 구성 하려면  
  
1.  관리자는 Windows PowerShell을 실행 합니다. w e b 1에서 입력 `explorer c:\`, 한 다음 ENTER를 누릅니다. C 드라이브를 Windows 탐색기가 열립니다.   
  
2.  C: 드라이브에 PKI 라는 새 폴더를 만듭니다. 이렇게 하려면 클릭 **홈**, 를 클릭 하 고 **새 폴더**합니다. 새 폴더를 강조 표시 된 임시 이름으로 만들어집니다. 형식 **pki** 한 다음 ENTER를 누릅니다.  
  
3.  위에 마우스 커서를 Windows 탐색기에서 방금 만든 폴더를 마우스 오른쪽 단추로 **공유할**, 를 클릭 하 고 **특정 한 사람들**합니다. **파일 공유** 대화 상자가 열립니다.  
  
4.  **파일 공유**, 형식 **Cert Publishers**, 를 클릭 하 고 **추가**합니다. Cert Publishers 그룹 목록에 추가 됩니다. 목록에서에서 **사용 권한 수준을**, 옆의 화살표를 클릭 **Cert Publishers**, 를 클릭 하 고 **읽기/쓰기**합니다. 클릭 **공유**, 를 클릭 하 고 **수행**합니다.  
  
5.  Windows 탐색기를 닫습니다.  
  
6.  IIS 콘솔을 엽니다. 서버 관리자에서 **도구**를 클릭하고 **IIS(인터넷 정보 서비스) 관리자**를 클릭합니다.  
  
7.  인터넷 정보 서비스 (IIS) 관리자 콘솔 트리에서 확장 **w e b 1**합니다. Microsoft 웹 플랫폼을 시작하도록 초대 받았다면 **취소**를 클릭합니다.  
  
8.  **Sites**를 확장하고 **Default Web Site**를 마우스 오른쪽 단추로 클릭한 뒤 **가상 디렉터리 추가**를 클릭합니다.  
  
9. **별칭**, 형식 **pki**합니다. **실제 경로** 유형 **C:\pki**, 를 클릭 한 다음 **확인**합니다.  
  
10. 익명을 사용 하도록 설정 모든 클라이언트는 CA 인증서 및 Crl의 유효성을 검사할 수 있도록 pki 가상 디렉터리에 액세스 합니다. 이를 수행하려면:  
  
    1.  **연결** 창에서 **pki**가 선택되었는지 확인합니다.  
  
    2.  **pki 홈**에서 **인증**을 클릭합니다.  
  
    3.  **작업** 창에서 **권한 편집**을 클릭합니다.  
  
    4.  **보안** 탭에서 **편집**을 클릭합니다.  
  
    5.  **pki에 대한 사용 권한** 대화 상자에서 **추가**를 클릭합니다.  
  
    6.  에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택**, 형식 **ANONYMOUS LOGON; 모든 사용자** 클릭 하 고 **이름 확인**합니다. **확인**을 클릭합니다.  
  
    7.  클릭 **확인** 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자입니다.  
  
    8.  클릭 **확인** 에 **pki에 대 한 사용 권한을** 대화 상자입니다.  
  
11. 클릭 **확인** 에 **pki 속성** 대화 상자입니다.  
  
12. **pki 홈** 창에서 **요청 필터링**을 두 번 클릭합니다.  
  
13. **파일 이름 확장명** 탭이 **요청 필터링** 창에서 기본적으로 선택되어 있습니다. **작업** 창에서 **기능 설정 편집**을 클릭합니다.  
  
14. **요청 필터링 설정 편집**에서 **이중 이스케이프 허용**을 선택하고 **확인**을 클릭합니다.  
  
15. 인터넷 정보 서비스 (IIS) 관리자 MMC에서 사용자의 웹 서버 이름을 클릭 합니다. 예를 들어 웹 서버 w e b 1 인 경우 클릭 하 여 **w e b 1**합니다.  
  
16. **작업**, 클릭 **다시 시작**합니다. 인터넷 서비스를 중지 했다가 다시 시작 합니다.  
  

