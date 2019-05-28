---
title: 원격 데스크톱 서비스 배포에 Windows Server 2016으로 마이그레이션
description: 이 문서에서는 새 Windows Server 2016 서버에 원격 데스크톱 서비스 배포를 마이그레이션하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
msreviewer: ''
nams.suite: ''
nams.technology: remote-desktop-services
ms.author: chrimo
ms.date: 11/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b1fa833-4325-48a8-bf34-46265f40c001
author: christianmontoya
manager: scottman
ms.openlocfilehash: 63037dd7e32320b6e640396e20344e5678ed91dd
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034435"
---
# <a name="migrate-your-remote-desktop-services-deployment-to-windows-server-2016"></a>원격 데스크톱 서비스 배포에 Windows Server 2016으로 마이그레이션

Windows Server 2012 R2의 원격 데스크톱 서비스를 현재 실행 중인 경우 Azure SQL 및 저장소 공간 다이렉트에 대 한 지원 같은 새로운 기능을 활용 하려면 Windows Server 2016으로 이동할 수 있습니다.

원격 데스크톱 서비스 배포에 대 한 마이그레이션 Windows Server 2016을 실행 하는 대상 서버에 Windows Server 2016을 실행 하는 원본 서버에서 지원 됩니다. 즉, Windows Server 2016으로 Windows Server 2012 R2에서 RDS에서 직접 없음-현재 위치 마이그레이션이 있습니다. 대신 대부분의 RDS 구성 요소에 대해 먼저 Windows Server 2016으로 업그레이드 하 다음 데이터 및 라이선스를 마이그레이션합니다. 직접 마이그레이션하는 유일한 구성 요소는 RD 웹, RD 게이트웨이 및 라이선스 서버.

업그레이드 프로세스 및 요구 사항에 대 한 자세한 내용은 참조 하세요. [원격 데스크톱 서비스 배포에 Windows Server 2016으로 업그레이드](upgrade-to-rds-2016.md)합니다.

원격 데스크톱 서비스 배포를 마이그레이션하려면 다음 단계를 사용 합니다.
- [RD 연결 브로커 서버 마이그레이션](#migrate-rd-connection-broker-servers)
- [세션 컬렉션 마이그레이션](#migrate-session-collections)
- [가상 데스크톱 컬렉션 마이그레이션](#migrate-virtual-desktop-collections)
- [RD 웹 액세스 서버 마이그레이션](#migrate-rd-web-access-servers)
- [RD 게이트웨이 서버 마이그레이션](#migrate-rd-gateway-servers)
- [RD 라이선싱 서버 마이그레이션](#migrate-rd-licensing-servers)
- [인증서 마이그레이션](#migrate-certificates)

## <a name="migrate-rdconnection-broker-servers"></a>RD 연결 브로커 서버 마이그레이션

이것은 마이그레이션에 대 한 가장 중요 한 첫 번째 단계: Windows Server 2016을 실행 하는 대상 서버로 RD 연결 브로커를 마이그레이션.
> [!IMPORTANT] 
> 원격 데스크톱 연결 브로커 (RD 연결 브로커) 원본 서버 마이그레이션을 지원 하려면 고가용성에 대해 구성 되어야 합니다. 자세한 내용은 [원격 데스크톱 연결 브로커 클러스터 배포](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)합니다.

1. 둘 이상의 RD 연결 브로커 서버가 고가용성으로 설정된 경우 현재 활성화된 서버를 제외하고 나머지 모든 RD 연결 브로커 서버를 제거하세요.
2. [업그레이드](upgrade-to-rds-2016.md) 나머지 RD 연결 브로커 서버에서 Windows Server 2016을 배포 합니다.
3. 고가용성 배포에 Windows Server 2016 RD 연결 브로커 서버를 추가 합니다.

> [!NOTE] 
> Windows Server 2016 및 Windows Server 2012 R2는 혼합 된 고가용성 구성은 RD 연결 브로커 서버에 대 한 지원 되지 않습니다. Windows Server 2016을 실행 하는 RD 연결 브로커 Windows Server 2012 R2를 실행 하는 RD 세션 호스트 서버를 사용 하 여 세션 컬렉션을 제공 하 고 Windows Server 2012 R2를 실행 하는 RD 가상화 호스트 서버를 사용 하 여 가상 데스크톱 컬렉션을 서비스할 수 있습니다.

## <a name="migrate-session-collections"></a>세션 컬렉션 마이그레이션

Windows Server 2016의 세션 컬렉션에 Windows Server 2012 R2의 세션 컬렉션을 마이그레이션하려면 다음이 단계를 수행 합니다.
> [!IMPORTANT] 
> 이전 단계를 완료 한 후에 세션 컬렉션을 마이그레이션하세요 [마이그레이션하려면 RD 연결 브로커 서버](#migrate-rd-connection-broker-servers)합니다.

1. [세션 컬렉션을 업그레이드](Upgrade-to-RDSH-2016.md) Windows Server 2012 R2를 Windows Server 2016에서.
2. 세션 컬렉션에 Windows Server 2016을 실행 하는 새 RD 세션 호스트 서버를 추가 합니다.
3. RD 세션 호스트 서버의 모든 세션에서 로그아웃한 후 마이그레이션해야 하는 서버를 세션 컬렉션에서 제거합니다. 
> [!NOTE]
> 세션 컬렉션에서 사용 템플릿 (uvhd-template.vhdx) 사용 하 고 파일 서버를 새 서버로 마이그레이션된, 경우에 사용자 프로필 디스크를 업데이트 합니다. 새 경로 사용 하 여 위치 컬렉션 속성입니다. 원본 서버와 동일한 새 위치의 상대 경로에서 사용자 프로필 디스크를 사용할 수 있어야 합니다.
>
> Windows Server 2012 R2 및 Windows Server 2016을 실행 하는 서버가 혼합 된 RD 세션 호스트 서버의 세션 컬렉션을 지원 되지 않습니다.

## <a name="migrate-virtual-desktop-collections"></a>가상 데스크톱 컬렉션 마이그레이션

Windows Server 2016을 실행 하는 대상 서버를 Windows Server 2012 R2를 실행 하는 원본 서버에서 가상 데스크톱 컬렉션을 마이그레이션하려면 다음이 단계를 수행 합니다.

> [!IMPORTANT] 
> 이전 단계를 완료 한 후에 가상 데스크톱 컬렉션을 마이그레이션하세요 [마이그레이션하려면 RD 연결 브로커 서버](#migrate-rd-connection-broker-servers)합니다.

1. [가상 데스크톱 컬렉션을 업그레이드](Upgrade-to-RDVH-2016.md) 서버에서 Windows Server 2016으로 Windows Server 2012 R2를 실행 합니다.
2. 가상 데스크톱 컬렉션에 새 Windows Server 2016 RD 가상화 호스트 서버를 추가 합니다.
3. 현재 RD 가상화 호스트 서버에서 실행 중인 가상 데스크톱 컬렉션의 모든 가상 컴퓨터를 새 서버로 마이그레이션합니다. 
4. 마이그레이션해야 하는 모든 RD 가상화 호스트 서버를 원본 서버의 가상 데스크톱 컬렉션에서 제거합니다.

> [!NOTE] 
> 세션 컬렉션에서 사용 템플릿 (uvhd-template.vhdx) 사용 하 고 파일 서버를 새 서버로 마이그레이션된, 경우에 사용자 프로필 디스크를 업데이트 합니다. 새 경로 사용 하 여 위치 컬렉션 속성입니다. 원본 서버와 동일한 새 위치의 상대 경로에서 사용자 프로필 디스크를 사용할 수 있어야 합니다.
>
> Windows Server 2012 R2 및 Windows Server 2016을 실행 하는 서버가 혼합 된 RD 가상화 호스트 서버의 가상 데스크톱 컬렉션은 지원 되지 않습니다.

## <a name="migrate-rdweb-access-servers"></a>RD 웹 액세스 서버 마이그레이션
RD 웹 액세스 서버를 마이그레이션하려면 다음이 단계를 수행 합니다.
- 원격 데스크톱 서비스 배포에 Windows Server 2016을 실행 하는 대상 서버를 가입 및 RD 웹 역할을 설치 합니다.
- 사용 하 여 [IIS 웹 배포 도구](https://www.iis.net/) Windows Server 2016을 실행 하는 대상 서버에 현재 RD 웹 액세스 서버에서 RD 웹 웹 사이트 설정을 마이그레이션할 수 있습니다.
- [인증서 마이그레이션](#migrate-certificates) 대상 서버에 Windows Server 2016을 실행 합니다.
- 원격 데스크톱 서비스 배포에서 원본 서버 제거  

## <a name="migrate-rdgateway-servers"></a>RD 게이트웨이 서버 마이그레이션
RD 게이트웨이 서버를 마이그레이션하려면 다음이 단계를 수행 합니다.
- 원격 데스크톱 서비스 배포에 Windows Server 2016을 실행 하는 대상 서버를 가입 및 RD 게이트웨이 역할 설치
- 사용 하 여 [IIS 웹 배포 도구](https://www.iis.net/) Windows Server 2016을 실행 하는 대상 서버에 현재 RD 게이트웨이 서버에서 RD 게이트웨이 끝점 설정을 마이그레이션할 수 있습니다.
- [인증서 마이그레이션](#migrate-certificates) 대상 서버에 Windows Server 2016을 실행 합니다.
- 원격 데스크톱 서비스 배포에서 원본 서버 제거  

## <a name="migrate-rdlicensing-servers"></a>RD 라이선싱 서버 마이그레이션

Windows Server 2016을 실행 하는 대상 서버를 Windows Server 2012 또는 Windows Server 2012 R2를 실행 하는 원본 서버에서 RD 라이선싱 서버를 마이그레이션하려면 다음이 단계를 따릅니다.

1. [원격 데스크톱 서비스 클라이언트 액세스 라이선스 (RDS Cal) 마이그레이션](migrate-rds-cals.md) 대상 서버에 원본 서버에서.
2. 편집 합니다 **배포 속성** 에서 **서버 관리자** (첫 번째 RD 연결 브로커 서버에서 실행 되 고 일반적으로)이 표시 되는 원격 데스크톱 관리 서버에만 새 RD 라이선싱을 포함 하려면 Windows Server 2016을 실행 하는 서버입니다.
3. 원본 RD 라이선싱 서버를 비활성화 합니다. **원격 데스크톱 라이선스 관리자**적절 한 서버를 마우스 오른쪽 단추로 클릭, 마우스로 **고급** 선택 **비활성화 서버**, 한 다음 마법사의 단계를 따릅니다 .
4. 배포에서 원본 RD 라이선싱 서버를 제거 **서버 관리자** 원격 데스크톱 관리 서버에 있습니다.

## <a name="migrate-certificates"></a>인증서 마이그레이션

성공적인 인증서 마이그레이션이 위해서는 모두 실제 프로세스 인증서 마이그레이션 및 원격 데스크톱 서비스 배포 속성에서 인증서 정보를 업데이트 합니다.

일반적인 인증서 마이그레이션에는 다음 단계가 포함 됩니다.
- 개인 키를 사용 하 여 인증서를 PFX 파일로 내보냅니다.
- PFX 파일에서 인증서를 가져옵니다.

적절 한 인증서를 마이그레이션한 후 서버 관리자 또는 PowerShell에서 원격 데스크톱 서비스 배포에 대 한 다음 필요한 인증서를 업데이트 합니다. 
- RD 연결 브로커-single sign-on
- RD 연결 브로커-RDP 파일 게시
- RD 게이트웨이-HTTPS 연결
- RD 웹 액세스-HTTPS 연결 및 RemoteApp 및 데스크톱 연결 구독
