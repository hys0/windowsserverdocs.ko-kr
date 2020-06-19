---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: 클라우드 폴더 개요
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 06/15/2020
description: 작업 폴더 개요-사용자가 Pc 및 장치에서 작업 파일에 액세스할 수 있는 일관 된 방법을 제공 하는 Windows Server의 서버 역할입니다.
ms.openlocfilehash: 4e670d61729d35ee9569b09e91ef5a953961241e
ms.sourcegitcommit: 568b924d32421256f64abfee171304f1daf320d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85070093"
---
# <a name="work-folders-overview"></a>클라우드 폴더 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

이 항목에서는 사용자가 Pc 및 장치에서 작업 파일에 액세스할 수 있는 일관 된 방법을 제공 하는 Windows Server를 실행 하는 파일 서버에 대 한 역할 서비스인 클라우드 폴더에 대해 설명 합니다.  
  
Windows 10, Windows 7 또는 Android 또는 iOS 장치에서 클라우드 폴더를 다운로드 하거나 사용 하려는 경우 다음을 참조 하세요.

- [Windows 10 용 클라우드 폴더](https://support.microsoft.com/help/12370/windows-10-work-folders)
- [Windows 7용 클라우드 폴더(64비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42558)
- [Windows 7용 클라우드 폴더(32비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42559)
- [IOS 용 클라우드 폴더](https://itunes.apple.com/app/work-folders/id950878067)
- [Android 용 클라우드 폴더](https://play.google.com/store/apps/details?id=com.microsoft.workfolders)

## <a name="role-description"></a>역할 설명

 클라우드 폴더를 통해 사용자는 개인용 컴퓨터 및 디바이스에 작업 파일을 저장하고 여기에 액세스할 수 있습니다. 이를 회사 PC 외의 BYOD(bring-your-own device)라고도 합니다. 사용자는 작업 파일을 저장하고 어디에서나 액세스할 수 있는 편리한 위치를 얻을 수 있습니다. 조직은 중앙에서 관리 되는 파일 서버에 파일을 저장하고 선택적으로 사용자 디바이스 정책(예: 암호화 및 잠금 화면 암호)을 지정하여 회사 데이터에 대한 제어를 유지합니다.  
  
 폴더 리디렉션, 오프라인 파일 및 홈 폴더의 기존 배포를 사용 하 여 클라우드 폴더를 배포할 수 있습니다. 클라우드 폴더는 서버에서 *동기화 공유*라는 폴더에 사용자 파일을 저장 합니다. 사용자 데이터를 이미 포함 하는 폴더를 지정할 수 있습니다. 이렇게 하면 서버 및 데이터를 마이그레이션하지 않고 기존 솔루션을 즉시 단계적으로 중단 작업 폴더를 채택할 수 있습니다.  
  
## <a name="practical-applications"></a>유용한 팁

 관리자는 회사 폴더를 사용 하 여 사용자에 게 회사 파일에 대 한 액세스 권한을 제공 하 고 중앙 집중화 된 저장소와 조직의 데이터에 대 한 제어를 유지할 수 있습니다. 클라우드 폴더에 대 한 몇 가지 특정 응용 프로그램은 다음과 같습니다.  
  
-   사용자의 회사 및 개인용 컴퓨터 및 장치에서 작업 파일에 대 한 단일 액세스 지점을 제공 합니다.  
  
-   오프 라인으로 작업 파일에 액세스 한 다음 PC 또는 장치 다음에 인터넷 또는 인트라넷 연결이 있는 경우 중앙 파일 서버와 동기화  
  
-   폴더 리디렉션, 오프라인 파일 및 홈 폴더의 기존 배포를 사용 하 여 배포  
  
-   파일 분류 및 폴더 할당량과 같은 기존 파일 서버 관리 기술을 사용 하 여 사용자 데이터 관리  
  
-   사용자의 Pc 및 장치에서 클라우드 폴더를 암호화 하 고 잠금 화면 암호를 사용 하도록 지시 하는 보안 정책 지정  
  
-   클라우드 폴더에 장애 조치 (Failover) 클러스터링을 사용 하 여 고가용성 솔루션 제공  
  
## <a name="important-functionality"></a>중요 기능

 클라우드 폴더에는 다음과 같은 기능이 포함 되어 있습니다.  
  
| 기능 | 가용성 | Description |  
| ------------------- | ------------------ | ----------------- |  
| 서버 관리자의 클라우드 폴더 역할 서비스 | Windows Server 2019, Windows Server 2016 또는 Windows Server 2012 R2 | 파일 및 저장소 서비스는 동기화 공유 (사용자의 작업 파일을 저장 하는 폴더)를 설정 하 고, 작업 폴더를 모니터링 하 고, 동기화 공유 및 사용자 액세스를 관리 하는 방법을 제공 합니다. |
| 클라우드 폴더 cmdlet | Windows Server 2019, Windows Server 2016 또는 Windows Server 2012 R2 | 클라우드 폴더 서버를 관리 하기 위한 포괄적인 cmdlet이 포함 된 Windows PowerShell 모듈입니다. |  
| Windows와 클라우드 폴더 통합 | 윈도우 10<p> Windows 8.1<p> Windows RT 8.1<p> Windows 7 (다운로드 필요) | 클라우드 폴더는 Windows 컴퓨터에서 다음과 같은 기능을 제공 합니다.<p> -작업 폴더를 설정 및 모니터링 하는 제어판 항목<br />-클라우드 폴더의 파일에 쉽게 액세스할 수 있도록 하는 파일 탐색기 통합<br />-배터리 수명 및 시스템 성능을 최대화 하는 동시에 중앙 파일 서버와 파일을 전송 하는 동기화 엔진 |
| 장치에 대 한 클라우드 폴더 앱 | Android<p> Apple iPhone 및 iPad® | 인기 있는 장치가 클라우드 폴더의 파일에 액세스할 수 있도록 허용 하는 앱 |  
  
## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능
  
다음 표에서는 클라우드 폴더의 주요 변경 사항 중 일부에 대해 설명 합니다.  
  
| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
| ---------------------------- | --------------------- | ----------------- |
| 향상된 로깅 | Windows Server 2019의 새로운 | 클라우드 폴더 서버의 이벤트 로그를 사용 하 여 동기화 작업을 모니터링 하 고 동기화 세션이 실패 한 사용자를 식별할 수 있습니다. Microsoft-Windows-SyncShare/Operational 이벤트 로그에서 이벤트 ID 4020를 사용 하 여 동기화 세션이 실패 한 사용자를 식별 합니다. Microsoft-Windows-SyncShare/Reporting 이벤트 로그에서 이벤트 ID 7000 및 이벤트 ID 7001를 사용 하 여 동기화 세션 업로드 및 다운로드를 성공적으로 완료 한 사용자를 모니터링 합니다. |
| 성능 카운터 | Windows Server 2019의 새로운 | 다음 성능 카운터가 추가 되었습니다. 다운로드 한 바이트 수/초, 업로드 된 바이트 수/초, 연결 된 사용자, 다운로드 한 파일 수/초, 업로드 한 파일/초, 변경 검색, 들어오는 요청/초 및 미해결 요청 |
| 향상 된 서버 성능 | Windows Server 2019에서 업데이트 됨 | 서버당 더 많은 사용자를 처리 하기 위한 성능이 향상 되었습니다. 서버당 제한은 파일 수 및 파일 변동에 따라 달라 집니다. 서버당 한도를 확인 하려면 사용자가 단계에서 서버에 추가 되어야 합니다. |
| 주문형 파일 액세스 | Windows 10 버전 1803에 추가 됨 | 모든 파일을 보고 액세스할 수 있습니다. PC에 저장 되 고 오프 라인에서 사용할 수 있는 파일을 제어 합니다. 나머지 파일은 항상 표시 되며 PC의 공간을 차지 하지는 않지만 작업 폴더 파일 서버에 연결 하 여 액세스 해야 합니다. |
| Azure AD 응용 프로그램 프록시 지원 | Windows 10 버전 1703, Android, iOS에 추가 됨 | 원격 사용자는 Azure AD 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 서버에서 해당 파일에 안전 하 게 액세스할 수 있습니다. |
| 빠른 변경 복제 | Windows 10 및 Windows Server 2016에서 업데이트 됨 | Windows Server 2012 R2의 경우 파일 변경을 작업 폴더 서버와 동기화하면 클라이언트는 해당 변경에 대해 알리지 않고 업데이트될 때까지 최대 10분을 기다립니다. Windows Server 2016를 사용 하는 경우 클라우드 폴더 서버는 즉시 Windows 10 클라이언트에 알리고 파일 변경 내용이 즉시 동기화 됩니다. 이 기능은 Windows Server 2016의 새로운 기능으로, Windows 10 클라이언트가 필요 합니다. 이전 클라이언트를 사용 하는 경우 또는 작업 폴더 서버가 Windows Server 2012 r 2 인 경우 클라이언트는 변경에 대해 10 분 마다 계속 폴링합니다. |  
| Windows Information Protection와 통합 (WIP) | Windows 10 버전 1607에 추가 됨 | 관리자가 WIP를 배포 하는 경우 작업 폴더는 PC에서 데이터를 암호화 하 여 데이터 보호를 적용할 수 있습니다. 암호화는 Microsoft Intune와 같은 지원 되는 모바일 장치 관리 패키지를 사용 하 여 원격으로 초기화할 수 있는 엔터프라이즈 ID와 연결 된 키를 사용 합니다. | 
  
## <a name="software-requirements"></a>소프트웨어 요구 사항

클라우드 폴더에는 파일 서버와 네트워크 인프라에 대한 다음과 같은 소프트웨어 요구 사항이 있습니다.  
  
-   사용자 파일과의 동기화 공유를 호스팅하기 위한 windows Server 2019, Windows Server 2016 또는 Windows Server 2012 r 2를 실행 하는 서버  
  
-   사용자 파일을 저장하기 위한 NTFS 파일 시스템으로 포맷된 볼륨  
  
-   Windows 7 PC에서 암호 정책을 적용하려면 그룹 정책 암호 정책을 사용해야 합니다. 또한 클라우드 폴더 암호 정책(사용하는 경우)에서 Windows 7 PC를 제외해야 합니다.

-   클라우드 폴더를 호스팅하는 각 파일 서버에 대 한 서버 인증서입니다. 이러한 인증서는 사용자가 신뢰할 수 있는 CA (인증 기관)에서 가져온 것입니다 (이상적으로는 공용 CA).

-   필드 여러 파일 서버를 사용할 때 Pc 및 장치를 올바른 파일 서버에 자동으로 참조 하는 기능을 지원 하기 위해 Windows Server 2012 r 2의 스키마 확장이 포함 된 Active Directory Domain Services 포리스트입니다.  
  
사용자가 인터넷을 통해 동기화할 수 있도록 하려면 다음과 같은 추가 요구 사항을 충족해야 합니다.  
  
-   조직의 역방향 프록시 또는 네트워크 게이트웨이에 게시 규칙을 만들어 인터넷에서 서버에 액세스할 수 있도록 하는 기능  
  
-   필드 공개적으로 등록 된 도메인 이름 및 도메인에 대 한 추가 공용 DNS 레코드를 만들 수 있는 기능  
  
-   (선택 사항) AD FS 인증을 사용할 경우 AD FS(Active Directory Federation Services) 인프라  
  
클라우드 폴더에는 클라이언트 컴퓨터에 대한 다음과 같은 소프트웨어 요구 사항이 있습니다.  
  
-   Pc 및 장치는 다음 운영 체제 중 하나를 실행 해야 합니다.  
  
    -   윈도우 10  
  
    -   Windows 8.1  
  
    -   Windows RT 8.1  
  
    -   Windows 7  
  
    -   Android 4.4 KitKat 이상  
  
    -   iOS 10.2 이상  
  
-   Windows 7 PC에서 다음 Windows 버전 중 하나를 실행해야 합니다.  
  
    -   Windows 7 Professional  
  
    -   Windows 7 Ultimate  
  
    -   Windows 7 Enterprise  
  
-   Windows 7 Pc는 조직의 도메인에 가입 되어 있어야 합니다 (작업 그룹에 가입 될 수 없음).  
  
-   NTFS로 포맷 된 로컬 드라이브에 모든 사용자 파일을 클라우드 폴더에 저장할 수 있는 충분 한 여유 공간이 있어야 하며, 클라우드 폴더가 시스템 드라이브에 있는 경우 기본적으로 6gb의 여유 공간을 추가로 제공 합니다. 클라우드 폴더의 위치는 기본적으로 **%USERPROFILE%\Work Folders**입니다.  
  
     그러나 설정하는 동안 사용자가 위치를 변경할 수 있습니다(NTFS 파일 시스템으로 포맷된 microSD 카드와 USB 드라이브가 지원되는 위치이며, 드라이브가 제거된 경우 동기화가 중지됨).  
  
     개별 파일의 최대 크기는 기본적으로 10GB입니다. 관리자가 파일 서버 리소스 관리자의 할당량 기능을 사용하여 할당량을 구현할 수 있지만 사용자당 스토리지 제한은 없습니다.  
  
-   클라우드 폴더는 클라이언트 가상 컴퓨터의 가상 컴퓨터 상태 롤백을 지원 하지 않습니다. 대신 시스템 이미지 백업 또는 다른 백업 응용 프로그램을 사용하여 클라이언트 가상 머신 내에서 백업 및 복원 작업을 수행합니다.  
  
## <a name="work-folders-compared-to-other-sync-technologies"></a>다른 동기화 기술과 비교한 작업 폴더  

다음 표에서는 다양 한 Microsoft 동기화 기술의 배치 방법과 각 동기화 기술이 사용 되는 시기에 대해 설명 합니다.  
  
| | 클라우드 폴더 | 오프라인 파일 | 비즈니스용 OneDrive | OneDrive |
| - | ------------------ | ------------------- | -------------------------- | -------------- |
| **기술 요약** | Pc 및 장치를 사용 하 여 파일 서버에 저장 된 파일을 동기화 합니다. | 회사 네트워크에 대 한 액세스 권한이 있는 Pc를 사용 하 여 파일 서버에 저장 된 파일을 동기화 합니다 (클라우드 폴더로 대체 가능). | 회사 및 장치가 회사 네트워크 내부 또는 외부에 있는 Office 365 또는 SharePoint에 저장 된 파일을 동기화 하 고 문서 공동 작업 기능을 제공 합니다. | Pc, Mac 컴퓨터 및 장치를 사용 하 여 OneDrive에 저장 된 개인 파일을 동기화 합니다. |
| **작업 파일에 대 한 사용자 액세스를 제공 하기 위한 것입니다.** | 예 | 예 | 예 | 예 |
| **클라우드 서비스** | None | None | Office 365 | Microsoft OneDrive |
| **내부 네트워크 서버** | Windows Server 2012 R2 또는 Windows Server 2016를 실행 하는 파일 서버 | 파일 서버 | SharePoint server (선택 사항) | None |
| **지원되는 클라이언트** | Pc, iOS, Android | 회사 네트워크의 Pc 또는 DirectAccess, Vpn 또는 기타 원격 액세스 기술을 통해 연결 된 Pc | Pc, iOS, Android, Windows Phone | Pc, Mac 컴퓨터, Windows Phone, iOS, Android |
  
> [!NOTE]
>  이전 표에 나와 있는 동기화 기술 외에도 Microsoft는 서버 간 복제를 위해 설계 된 DFS 복제 및 지점 WAN 가속 기술로 설계 된 BranchCache를 비롯 한 다른 복제 기술을 제공 합니다. 자세한 내용은 [DFS 네임 스페이스 및 DFS 복제](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) 및 [BranchCache 개요](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx) 를 참조 하세요. 
  
## <a name="server-manager-information"></a>서버 관리자 정보  

작업 폴더는 파일 및 저장소 서비스 역할의 일부입니다. 역할 및 기능 추가 마법사 또는 cmdlet을 사용 하 여 클라우드 폴더를 설치할 수 있습니다 `Install-WindowsFeature` . 두 방법 모두 다음 작업을 수행 합니다.  
  
-   서버 관리자의 **파일 및 저장소 서비스** 에 **클라우드 폴더** 페이지를 추가 합니다.  
  
-   Windows Server에서 동기화 공유를 호스트 하는 데 사용 하는 Windows 동기화 공유 서비스를 설치 합니다.  
  
-   서버에서 클라우드 폴더를 관리 하는 SyncShare Windows PowerShell 모듈을 설치 합니다.  
  
## <a name="interoperability-with-windows-azure-virtual-machines"></a>Microsoft Azure 가상 컴퓨터와의 상호 운용성

 Windows Azure의 가상 머신에서이 Windows Server 역할 서비스를 실행할 수 있습니다. 이 시나리오는 Windows Server 2012 R2 및 Windows Server 2016에서 테스트 되었습니다.  
  
Microsoft Azure 가상 컴퓨터를 시작 하는 방법에 대 한 자세한 내용은 [Windows azure 웹 사이트](http://www.windowsazure.com/documentation/services/virtual-machines)를 참조 하십시오.  
  
## <a name="see-also"></a>참고 항목

 자세한 내용은 다음 리소스를 참조하세요.  
  
| 콘텐츠 유형 | 참조 |
| ------------------ | ---------------- |
| **제품 평가** | -   [Android 용 클라우드 폴더 – 릴리스](https://blogs.technet.microsoft.com/filecab/2016/03/16/work-folders-for-android-released) (블로그 게시물)<br />-   [IOS 용 클라우드 폴더 – IPad 앱 릴리스](https://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx) (블로그 게시물)<br />-   [Windows Server 2012 r 2의 클라우드 폴더 소개](https://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx) (블로그 게시물)<br />-   [클라우드 폴더 소개](https://channel9.msdn.com/posts/Introduction-to-Work-Folders) (Channel 9 비디오)<br />-   [클라우드 폴더 테스트 랩 배포](https://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) (블로그 게시물)<br />-   [Windows 7 용 클라우드 폴더](https://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) (블로그 게시물) |
| **배포** | -   [클라우드 폴더 구현 디자인](plan-work-folders.md)<br />-   [클라우드 폴더 배포](deploy-work-folders.md)<br />-   [AD FS 및 WAP (웹 응용 프로그램 프록시)를 사용 하 여 클라우드 폴더 배포](deploy-work-folders-adfs-overview.md)<br />-   [Azure AD 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)<br />- [작업 폴더 마이그레이션 가이드에 대 한 오프라인 파일 (CSC)](https://blogs.technet.microsoft.com/filecab/2016/08/12/offline-files-csc-to-work-folders-migration-guide/)<br />-   [클라우드 폴더 배포를 위한 성능 고려 사항](https://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />-   [Windows 7 용 클라우드 폴더 (64 비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42558)<br />-   [Windows 7 용 클라우드 폴더 (32 비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42559) |
| **작업** | -   [클라우드 폴더 iPad 앱: FAQ](https://windows.microsoft.com/windows/work-folders-ipad-faq) (사용자 용)<br />-   [클라우드 폴더 인증서 관리](https://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx) (블로그 게시물)<br />-   [Windows Server 2012 R2 클라우드 폴더 배포 모니터링](https://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx) (블로그 게시물)<br />-   [Windows PowerShell의 SyncShare (작업 폴더) Cmdlet](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)<br />-   [Windows Server 2012 R2 Preview 버전용 Storage 및 File Services PowerShell Cmdlet 빠른 참조 카드](https://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx) |
| **문제 해결** | -   [Windows Server 2012 R2 – IIS 웹 사이트 및 작업 폴더와의 포트 충돌 해결](https://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx) (블로그 게시물)<br />-   [클라우드 폴더의 일반적인 오류](https://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx) |
| **커뮤니티 리소스** | -   [파일 서비스 및 저장소 포럼](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />-   [Microsoft의 저장소 팀-파일 캐비닛 블로그](https://blogs.technet.com/b/filecab/)<br />-   [디렉터리 서비스 팀 블로그 확인](https://blogs.technet.com/b/askds/) |  
| **관련 기술** | -   [Windows Server 2016의 저장소](../storage.yml)<br>-   [파일 및 저장소 서비스](https://technet.microsoft.com/library/hh831487(v=ws.11).aspx)<br />-   [파일 서버 리소스 관리자](https://technet.microsoft.com/library/hh831701(v=ws.11).aspx)<br />-   [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필](https://technet.microsoft.com/library/hh848267(v=ws.11).aspx)<br />-   [BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)<br />-   [DFS 네임 스페이스 및 DFS 복제](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) |
