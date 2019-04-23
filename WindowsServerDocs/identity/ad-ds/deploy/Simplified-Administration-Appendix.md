---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: 관리 간소화 부록
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 36cdacec27e64586c359146b858a9d68750e5026
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858264"
---
# <a name="simplified-administration-appendix"></a>관리 간소화 부록

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
-   [서버 관리자 서버 대화 상자 (Active Directory)를 추가 합니다.](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)  
  
-   [서버 관리자 원격 서버 상태](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)  
  
-   [Windows PowerShell 모듈 로드](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)  
  
-   [이전 운영 체제에 대 한 발급 핫픽스를 제거 합니다.](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)  
  
-   [Ntdsutil.exe 설치 미디어에서 변경](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)  
  
## <a name="BKMK_AddServers"></a>서버 관리자 서버 대화 상자 (Active Directory)를 추가 합니다.  

**서버 추가** 대화 상자에서는 와일드 카드를 사용 하 여 운영 체제에 의해 및 위치에 따라 서버에 대 한 Active Directory를 검색 합니다. 대화 상자에서는 정규화 된 도메인 이름 또는 접두사 이름으로 DNS 쿼리를 사용 하 여 합니다. 이러한 검색을 통해.NET, 서버 관리자가 연락 하는 도메인 컨트롤러에 Windows Server 2003 실행할도 수 있음을-SOAP 통해 AD 관리 게이트웨이에 대 한 AD Windows PowerShell이 아닌 구현 하는 네이티브 DNS 및 LDAP 프로토콜을 사용 합니다. 목적으로 프로 비전에 대 한 서버 이름으로 파일을 가져올 수도 있습니다.  
  
Active Directory 검색에는 다음 LDAP 필터를 사용합니다.  
  
```  
(&(ObjectCategory=computer)  
  
(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))  
  
(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))  
  
```  
  
Active Directory 검색 다음과 같은 특성을 반환합니다.  
  
```  
( dnsHostName )( operatingSystem )( cn )  
  
```  
  
## <a name="BKMK_ServerMgrStatus"></a>서버 관리자 원격 서버 상태  
서버 관리자 주소 라우팅 프로토콜을 사용 하 여 원격 서버 액세스 가능성을 테스트 합니다. ARP 요청에 응답 하지 모든 서버 풀에서 하는 경우에 표시 되지 않습니다.  
  
ARP 응답 하는 경우 다음 DCOM 및 WMI에 대해 연결을 서버 상태 정보를 반환 합니다. RPC, DCOM 및 WMI를 연결할 수 없는 경우 서버 관리자 서버를 완전 하 게 관리할 수 없습니다.  
  
## <a name="BKMK_PSLoadModule"></a>Windows PowerShell 모듈 로드  
Windows PowerShell 3.0을 로드 하는 동적 모듈을 구현 합니다. 사용 하는 **모듈 가져오기** cmdlet 일반적으로 더 이상 필요 합니다; 대신, 모듈 로드 단순히 cmdlet, 별칭 또는 함수를 자동으로 호출 합니다.  
  
로드 된 모듈을 보려면 사용 하 여는 **Get-module** cmdlet입니다.  
  
```  
Get-Module  
  
```  
  
![간편한 관리](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)  
  
내보낸된 함수 및 cmdlet과 함께 설치 된 모든 모듈을 확인 하려면 다음을 사용 합니다.  
  
```  
Get-Module -ListAvailable  
  
```  
  
기본 사례를 **은 import-module** 명령에 액세스 해야 하는 경우입니다는 "AD:" Windows PowerShell 가상 드라이브와 겉가 이미 로드 된 모듈입니다. 예를 들어, 다음 명령을 사용 합니다.  
  
```  
import-module activedirectory  
cd ad:  
dir  
  
```  
  
## <a name="BKMK_Rid"></a>이전 운영 체제에 대 한 발급 핫픽스를 제거 합니다.  
참조 [는 업데이트를 검색 하 고 Windows Server 2008 r 2를 실행 하는 도메인 컨트롤러에 전역 RID 풀이 너무 많이 사용 하지 않도록 방지할 수 있습니다](https://support.microsoft.com/kb/2618669)합니다.  
  
## <a name="BKMK_IFM"></a>Ntdsutil.exe 설치 미디어에서 변경  
Ntdsutil.exe 명령줄 도구에 대 한 두 개의 추가 옵션을 추가 하는 Windows Server 2012는 **IFM (미디어 만들기 IFM)** 메뉴. 이러한 방법으로 내보낸된 NTDS의 오프 라인 조각 모음을 수행 하지 않고 IFM 저장소를 만들 수 있습니다. DIT 데이터베이스 파일입니다. 디스크 공간이 중요할 경우 그렇게 하면는 IFM 만드는 시간이 줄어듭니다.  
  
다음 표에서 두 가지 새 메뉴 항목을 보여 줍니다.  
  
|||  
|-|-|  
|메뉴 항목|설명|  
|전체 NoDefrag %s 만들기|전체 AD DC 또는 AD/LDS 인스턴스 폴더 %s 대 한 조각 모음을 수행 하지 않고 IFM 미디어 만들기|  
|Sysvol 전체 NoDefrag %s 만들기|SYSVOL와 전체 AD DC에 대 한 %s 폴더에 조각 모음을 수행 하지 않는 IFM 미디어 만들기|  
  
![간편한 관리](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)  
  
![간편한 관리](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)  
  


