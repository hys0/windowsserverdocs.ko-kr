---
title: AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포 - 5단계, 클라이언트 설치
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: f168292b-0dbc-44b9-965f-d480e5134a0c
ms.openlocfilehash: 44e3ab06ac29d770ad47b43db5eba06f0eb08a60
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447789"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-5-set-up-clients"></a>AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 5 단계 설정 클라이언트

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 AD FS(Active Directory Federation Services) 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 배포하는 다섯 번째 단계를 설명합니다. 이 과정의 다른 단계는 다음 항목에서 찾을 수 있습니다.  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 개요](deploy-work-folders-adfs-overview.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 1 단계, AD FS 설정](deploy-work-folders-adfs-step1.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 2에서 AD FS 구성 후 작업](deploy-work-folders-adfs-step2.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 3, 작업 폴더 설정](deploy-work-folders-adfs-step3.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 4 단계, 웹 응용 프로그램 프록시 설정](deploy-work-folders-adfs-step4.md)  
  
다음 절차에 따라 도메인에 가입된 Windows 클라이언트 및 도메인에 가입되지 않은 Windows 클라이언트를 설치합니다. 이러한 클라이언트를 사용하여 클라이언트의 클라우드 폴더 간에 파일이 올바르게 동기화되고 있는지 테스트할 수 있습니다.  
  
## <a name="set-up-a-domain-joined-client"></a>도메인에 가입된 클라이언트 설치  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS 및 클라우드 폴더 인증서 설치  
앞에서 만든 AD FS 및 클라우드 폴더 인증서를 도메인에 가입된 클라이언트 컴퓨터의 로컬 컴퓨터 인증서 저장소에 설치해야 합니다.  
  
지금 여러분이 설치하는 것은 신뢰할 수 있는 루트 인증 기관 인증서 저장소의 게시자까지 추적할 수 없는 자체 서명된 인증서이기 때문에 해당 스토어에도 인증서를 복사해야 합니다.  
  
인증서를 설치하려면 다음 단계를 수행합니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  **MMC**를 입력합니다.  
  
3.  **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
4.  **사용 가능한 스냅인** 목록에서 **인증서**를 선택한 다음 **추가**를 클릭합니다. 인증서 스냅인 마법사가 시작됩니다.  
  
5.  **컴퓨터 계정**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 를 선택하고 **마침**을 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  Console Root\Certificates\(Local Computer)\Personal\Certificates 폴더를 확장합니다.  
  
9. **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **가져오기**를 클릭합니다.  
  
10. AD FS 인증서가 들어 있는 폴더를 찾은 후 마법사의 지침에 따라 파일을 가져와서 인증서 저장소에 배치합니다.  
  
11. 9 및 10단계를 반복하되, 이번에는 클라우드 폴더 인증서를 찾아서 가져옵니다.  
  
12. Console Root\Certificates\(Local Computer)\Trusted Root Certification Authorities\Certificates 폴더를 확장합니다.  
  
13. **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **가져오기**를 클릭합니다.  
  
14. AD FS 인증서가 들어 있는 폴더를 찾은 후 마법사의 지침에 따라 파일을 가져와서 신뢰할 수 있는 루트 인증 기관 저장소에 배치합니다.  
  
15. 13 및 14단계를 반복하되, 이번에는 클라우드 폴더 인증서를 찾아서 가져옵니다.  
  
### <a name="configure-work-folders-on-the-client"></a>클라이언트에서 클라우드 폴더 구성  
클라이언트 컴퓨터에서 클라우드 폴더를 구성하려면 다음 단계를 따릅니다.  
  
1. 클라이언트 컴퓨터에서 **제어판**을 열고 **클라우드 폴더**를 클릭합니다.  
  
2. **클라우드 폴더 설정**을 클릭합니다.  
  
3. 에 **회사 메일 주소를 입력** 페이지에서 사용자의 전자 메일 주소를 입력 (예를 들어 user@contoso.com) 또는 클라우드 폴더 URL (테스트 예제에서는 https:\//workfolders.contoso.com), 를클릭하고 **다음**합니다.  
  
4. 사용자가 회사 네트워크에 연결된 경우 Windows 통합 인증을 통해 인증이 수행됩니다. 사용자가 회사 네트워크에 연결되지 않은 경우 ADFS(OAuth)를 통해 인증이 수행되고 사용자는 자격 증명을 입력해야 합니다. 자격 증명을 입력하고 **확인**을 클릭합니다.  
  
5. 사용자가 인증되면 **클라우드 폴더 소개** 페이지가 표시되고, 원한다면 이 페이지에서 클라우드 폴더 디렉터리 위치를 변경할 수 있습니다. **다음**을 클릭합니다.  
  
6. 클라우드 폴더에 설정한 보안 정책이 나열되는 **보안 정책** 페이지가 표시됩니다. **다음**을 클릭합니다.  
  
7. 클라우드 폴더가 PC와 동기화를 시작했다는 내용의 메시지가 표시됩니다. **닫기**를 클릭합니다.  
  
8. **클라우드 폴더 관리** 페이지에 서버에서 사용 가능한 공간, 동기화 상태 등이 표시됩니다. 필요한 경우 여기서 자격 증명을 다시 입력할 수 있습니다. 창을 닫습니다.  
  
9. 클라우드 폴더가 자동으로 열립니다. 이 폴더에 콘텐츠를 추가하여 디바이스 간에 동기화할 수 있습니다.  
  
    테스트 예제에서는 클라우드 폴더에 테스트 파일을 추가하겠습니다. 도메인에 가입되지 않은 컴퓨터에서 클라우드 폴더를 설정한 후에는 각 컴퓨터의 클라우드 폴더 간에 파일을 동기화할 수 있습니다.  
  
## <a name="set-up-a-non-domain-joined-client"></a>도메인에 가입되지 않은 클라이언트 설치  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS 및 클라우드 폴더 인증서 설치  
도메인에 가입된 컴퓨터에 사용한 것과 동일한 절차에 따라 도메인에 가입되지 않은 컴퓨터에 AD FS 및 클라우드 폴더 인증서를 설치합니다.  
  
### <a name="update-the-hosts-file"></a>호스트 파일 업데이트  
도메인에 가입되지 않은 클라이언트의 호스트 파일을 테스트 환경에 사용할 수 있도록 업데이트해야 합니다. 클라우드 폴더의 공용 DNS 레코드가 하나도 없기 때문입니다. 호스트 파일에 다음 항목을 추가합니다.  
  
-  workfolders.domain  
  
-  AD FS service name.domain  
  
-  enterpriseregistration.domain  
  
테스트 예제에서는 다음 값을 사용합니다.  
  
-  **10.0.0.10 workfolders.contoso.com**  
  
-  **10.0.0.10 blueadfs.contoso.com**  
  
-  **10.0.0.10 enterpriseregistration.contoso.com**  
  
### <a name="configure-work-folders-on-the-client"></a>클라이언트에서 클라우드 폴더 구성  
도메인에 가입된 컴퓨터에 사용한 것과 동일한 절차에 따라 도메인에 가입되지 않은 컴퓨터에서 클라우드 폴더를 구성합니다.  
  
이 클라이언트에서 새 클라우드 폴더가 열리면 도메인에 가입된 컴퓨터의 파일이 도메인에 가입되지 않은 컴퓨터에도 이미 동기화된 것을 볼 수 있습니다. 이제부터 이 폴더에 콘텐츠를 추가하여 디바이스 간에 동기화할 수 있습니다.  
  
이것으로 Windows Server UI를 통해 클라우드 폴더, AD FS 및 웹 응용 프로그램 프록시를 배포하는 절차를 마치겠습니다.  
  
## <a name="see-also"></a>관련 항목  
[클라우드 폴더 개요](Work-Folders-Overview.md)  
  

