---
title: AD 포리스트 복구를 구성 하는 DNS 서버 서비스
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2c37428a0fb685e6a7fa4875366f3cd13401bd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842964"
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD 포리스트 복구-DNS 서버 서비스 구성

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

백업에서 복원 하는 DC에 DNS 서버 역할 설치 되어 있지 않으면를 설치 하 고 DNS 서버를 구성 해야 합니다. 

## <a name="install-and-configure-the-dns-server-service"></a>DNS 서버 서비스 설치 및 구성

복원이 완료 된 후 DNS 서버를 실행 하지 않는 각 복원 된 DC에 대 한이 단계를 완료 합니다. 

> [!NOTE]
> 백업에서 복원 하는 DC가 Windows Server 2008 R2를 실행 하는 경우 DNS 서버를 설치 하기 위해 격리 된 네트워크에 DC를 연결 해야 합니다. 다음 DNS 서버를 복원 된 각 상호 공유 되는 격리 된 네트워크에 연결 합니다. 복원 된 DNS 서버 간 복제가 작동 중인지 확인 하려면 repadmin /replsum을 실행 합니다. 복제를 확인 한 후 DNS 서버 역할이 이미 설치 하는 경우 복원 된 dc가 프로덕션 네트워크에 연결할 수 있습니다, DNS 서버는 서버가 네트워크에 연결 되지 않은 동안에 시작할 수 있도록 하는 핫픽스를 적용할 수 있습니다. 자동화 된 빌드 프로세스 중 운영 체제 설치 이미지에 핫픽스를 통합 설치할 해야 있습니다. 핫픽스에 대 한 자세한 내용은 참조 하세요. [문서 975654](https://go.microsoft.com/fwlink/?LinkId=184691) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=184691)합니다. 

아래 설치 및 구성 단계를 완료 합니다.

### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>설치 및 서버 관리자를 사용 하 여 DNS 서버 서비스  

1. 서버 관리자를 열고 클릭 **역할 및 기능 추가**합니다. 
2. 역할 추가 마법사에서 **시작하기 전에** 페이지가 나타나면 **다음**을 클릭합니다. 
3. 에 **설치 유형을** 화면 **역할 기반 또는 기능 기반 설치** 클릭 **다음**합니다.
4. 에 **서버 선택** 화면 서버를 선택 하 고 클릭 **다음**합니다.
5. 에 **서버 역할** 화면 **DNS 서버**클릭 메시지가 표시 되 면, **추가 기능** 클릭 **다음**합니다.
6. 에 **기능** 화면 클릭 **다음**합니다.
7. 정보를 읽은 합니다 **DNS 서버** 페이지를 선택한 다음 클릭 **다음**합니다.
   ![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8. 에 **확인** 페이지에서 확인 하는 DNS 서버 역할 설치 되 고 클릭 **설치**합니다. 

### <a name="to-configure-the-dns-server-service"></a>DNS 서버 서비스를 구성 하려면

1. 서버 관리자를 열고 **도구가** 클릭 **DNS**합니다.
   ![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns2.png)
2. 중요 한 고장 하기 전에 DNS 서버에서 호스팅되는 동일한 DNS 도메인 이름에 대 한 DNS 영역을 만듭니다. 자세한 내용은 정방향 조회 영역을 추가 참조 ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).
3. 중요 한 고장 전에 존재 했던 대로 DNS 데이터를 구성 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

   - AD DS에 저장 될 DNS 영역을 구성 합니다. 자세한 내용은 참조 영역 종류 변경 ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).
   - 보안 동적 업데이트를 허용 하도록 도메인 컨트롤러 로케이터 (DC 로케이터) 리소스 레코드에 대 한 권한이 있는 DNS 영역을 구성 합니다. 자세한 내용은 허용 보안 동적 업데이트만 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).

4. 부모 DNS 영역에 위임 리소스 레코드 (이름 서버 (NS) 및 붙이기 호스트 (A) 리소스 레코드)이 DNS 서버에서 호스트 되는 자식 영역에 대 한이 포함 되어 있는지 확인 합니다. 자세한 내용은 영역 위임을 만들기를 참조 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).
5. DNS를 구성 하 고 나면 NETLOGON 레코드의 등록을 단축할 수 있습니다.

   > [!NOTE]
   > 보안 동적 업데이트는 글로벌 카탈로그 서버를 사용할 수 있을 때에 작동 합니다. 

   명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.  

   **net stop netlogon**  

6. 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   **net 시작 netlogon**  

   ![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
