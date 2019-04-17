---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: "부록 간편한 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5de7431d0f3fe9a078432b11a63ce996d3abe447
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="simplified-administration-appendix"></a>부록 간편한 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
-   [서버 관리자 추가 서버 대화 (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)  
  
-   [서버 Manager Remote 서버 상태](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)  
  
-   [Windows PowerShell 모듈 로드](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)  
  
-   [이전 운영 체제에 대해 발급 핫픽스 제거](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)  
  
-   [Ntdsutil.exe 미디어를 변경 하 여 설치](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)  
  
## <a name="BKMK_AddServers"></a>서버 관리자 추가 서버 대화 (Active Directory)  

**서버 추가** 대화 상자에서는 위치 하 고 운영 체제를 와일드 카드를 사용 하 여 서버에 대 한 Active Directory를 검색 합니다. 대화 상자의 DNS 쿼리에 정식된 도메인 이름 또는 접두사 이름으로 사용할 수도 있습니다. 이러한 검색 되지 광고 Windows PowerShell 비누-도메인 컨트롤러 서버 관리자가 연락처에 연락한 Windows Server 2003도 실행 될 수 있음을 의미 통해 광고 관리 게이트웨이 대 한.NET 통해 구현 기본 DNS 및 LDAP 프로토콜을 사용 합니다. 서버 이름 목적 프로비저닝에 대 한 파일을 가져올 수 있습니다.  
  
Active Directory 검색 다음 LDAP 필터를 사용합니다.  
  
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
  
## <a name="BKMK_ServerMgrStatus"></a>서버 Manager Remote 서버 상태  
관리자 서버 주소 경로 프로토콜을 사용 하 여 원격 서버 접근성을 테스트 합니다. 풀에 있는 경우에 ARP 요청에 응답 하지 서버가 나열 되지 않습니다.  
  
ARP 응답 하는 경우 다음 DCOM 연결과 WMI 사항이 서버에 반환할 상황 정보 합니다. RPC, DCOM 및 WMI을 연결할 수 없는 서버 관리자 서버 완벽 하 게 관리할 수 없습니다.  
  
## <a name="BKMK_PSLoadModule"></a>Windows PowerShell 모듈 로드  
Windows PowerShell 3.0 구현 동적 모듈 로드 합니다. 사용 하 여 **가져오기 모듈** cmdlet 일반적으로 필요 하지 않습니다. 대신, 간단히 cmdlet, 별칭 또는 기능을 자동으로 호출 모듈을 로드 합니다.  
  
사용 하 여 로드 모듈을 보려면는 **Get 모듈** cmdlet 합니다.  
  
```  
Get-Module  
  
```  
  
![단순한 관리](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)  
  
내보낸된 기능 및 cmdlet과 함께 설치 된 모든 모듈을 보려면 사용:  
  
```  
Get-Module -ListAvailable  
  
```  
  
사용 되는 주요 경우는 **가져오기 모듈** 명령에 액세스 해야 하는 경우이 "광고:" Windows PowerShell 가상 드라이브 및 가기만 모듈 이미 로드 합니다. 예를 들어 뒤 다음 명령을 사용 하 여 다음과 같습니다.  
  
```  
import-module activedirectory  
cd ad:  
dir  
  
```  
  
## <a name="BKMK_Rid"></a>이전 운영 체제에 대해 발급 핫픽스 제거  
참조 [검출 및 방지 너무 많은 소비 실행 하는 Windows Server 2008 R2 도메인 컨트롤러에서 전 세계 RID 풀의 사용 가능한 업데이트를](https://support.microsoft.com/kb/2618669)합니다.  
  
## <a name="BKMK_IFM"></a>미디어에서 Ntdsutil.exe 설치 변경  
Windows Server 2012에 대 한 Ntdsutil.exe 명령줄 도구에 두 가지 추가 옵션을 추가 **IFM (IFM 미디어를 만드는)** 메뉴 합니다. 이러한 내보낸된 NTDS.DIT 파일을 데이터베이스 합니다. 디스크 공간을 프리미엄 때의 IFM 만드는 시간을 절약할이 합니다.  
  
다음 표에서 두 가지 새로운 메뉴 항목에 설명 합니다.  
  
|||  
|-|-|  
|메뉴 항목|설명|  
|전체 NoDefrag %s 만들기|전체 광고 DC 또는 %s 폴더로 광고/LDS 인스턴스 조각 모음을 수행 하지 않고도 IFM 미디어 만들기|  
|Sysvol 전체 NoDefrag %s 만들기|전체 광고 DC에 대 한 %s 폴더로 조각 모음을 수행 하지 않고도 SYSVOL와 IFM 미디어 만들기|  
  
![단순한 관리](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)  
  
![단순한 관리](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)  
  


