---
title: AD DS 서버 메타 데이터 정리
description: 기본 제공 도구를 사용 하 여 제거 된 도메인 컨트롤러에서 메타 데이터 정리
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 7c9750a4f59cd17d0495e58dbc2fd8b2d2802c89
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369531"
---
# <a name="clean-up-active-directory-domain-controller-server-metadata"></a>Active Directory 도메인 컨트롤러 서버 메타 데이터 정리

적용 대상: Windows Server

메타 데이터 정리는 Active Directory Domain Services (AD DS)를 강제로 제거한 후에 필요한 절차입니다. 강제로 제거한 도메인 컨트롤러의 도메인에 있는 도메인 컨트롤러에서 메타 데이터 정리를 수행 합니다. 메타 데이터 정리는 도메인 컨트롤러를 식별 하는 AD DS에서 복제 시스템으로 데이터를 제거 합니다. 또한 메타 데이터 정리는 FRS (파일 복제 서비스) 및 분산 파일 시스템 (DFS) 복제 연결을 제거 하 고, 사용 중지 된 도메인에 있는 모든 작업 마스터 (FSMO (신축 단일 마스터 작업) 라고도 함) 역할을 양도 하거나 점유 하려고 합니다. 컨트롤러 보유.

서버 메타 데이터를 정리 하는 세 가지 옵션이 있습니다.

- GUI 도구를 사용 하 여 서버 메타 데이터 정리
- 명령줄을 사용 하 여 서버 메타 데이터 정리
- 스크립트를 사용 하 여 서버 메타 데이터 정리

> [!NOTE]
> 이러한 방법 중 하나를 사용 하 여 메타 데이터 정리를 수행 하는 경우 "액세스가 거부 되었습니다." 오류가 표시 되 면 도메인 컨트롤러에 대 한 컴퓨터 개체와 NTDS 설정 개체가 실수로 삭제 되지 않도록 보호 되는지 확인 합니다. 컴퓨터 개체 또는 NTDS 설정 개체를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 **개체**를 클릭 하 고 **실수로 삭제 되지 않도록 개체 보호** 확인란의 선택을 취소 하 여이를 확인 합니다. 사용자 및 컴퓨터 Active Directory에서 **보기** 를 클릭 한 다음 **고급 기능**을 클릭 하면 개체의 **개체** 탭이 표시 됩니다.

## <a name="clean-up-server-metadata-using-gui-tools"></a>GUI 도구를 사용 하 여 서버 메타 데이터 정리

도메인 컨트롤러 OU (조직 구성 단위)에서 도메인 컨트롤러 컴퓨터 계정을 삭제 하기 위해 Windows Server에 포함 된 Active Directory 사용자 및 컴퓨터 콘솔 (Dsa.msc) 또는 원격 서버 관리 도구 (RSAT)를 사용 하는 경우 서버 메타 데이터의 정리는 자동으로 수행 됩니다. Windows Server 2008 이전에는 별도의 메타 데이터 정리 절차를 수행 해야 했습니다.

Active Directory 사이트 및 서비스 콘솔 (Dssite.msc)을 사용 하 여 도메인 컨트롤러의 컴퓨터 계정을 삭제할 수도 있습니다. 이렇게 하면 메타 데이터 정리가 자동으로 완료 됩니다. 그러나 Active Directory 사이트와 서비스는 먼저 Dssite.msc의 컴퓨터 계정 아래에서 NTDS 설정 개체를 삭제 하는 경우에만 메타 데이터를 자동으로 제거 합니다.

Windows Server 2008 또는 새 RSAT 버전의 Dsa.msc 또는 Dssite.msc를 사용 하는 동안 이전 버전의 Windows 운영 체제를 실행 하는 도메인 컨트롤러에 대해 메타 데이터를 자동으로 정리할 수 있습니다.

멤버 자격이 **Domain Admins**, 또는 이와 동등한 다음이 절차를 완료 하려면 최소한 합니다.

## <a name="clean-up-server-metadata-using-activedirectory-users-and-computers"></a>Active Directory 사용자 및 컴퓨터를 사용 하 여 서버 메타 데이터 정리

1. **Active Directory 사용자 및 컴퓨터**를 엽니다.
2. 이 절차를 준비 하는 동안 복제 파트너를 확인 했 고 해당 메타 데이터를 제거 하는 제거 된 도메인 컨트롤러의 복제 파트너에 연결 하지 않은 경우 **Active Directory 사용자 및 컴퓨터** 노드를 마우스 오른쪽 단추로 클릭 합니다. 을 클릭 한 다음 **도메인 컨트롤러 변경**을 클릭 합니다. 메타 데이터를 제거할 도메인 컨트롤러의 이름을 클릭 한 다음 **확인**을 클릭 합니다.
3. 강제로 제거 된 도메인 컨트롤러의 도메인을 확장 한 다음 **도메인 컨트롤러**를 클릭 합니다.
4. 세부 정보 창에서 메타 데이터를 정리할 도메인 컨트롤러의 컴퓨터 개체를 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 클릭 합니다.
5. **Active Directory Domain Services** 대화 상자에서 삭제 하려는 도메인 컨트롤러의 이름이 표시 되는지 확인 하 고 **예** 를 클릭 하 여 컴퓨터 개체 삭제를 확인 합니다.
6. **도메인 컨트롤러 삭제** 대화 상자에서 **이 도메인 컨트롤러가 영구적으로 오프 라인 상태이 고 Active Directory Domain Services 설치 마법사 (DCPROMO)를 사용 하 여 더 이상 수준을 내릴 수 없음**을 선택 하 고 **삭제**를 클릭 합니다.
7. 도메인 컨트롤러가 글로벌 카탈로그 서버인 경우 **도메인 컨트롤러 삭제** 대화 상자에서 **예** 를 클릭 하 여 삭제를 계속 합니다.
8. 도메인 컨트롤러가 현재 하나 이상의 작업 마스터 역할을 보유 하는 경우 **확인** 을 클릭 하 여 표시 된 도메인 컨트롤러로 역할을 이동 합니다. 이 도메인 컨트롤러를 변경할 수 없습니다. 역할을 다른 도메인 컨트롤러로 이동 하려면 서버 메타 데이터 정리 절차를 완료 한 후 역할을 이동 해야 합니다.

## <a name="clean-up-server-metadata-using-activedirectory-sites-and-services"></a>Active Directory 사이트 및 서비스를 사용 하 여 서버 메타 데이터 정리

1. Active Directory 사이트 및 서비스를 엽니다.
2. 이 절차를 준비 하는 동안 복제 파트너를 확인 했 고 해당 메타 데이터를 제거 하는 제거 된 도메인 컨트롤러의 복제 파트너에 연결 되어 있지 않은 경우 **사이트 및 서비스 Active Directory**를 마우스 오른쪽 단추로 클릭 하 고 그런 다음 **도메인 컨트롤러 변경**을 클릭 합니다. 메타 데이터를 제거할 도메인 컨트롤러의 이름을 클릭 한 다음 **확인**을 클릭 합니다.
3. 강제로 제거 된 도메인 컨트롤러의 사이트를 확장 하 고 **서버**를 확장 한 다음 도메인 컨트롤러의 이름을 확장 하 고 NTDS 설정 개체를 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 클릭 합니다.
4. **사이트 및 서비스 Active Directory** 대화 상자에서 **예** 를 클릭 하 여 NTDS 설정 삭제를 확인 합니다.
5. **도메인 컨트롤러 삭제** 대화 상자에서 **이 도메인 컨트롤러가 영구적으로 오프 라인 상태이 고 Active Directory Domain Services 설치 마법사 (DCPROMO)를 사용 하 여 더 이상 수준을 내릴 수 없음**을 선택 하 고 **삭제**를 클릭 합니다.
6. 도메인 컨트롤러가 글로벌 카탈로그 서버인 경우 **도메인 컨트롤러 삭제** 대화 상자에서 **예** 를 클릭 하 여 삭제를 계속 합니다.
7. 도메인 컨트롤러가 현재 하나 이상의 작업 마스터 역할을 보유 하는 경우 **확인** 을 클릭 하 여 표시 된 도메인 컨트롤러로 역할을 이동 합니다.
8. 강제로 제거 된 도메인 컨트롤러를 마우스 오른쪽 단추로 클릭 한 다음 삭제를 클릭 합니다.
9. **Active Directory Domain Services** 대화 상자에서 **예** 를 클릭 하 여 도메인 컨트롤러 삭제를 확인 합니다.

## <a name="clean-up-server-metadata-using-the-command-line"></a>명령줄을 사용 하 여 서버 메타 데이터 정리

또는 Active Directory LDS(Lightweight Directory Services) (AD LDS)를 설치한 모든 도메인 컨트롤러 및 서버에 자동으로 설치 되는 명령줄 도구인 Ntdsutil.exe를 사용 하 여 메타 데이터를 정리할 수 있습니다. Ntdsutil.exe는 RSAT가 설치 된 컴퓨터 에서도 사용할 수 있습니다.

## <a name="to-clean-up-server-metadata-by-using-ntdsutil"></a>Ntdsutil을 사용 하 여 서버 메타 데이터를 정리 하려면

1. 관리자 권한으로 명령 프롬프트를 엽니다. **시작** 메뉴에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 필요한 경우 엔터프라이즈 관리자의 자격 증명을 입력 하 고 **계속**을 클릭 합니다.
2. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

   `ntdsutil`

3. `ntdsutil:` 프롬프트에 다음 명령을 입력한 다음 Enter 키를 누릅니다.

   `metadata cleanup`

4. `metadata cleanup:` 프롬프트에 다음 명령을 입력한 다음 Enter 키를 누릅니다.

   `remove selected server <ServerName>`

5. **서버 구성 제거 대화 상자**에서 정보 및 경고를 검토 한 다음 **예** 를 클릭 하 여 서버 개체 및 메타 데이터를 제거 합니다.

   이 시점에서 Ntdsutil은 도메인 컨트롤러가 성공적으로 제거 되었음을 확인 합니다. 개체를 찾을 수 없음을 나타내는 오류 메시지가 표시 되 면 도메인 컨트롤러가 이전에 제거 되었을 수 있습니다.

6. 및 프롬프트에서를 입력 `quit`한 다음 enter 키를 누릅니다. `ntdsutil:` `metadata cleanup:`

7. 도메인 컨트롤러의 제거를 확인 하려면:

   Active Directory 사용자 및 컴퓨터를 엽니다. 제거 된 도메인 컨트롤러의 도메인에서 **도메인 컨트롤러**를 클릭 합니다. 세부 정보 창에서 제거한 도메인 컨트롤러에 대 한 개체는 표시 되지 않습니다.

   Active Directory 사이트 및 서비스를 엽니다. **서버** 컨테이너로 이동 하 여 제거한 도메인 컨트롤러에 대 한 서버 개체에 NTDS 설정 개체가 포함 되어 있지 않은지 확인 합니다. 서버 개체 아래에 자식 개체가 나타나지 않으면 서버 개체를 삭제할 수 있습니다. 자식 개체가 표시 되는 경우 다른 응용 프로그램에서 개체를 사용 하 고 있기 때문에 서버 개체를 삭제 하지 마십시오.

## <a name="see-also"></a>관련 항목

* [도메인 컨트롤러 수준 내리기](Demoting-Domain-Controllers-and-Domains--Level-200-.md)
* [Ntdsutil 명령 참조](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753343(v=ws.10))
