---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: 클라우드 폴더 개요
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 6/11/2017
description: 클라우드 폴더 개요 - 사용자가 PC와 디바이스에서 일관적인 방법으로 작업 파일에 액세스할 수 있게 해주는 Windows Server의 서버 역할입니다.
ms.openlocfilehash: dd32b84e6442ec55414da27ea94ef16eeab769eb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890484"
---
# <a name="work-folders-overview"></a>클라우드 폴더 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

이 항목에서는 Windows Server를 실행하는 파일 서버에 대한 역할 서비스로써 사용자가 PC와 디바이스에서 일관적인 방법으로 작업 파일에 액세스할 수 있게 해주는 클라우드 폴더에 대해 알아봅니다.  
  
다운로드 하 여 클라우드 폴더를 사용 하 여 Windows 10, Windows 7, Android 또는 iOS 장치에 원하는 경우 다음을 참조 합니다.

-   [Windows 10 용 작업 폴더](https://support.microsoft.com/help/12370/windows-10-work-folders)
-   [Windows 7 용 작업 폴더 (64 비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42558)
-   [Windows 7 용 작업 폴더 (32 비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42559)
- [IOS 용 작업 폴더](https://itunes.apple.com/app/work-folders/id950878067)
- [Android 용 작업 폴더](https://play.google.com/store/apps/details?id=com.microsoft.workfolders)

##  <a name="BKMK_OVER"></a> 역할 설명  
 클라우드 폴더를 통해 사용자는 개인용 컴퓨터 및 장치에 작업 파일을 저장하고 여기에 액세스할 수 있습니다. 이를 회사 PC 외의 BYOD(bring-your-own device)라고도 합니다. 사용자는 작업 파일을 저장하고 어디에서나 액세스할 수 있는 편리한 위치를 얻을 수 있습니다. 조직은 중앙에서 관리 되는 파일 서버에 파일을 저장하고 선택적으로 사용자 장치 정책(예: 암호화 및 잠금 화면 암호)을 지정하여 회사 데이터에 대한 제어를 유지합니다.  
  
 기존에 배포된 폴더 리디렉션, 오프라인 파일 및 홈 폴더를 사용하여 클라우드 폴더를 배포할 수 있습니다. 클라우드 폴더는 *동기화 공유*라고 하는 서버의 폴더에 사용자 파일을 저장합니다. 이미 사용자 데이터가 포함된 폴더를 지정할 수 있으며, 따라서 서버와 데이터를 마이그레이션하거나 기존 솔루션을 즉시 폐지하지 않고도 클라우드 폴더를 채택할 수 있습니다.  
  
##  <a name="BKMK_APP"></a> 실제 응용 프로그램  
 관리자는 클라우드 폴더를 사용하여 사용자에게 작업 파일에 대한 액세스를 제공하면서도 중앙 집중식 저장소를 유지하고 조직의 데이터를 제어할 수 있습니다. 클라우드 폴더는 다음과 같은 방식으로 응용이 가능합니다.  
  
-   사용자의 회사/개인용 컴퓨터 및 디바이스에서 작업 파일에 액세스할 수 있는 단일 액세스 지점을 제공  
  
-   오프라인 상태에서 작업 파일에 액세스한 후 나중에 PC 또는 디바이스가 인터넷이나 인트라넷에 연결되면 중앙의 파일 서버와 동기화  
  
-   기존에 배포된 폴더 리디렉션, 오프라인 파일 및 홈 폴더를 사용하여 배포  
  
-   파일 분류, 폴더 할당량 등의 기존 파일 서버 관리 기술을 사용하여 사용자 데이터 관리  
  
-   사용자의 PC 및 디바이스에 클라우드 폴더를 암호화하고 잠금 화면 비밀번호를 사용하도록 지시하는 보안 정책 지정  
  
-   클라우드 폴더에 장애 조치(failover) 클러스터링을 사용하여 고가용성 솔루션 제공  
  
##  <a name="BKMK_NEW"></a> 중요 한 기능  
 클라우드 폴더는 다음 기능을 포함하고 있습니다.  
  
|기능|가용성|설명|  
|-------------------|------------------|-----------------|  
|서버 관리자의 클라우드 폴더 역할 서비스|Windows Server 2012 R2 또는 Windows Server 2016|파일 및 저장소 서비스는 동기화 공유(사용자의 작업 파일을 저장하는 폴더)를 설정하고 클라우드 폴더를 모니터링하고 동기화 공유 및 사용자 액세스를 관리하는 방법을 제공|  
|클라우드 폴더 cmdlet|Windows Server 2012 R2 또는 Windows Server 2016|클라우드 폴더 서버를 관리하기 위한 포괄적인 cmdlet이 포함된 Windows PowerShell 모듈|  
|클라우드 폴더를 Windows와 통합|Windows 10<br /><br /> Windows 8.1<br /><br /> Windows RT 8.1<br /><br /> Windows 7(다운로드 필요)|클라우드 폴더는 Windows 컴퓨터에서 다음 기능을 제공합니다.<br /><br /> -   클라우드 폴더를 설정하고 모니터링하는 제어판 항목<br />-   클라우드 폴더의 파일에 쉽게 액세스할 수 있도록 파일 탐색기 통합<br />-   중앙의 파일 서버와 파일을 주고 받는 한편 배터리 사용 시간과 시스템 성능을 최대화하는 동기화 엔진|  
|디바이스용 클라우드 폴더 앱|Android<br /><br /> Apple iPhone 및 iPad®|인기 있는 디바이스에서 클라우드 폴더의 파일에 액세스할 수 있게 해주는 앱|  
  
##  <a name="BKMK_New"></a> 새로운 기능과 변경 된 기능  
 다음 표에는 클라우드 폴더의 주요 변경 내용 중 일부가 설명되어 있습니다.  
  
|기능|새로운 기능 또는 업데이트된 기능|설명|  
|----------------------------|---------------------|-----------------|  
|Azure AD 응용 프로그램 프록시 지원|Windows 10 버전 1703, Android, iOS에 추가|원격 사용자가 Azure AD 응용 프로그램 프록시를 사용하여 클라우드 폴더 서버에 있는 자신의 파일에 안전하게 액세스할 수 있습니다.|
|더 빠르게 변경 내용 복제|Windows 10 및 Windows Server 2016에서 업데이트된 기능|Windows Server 2012 R2의 경우 파일 변경을 작업 폴더 서버와 동기화하면 클라이언트는 해당 변경에 대해 알리지 않고 업데이트될 때까지 최대 10분을 기다립니다. Windows Server 2016을 사용 하는 경우 작업 폴더 서버가 즉시 Windows 10 클라이언트 알리고 파일 변경 내용이 즉시 동기화 합니다. 이 기능은 Windows Server 2016의 새로운 기능이며 Windows 10 클라이언트가 필요합니다. 이전 클라이언트를 사용하거나 클라우드 폴더 서버가 Windows Server 2012 R2인 경우 클라이언트가 10분마다 변경 내용을 계속 폴링합니다.|  
|WIP(Windows Information Protection)와 통합|Windows 10 버전 1607에 추가|관리자가 WIP를 배포하면 클라우드 폴더는 PC의 데이터를 암호화하여 데이터 보호를 적용할 수 있습니다. 암호화에는 엔터프라이즈 ID와 연결된 키가 사용되며, 이 키는 Microsoft Intune 등의 지원되는 모바일 디바이스 관리 패키지를 사용하여 원격으로 지울 수 있습니다.|  
|Microsoft Office 통합|Windows 10 버전 1511에 추가|Windows 8.1에서는 이 PC를 클릭하거나 탭한 후 PC의 클라우드 폴더 위치를 탐색하여 Office 앱 내부에서 클라우드 폴더를 탐색할 수 있습니다. Windows 10에서는 파일을 저장하거나 열 때 Office가 표시하는 위치 목록에 클라우드 폴더를 추가하면 훨씬 간편하게 클라우드 폴더로 이동할 수 있습니다. 자세한 내용은 [Windows 10의 클라우드 폴더](https://windows.microsoft.com/windows-10/work-folders-in-windows-10) 및  [Troubleshooting using Work Folders as a Place in Microsoft Office(클라우드 폴더를 Microsoft Office의 장소로 사용할 때의 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/32881.troubleshooting-using-work-folders-as-a-place-in-microsoft-office.aspx)를 참조하세요.|  
  
##  <a name="BKMK_SOFT"></a> 소프트웨어 요구 사항  

클라우드 폴더에는 파일 서버와 네트워크 인프라에 대한 다음과 같은 소프트웨어 요구 사항이 있습니다.  
  
-   사용자 파일과의 동기화 공유를 호스트하기 위해 Windows Server 2012 R2 또는 Windows Server 2016을 실행하는 서버  
  
-   사용자 파일을 저장하기 위한 NTFS 파일 시스템으로 포맷된 볼륨  
  
-   Windows 7 PC에서 암호 정책을 적용하려면 그룹 정책 암호 정책을 사용해야 합니다. 또한 클라우드 폴더 암호 정책(사용하는 경우)에서 Windows 7 PC를 제외해야 합니다.

-   클라우드 폴더를 호스팅할 각 파일 서버에 대한 서버 인증서가 있어야 합니다. 이러한 인증서는 사용자가 신뢰할 수 있는 CA(인증 기관)(공용 CA가 가장 적합)에서 발급한 것이어야 합니다.

-   (선택 사항) 여러 파일 서버를 사용할 때 PC 및 장치에서 올바른 파일 서버를 자동으로 참조할 수 있도록 지원하는 Windows Server 2012 R2의 스키마 확장이 포함된 Active Directory Domain Services 포리스트.  
  
사용자가 인터넷을 통해 동기화할 수 있도록 하려면 다음과 같은 추가 요구 사항을 충족해야 합니다.  
  
-   조직의 역방향 프록시 서버 또는 네트워크 게이트웨이에 게시 규칙을 만들어 인터넷에서 서버에 액세스할 수 있도록 하는 기능  
  
-   (선택 사항) 공개적으로 등록된 도메인 이름과 도메인에 대한 추가 공용 DNS 레코드를 만들 수 있는 기능  
  
-   (선택 사항) AD FS 인증을 사용할 경우 AD FS(Active Directory Federation Services) 인프라  
  
클라우드 폴더에는 클라이언트 컴퓨터에 대한 다음과 같은 소프트웨어 요구 사항이 있습니다.  
  
-   PC 및 디바이스가 다음 운영 체제 중 하나에서 실행되어야 합니다.  
  
    -   Windows 10  
  
    -   Windows 8.1  
  
    -   Windows RT 8.1  
  
    -   Windows 7  
  
    -   Android 4.4 KitKat 이상  
  
    -   iOS 10.2 이상  
  
-   Windows 7 PC에서 다음 Windows 버전 중 하나를 실행해야 합니다.  
  
    -   Windows 7 Professional  
  
    -   Windows 7 Ultimate  
  
    -   Windows 7 Enterprise  
  
-   Windows 7 PC는 조직의 도메인에 가입되어 있어야 하며 작업 그룹에는 가입할 수 없습니다.  
  
-   모든 사용자 파일을 클라우드 폴더에 저장할 수 있는 충분한 여유 공간이 NTFS로 포맷된 로컬 드라이브에 있어야 하며, 클라우드 폴더가 시스템 드라이브에 있는 경우 기본적으로 6GB의 추가 여유 공간이 있어야 합니다. 클라우드 폴더의 위치는 기본적으로 **%USERPROFILE%\Work Folders**입니다.  
  
     그러나 설정하는 동안 사용자가 위치를 변경할 수 있습니다(NTFS 파일 시스템으로 포맷된 microSD 카드와 USB 드라이브가 지원되는 위치이며, 드라이브가 제거된 경우 동기화가 중지됨).  
  
     개별 파일의 최대 크기는 기본적으로 10GB입니다. 관리자가 파일 서버 리소스 관리자의 할당량 기능을 사용하여 할당량을 구현할 수 있지만 사용자당 저장소 제한은 없습니다.  
  
-   클라우드 폴더는 클라이언트 가상 컴퓨터의 가상 컴퓨터 상태 롤백을 지원하지 않습니다. 대신 시스템 이미지 백업 또는 다른 백업 응용 프로그램을 사용하여 클라이언트 가상 컴퓨터 내에서 백업 및 복원 작업을 수행합니다.  
  
##  <a name="BKMK_Comparison"></a> 클라우드 폴더 동기화 기술과 비교  

다음 표에서는 다양한 Microsoft 동기화 기술의 위치와 각 기술을 사용하는 시기에 대해 설명합니다.  
  
||클라우드 폴더|오프라인 파일|비즈니스용 OneDrive|OneDrive|  
|-|------------------|-------------------|---------------------------|--------------|  
|**기술 요약**|파일 서버에 저장된 파일을 PC 및 디바이스와 동기화|파일 서버에 저장된 파일을 회사 네트워크에 액세스할 수 있는 PC와 동기화(클라우드 폴더로 대체 가능)|Office 365 또는 SharePoint에 저장된 파일을 회사 네트워크 내부 또는 외부의 PC 및 디바이스와 동기화하고 문서 공동 작업 기능 제공|OneDrive에 저장된 파일을 PC, Mac 컴퓨터 및 디바이스와 동기화|  
|**작업 파일에 대 한 사용자 액세스를 제공 하기 위한**|예|예|예|아니오|  
|**클라우드 서비스**|없음|없음|Office 365|Microsoft OneDrive|  
|**내부 네트워크 서버**|Windows Server 2012 R2 또는 Windows Server 2016을 실행하는 파일 서버|파일 서버|SharePoint 서버(선택 사항)|없음|  
|**지원 되는 클라이언트**|PC, iOS, Android|회사 네트워크의 PC 또는 DirectAccess, VPN, 기타 원격 액세스 기술을 통해 연결된 PC|PC, iOS, Android, Windows Phone|PC, Mac 컴퓨터, Windows Phone, iOS, Android|  
  
> [!NOTE]
>  위의 표에 나열된 동기화 기술 외에도 Microsoft는 서버 간 복제를 위해 설계된 DFS 복제와 지사 WAN 가속 기술로 설계된 BranchCache를 비롯한 다른 복제 기술을 제공합니다. 자세한 내용은 [DFS 네임스페이스 및 DFS 복제](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) 및 [BranchCache 개요](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)를 참조하세요.  
  
##  <a name="BKMK_INSTALL"></a> 서버 관리자 정보  

클라우드 폴더는 파일 및 저장소 서비스 역할의 일부입니다. 역할 및 기능 추가 마법사 또는 `Install-WindowsFeature` cmdlet을 사용하여 클라우드 폴더를 설치할 수 있습니다. 두 방법 모두 다음 작업을 수행합니다.  
  
-   서버 관리자에서 **클라우드 폴더** 페이지를 **파일 및 저장소 서비스**에 추가  
  
-   Windows Server가 동기화 공유를 호스트하는 데 사용되는 Windows 동기화 공유 서비스 설치  
  
-   클라우드 폴더를 관리하기 위해 서버에 SyncShare Windows PowerShell 모듈 설치  
  
##  <a name="BKMK_Azure"></a> Windows Azure 가상 컴퓨터와의 상호 운용성  
 Windows Azure의 가상 컴퓨터에서 이 Windows Server 역할 서비스를 실행할 수 있습니다. 이 시나리오는 Windows Server 2012 R2 및 Windows Server 2016에서 테스트되었습니다.  
  
Windows Azure 가상 컴퓨터를 시작하는 방법에 대해 자세히 알아보려면 [Windows Azure 웹 사이트](http://www.windowsazure.com/documentation/services/virtual-machines)를 방문하세요.  
  
##  <a name="BKMK_LINKS"></a> 참고 항목  
 자세한 내용은 다음 리소스를 참조하십시오.  
  
|콘텐츠 형식|참조|  
|------------------|----------------|  
|**제품 평가**|-   [Android-에 대 한 작업 폴더 릴리스됨](https://blogs.technet.microsoft.com/filecab/2016/03/16/work-folders-for-android-released) (블로그 게시물)<br />-   [IPad 앱 릴리스 – iOS에 대 한 작업 폴더](https://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx) (블로그 게시물)<br />-   [Windows Server 2012 R2의 클라우드 폴더 소개](http://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx) (블로그 게시물)<br />-   [클라우드 폴더 소개](http://channel9.msdn.com/posts/Introduction-to-Work-Folders) (채널 9 비디오)<br />-   [클라우드 폴더 테스트 랩 배포](http://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) (블로그 게시물)<br />-   [Windows 7 용 폴더 클라우드](http://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) (블로그 게시물)|  
|**배포**|-   [클라우드 폴더 구현 디자인](plan-work-folders.md)<br />-   [클라우드 폴더 배포](deploy-work-folders.md)<br />-   [AD FS 및 WAP (웹 응용 프로그램 프록시)를 사용 하 여 클라우드 폴더 배포](deploy-work-folders-adfs-overview.md)<br />-   [Azure AD 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)<br />- [오프 라인 파일 (CSC) 작업 폴더 마이그레이션 가이드](https://blogs.technet.microsoft.com/filecab/2016/08/12/offline-files-csc-to-work-folders-migration-guide/)<br />-   [클라우드 폴더 배포를 위한 성능 고려 사항](https://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />-   [Windows 7 용 작업 폴더 (64 비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42558)<br />-   [Windows 7 용 작업 폴더 (32 비트 다운로드)](https://www.microsoft.com/download/details.aspx?id=42559)|  
|**작업**|-   [작업 폴더 iPad 앱: FAQ](https://windows.microsoft.com/windows/work-folders-ipad-faq) (사용자 용)<br />-   [작업 폴더 인증서 관리](https://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx) (블로그 게시물)<br />-   [Windows Server 2012 R2의 클라우드 폴더 배포를 모니터링](https://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx) (블로그 게시물)<br />-   [Windows PowerShell의 SyncShare (작업 폴더) Cmdlet](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)<br />-   [Windows Server 2012 R2 미리 보기 버전에 대 한 빠른 참조 카드 저장소 및 파일 서비스 PowerShell Cmdlet](http://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx)|  
|**문제 해결**|-   [Windows Server 2012 R2 – IIS 웹 사이트 클라우드 폴더와 Resolving 포트 충돌이](https://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx) (블로그 게시물)<br />-   [클라우드 폴더에 있는 일반적인 오류](https://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx)|  
|**커뮤니티 리소스**|-   [파일 서비스 및 저장소 포럼](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />-   [Microsoft-파일 캐비닛 블로그 저장소 팀](http://blogs.technet.com/b/filecab/)<br />-   [디렉터리 서비스 팀 블로그에 요청](http://blogs.technet.com/b/askds/)|  
|**관련 기술**|-   [Windows Server 2016의 저장소](../storage.md)<br>-   [File and Storage Services](https://technet.microsoft.com/library/hh831487(v=ws.11).aspx)<br />-   [파일 서버 리소스 관리자](https://technet.microsoft.com/library/hh831701(v=ws.11).aspx)<br />-   [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필](https://technet.microsoft.com/library/hh848267(v=ws.11).aspx)<br />-   [BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)<br />-   [DFS 네임 스페이스 및 DFS 복제](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx)|
