---
title: mapadmin
description: 네트워크 파일 시스템용 Microsoft 서비스에 대 한 사용자 이름 매핑를 관리 하는 mapadmin 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 059419a134b62ec92b30feacd086e7d7116aab25
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354653"
---
# <a name="mapadmin"></a>mapadmin

**Mapadmin** 명령줄 유틸리티는 네트워크 파일 시스템용 Microsoft 서비스를 실행 하는 로컬 또는 원격 컴퓨터에서 사용자 이름 매핑를 관리 합니다. 관리 자격 증명이 없는 계정으로 로그온 하는 경우에 사용자 이름 및 수행 하는 계정의 암호를 지정할 수 있습니다.

## <a name="syntax"></a>구문

```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <windowsuser> -uu <UNIXuser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <windowsgroup> -ug <UNIXgroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <Windowsuser> [-uu <UNIXuser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <Windowsgroup> [-ug <UNIXgroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <Windowsdomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <Windowsdomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<computer>` | 관리 하려는 사용자 이름 매핑 서비스를 실행 하는 원격 컴퓨터를 지정 합니다. 인터넷 이름 서비스 WINS (Windows) 이름 또는 도메인 이름 시스템 (DNS) 이름을 사용 하 여 컴퓨터를 지정 하거나 하 여 IP (인터넷 프로토콜) 주소 수 있습니다. |
| -u`<user>` | 자격 증명에 사용 하려는 사용자의 사용자 이름을 지정 합니다. 사용자 이름에 도메인 이름을 *domain\username*형식으로 추가 해야 할 수도 있습니다. |
| -p `<password>` | 사용자의 암호를 지정 합니다. 지정 하는 경우는 **-u** 옵션은 있 생략 된 **-p** 옵션을 사용자의 암호를 묻는 메시지가 나타납니다. |
| `start | stop` | 사용자 이름 매핑 서비스를 시작 하거나 중지 합니다. |
| config | 사용자 이름 매핑에 대 한 일반 설정을 지정합니다. 이 매개 변수와 함께 사용할 수 있는 옵션은 다음과 같습니다.<ul><li>**-r `<dddd>:<hh>:<mm>` :** Windows 및 NIS 데이터베이스에서 업데이트를 위한 새로 고침 간격을 일, 시간 및 분 단위로 지정 합니다. 최소 간격은 5 분입니다.</li><li>**-i `{yes | no}` :** 단순 매핑을 설정 (**예**) 또는 해제 (**아니요**) 합니다. 기본적으로 매핑은 설정 되어 있습니다.</li></ul> |
| 추가 | 사용자 또는 그룹에 대 한 새 매핑을 만듭니다. 이 매개 변수와 함께 사용할 수 있는 옵션은 다음과 같습니다.<ul><li>**-wu `<name>` :** 새 매핑을 만들 Windows 사용자의 이름을 지정 합니다.</li><li>**-uu `<name>` :** 새 매핑을 만들 UNIX 사용자의 이름을 지정 합니다.</li><li>**-wg `<group>` :** 새 매핑을 만들 Windows 그룹의 이름을 지정 합니다.</li><li>**-ug `<group>` :** 새 매핑을 만들 UNIX 그룹의 이름을 지정 합니다.</li><li>**-setprimary:** 새 매핑이 기본 매핑 임을 지정 합니다.</li></ul> |
| setprimary | 여러 매핑이 있는 UNIX 사용자 또는 그룹에 대 한 기본 매핑 인 매핑을 지정 합니다. 이 매개 변수와 함께 사용할 수 있는 옵션은 다음과 같습니다.<ul><li>**-wu `<name>` :** 기본 매핑의 Windows 사용자를 지정 합니다. 사용 하 여 사용자에 대 한 개 이상의 매핑이 있는 경우는 **-uu** 기본 매핑을 지정 하는 옵션입니다.</li><li>**-uu `<name>` :** 기본 매핑의 UNIX 사용자를 지정 합니다.</li><li>**-wg `<group>` :** 기본 매핑의 Windows 그룹을 지정 합니다. 사용 하 여 그룹에 대 한 개 이상의 매핑이 있는 경우는 **-ug** 기본 매핑을 지정 하는 옵션입니다.</li><li>**-ug `<group>` :** 기본 매핑의 UNIX 그룹을 지정 합니다.</li></ul> |
| delete | 사용자 또는 그룹에 대 한 매핑을 제거 합니다. 이 매개 변수에 사용할 수 있는 옵션은 다음과 같습니다.<ul><li>**-wu `<user>` :** 매핑을 삭제할 Windows 사용자를 지정 하며로 지정 됩니다 `<windowsdomain>\<username>` .<p>지정 해야는 **-wu** 또는 **-uu** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-wu** 옵션을 모든 매핑이 지정된 된 사용자 삭제 됩니다.</li><li>**-uu `<user>` :** 매핑을 삭제할 UNIX 사용자를 지정 합니다 .이 사용자는로 지정 됩니다 `<username>` .<p>지정 해야는 **-wu** 또는 **-uu** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-uu** 옵션을 모든 매핑이 지정된 된 사용자 삭제 됩니다.</li><li>**-wg `<group>` :** 매핑을 삭제할 Windows 그룹을 지정 합니다. 여기서로 지정 됩니다 `<windowsdomain>\<username>` .<p>지정 해야는 **-wg** 또는 **-ug** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-wg** 옵션을 모든 매핑이 지정 된 그룹이 삭제 됩니다.</li><li>**-ug `<group>` :** 매핑을 삭제할 UNIX 그룹을 지정 합니다. 여기서로 지정 됩니다 `<groupname>` .<p>지정 해야는 **-wg** 또는 **-ug** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-ug** 옵션을 모든 매핑이 지정 된 그룹이 삭제 됩니다.</li></ul> |
| list | 사용자 및 그룹 매핑에 대 한 정보를 표시 합니다. 이 매개 변수와 함께 사용할 수 있는 옵션은 다음과 같습니다.<ul><li>**-모두:** 사용자 및 그룹에 대 한 단순 및 고급 매핑을 모두 나열 합니다.</li><li>**-단순:** 모든 단순 매핑된 사용자 및 그룹을 나열 합니다.</li><li>**-고급:** 모든 고급 매핑된 사용자 및 그룹을 나열 합니다. 지도 평가 되는 순서에 나열 됩니다. 별표 ()로 표시 된 기본 맵은*먼저 나열 되 고 그 뒤에 캐럿로 표시 된 보조 맵이 나열 됩니다 `(^)` . </li> <li> * *-wu `<name>` :** 지정 된 Windows 사용자에 대 한 매핑을 나열 합니다.</li><li>**-wg `<group>` :** Windows 그룹에 대 한 매핑을 나열 합니다.</li><li>**-uu `<name>` :** UNIX 사용자에 대 한 매핑을 나열 합니다.</li><li>**-ug `<group>` :** UNIX 그룹에 대 한 매핑을 나열 합니다.</li></ul> |
| 백업(backup) | 사용자 이름 매핑 구성 및 매핑 데이터를에 지정 된 파일에 저장 `<filename>` 합니다. |
| 복원 | 구성 및 매핑 데이터를 `<filename>` **백업** 매개 변수를 사용 하 여 만든 파일의 데이터 (에 의해 지정 됨)로 바꿉니다. |
| adddomainmap | Windows 도메인과 NIS 도메인 또는 암호 및 그룹 파일 간에 간단한 맵을 추가 합니다. 이 매개 변수에 사용할 수 있는 옵션은 다음과 같습니다.<ul><li>**-d `<windowsdomain>` :** 매핑할 Windows 도메인을 지정 합니다.</li><li>**-y `<NISdomain>` :** 매핑할 NIS 도메인을 지정 합니다. - **Y** 옵션으로 지정 된 nis 도메인에 대해 nis 서버를 지정 하려면 **-n `<NISserver>` ** 매개 변수를 사용 해야 합니다.</li><li>**-f `<path>` :** 매핑할 암호 및 그룹 파일을 포함 하는 디렉터리의 정규화 된 경로를 지정 합니다. 파일은 관리 되는 컴퓨터에 있어야 하며, **mapadmin** 을 사용 하 여 원격 컴퓨터를 관리 하 고 암호 및 그룹 파일에 따라 맵을 설정할 수 없습니다.</li></ul> |
| removedomainmap | Windows 도메인과 NIS 도메인 간의 단순 맵을 제거 합니다. 이 매개 변수에 사용할 수 있는 옵션 및 인수는 다음과 같습니다.<ul><li>**-d `<windowsdomain>` :** 제거할 맵의 Windows 도메인을 지정 합니다.</li><li>**-y `<NISdomain>` :** 제거할 맵의 NIS 도메인을 지정 합니다.</li><li>**-모두:** Windows와 NIS 도메인 간의 모든 단순 맵을 제거 하도록 지정 합니다. 그러면 Windows 도메인 및 암호 및 그룹 파일 간의 모든 단순 맵도 제거 됩니다.</li></ul> |
| listdomainmaps | NIS 도메인 또는 암호 및 그룹 파일에 매핑된 Windows 도메인을 나열 합니다. |

#### <a name="remarks"></a>설명

- 매개 변수를 지정 하지 않으면 **mapadmin** 명령은 사용자 이름 매핑에 대 한 현재 설정을 표시 합니다.

- 사용자 또는 그룹 이름을 지정 하는 모든 옵션에 대 한 다음 형식은 사용할 수 있습니다.

    - Windows 사용자의 경우 형식 (,, `<domain>\<username>` `\\<computer>\<username>` `\<computer>\<username>` 또는)을 사용 합니다.`<computer>\<username>`

    - Windows 그룹의 경우,, 또는 형식을 사용 합니다. `<domain>\<groupname>` `\\<computer>\<groupname>` `\<computer>\<groupname>``<computer>\<groupname>`

    - UNIX 사용자의 경우 형식 (,, `<NISdomain>\<username>` `<username>@<NISdomain>` `<username>@PCNFS` 또는)을 사용 합니다.`PCNFS\<username>`

    - UNIX 그룹의 경우,, 또는 형식을 사용 합니다. `<NISdomain>\<groupname>` `<groupname>@<NISdomain>` `<groupname>@PCNFS``PCNFS\<groupname>`

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
