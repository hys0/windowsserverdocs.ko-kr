---
title: AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포 개요
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
ms.assetid: ea19f0f0-6cc0-4322-b387-c0873f7795ad
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.openlocfilehash: 40cc953ce7393781497d957fc8e6690c5c9abc0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365917"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-overview"></a>AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 섹션의 항목에서는 AD FS(Active Directory Federation Services) 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 배포하는 방법에 대한 지침을 제공합니다. 이 지침은 온-프레미스 또는 인터넷을 통해 클라우드 폴더를 사용하여 즉시 시작할 수 있는 클라이언트 컴퓨터가 포함된 완전하게 작동하는 클라우드 폴더 설치를 만들 수 있도록 설계되었습니다.  
  
클라우드 폴더는 정보 작업자들이 디바이스 간에 작업 파일을 동기화할 수 있도록 Windows Server 2012 R2에 도입된 구성 요소입니다. 클라우드 폴더에 대한 자세한 내용은 [클라우드 폴더 개요](Work-Folders-Overview.md)를 참조하세요.  
  
사용자가 인터넷을 통해 자신의 클라우드 폴더를 동기화할 수 있도록 하려면 외부에서 인터넷을 통해 클라우드 폴더를 사용할 수 있도록 역방향 프록시를 통해 클라우드 폴더를 게시해야 합니다. AD FS에 포함된 웹 응용 프로그램 프록시는 역방향 프록시 기능을 제공하는 데 사용할 수 있는 옵션 중 하나입니다. 웹 응용 프로그램 프록시는 모든 디바이스 사용자가 회사 네트워크 외부에서도 클라우드 폴더에 액세스할 수 있도록 AD FS를 사용하여 클라우드 폴더 웹 응용 프로그램에 대한 액세스를 미리 인증합니다. 

> [!NOTE]
>   이 섹션에서는 Windows Server 2016 환경에 대한 지침을 다룹니다. Windows Server 2012 R2를 사용하는 경우 [Windows Server 2012 R2 instructions(Windows Server 2012 R2 지침)](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx)을 따르세요.
  
다음 항목에서는 다음과 같은 정보를 제공합니다.  
  
-   Windows Server 사용자 인터페이스를 통해 AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 설치하고 배포하는 방법에 대한 단계별 지침. 이 지침에서는 자체 서명된 인증서를 사용하여 간단한 테스트 환경을 설정하는 방법을 설명합니다. 그런 다음 테스트 예제를 가이드로 사용하여 공개적으로 신뢰할 수 있는 인증서를 사용하는 프로덕션 환경을 만들 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 항목의 절차 및 예제를 수행하려면 다음과 같은 구성 요소가 필요합니다.  
  
-   여러 파일 서버를 사용할 때 PC 및 디바이스에서 올바른 파일 서버를 자동으로 참조할 수 있도록 지원하는 Windows Server 2012 R2의 스키마 확장이 포함된 Active Directory® Domain Services 포리스트. 포리스트에서 DNS를 사용하도록 설정하는 것이 좋지만 필수 사항은 아닙니다.  
  
-   도메인 컨트롤러: AD DS 역할을 사용 하도록 설정 하 고 도메인 (테스트 예: contoso.com)으로 구성 된 서버입니다.  
  
    Workplace Join에 사용할 디바이스를 등록하려면 Windows Server 2012 R2 이상을 실행하는 도메인 컨트롤러가 필요합니다. Workplace Join을 사용하지 않으려면 도메인 컨트롤러에서 Windows Server 2012를 실행해도 됩니다.  
  
-   도메인(예: contoso.com)에 가입되어 있고 Windows Server 2016을 실행하는 서버 두 대. 한 서버는 AD FS에 사용되고 다른 서버는 클라우드 폴더에 사용됩니다.  
  
-   도메인에 가입되지 않았고 Windows Server 2016을 실행하는 서버 한 대. 이 서버는 웹 응용 프로그램 프록시를 실행할 것이며, 네트워크 도메인(예: contoso.com)에 사용할 네트워크 카드와 외부 네트워크에 사용할 네트워크 카드가 설치되어 있어야 합니다.  
  
-   도메인에 가입되어 있고 Windows 7 이상을 실행하는 컴퓨터 한 대.  
  
-   도메인에 가입되지 않았고 Windows 7 이상을 실행하는 컴퓨터 한 대.  
  
이 가이드에서 다루는 테스트 환경의 경우 다음 다이어그램에 표시된 토폴로지가 있어야 합니다. 컴퓨터는 실제 컴퓨터도 되고 VM(가상 컴퓨터)도 됩니다. 
  
![인터넷, DMZ 및 Contoso 네트워크 세그먼트를 보여 주는 다이어그램. 인터넷 세그먼트에서 다음을 수행 합니다. Client2 DMZ에서: WAP 서버 Contoso 세그먼트에서 다음을 수행 합니다. 클라우드 폴더 서버, 도메인 컨트롤러, AD FS 서버, Client1](media/deploy-work-folders-adfs/WF_ADFS_WAP_Diagram.png)

## <a name="deployment-overview"></a>배포 개요  
이 항목 그룹에서는 테스트 환경에 AD FS, 웹 응용 프로그램 프록시 및 클라우드 폴더를 설치하는 단계별 예제를 연습하겠습니다. 구성 요소는 다음 순서로 설치됩니다.  
  
1.  AD FS  
  
2.  클라우드 폴더  
  
3.  웹 응용 프로그램 프록시  
  
4.  도메인에 가입된 워크스테이션 및 도메인에 가입되지 않은 워크스테이션  
  
또한 Windows PowerShell 스크립트를 사용하여 자체 서명된 인증서를 만들겠습니다.  
  
## <a name="deployment-steps"></a>배포 단계  
Windows Server 사용자 인터페이스를 사용하여 배포를 수행하려면 다음 항목의 단계를 따르세요.  
  
-   [ AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 1 단계, AD FS 설정 @ no__t-0  
  
-   [ AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 2 단계 AD FS 구성 후 작업 @ no__t-0  
  
-   [ AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 3 단계, 클라우드 폴더 설정 @ no__t-0  
  
-   [ AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 4 단계, 웹 응용 프로그램 프록시 설정 @ no__t-0  
  
-   [ AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 5 단계, 클라이언트 설정 @ no__t-0  

## <a name="see-also"></a>관련 항목  
[클라우드 폴더 개요](Work-Folders-Overview.md)  
[클라우드 폴더 구현 디자인](Plan-Work-Folders.md)  
[클라우드 폴더 배포](Deploy-Work-Folders.md)  
  

