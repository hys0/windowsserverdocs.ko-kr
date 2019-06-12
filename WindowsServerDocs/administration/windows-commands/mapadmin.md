---
title: mapadmin
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ad9f55ba130014227326f4abe8540c78755f6c5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437368"
---
# <a name="mapadmin"></a>mapadmin



사용할 수 있습니다 **Mapadmin** 네트워크 파일 시스템에 대 한 Microsoft 서비스에 대 한 사용자 이름 매핑을 관리할 수 있습니다.

## <a name="syntax"></a>구문
```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <WindowsUser> -uu <UNIXUser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <WindowsGroup> -ug <UNIXGroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <WindowsUser> [-uu <UNIXUser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <WindowsGroup> [-ug <UNIXGroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename> 
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <WindowsDomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <WindowsDomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

## <a name="description"></a>설명
**mapadmin** 명령줄 유틸리티는 네트워크 파일 시스템에 대 한 Microsoft 서비스를 실행 하는 로컬 또는 원격 컴퓨터에서 사용자 이름 매핑를 관리 합니다. 관리 자격 증명이 없는 계정으로 로그온 하는 경우에 사용자 이름 및 수행 하는 계정의 암호를 지정할 수 있습니다.

특정 명령 인수 외에도 **mapadmin** 때 다음 인수와 옵션을 허용 합니다.

&lt;컴퓨터&gt; 관리 하려는 사용자 이름 매핑 서비스를 실행 하는 원격 컴퓨터를 지정 합니다. 인터넷 이름 서비스 WINS (Windows) 이름 또는 도메인 이름 시스템 (DNS) 이름을 사용 하 여 컴퓨터를 지정 하거나 하 여 IP (인터넷 프로토콜) 주소 수 있습니다.

-u &lt;사용자&gt; 자격 증명에 사용 하려는 사용자의 사용자 이름을 지정 합니다. 양식에서 사용자 이름에 도메인 이름을 추가 하려면 할 수 있습니다 <em>도메인</em> **\\** <em>사용자 이름</em>합니다.

-p &lt;암호&gt; 사용자의 암호를 지정 합니다. 지정 하는 경우는 **-u** 옵션은 있 생략 된 **-p** 옵션을 사용자의 암호를 묻는 메시지가 나타납니다.
특정 작업 하는 **mapadmin** 수행 지정 하는 명령 인수에 따라 달라 집니다.

## <a name="parameters"></a>매개 변수
### <a name="start"></a>start
사용자 이름 매핑 서비스를 시작합니다.

### <a name="stop"></a>stop
사용자 이름 매핑 서비스를 중지합니다.

### <a name="config"></a>구성
사용자 이름 매핑에 대 한 일반 설정을 지정합니다. 다음 옵션은이 명령 인수를 사용 하 여 사용할 수 있습니다: **-r &lt;dddd&gt;:&lt;hh&gt;:&lt;mm&gt;**  -새로 고침 간격을 지정 일, 시간 및 분 단위로 Windows 및 NIS 데이터베이스에서 업데이트 합니다. 최소 간격은 5 분입니다.
**-i {예 | 없는}** -단순한 매핑 켜 집니다 (**예**) / 사용 안 함 (**없는**). 기본적으로 단순 매핑 켜져 있습니다.
**추가** -사용자 또는 그룹에 대 한 새 매핑을 만듭니다. 다음 옵션을이 명령 인수를 사용할 수 있습니다.

|옵션|정의|
|-----|-------|
|-wu &lt;name&gt;|새 매핑을 만들 Windows 사용자의 이름을 지정 합니다.|
|-uu &lt;name&gt;|새 매핑을 만들 UNIX 사용자의 이름을 지정 합니다.|
|-wg &lt;group&gt;|새 매핑을 만들 Windows 그룹의 이름을 지정 합니다.|
|-ug &lt;group&gt;|새 매핑을 만들 UNIX 그룹의 이름을 지정 합니다.|
|-setprimary|새 매핑이 기본 매핑 임을 지정 합니다.|

**setprimary** -매핑이 여러 매핑 사용 하 여 UNIX 사용자 또는 그룹에 대 한 기본 매핑을 지정 합니다. 다음 옵션을이 명령 인수를 사용할 수 있습니다.

|옵션|정의|
|-----|-------|
|-wu &lt;name&gt;|Windows 사용자의 기본 매핑 지정합니다. 사용 하 여 사용자에 대 한 개 이상의 매핑이 있는 경우는 **-uu** 기본 매핑을 지정 하는 옵션입니다.|
|-uu &lt;name&gt;|기본 매핑 UNIX 사용자를 지정합니다.|
|-wg &lt;group&gt;|Windows 그룹의 기본 매핑 지정합니다. 사용 하 여 그룹에 대 한 개 이상의 매핑이 있는 경우는 **-ug** 기본 매핑을 지정 하는 옵션입니다.|
|-ug &lt;group&gt;|기본 매핑 UNIX 그룹을 지정합니다.|

**삭제** -사용자 또는 그룹에 대 한 매핑을 제거 합니다. 다음 옵션을이 명령 인수에 사용할 수 있습니다.

|옵션|정의|
|-----|-------|
|-wu &lt;user&gt;|에 대 한 매핑을 삭제 합니다로 지정 된 Windows 사용자 &lt; *WindowsDomain&gt;\\&lt;사용자 이름&gt;* 합니다. 지정 해야는 **-wu** 또는 **-uu** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-wu** 옵션을 모든 매핑이 지정된 된 사용자 삭제 됩니다.|
|-wg &lt;group&gt;|에 대 한 매핑을 삭제 합니다로 지정 된 Windows 그룹 &lt;WindowsDomain&gt;\\&lt;groupname&gt;합니다. 지정 해야는 **-wg** 또는 **-ug** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-wg** 옵션을 모든 매핑이 지정 된 그룹이 삭제 됩니다.|
|-uu &lt;user&gt;|UNIX 사용자에 대 한 매핑을 삭제 합니다으로 지정 &lt;사용자 이름&gt;합니다. 지정 해야는 **-wu** 또는 **-uu** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-uu** 옵션을 모든 매핑이 지정된 된 사용자 삭제 됩니다.|
|-ug &lt;group&gt;|에 대 한 매핑을 삭제 합니다로 지정 된 UNIX 그룹 &lt;groupname&gt;합니다. 지정 해야는 **-wg** 또는 **-ug** 옵션 중 하나 또는 둘 다. 두 옵션을 지정 하면 두 옵션을 통해 식별 된 특정 매핑을 삭제 됩니다. 만 지정한 경우는 **-ug** 옵션을 모든 매핑이 지정 된 그룹이 삭제 됩니다.|

**목록** -사용자 및 그룹 매핑에 대 한 정보를 표시 합니다. 다음 옵션을이 명령 인수를 사용할 수 있습니다.

|옵션|정의|
|-----|-------|
|-모두|사용자 및 그룹에 대 한 간단 하 고 고급 매핑을 나열합니다.|
|-간단한|모든 단순 매핑된 사용자 및 그룹을 나열합니다.|
|-고급|모든 고급 매핑된 사용자 및 그룹을 나열합니다. 지도 평가 되는 순서에 나열 됩니다. 별표 (*)로 표시 하는 기본 지도, 캐럿 (^)로 표시 된 보조 맵, 이어서 나열 됩니다.|
|-wu &lt;name&gt;|지정된 된 Windows 사용자에 대 한 매핑을 나열합니다.|
|-wg &lt;group&gt;|Windows 그룹에 대 한 매핑을 나열 합니다.|
|-uu &lt;name&gt;|UNIX 사용자에 대 한 매핑을 나열합니다.|
|-ug &lt;group&gt;|UNIX 그룹에 대 한 매핑을 나열 합니다.|

**백업** -저장 사용자 이름 매핑 구성 및 데이터에서 지정 된 파일 매핑 &lt;filename&gt;합니다.
**복원** -데이터 구성 및 매핑 파일에서에서 데이터를 바꿉니다 (지정 된 &lt;filename&gt;)를 사용 하 여 생성 된 합니다 **백업** 인수입니다.
**adddomainmap** -Windows 도메인 및는 NIS 도메인 또는 암호 및 그룹 파일 간의 간단한 지도 추가 합니다. 다음 옵션을이 명령 인수에 사용할 수 있습니다.

|옵션|정의|
|-----|-------|
|-d &lt;WindowsDomain&gt;|매핑할 Windows 도메인을 지정 합니다.|
|-y &lt;NISdomain&gt;|매핑할 NIS 도메인을 지정 합니다. &lt;b r /&gt;&lt;b r /&gt; **-n** &lt;nisServer&gt; 사용 하 여 지정 된 NIS 도메인에 대 한 NIS 서버를 지정 합니다 **-y**옵션입니다.|
|-f &lt;path&gt;|매핑할 암호 및 그룹 파일을 포함 하는 디렉터리의 정규화 된 경로 지정 합니다. 파일 관리 되는 컴퓨터에 있어야 하 고 사용할 수 없습니다 **mapadmin** 암호 및 그룹 파일을 기반으로 지도를 설정 하는 원격 컴퓨터를 관리 합니다.|

**removedomainmap** -Windows 도메인 / NIS 도메인 간의 간단한 맵을 제거 합니다. 다음 옵션 및 인수에는이 명령 인수에 사용할 수 있습니다.

|옵션|정의|
|-----|-------|
|-d &lt;WindowsDomain&gt;|지도를 제거할 수의 Windows 도메인을 지정 합니다.|
|-y &lt;NISdomain&gt;|제거할 맵의 NIS 도메인을 지정 합니다.|
|-모두|Windows와 NIS 도메인 간의 모든 단순 매핑 제거할 되도록 지정 합니다. 그러면 Windows 도메인 및 암호 및 그룹 파일 간의 모든 단순 맵도 제거 됩니다.|

**listdomainmaps** -NIS 도메인 또는 암호 및 그룹 파일에 매핑되는 Windows 도메인을 나열 합니다.

## <a name="notes"></a>참고
-   명령 인수를 지정 하지 않으면 **mapadmin** 사용자 이름 매핑에 대 한 현재 설정을 표시 합니다.
-   사용자 또는 그룹 이름을 지정 하는 모든 옵션에 대해 다음 형식은 사용할 수 있습니다.
-   Windows 사용자에 대 한 형식을 사용 하 여 &lt;도메인&gt;\\&lt;사용자 이름&gt;하십시오 \\ \\ &lt;컴퓨터&gt;\\&lt;사용자 이름을&gt;하십시오 \\ &lt;컴퓨터&gt;\\&lt;사용자 이름&gt;, 또는 &lt;컴퓨터&gt;\\&lt;사용자 이름&gt;
-   Windows 그룹에 대 한 형식을 사용 하 여 &lt;도메인&gt;\\&lt;&lt;groupname&gt;&gt;하십시오 \\ \\ &lt;컴퓨터&gt; \\ &lt; &lt;groupname&gt;&gt;하십시오 \\ &lt;컴퓨터&gt;\\&lt;&lt;groupname&gt; &gt;, 또는 &lt;컴퓨터&gt;\\&lt;&lt;groupname&gt;&gt;
-   UNIX 사용자에 대 한 형식을 사용 하 여 &lt;NISdomain&gt;\\&lt;사용자 이름&gt;하십시오 &lt;사용자 이름&gt;@&lt;NISdomain&gt;, 사용자&lt;이름을&gt;@PCNFS, 또는 PCNFS\\&lt;사용자 이름&gt;
-   UNIX 그룹에 대 한 형식을 사용 하 여 &lt;NISdomain&gt;\\&lt;groupname&gt;하십시오 &lt;groupname&gt;@&lt;NISdomain&gt;합니다 &lt;groupname&gt;@PCNFS, 또는 PCNFS\\&lt;groupname&gt;

## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
