---
title: BranchCache 배포 안내서
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: lizross
author: eross-msft
ms.openlocfilehash: df6287f35c3fbf397df3b4d61812db3b14f3ce38
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318513"
---
# <a name="branchcache-deployment-guide"></a>BranchCache 배포 안내서

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016의 BranchCache를 배포 하는 방법에 알아보려면이 가이드를 사용할 수 있습니다.  
  
이 항목 외에도이 가이드는 다음 섹션을 포함합니다.  
  
-   [BranchCache 디자인 선택](../../branchcache/plan/Choosing-a-BranchCache-Design.md)  
  
-   [BranchCache 배포](../../branchcache/deploy/Deploy-BranchCache.md)  
  
## <a name="branchcache-deployment-overview"></a>BranchCache 배포 개요

BranchCache는 Windows Server 2016, Windows Server의 일부 버전에 포함 되어 있는 광역 네트워크 (WAN) 대역폭 최적화 기술&reg; 2012 R2, Windows Server&reg; 2012, Windows Server&reg; 2008 r 2와 관련 된 Windows 클라이언트 운영 체제입니다.  
  
WAN 대역폭을 최적화하기 위해 BranchCache는 본사 콘텐츠 서버의 콘텐츠를 복사하여 지점 위치에서 캐시합니다. 따라서 지점의 클라이언트 컴퓨터에서 WAN을 통하지 않고 로컬로 콘텐츠에 액세스할 수 있습니다.  
  
콘텐츠 중 하나에 Windows Server 2016의 BranchCache 기능을 실행 하는 서버, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2-지점에서 캐시 또는 Windows 10을 실행 하는 클라이언트 컴퓨터에 콘텐츠 캐시 종속성 경우 서버가 사용할 수 있는 지점에&reg;, Windows&reg; 8.1, Windows 8 또는 Windows 7&reg; 합니다.  
  
클라이언트 컴퓨터를 요청 하 고 후 주 사무실 이나 클라우드 데이터 센터에서 콘텐츠를 받는 지점에서 콘텐츠가 캐시 되며, 같은 지점의 다른 컴퓨터 WAN 링크를 통해 콘텐츠 서버에 연결 하는 대신 로컬로 콘텐츠를 가져올 수 있습니다.  
  
**BranchCache 배포의 이점**  
  
BranchCache 캐시 파일, 웹 및 애플리케이션 콘텐츠 지점 사무실 위치에서 클라이언트 컴퓨터의 속도가 느린 WAN 연결을 통해 콘텐츠를 액세스 하는 대신 로컬 영역 네트워크 (LAN)를 사용 하 여 데이터 액세스를 허용 합니다.  
  
BranchCache는 WAN 트래픽 및 지점 사용자가 네트워크에서 파일을 열에 필요한 시간을 줄일 수 있습니다.  BranchCache에는 항상 가장 최근의 데이터와 사용자가 제공 하 고 호스트 캐시 서버 및 클라이언트 컴퓨터에서 캐시를 암호화 하 여 콘텐츠에 대 한 보안 보호 합니다.  
  
### <a name="what-this-guide-provides"></a>이 가이드에 포함된 내용  
이 배포 가이드를 사용 하면 다음과 같은 모드에서 BranchCache를 배포할 수 있습니다.  
  
-   분산된 캐시 모드입니다. 이 모드에서는 지점의 클라이언트 컴퓨터 본사 또는 클라우드 콘텐츠 서버에서 콘텐츠를 다운로드 하 고 같은 지점의 다른 컴퓨터에 대 한 콘텐츠를 캐시 합니다. 분산된 캐시 모드는 지사에 서버 컴퓨터를 필요 하지 않습니다.  
  
-   호스트 캐시 모드입니다. 이 모드에서는 분기 office 클라이언트 컴퓨터 다운로드 본사 또는 클라우드 콘텐츠 서버와 호스트 캐시 서버에서 콘텐츠는 클라이언트에서 콘텐츠를 검색합니다. 호스트 캐시 서버는 다른 클라이언트 컴퓨터에 대 한 콘텐츠를 캐시합니다.  
  
이 가이드는 또한 세 가지 유형의 콘텐츠 서버를 배포 하는 방법에 지침을 제공 합니다. 분기 office 클라이언트 컴퓨터에서 다운로드 된 원본 콘텐츠를 포함 하는 콘텐츠 서버 및 하나 이상의 콘텐츠 서버 모드에서 BranchCache를 배포 해야 합니다. 콘텐츠 서버 유형은 다음과 같습니다.  
  
-   **웹 콘텐츠 서버의 서버 기반**합니다. 다음 콘텐츠 서버는 HTTP 및 HTTPS 프로토콜을 사용 하 여 BranchCache 클라이언트 컴퓨터에 콘텐츠를 보냅니다. 다음 콘텐츠 서버를 지 원하는 BranchCache Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 버전을 실행 해야 하며 BranchCache 기능이 설치 됩니다.  
  
-   **BITS 기반 응용 프로그램 서버**합니다. 다음 콘텐츠 서버는 BITS Background Intelligent Transfer Service ()를 사용 하 여 BranchCache 클라이언트 컴퓨터에 콘텐츠를 보냅니다. 다음 콘텐츠 서버를 지 원하는 BranchCache Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 버전을 실행 해야 하며 BranchCache 기능이 설치 됩니다.  
  
-   **파일 서버 기반 콘텐츠 서버**합니다. 다음 콘텐츠 서버를 지 원하는 BranchCache Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 버전을 실행 해야 하 고 어떤 파일 서비스에 서버 역할 설치 됩니다. 또한는 **네트워크 파일용 BranchCache** 파일 서비스 서버 역할의 역할 서비스를 설치 하 고 구성 해야 합니다. 다음 콘텐츠 서버는 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 BranchCache 클라이언트 컴퓨터에 콘텐츠를 보냅니다.  
  
자세한 내용은 참조 [BranchCache에 대 한 운영 체제 버전](https://technet.microsoft.com/windows-server-docs/networking/branchcache/branchcache#a-namebkmkosaoperating-system-versions-for-branchcache)합니다.  
  
### <a name="branchcache-deployment-requirements"></a>BranchCache 배포 요구 사항

다음은이 가이드를 사용 하 여 BranchCache를 배포 하기 위한 요구 사항입니다.  
  
-   **파일 및 웹 콘텐츠 서버** BranchCache 기능을 제공 하는 다음 운영 체제 중 하나를 실행 해야 합니다: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2입니다. Windows 8 및 이후 클라이언트 계속 만들 수 있지만 Windows Server 2008 r 2를 실행 하는 콘텐츠 서버에 액세스할 때 BranchCache에서 혜택을 볼 새 청크 및 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012의 기술 해시를 사용 합니다.  
  
-   **클라이언트 컴퓨터** 수 있도록 하는 Windows 10, Windows 8.1 또는 Windows 8 실행 해야 가장 최근의 배포 모델 및 청크 및 Windows Server 2012에서 도입 된 향상 된 기능 해시를 사용 합니다.  
  
-   **호스트 캐시 서버** 배포의 향상 된 사용 하 고이 문서에서 설명 하는 기능을 확장할 수 있도록 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행 해야 합니다.  이러한 운영 체제 중 하나를 실행 하는 컴퓨터는 Windows 7을 실행 하는 클라이언트 컴퓨터에서 사용할 수 있지만 작업을 수행할 수는 호스트 캐시 서버 계속으로 구성 된, 적합 한에 대 한 보안 TLS (전송 계층), Windows Server 2008 R2 및 Windows 7에 설명 된 대로 인증서를 장착할 수 해야 [BranchCache 배포 가이드](https://technet.microsoft.com/library/ee649232.aspx)합니다.  
  
-   **Active Directory 도메인** 그룹 정책 및 호스트 캐시 자동 검색을 활용 하는 데 필요 하지만 도메인에서 BranchCache를 사용할 필요가 없습니다.  Windows PowerShell을 사용 하 여 개별 컴퓨터를 구성할 수 있습니다. 또한 없는 도메인 컨트롤러에 Windows Server 2012 이상을 실행 새 BranchCache 그룹 정책 설정을 사용 하는 데 필요한 이전 버전의 운영 체제를 실행 하는 도메인 컨트롤러에 BranchCache 관리 템플릿을 가져오거나 Windows 10, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows 8 또는 Windows Server 2012를 실행 하는 다른 컴퓨터에 원격으로 그룹 정책 개체를 작성할 수 있습니다.

-   **Active Directory 사이트** 호스트 캐시 서버는 자동으로 검색 하는 범위를 제한 하는 데 사용 됩니다.  호스트 캐시 서버를 자동으로 검색 하려면 클라이언트와 서버 컴퓨터는 동일한 사이트에 속해야 합니다. BranchCache는 클라이언트와 서버에 미치는 영향을 최소화 하도록 설계 되었습니다 및에서는 해당 운영 체제를 실행 하는 데 필요한 것 이외의 추가 하드웨어 요구 사항을 적용 하지 않습니다.  

**BranchCache 기록 및 설명서**

BranchCache는 Windows 7에 처음 도입 된&reg; 및 Windows Server&reg; 2008 R2, Windows Server 2012, Windows 8 이상의 운영 체제에서 향상 되었습니다.

> [!NOTE]
> Windows Server 2016 이외의 운영 체제에서 BranchCache를 배포 하는 경우 다음 설명서 리소스를 사용할 수 있습니다.
> 
> - Windows 8, Windows 8.1, Windows Server 2012 및 Windows Server 2012 r 2의 BranchCache에 대 한 정보를 참조 하십시오. [BranchCache 개요](https://technet.microsoft.com/library/hh831696.aspx)합니다.  
> - Windows 7 및 Windows Server 2008 r 2의 BranchCache에 대 한 정보를 참조 하십시오.  [BranchCache에 대 한 Windows Server 2008 R2](https://technet.microsoft.com/library/dd996634.aspx)합니다.  
  


