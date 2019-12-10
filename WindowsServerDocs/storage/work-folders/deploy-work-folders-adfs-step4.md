---
title: AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포 - 4단계, 웹 응용 프로그램 프록시 설치
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 6/24/2017
ms.assetid: 4a11ede0-b000-4188-8190-790971504e17
ms.openlocfilehash: 17adf89d3a26767bbc736a31da7b7b2b204570a2
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945228"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-4-set-up-web-application-proxy"></a>AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포: 4단계, 웹 응용 프로그램 프록시 설치

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 AD FS(Active Directory Federation Services) 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 배포하는 네 번째 단계를 설명합니다. 이 과정의 다른 단계는 다음 항목에서 찾을 수 있습니다.  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 개요](deploy-work-folders-adfs-overview.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 1 단계, AD FS 설정](deploy-work-folders-adfs-step1.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 2 단계, AD FS 후 구성 작업](deploy-work-folders-adfs-step2.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 3 단계, 클라우드 폴더 설정](deploy-work-folders-adfs-step3.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 5 단계, 클라이언트 설정](deploy-work-folders-adfs-step5.md)  

> [!NOTE]
>   이 섹션에서 설명 하는 지침은 Windows Server 2019 또는 Windows Server 2016 환경용입니다. Windows Server 2012 R2를 사용하는 경우 [Windows Server 2012 R2 instructions(Windows Server 2012 R2 지침)](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx)을 따르세요.

클라우드 폴더에 사용할 웹 응용 프로그램 프록시를 설정하려면 다음 절차를 수행합니다.  
  
## <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS 및 클라우드 폴더 인증서 설치  
이전에(1단계 AD FS 설치 및 3단계 클라우드 폴더 설치에서) 만든 AD FS 및 클라우드 폴더 인증서를 웹 응용 프로그램 프록시 역할을 설치할 컴퓨터의 로컬 컴퓨터 인증서 저장소에 설치해야 합니다.  
  
지금 여러분이 설치하는 것은 신뢰할 수 있는 루트 인증 기관 인증서 저장소의 게시자까지 추적할 수 없는 자체 서명된 인증서이기 때문에 해당 스토어에도 인증서를 복사해야 합니다.  
  
인증서를 설치하려면 다음 단계를 수행합니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  **MMC**를 입력합니다.  
  
3.  **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
4.  **사용 가능한 스냅인** 목록에서 **인증서**를 선택한 다음 **추가**를 클릭합니다. 인증서 스냅인 마법사가 시작됩니다.  
  
5.  **컴퓨터 계정**을 선택하고 **다음**을 클릭합니다.  
  
6.  **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 를 선택하고 **마침**을 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **Console Root\Certificates\(Local Computer)\Personal\Certificates** 폴더를 확장합니다.  
  
9. **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **가져오기**를 클릭합니다.  
  
10. AD FS 인증서가 들어 있는 폴더를 찾은 후 마법사의 지침에 따라 파일을 가져와서 인증서 저장소에 배치합니다.  
  
11. 9 및 10단계를 반복하되, 이번에는 클라우드 폴더 인증서를 찾아서 가져옵니다.  
  
12. **Console Root\Certificates\(Local Computer)\Trusted Root Certification Authorities\Certificates** 폴더를 확장합니다.  
  
13. **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **가져오기**를 클릭합니다.  
  
14. AD FS 인증서가 들어 있는 폴더를 찾은 후 마법사의 지침에 따라 파일을 가져와서 신뢰할 수 있는 루트 인증 기관 저장소에 배치합니다.  
  
15. 13 및 14단계를 반복하되, 이번에는 클라우드 폴더 인증서를 찾아서 가져옵니다.  
  
## <a name="install-web-application-proxy"></a>웹 응용 프로그램 프록시 설치  
웹 응용 프로그램 프록시를 설치하려면 다음 단계를 따릅니다.  
  
1.  웹 응용 프로그램 프록시를 설치할 서버에서 **서버 관리자**를 열고 **역할 및 기능 추가** 마법사를 시작합니다.  
  
2.  마법사의 첫 번째 페이지와 두 번째 페이지에서 **다음**을 클릭합니다.  
  
3.  **서버 선택** 페이지에서 서버를 선택하고 **다음**을 클릭합니다.  
  
4.  **서버 역할** 페이지에서 **원격 액세스** 역할을 선택하고 **다음**을 클릭합니다.  
  
5.  기능 페이지와 원격 액세스 페이지에서 **다음**을 클릭합니다.  
  
6.  **역할 서비스** 페이지에서 **웹 응용 프로그램 프록시**를 선택하고, **기능 추가**를 클릭하고, **다음**을 클릭합니다.

7.  **Confirm installation selections** 페이지에서 **Install**을 클릭합니다.  
  
## <a name="configure-web-application-proxy"></a>웹 응용 프로그램 프록시 구성  
웹 응용 프로그램 프록시를 구성하려면 다음 단계를 따릅니다.  
  
1.  서버 관리자 맨 위에서 경고 플래그를 클릭한 다음 웹 응용 프로그램 프록시 구성 마법사를 여는 링크를 클릭합니다.  
  
2.  시작 페이지에서 **다음**을 누릅니다.  
  
3.  **페더레이션 서버** 페이지에서 페더레이션 서비스 이름을 입력합니다. 테스트 예제에서는 **blueadfs.contoso.com**입니다.  
  
4.  페더레이션 서버의 로컬 관리자 계정 자격 증명을 입력합니다. 도메인 자격 증명(예: contoso\administrator)이 아니라 로컬 자격 증명(예: 관리자)을 입력해야 합니다.  
  
5.  **AD FS 프록시 인증서** 페이지에서 이전에 가져온 AD FS 인증서를 선택합니다. 테스트 예제에서는 **blueadfs.contoso.com**입니다. **다음**을 클릭합니다.  
  
6.  확인 페이지에 서비스 구성을 실행하는 Windows PowerShell 명령이 표시됩니다. **구성**을 클릭합니다.  
  
## <a name="publish-the-work-folders-web-application"></a>클라우드 폴더 웹 응용 프로그램 게시  
다음 단계는 클라이언트에 클라우드 폴더를 제공할 웹 응용 프로그램을 게시하는 것입니다. 클라우드 폴더 웹 응용 프로그램을 게시하려면 다음 단계를 따릅니다.  
  
1. **서버 관리자**를 열고 **도구** 메뉴에서 **원격 액세스 관리**를 클릭하여 원격 액세스 관리 콘솔을 엽니다.  
  
2. **구성**에서 **웹 응용 프로그램 프록시**를 클릭합니다.  
  
3. **작업** 아래에서 **게시**를 클릭합니다. 새 응용 프로그램 게시 마법사가 열립니다.  
  
4. 시작 페이지에서 **다음**을 클릭합니다.  
  
5. **사전 인증** 페이지에서 **AD FS(Active Directory Federation Services)** 를 선택하고 **다음**을 클릭합니다.  
  
6. **클라이언트 지원** 페이지에서 **OAuth2**를 선택하고 **다음**을 클릭합니다.

7. **신뢰 당사자** 페이지에서 **클라우드 폴더**를 선택하고 **다음**을 클릭합니다. 이 목록은 AD FS의 웹 응용 프로그램 프록시에 게시됩니다.  
  
8. **게시 설정** 페이지에서 다음 항목을 입력하고 **다음**을 클릭합니다.  
  
   -   웹 응용 프로그램에 사용할 이름  
  
   -   클라우드 폴더의 외부 URL  
  
   -   클라우드 폴더 인증서의 이름  
  
   -   클라우드 폴더의 백 엔드 URL  
  
   기본적으로 마법사는 외부 URL과 똑같은 백 엔드 URL을 만듭니다.  
  
   테스트 예제에서는 다음 값을 사용합니다.  
  
   이름: **WorkFolders**  
  
   외부 URL: **https://workfolders.contoso.com**  
  
   외부 인증서: **이전에 설치한 클라우드 폴더 인증서**  
  
   백 엔드 서버 URL: **https://workfolders.contoso.com**  
  
9. 확인 페이지에 응용 프로그램을 게시하는 Windows PowerShell 명령이 표시됩니다. **게시**를 클릭합니다.  
  
10. **결과** 페이지에 응용 프로그램이 게시되었다고 표시될 것입니다.
    >[!NOTE]
    > 여러 클라우드 폴더 서버가 있는 경우, 각 클라우드 폴더 서버에 대해 클라우드 폴더 웹 응용 프로그램을 게시(1 ~ 10단계 반복)해야 합니다.  
  
다음 단계: [AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포: 5단계, 클라이언트 설치](deploy-work-folders-adfs-step5.md)  
  
## <a name="see-also"></a>참고 항목  
[클라우드 폴더 개요](Work-Folders-Overview.md)  
  

