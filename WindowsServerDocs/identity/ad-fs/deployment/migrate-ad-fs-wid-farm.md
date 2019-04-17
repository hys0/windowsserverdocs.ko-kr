---
title: "마이그레이션 ADFS 2.0 federation 서버 WID 농장"
description: "Windows Server 2012 ADFS 2.0 서버 WID 농장 마이그레이션에 정보를 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbef7d07041a1fd32656c95947d5202b566c068a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>마이그레이션 AD 2.0 FS WID 농장  
이 문서는 광고에 자세히 설명 Windows Server 2012 농장 FS 2.0 Windows 내부 데이터베이스 (WID).

## <a name="migrate-an-ad-fs-wid-farm"></a>마이그레이션 AD FS WID 농장
Windows Server 2012 WID 농장 마이그레이션할 다음 절차를 수행 합니다.  
  
1.  에서 모든 노드에서 (서버) WID 농장을 검토 하 고에 절차를 수행 [WID 농장 마이그레이션을 준비](prepare-to-migrate-a-wid-farm.md)합니다.  
  
2.  기본 비 노드 부하 분산에서 제거 합니다.  
  
3.  Windows Server 2012를 Windows Server 2008 또는 Windows Server 2008 R2에서이 서버 운영 체제의 업그레이드 합니다. 자세한 내용은 참조 [Windows Server 2012를 설치](https://technet.microsoft.com/library/jj134246.aspx)합니다.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드 결과이 서버의 ADFS 구성 삭제 되 고 ADFS 2.0 서버 역할은 제거 됩니다. Windows Server 2012 ADFS 서버 역할 대신 설치 되어 있지만 구성 되어 있지 않습니다. 원래 ADFS 구성 만들고 federation 서버 마이그레이션을 완료 하 나머지 ADFS 설정으로 복원 해야 합니다.  
  
4.  이 서버에 원래 ADFS 구성을 만듭니다.  
  
사용 하 여 원래 ADFS 구성 만들 수는 **광고 FS Federation 서버 구성 마법사** federation 서버 WID 농장을 추가 하 합니다. 자세한 내용은 참조 [Federation 서버 Federation 서버 팜을 추가](add-a-federation-server-to-a-federation-server-farm.md)합니다.  
  
> [!NOTE]
> 연결할 때의 **주 Federation 서버 및 서비스 계정을 지정** 페이지에서 **광고 FS Federation 서버 구성 마법사**기본 federation 서버 WID 농장의 이름을 입력 하 고 ADFS 마이그레이션에 대 한 준비 하는 동안 녹화 되는 서비스 계정 정보를 입력 해야 합니다. 자세한 내용은 참조 [2.0 Federation 서버 AD 마이그레이션 FS 준비](prepare-to-migrate-a-wid-farm.md)합니다. 
>  
> 연결할 때의 **해당 Federation 서비스 이름을 지정** 페이지에서 "마이그레이션을 준비 WID 농장"에 기록 동일한 SSL 인증서에서 선택 해야 [2.0 Federation 서버 AD 마이그레이션 FS 준비](prepare-to-migrate-a-wid-farm.md)합니다.  
  
5.  이 서버에 사용자 ADFS 웹 페이지를 업데이트 합니다. 사용 하 여 사용자의 데이터 백업 덮어쓰기를 기본 ADFS 웹 페이지에서 기본적으로 만들어진 필요 마이그레이션에 대 한 준비 하는 동안 사용자 정의 ADFS 웹 페이지를 백업 하는 경우는 **%systemdrive%\inetpub\adfs\ls** Windows Server 2012에서 ADFS 구성 결과 디렉터리 합니다.  
  
6.  서버 방금 업그레이드에 Windows Server 2012 부하 분산에 추가 합니다.  
  
7.  WID 농장의 나머지 보조 서버에 대 한 1-6 단계를 반복 합니다.  
  
8.  업그레이드 보조 서버 WID 농장의 주 서버로 중 하나를 홍보 합니다. 이렇게 하려면 Windows PowerShell 연 다음 명령을 실행: `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`합니다.  
  
9. WID 농장의 원래 주 서버 부하 분산에서 제거 합니다.  
  
10. Windows PowerShell를 사용 하 여 보조 서버 하 여 WID 그룹에 원래 주 서버를 내리기 합니다. Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 보조 서버 원래 주 서버를 다음 명령을 실행: `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`합니다.  
  
11. Windows Server 2008 R2 또는 Windows Server 2008 사용자 WID 농장 Windows Server 2012에서이 지난 노드에서 (서버) 운영 체제의 업그레이드 합니다. 자세한 내용은 참조 [Windows Server 2012를 설치](https://technet.microsoft.com/library/jj134246.aspx)합니다.  
  
> [!IMPORTANT]
>  업그레이드는 운영 체제의 결과로이 서버의 ADFS 구성 삭제 되 고 ADFS 2.0 서버 역할은 제거 됩니다. Windows Server 2012 ADFS 서버 역할 대신 설치 되어 있지만 구성 되어 있지 않습니다. 수동으로 만들 원래 ADFS 구성 하 고 federation 서버 마이그레이션을 완료 하 나머지 ADFS 설정으로 복원 해야 합니다.  
  
12. 원래 ADFS 구성을 WID 팜에서이 지난 노드 (서버)을 만듭니다.  
  
사용 하 여 원래 ADFS 구성 만들 수는 **광고 FS Federation 서버 구성 마법사** federation 서버 WID 농장을 추가 하 합니다. 자세한 내용은 참조 [Federation 서버 Federation 서버 팜을 추가](add-a-federation-server-to-a-federation-server-farm.md)합니다.  
  
> [!NOTE]
> 연결할 때의 **기본 Federation 서버 및 서비스 계정을 지정** 페이지에서 **광고 FS Federation 서버 구성 마법사**, ADFS 마이그레이션에 대 한 준비 하는 동안 기록 서비스 계정 정보를 입력 합니다. 자세한 내용은 참조 [2.0 Federation 서버 AD 마이그레이션 FS 준비](prepare-to-migrate-a-wid-farm.md)합니다. 
>  
> 연결할 때의 **해당 Federation 서비스 이름을 지정** 페이지에서 동일한 SSL 인증서에 기록 선택 해야 [2.0 Federation 서버 AD 마이그레이션 FS 준비](prepare-to-migrate-a-wid-farm.md)합니다.  
  
13. 이 지난 WID 농장 서버에 사용자 ADFS 웹 페이지를 업데이트 합니다. 마이그레이션에 대 한 준비 하는 동안 사용자 정의 ADFS 웹 페이지를 백업 백업 데이터를 사용 하 여 기본 ADFS 웹 페이지에서 기본적으로 만들어진 덮어씁니다는 **%systemdrive%\inetpub\adfs\ls** Windows Server 2012에서 ADFS 구성 결과 디렉터리 합니다.  
  
14. 방금 업그레이드에 Windows Server 2012 부하 분산 하 여 WID 농장의 마지막이 서버에 추가 합니다.  
  
15. 사용자 지정 된 특성 스토어 등 모든 나머지 ADFS 사용자 지정 복원 합니다.  
  
## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)