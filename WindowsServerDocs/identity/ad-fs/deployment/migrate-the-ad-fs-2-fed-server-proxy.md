---
title: "ADFS 2.0 federation 서버 프록시 마이그레이션"
description: "Windows Server 2012 ADFS federation 서버 프록시 마이그레이션에 대해 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98e28c9be808f63ed39a3ac24dd95014b388d001
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>ADFS 2.0 federation 서버 프록시 마이그레이션
이 문서는 Windows Server 2012 ADFS 2.0 federation 프록시 서버에 자세한 정보를 제공 합니다.

## <a name="migrate-the-proxy"></a>프록시 마이그레이션

Windows Server 2012 ADFS 2.0 federation 서버 프록시 마이그레이션할 다음 절차를 수행 합니다.  
  
1.  Windows Server 2012 마이그레이션을 계획 하는 모든 federation 서버 프록시 검토 및에 절차를 수행 [2.0 Federation 서버 프록시 마이그레이션 광고 FS 준비](prepare-to-migrate-ad-fs-fed-proxy.md)합니다.  
  
2.  Federation 서버 프록시 부하 분산에서 제거 합니다.  
  
3.  Windows Server 2012를 Windows Server 2008 또는 Windows Server 2008 R2에서이 서버에서 업그레이드 운영 체제를 수행 합니다. 자세한 내용은 참조 [Windows Server 2012를 설치](https://technet.microsoft.com/library/jj134246.aspx)합니다.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드 결과이 서버의 ADFS 프록시 구성을 삭제 되 고 ADFS 2.0 서버 역할은 제거 됩니다. Windows Server 2012 ADFS 서버 역할 대신 설치 되어 있지만 구성 되어 있지 않습니다. 수동으로 원래 ADFS 프록시 구성을 작성 하 고 federation 서버 프록시 마이그레이션을 완료 하 고 나머지 ADFS 프록시 설정 복원 해야 합니다.  
  
4.  사용 하 여 원래 ADFS 프록시 구성을 만들기는 **광고 FS Federation 서버 프록시 구성을 마법사**합니다. 자세한 내용은 참조 [Federation 서버 프록시 역할 컴퓨터 구성](configure-a-computer-for-the-federation-server-proxy-role.md)합니다. 마법사를 실행 하면으로 사용할 수집한 정보 준비의 광고 마이그레이션 FS에 2.0 Federation 서버 프록시 다음과 같습니다.  
  
 
|**Federation 프록시 서버 마법사 입력된 옵션**|**다음 값을 사용 하 여**|
|-----|-----|  
|**Federation 서비스 이름**|Proxyproperties.txt 파일에서 BaseHostName 값을 입력 합니다.|  
|**이 Federation에 요청을 보낼 때 HTTP 프록시 서버를 사용 하 여** 서비스 확인란|이 확인란을 proxyproperties.txt 파일 ForwardProxyUrl 속성에 대 한 값을 포함 하는 경우|  
|**프록시 서버 주소 HTTP**|Proxyproperties.txt 파일에서 ForwardProxyUrl 값을 입력 합니다.|  
|자격 증명 확인|ADFS federation 서버 관리자 계정 또는 ADFS federation 서비스가 실행 되는 서비스 계정 자격 증명을 입력 합니다.|  
  
5.  이 서버에 사용자 ADFS 웹 페이지를 업데이트 합니다. 마이그레이션에 대 한 프록시 서버 federation 준비 하는 동안 사용자 지정 된 ADFS 프록시 웹 페이지를 백업 백업 데이터를 사용 하 여 기본 ADFS 웹 페이지에서 기본적으로 만들어진 덮어씁니다는 **%systemdrive%\inetpub\adfs\ls** Windows Server 2012에서 ADFS 프록시 구성을 결과 디렉터리 합니다.  
  
6.  이 서버 부하 분산을 다시 추가 됩니다.  
  
7.  다른 ADFS 2.0 federation 서버 프록시 마이그레이션하를 사용 하는 경우 나머지 federation 서버 프록시 컴퓨터에 대해 2-6 단계를 반복 합니다.  
  
  
## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)