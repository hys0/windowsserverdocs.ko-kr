---
title: BranchCache 배포 가이드
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e7aa35260213a8a236b7c27cf74e36692438cd2a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-deployment-guide"></a>BranchCache 배포 가이드

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016에 BranchCache 배포 하는 방법을 자세히 알아보려면이 가이드를 사용할 수 있습니다.  
  
이 항목 외에이 가이드는 다음 섹션 포함 되어 있습니다.  
  
-   [BranchCache 디자인을 선택](../../branchcache/plan/Choosing-a-BranchCache-Design.md)  
  
-   [BranchCache 배포](../../branchcache/deploy/Deploy-BranchCache.md)  
  
## <a name="branchcache-deployment-overview"></a>BranchCache 배포 개요

BranchCache은 Windows Server, Windows Server 2016의 일부 버전에 포함 되어 있는 다양 한 영역 (네트워크) 대역폭 최적화 기술&reg; Windows Server 2012 r 2&reg; Windows Server 2012&reg; 2008 r 2와 관련된 Windows 클라이언트 운영 체제입니다.  
  
WAN 대역폭을 최적화 하기 위해 BranchCache 본사 콘텐츠 서버에서 콘텐츠를 복사 하 고 허용 클라이언트 wan가 대신 로컬 콘텐츠에 액세스 하는 지점에 컴퓨터 콘텐츠 지점 위치를 캐시 합니다.  
  
콘텐츠에서의 Windows Server 2016 BranchCache 기능을 실행 하는 서버, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2-분기 사무실에서 캐시 또는 Windows 10을 실행 하는 클라이언트 컴퓨터에 콘텐츠 캐시 지점에서 사용할 수 없는 서버 사항이, 경우&reg;, Windows&reg; 8.1, Windows 8 또는 Windows 7&reg; 합니다.  
  
클라이언트 컴퓨터를 요청 하 고 주요 office 스토어 또는 클라우드 데이터 센터에서 콘텐츠를 받는 및 콘텐츠 지점에서 캐시 된 후 같은 지점에서 다른 컴퓨터 WAN 링크를 통해 콘텐츠 서버에 연결 하는 것이 아니라 로컬 콘텐츠를 받을 수 있습니다.  
  
**BranchCache 배포할 때의 이점**  
  
BranchCache 캐시 파일, 웹 및 응용 프로그램 콘텐츠 지점 위치를 클라이언트 슬로우 WAN 연결을 통해의 콘텐츠에 액세스 하는 대신 (lan)를 사용 하 여 데이터에 액세스 하도록 허용 합니다.  
  
BranchCache WAN 교통량과 지점 사용자를 네트워크에 있는 파일을 열려면 해야 하는 시간을 줄일 수 있습니다.  클라이언트 컴퓨터와 여 호스팅된 캐시 서버에서 캐시 암호화 하 여 콘텐츠가 보안 보호 및 BranchCache 항상 가장 최근에 데이터를 사용자에 게 제공 합니다.  
  
### <a name="what-this-guide-provides"></a>이 가이드에서는  
이 배포 가이드 BranchCache 다음 모드에 배포할 수 있습니다.  
  
-   분산된 캐시 모드입니다. 이 모드에서는 지점 클라이언트 컴퓨터 본사 또는 클라우드 콘텐츠 서버에서 콘텐츠를 다운로드 하 고 같은 지사에서 다른 컴퓨터에 대 한 콘텐츠를 캐시 합니다. 분산된 캐시 모드 서버 컴퓨터 지점에서 필요 하지 않습니다.  
  
-   호스트 캐시 모드입니다. 이 모드에서는 분기 office 클라이언트 컴퓨터 다운로드 본사 또는 클라우드 콘텐츠 서버 및 호스트 캐시 서버에서 콘텐츠는 클라이언트에서 콘텐츠를 검색합니다. 호스트 캐시 서버 클라이언트 다른 컴퓨터에 대 한 콘텐츠를 캐시합니다.  
  
이 가이드 세 가지 유형의 콘텐츠 서버를 배포 하는 방법에 대해 설명 수도 있습니다. 콘텐츠 서버 지점 클라이언트 컴퓨터, 하 여 다운로드 한 소스 콘텐츠가 포함 하 고 BranchCache 모드에서 배포 하는 하나 이상의 콘텐츠 서버 필요 합니다. 콘텐츠 서버 유형은 다음과 같습니다.  
  
-   **웹 콘텐츠 서버 서버 기반**합니다. 이러한 콘텐츠 서버 BranchCache HTTPS 및 HTTP 프로토콜을 사용 하는 클라이언트 컴퓨터에 콘텐츠를 보냅니다. 이러한 콘텐츠 서버 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 지원 버전을 BranchCache 실행 중 이어야 합니다 및 시 BranchCache 기능이 설치 되어 있습니다.  
  
-   **비트 기반 응용 프로그램이 서버**합니다. 이러한 콘텐츠 서버를 사용 하 여 지능형 전송 BITS 백그라운드 서비스 () BranchCache 클라이언트 컴퓨터에 콘텐츠를 보냅니다. 이러한 콘텐츠 서버 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 지원 버전을 BranchCache 실행 중 이어야 합니다 및 시 BranchCache 기능이 설치 되어 있습니다.  
  
-   **파일 서버 기반 콘텐츠 서버**합니다. 이러한 콘텐츠 서버 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 지원 버전을 BranchCache 실행 중 이어야 합니다 및 파일 서비스는 시 서버 역할 설치 되어 있습니다. 또한는 **네트워크 파일에 대 한 BranchCache** 파일 서비스 거부의 역할 서비스를 설치 하 고 구성 해야 합니다. 이러한 콘텐츠 서버 BranchCache 블록 SMB (서버 메시지) 프로토콜을 사용 하는 클라이언트 컴퓨터에 콘텐츠를 보냅니다.  
  
자세한 내용은 참조 [BranchCache에 대 한 운영 체제 버전](https://technet.microsoft.com/en-us/windows-server-docs/networking/branchcache/branchcache#a-namebkmkosaoperating-system-versions-for-branchcache)합니다.  
  
### <a name="branchcache-deployment-requirements"></a>BranchCache 배포 요구 사항

다음은 BranchCache이이 가이드를 사용 하 여 배포를 위해 요구 사항입니다.  
  
-   **파일 및 웹 콘텐츠 서버** BranchCache 기능을 제공 하는 다음 운영 체제 중 하나를 실행 해야: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2. Windows 8 및 이후 클라이언트 계속 향상할 수 없는 있지만 Windows Server 2008 R2 실행 하는 콘텐츠 서버에 액세스할 때 BranchCache에서 혜택 볼 새로운 청크 및 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 기술을 해시 사용 합니다.  
  
-   **클라이언트 컴퓨터** 하도록 Windows 10, Windows 8.1 또는 Windows 8 실행 중 이어야 합니다 가장 최근 배포 모델 청크 및 해시 도입 된 것과 Windows Server 2012 향상 된 기능을 사용 합니다.  
  
-   **캐시 서버 호스트** 사용 배포 개선 사항 및 기능이이 문서에서 설명한 크기가 조정 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행 중 이어야 합니다.  Windows 7을 실행 하는 클라이언트 컴퓨터를 사용할 수 있지만 이렇게 하 여 호스팅된 캐시 서버 수 지속적으로 다음 운영 체제 중 하나를 실행 하는 컴퓨터 구성, 적절 한에 대 한 Transport Layer Security TLS (), Windows Server 2008 R2 및 Windows 7에 설명 된 대로 되는 인증서를 설치 해야 [BranchCache 배포 가이드](https://technet.microsoft.com/en-us/library/ee649232.aspx)합니다.  
  
-   **Active Directory 도메인** 호스트 캐시 자동 검색 및 그룹 정책을 활용 하는 데 필요한 하지만 도메인 BranchCache을 사용할 필요가 없습니다.  Windows PowerShell를 사용 하 여 개별 컴퓨터를 구성할 수 있습니다. 또한 유효 하지는 도메인 컨트롤러 이상을 실행 하 고 Windows Server 2012 새로운 BranchCache 그룹 정책 설정을; 활용 하는 데 필요한 이전 운영 체제를 실행 하는 도메인 컨트롤러에 BranchCache 관리 템플릿 가져오거나 Windows 10, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows 8 또는 Windows Server 2012를 실행 하는 다른 컴퓨터에서 원격 그룹 정책 개체를 작성할 수 있습니다.

-   **Active Directory 사이트** 자동으로 검색 되는 호스트 캐시 서버 범위를 제한 하는 데 사용 됩니다.  호스트 캐시 서버를 자동으로 검색 하는 클라이언트 및 서버 컴퓨터 같은 사이트에 속해야 합니다. BranchCache는 클라이언트 및 서버에 미치는 영향을 최소화 하는 설계 되었으며 이상의 자녀가 해당 운영 체제를 실행 하는 데 필요한 추가 하드웨어 요구 사항을 부과 되지 않습니다.  

**설명서 및 BranchCache 기록**

Windows 7에서 처음으로 BranchCache 도입 되었습니다&reg; 및 Windows Server&reg; 2008 R2, Windows Server 2012, Windows 8 및 이상 운영 체제에서 개선 되었습니다.

> [!NOTE]
> Windows Server 2016이 아닌는 운영 체제에 BranchCache을 배포 하는 경우 다음과 같은 설명서 리소스를 사용할 수 있습니다.
> 
> - Windows 8, Windows 8.1, Windows Server 2012 및 Windows Server 2012 r 2에 BranchCache에 대 한 정보를 참조 하세요. [BranchCache 개요](https://technet.microsoft.com/en-us/library/hh831696.aspx)합니다.  
> - Windows 7 및 Windows Server 2008 R2 BranchCache에 대 한 내용은 [BranchCache에 대 한 Windows Server 2008 R2](https://technet.microsoft.com/en-us/library/dd996634.aspx)합니다.  
  


