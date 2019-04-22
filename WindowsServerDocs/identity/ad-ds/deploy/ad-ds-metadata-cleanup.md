---
title: AD DS 서버 메타 데이터 정리
description: 기본 제공 도구를 사용 하 여 제거 도메인 컨트롤러에서 메타 데이터를 정리 하려면
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fbb6e720c9289c608d71d3c36695ba623a9df5f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818084"
---
# <a name="clean-up-active-directory-domain-controller-server-metadata"></a>Active Directory 도메인 컨트롤러 서버 메타 데이터 정리

적용 대상: Windows Server

메타 데이터 정리는 Active Directory Domain Services (AD DS)를 강제 제거한 후에 필요한 프로시저입니다. 강제로 제거 하는 도메인 컨트롤러를 도메인에 도메인 컨트롤러에서 메타 데이터 정리를 수행 합니다. 메타 데이터 정리는 복제 시스템에 도메인 컨트롤러를 식별 하는 AD DS에서 데이터를 제거 합니다. 메타 데이터 정리도 복제 서비스 FRS (파일) 및 분산 파일 시스템 (DFS) 복제 연결을 제거 하 고 작업 마스터 (라고도 신축 단일 마스터 작업 또는 FSMO) 역할을 점유 하거나 전송 하려고 시도 하는 사용 중지 된 도메인 컨트롤러를 보유합니다.

서버 메타 데이터를 정리 하는 방법은 세 가지가 있습니다.

- GUI 도구를 사용 하 여 서버 메타 데이터 정리
- 명령줄을 사용 하 여 서버 메타 데이터 정리
- 스크립트를 사용 하 여 서버 메타 데이터 정리

> [!NOTE]
> 메타 데이터 정리를 수행 하려면 다음이 방법 중 하나를 사용 하는 경우 "액세스가 거부 되었습니다." 오류가 표시 되 면 컴퓨터 개체와 도메인 컨트롤러의 NTDS 설정 개체를 실수로 인 한 삭제 로부터 보호 되지 않습니다 있는지 확인 합니다. 컴퓨터 개체 또는 NTDS 설정 개체를 마우스 오른쪽이 단추로 확인 하려면 **속성**, 클릭 **개체**를 선택 취소 하 고는 **실수로 삭제 되지 않도록에서 개체 보호** 확인란입니다. Active Directory 사용자 및 컴퓨터를 **개체** 클릭 하면 개체의 탭이 나타납니다 **뷰** 클릭 하 고 **고급 기능**합니다.

## <a name="clean-up-server-metadata-using-gui-tools"></a>GUI 도구를 사용 하 여 서버 메타 데이터 정리

원격 서버 관리 도구 (RSAT) 또는 Active Directory 사용자 및 도메인 컨트롤러 조직 구성 단위 (OU)에서 도메인 컨트롤러 컴퓨터 계정을 삭제 하려면 Windows Server에 포함 되어 있는 컴퓨터 콘솔 (Dsa.msc)를 사용 하는 경우는 서버 메타 데이터의 정리를 자동으로 수행 됩니다. Windows Server 2008 이전을 별도 메타 데이터 정리 절차를 수행 해야 했습니다.

또한 Active Directory 사이트 및 서비스 콘솔에서 도메인 컨트롤러의 컴퓨터 계정을 삭제 하려면 (Dssite.msc)도 메타 데이터 정리를 자동으로 완료를 사용할 수 있습니다. 그러나 Active Directory 사이트 및 서비스 메타 데이터를 자동으로 제거 합니다 dssite에서 컴퓨터 계정 아래의 NTDS 설정 개체를 먼저 삭제 해야 하는 경우에 합니다.

Windows Server 2008 또는 최신 RSAT 버전의 Dsa.msc 또는 Dssite.msc를 사용 하는으로 자동으로 이전 버전의 Windows 운영 체제를 실행 하는 도메인 컨트롤러에 대 한 메타 데이터를 정리할 수 있습니다.

멤버 자격이 **Domain Admins**, 또는 이와 동등한 다음이 절차를 완료 하려면 최소한 합니다.

## <a name="clean-up-server-metadata-using-activedirectory-users-and-computers"></a>Active Directory 사용자 및 컴퓨터를 사용 하 여 서버 메타 데이터 정리

1. **Active Directory 사용자 및 컴퓨터**를 엽니다.
2. 이 프로시저는 준비 과정에서 복제 파트너를 식별 했 고이를 정리 하는 해당 메타 데이터가 제거 도메인 컨트롤러의 복제 파트너에 연결 되지 않은 경우 마우스 오른쪽 단추로 클릭 하는 경우 **Active Directory 사용자 및 컴퓨터** 노드를 차례로 클릭 한 다음 **도메인 컨트롤러 변경**합니다. 메타 데이터를 제거 하 고 클릭 하려는는 도메인 컨트롤러의 이름을 클릭 **확인**합니다.
3. 강제로 제거 하 고 클릭 하는 도메인 컨트롤러의 도메인을 확장 **도메인 컨트롤러**합니다.
4. 세부 정보 창에서 해당 메타 데이터를 정리 하 고 클릭 하려는 도메인 컨트롤러의 컴퓨터 개체를 마우스 오른쪽 단추로 **삭제**합니다.
5. 에 **Active Directory Domain Services** 대화 상자에서 삭제 하려는 도메인 컨트롤러의 이름을 표시 되 고 클릭 **예** 컴퓨터 개체 삭제를 확인 합니다.
6. 에 **도메인 컨트롤러가 삭제** 대화 상자에서 **이 도메인 컨트롤러 영구적으로 오프 라인 상태 이며 더 이상 Active Directory Domain Services 설치 마법사 (DCPROMO)를사용하여강등수**를 클릭 하 고 **삭제**합니다.
7. 도메인 컨트롤러에서 글로벌 카탈로그 서버 인지를 **도메인 컨트롤러를 삭제** 대화 상자에서 클릭 **예** 삭제를 사용 하 여 계속 합니다.
8. 도메인 컨트롤러는 현재 하나 이상의 작업 마스터 역할 보유, 클릭 **확인** 표시 되는 도메인 컨트롤러 역할을 이동할 수 있습니다. 이 도메인 컨트롤러를 변경할 수 없습니다. 역할을 다른 도메인 컨트롤러를 이동 하려는 경우 서버 메타 데이터 정리 절차를 완료 한 후 역할을 이동 해야 합니다.

## <a name="clean-up-server-metadata-using-activedirectory-sites-and-services"></a>Active Directory 사이트 및 서비스를 사용 하 여 서버 메타 데이터 정리

1. Active Directory 사이트 및 서비스를 엽니다.
2. 이 프로시저는 준비 과정에서 복제 파트너를 식별 했 고이를 정리 하는 해당 메타 데이터가 제거 도메인 컨트롤러의 복제 파트너에 연결 되지 않은 경우 마우스 오른쪽 단추로 클릭 하는 경우 **Active Directory 사이트 및 서비스** 를 클릭 하 고 **도메인 컨트롤러 변경**합니다. 메타 데이터를 제거 하 고 클릭 하려는는 도메인 컨트롤러의 이름을 클릭 **확인**합니다.
3. 강제로 제거 된 도메인 컨트롤러의 사이트를 확장 **서버**, 도메인 컨트롤러의 이름을 확장, NTDS 설정 개체를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.
4. 에 **Active Directory 사이트 및 서비스** 대화 상자에서 클릭 **예** NTDS 설정 삭제를 확인 합니다.
5. 에 **도메인 컨트롤러가 삭제** 대화 상자에서 **이 도메인 컨트롤러 영구적으로 오프 라인 상태 이며 더 이상 Active Directory Domain Services 설치 마법사 (DCPROMO)를사용하여강등수**를 클릭 하 고 **삭제**합니다.
6. 도메인 컨트롤러에서 글로벌 카탈로그 서버 인지를 **도메인 컨트롤러를 삭제** 대화 상자에서 클릭 **예** 삭제를 사용 하 여 계속 합니다.
7. 도메인 컨트롤러는 현재 하나 이상의 작업 마스터 역할 보유, 클릭 **확인** 표시 되는 도메인 컨트롤러 역할을 이동할 수 있습니다.
8. 강제로 제거 하는 도메인 컨트롤러를 마우스 오른쪽 단추로 클릭 하 고 삭제를 클릭 합니다.
9. 에 **Active Directory Domain Services** 대화 상자에서 클릭 **예** 도메인 컨트롤러가 삭제를 확인 합니다.

## <a name="clean-up-server-metadata-using-the-command-line"></a>명령줄을 사용 하 여 서버 메타 데이터 정리

대신 Ntdsutil.exe, 모든 도메인 컨트롤러와 Active Directory Lightweight Directory Services (AD LDS) 설치 되어 있는 서버에 자동으로 설치 되어 있는 명령줄 도구를 사용 하 여 메타 데이터를 정리할 수 있습니다. Ntdsutil.exe는 rsat가 설치 된 컴퓨터에서 사용할 수도 있습니다.

## <a name="to-clean-up-server-metadata-by-using-ntdsutil"></a>Ntdsutil을 사용 하 여 서버 메타 데이터를 정리 하려면

1. 관리자 권한으로 명령 프롬프트를 엽니다. 에 **시작** 메뉴를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행**합니다. 경우는 **사용자 계정 컨트롤** 대화 상자가 나타나면 엔터프라이즈 관리자의 필요한 경우 자격 증명을 제공 하 고 클릭 **계속**합니다.
2. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

   `ntdsutil`

3. `ntdsutil:` 프롬프트에 다음 명령을 입력한 다음 Enter 키를 누릅니다.

   `metadata cleanup`

4. `metadata cleanup:` 프롬프트에 다음 명령을 입력한 다음 Enter 키를 누릅니다.

   `remove selected server <ServerName>`

5. **서버 제거 구성 대화 상자**, 정보 및 경고를 검토 한 다음 클릭 **예** 서버 개체 및 메타 데이터를 제거 합니다.

   이 시점에서 Ntdsutil 도메인 컨트롤러를 성공적으로 제거 되었는지 확인 합니다. 개체를 찾을 수 없음을 나타내는 오류 메시지가 나타나면, 도메인 컨트롤러 제거 되었거나 이전 합니다.

6. 에 `metadata cleanup:` 및 `ntdsutil:` 표시 되는 메시지를 입력 `quit`, 한 다음 ENTER를 누릅니다.

7. 에 도메인 컨트롤러의 제거를 확인 합니다.

   Active Directory 사용자 및 컴퓨터를 엽니다. 제거 된 도메인 컨트롤러의 도메인에서 클릭 **도메인 컨트롤러**합니다. 세부 정보 창에서 제거 하는 도메인 컨트롤러에 대 한 개체 표시 되지 됩니다.

   Active Directory 사이트 및 서비스를 엽니다. 로 이동 합니다 **서버** 컨테이너 NTDS 설정 개체를 제거 하는 도메인 컨트롤러에 대 한 서버 개체에 들어 있지 않음을 확인 합니다. 자식 개체가 없으면 서버 개체 아래에 나타나면, 서버 개체를 삭제할 수 있습니다. 자식 개체에 표시 되 면 다른 응용 프로그램 개체를 사용 중이기 때문에 서버 개체 삭제 하지 마세요.

## <a name="see-also"></a>관련 항목

* [도메인 컨트롤러 수준 내리기](Demoting-Domain-Controllers-and-Domains--Level-200-.md)
* [Ntdsutil 명령 참조](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753343(v=ws.10))
