---
title: 원격 데스크톱 서비스 배포를 Windows Server 2016으로 마이그레이션
description: 이 문서에서는 원격 데스크톱 서비스 배포를 새로운 Windows Server 2016 서버로 마이그레이션하는 방법을 설명합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 11/01/2016
ms.topic: article
ms.assetid: 9b1fa833-4325-48a8-bf34-46265f40c001
author: christianmontoya
manager: scottman
ms.openlocfilehash: 88806c7302474b111b700376c75b9b09f4da9236
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853006"
---
# <a name="migrate-your-remote-desktop-services-deployment-to-windows-server-2016"></a>원격 데스크톱 서비스 배포를 Windows Server 2016으로 마이그레이션

현재 Windows Server 2012 R2에서 원격 데스크톱 서비스를 실행 중인 경우 Windows Server 2016으로 이전하여 Azure SQL 및 스토리지 공간 다이렉트 지원과 같은 새 기능을 활용할 수 있습니다.

원격 데스크톱 서비스 배포는 Windows Server 2016을 실행하는 원본 서버에서 Windows Server 2016을 실행하는 대상 서버로의 마이그레이션을 지원합니다. 즉, Windows Server 2012 R2의 RDS에서 Windows Server 2016으로의 직접적인 현재 위치 마이그레이션은 지원되지 않습니다. 대신 대부분의 RDS 구성 요소의 경우 먼저 Windows Server 2016으로 업그레이드한 다음, 데이터 및 라이선스를 마이그레이션합니다. 직접 마이그레이션하는 유일한 구성 요소는 RD 웹, RD 게이트웨이 및 라이선싱 서버입니다.

업그레이드 프로세스 및 요구 사항에 대한 자세한 내용은 [원격 데스크톱 서비스 배포를 Windows Server 2016으로 업그레이드](upgrade-to-rds-2016.md)를 참조하세요.

원격 데스크톱 서비스 배포를 마이그레이션하려면 다음 단계를 따르세요.

- [RD 연결 브로커 서버 마이그레이션](#migrate-rdconnection-broker-servers)

- [세션 컬렉션 마이그레이션](#migrate-session-collections)

- [가상 데스크톱 컬렉션 마이그레이션](#migrate-virtual-desktop-collections)

- [RD 웹 액세스 서버 마이그레이션](#migrate-rdweb-access-servers)

- [RD 게이트웨이 서버 마이그레이션](#migrate-rdgateway-servers)

- [RD 라이선싱 서버 마이그레이션](#migrate-rdgateway-servers)

- [인증서 마이그레이션](#migrate-certificates)

## <a name="migrate-rdconnection-broker-servers"></a>RD 연결 브로커 서버 마이그레이션

이는 마이그레이션의 첫 번째 단계이자 가장 중요한 단계인 RD 연결 브로커를 Windows Server 2016을 실행 중인 대상 서버로 마이그레이션하는 단계입니다.

> [!IMPORTANT]
> RD(원격 데스크톱) 연결 브로커 원본 서버에서 마이그레이션을 지원하려면 서버에 고가용성을 구성해야 합니다. 자세한 내용은 [원격 데스크톱 연결 브로커 클러스터 배포](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)를 참조하세요.

1. 둘 이상의 RD 연결 브로커 서버가 고가용성으로 설정된 경우 현재 활성화된 서버를 제외하고 나머지 모든 RD 연결 브로커 서버를 제거하세요.

2. 배포의 나머지 RD 연결 브로커 서버를 Windows Server 2016으로 [업그레이드](upgrade-to-rds-2016.md)합니다.

3. 고가용성 배포에 Windows Server 2016 RD 연결 브로커 서버를 추가합니다.

> [!NOTE] 
> Windows Server 2016과 Windows Server 2012 R2가 혼합된 고가용성 구성은 RD 연결 브로커 서버에서 지원되지 않습니다. Windows Server 2016을 실행하는 RD 연결 브로커는 Windows Server 2012 R2를 실행하는 RD 세션 호스트 서버와 함께 세션 컬렉션을 제공하고, Windows Server 2012 R2를 실행하는 RD 가상화 호스트 서버와 함께 가상 데스크톱 컬렉션을 제공할 수 있습니다.

## <a name="migrate-session-collections"></a>세션 컬렉션 마이그레이션

Windows Server 2012 R2의 세션 컬렉션을 Windows Server 2016의 세션 컬렉션으로 마이그레이션하려면 다음 단계를 따릅니다.

> [!IMPORTANT]
> 위의 [RD 연결 브로커 서버 마이그레이션](#migrate-rdconnection-broker-servers) 단계를 완료한 후에만 세션 컬렉션을 마이그레이션하세요.

1. Windows Server 2012 R2에서 Windows Server 2016으로 [세션 컬렉션을 업그레이드](Upgrade-to-RDSH-2016.md)합니다.

2. Windows Server 2016을 실행하는 새 RD 세션 호스트 서버를 세션 컬렉션에 추가합니다.

3. RD 세션 호스트 서버의 모든 세션에서 로그아웃한 후 마이그레이션해야 하는 서버를 세션 컬렉션에서 제거합니다.

   > [!NOTE]
   > 세션 컬렉션에서 UVHD 템플릿(UVHD-template.vhdx)을 사용하는 경우 파일 서버를 새 서버로 마이그레이션했으면 사용자 프로필 디스크: 위치 컬렉션 속성을 새 경로로 업데이트합니다. 원본 서버와 동일한 새 위치의 상대 경로에서 사용자 프로필 디스크를 사용할 수 있어야 합니다.
   >
   > Windows Server 2012 R2와 Windows Server 2016을 실행하는 서버가 혼합된 RD 세션 호스트 서버의 세션 컬렉션은 지원되지 않습니다.

## <a name="migrate-virtual-desktop-collections"></a>가상 데스크톱 컬렉션 마이그레이션

Windows Server 2012 R2를 실행하는 원본 서버에서 Windows Server 2016을 실행하는 대상 서버로 가상 데스크톱 컬렉션을 마이그레이션하려면 다음 단계를 따릅니다.

> [!IMPORTANT]
> 위의 [RD 연결 브로커 서버 마이그레이션](#migrate-rdconnection-broker-servers) 단계를 완료한 후에만 가상 데스크톱 컬렉션을 마이그레이션하세요.

1. Windows Server 2012 R2를 실행하는 서버에서 Windows Server 2016을 실행하는 서버로 [가상 데스크톱 컬렉션을 업그레이드](Upgrade-to-RDVH-2016.md)합니다.

2. 새 Windows Server 2016 RD 가상화 호스트 서버를 가상 데스크톱 컬렉션에 추가합니다.

3. 현재 RD 가상화 호스트 서버에서 실행 중인 가상 데스크톱 컬렉션의 모든 가상 컴퓨터를 새 서버로 마이그레이션합니다.

4. 마이그레이션해야 하는 모든 RD 가상화 호스트 서버를 원본 서버의 가상 데스크톱 컬렉션에서 제거합니다.

> [!NOTE]
> 세션 컬렉션에서 UVHD 템플릿(UVHD-template.vhdx)을 사용하는 경우 파일 서버를 새 서버로 마이그레이션했으면 사용자 프로필 디스크: 위치 컬렉션 속성을 새 경로로 업데이트합니다. 원본 서버와 동일한 새 위치의 상대 경로에서 사용자 프로필 디스크를 사용할 수 있어야 합니다.
>
> Windows Server 2012 R2와 Windows Server 2016을 실행하는 서버가 혼합된 RD 가상화 호스트 서버의 가상 데스크톱 컬렉션은 지원되지 않습니다.

## <a name="migrate-rdweb-access-servers"></a>RD 웹 액세스 서버 마이그레이션

RD 웹 액세스 서버를 마이그레이션하려면 다음 단계를 따르세요.

- Windows Server 2016을 실행하는 대상 서버를 원격 데스크톱 서비스 배포에 가입시키고 RD 웹 역할을 설치합니다.

- [IIS 웹 배포 도구](https://www.iis.net/)를 사용하여 RD 웹의 웹 사이트 설정을 현재 RD 웹 액세스 서버에서 Windows Server 2016을 실행하는 대상 서버로 마이그레이션합니다.

- Windows Server 2016을 실행하는 대상 서버로 [인증서를 마이그레이션](#migrate-certificates)합니다.

- 원격 데스크톱 서비스 배포에서 원본 서버를 제거합니다.

## <a name="migrate-rdgateway-servers"></a>RD 게이트웨이 서버 마이그레이션

RD 게이트웨이 서버를 마이그레이션하려면 다음 단계를 따르세요.

- Windows Server 2016을 실행하는 대상 서버를 원격 데스크톱 서비스 배포에 가입시키고 RD 게이트웨이 역할을 설치합니다.

- [IIS 웹 배포 도구](https://www.iis.net/)를 사용하여 RD 게이트웨이 엔드포인트 설정을 현재 RD 게이트웨이 서버에서 Windows Server 2016을 실행하는 대상 서버로 마이그레이션합니다.

- Windows Server 2016을 실행하는 대상 서버로 [인증서를 마이그레이션](#migrate-certificates)합니다.

- 원격 데스크톱 서비스 배포에서 원본 서버를 제거합니다.

## <a name="migrate-rdlicensing-servers"></a>RD 라이선싱 서버 마이그레이션

Windows Server 2012 또는 Windows Server 2012 R2를 실행하는 원본 서버에서 Windows Server 2016을 실행하는 대상 서버로 RD 라이선싱 서버를 마이그레이션하려면 다음 단계를 따릅니다.

1. 원본 서버에서 대상 서버로 [RDS CAL(원격 데스크톱 서비스 클라이언트 액세스 라이선스)을 마이그레이션](migrate-rds-cals.md)합니다.

2. 원격 데스크톱 관리 서버의 **서버 관리자**에서 Windows Server 2016을 실행하는 새 RD 라이선싱 서버만 포함하도록 **배포 속성**을 편집합니다.

3. 원본 RD 라이선싱 서버를 비활성화합니다. **원격 데스크톱 라이선싱 관리자**에서 적절한 서버를 마우스 오른쪽 단추로 클릭하고 **고급**을 가리켜 **서버 비활성화**를 선택한 후 마법사의 단계를 따릅니다.

4. 원격 데스크톱 관리 서버의 **서버 관리자**에서 배포의 RD 라이선싱 서버를 제거합니다.

## <a name="migrate-certificates"></a>인증서 마이그레이션

인증서 마이그레이션에 성공하려면 원격 데스크톱 서비스 배포 속성에서 인증서를 마이그레이션하고 인증서 정보를 업데이트하는 실제 프로세스가 필요합니다.

일반적인 인증서 마이그레이션에는 다음 단계가 포함됩니다.

- 프라이빗 키와 함께 인증서를 PFX 파일로 내보내기

- PFX 파일에서 인증서 가져오기

적절한 인증서를 마이그레이션한 후에는 서버 관리자 또는 PowerShell에서 원격 데스크톱 서비스 배포에 필요한 다음과 같은 인증서를 업데이트합니다.

- RD 연결 브로커 - Single Sign-On

- RD 연결 브로커 - RDP 파일 게시

- RD 게이트웨이 - HTTPS 연결

- RD 웹 액세스 - HTTPS 연결 및 RemoteApp/데스크톱 연결 구독
