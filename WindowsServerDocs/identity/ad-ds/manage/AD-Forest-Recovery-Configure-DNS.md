---
title: AD 포리스트 복구-DNS 서버 서비스 구성
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 144a45f2a835d9cca60b5be5aac7569809c45b7c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824176"
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD 포리스트 복구-DNS 서버 서비스 구성

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

백업에서 복원 하는 DC에 DNS 서버 역할이 설치 되어 있지 않으면 DNS 서버를 설치 하 고 구성 해야 합니다. 

## <a name="install-and-configure-the-dns-server-service"></a>DNS 서버 서비스 설치 및 구성

복원이 완료 된 후 DNS 서버로 실행 되지 않는 복원 된 각 DC에 대해이 단계를 완료 합니다. 

> [!NOTE]
> 백업에서 복원한 DC가 Windows Server 2008 r 2를 실행 하는 경우 DNS 서버를 설치 하려면 격리 된 네트워크에 DC를 연결 해야 합니다. 그런 다음, 복원 된 각 DNS 서버를 상호 공유 격리 된 네트워크에 연결 합니다. Repadmin/replsum를 실행 하 여 복원 된 DNS 서버 간에 복제가 작동 하는지 확인 합니다. 복제를 확인 한 후에는 복원 된 Dc를 프로덕션 네트워크에 연결할 수 있습니다. DNS 서버 역할이 이미 설치 되어 있으면 서버가 네트워크에 연결 되어 있지 않은 상태에서 DNS 서버를 시작할 수 있도록 하는 핫픽스를 적용할 수 있습니다. 자동화 된 빌드 프로세스 중에 핫픽스를 운영 체제 설치 이미지에 통합 설치 해야 합니다. 핫픽스에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 975654](https://go.microsoft.com/fwlink/?LinkId=184691) (https://go.microsoft.com/fwlink/?LinkId=184691)를 참조 하십시오. 

아래 설치 및 구성 단계를 완료 합니다.

### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>서버 관리자를 사용 하 여 및 DNS 서버 서비스를 설치 하려면  

1. 서버 관리자 열고 **역할 및 기능 추가**를 클릭 합니다. 
2. 역할 추가 마법사에서 **시작하기 전에** 페이지가 나타나면 **다음**을 클릭합니다. 
3. **설치 유형** 화면에서 **역할 기반 또는 기능 기반 설치** 를 선택 하 고 **다음**을 클릭 합니다.
4. **서버 선택** 화면에서 서버를 선택 하 고 **다음**을 클릭 합니다.
5. **서버 역할** 화면에서 **DNS 서버**를 선택 하 고, 메시지가 표시 되 면 **기능 추가** 를 클릭 하 고 **다음**을 클릭 합니다.
6. **기능** 화면에서 **다음**을 클릭 합니다.
7. **DNS 서버** 페이지의 정보를 읽은 후 **다음**을 클릭 합니다.
   DNS 서버 ![](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8. **확인** 페이지에서 DNS 서버 역할이 설치 되어 있는지 확인 한 다음 **설치**를 클릭 합니다. 

### <a name="to-configure-the-dns-server-service"></a>DNS 서버 서비스를 구성 하려면

1. 서버 관리자 열고 **도구** 를 클릭 한 다음 **DNS**를 클릭 합니다.
   DNS 서버 ![](media/AD-Forest-Recovery-Configure-DNS/dns2.png)
2. 중요 한 오작동 전에 DNS 서버에 호스트 된 동일한 DNS 도메인 이름에 대 한 DNS 영역을 만듭니다. 자세한 내용은 전방 조회 영역 추가 ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))를 참조 하세요.
3. 중요 한 오작동 이전의 DNS 데이터를 구성 합니다. 예를 들면 다음과 같습니다.  

   - AD DS에 저장할 DNS 영역을 구성 합니다. 자세한 내용은 영역 유형 변경 ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))을 참조 하세요.
   - 도메인 컨트롤러 로케이터 (DC 로케이터) 리소스 레코드에 대 한 권한이 있는 DNS 영역을 구성 하 여 보안 동적 업데이트를 허용 합니다. 자세한 내용은 보안 동적 업데이트만 허용 ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))을 참조 하세요.

4. 부모 DNS 영역에이 DNS 서버에서 호스트 되는 자식 영역에 대 한 위임 리소스 레코드 (이름 서버 (NS) 및 glue host (A) 리소스 레코드)가 포함 되어 있는지 확인 합니다. 자세한 내용은 영역 위임 만들기 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562))를 참조 하세요.
5. DNS를 구성한 후에는 NETLOGON 레코드 등록 속도를 높일 수 있습니다.

   > [!NOTE]
   > 보안 동적 업데이트는 글로벌 카탈로그 서버를 사용할 수 있는 경우에만 작동 합니다. 

   명령 프롬프트에서 다음 명령을 입력한 다음 Enter 키를 누릅니다.  

   **net stop netlogon**  

6. 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   **net start netlogon**  

   ![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
