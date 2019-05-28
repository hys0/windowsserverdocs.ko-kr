---
title: 구성 AD FS로 IP 주소 차단
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/28/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 01ef992554a1e0961d8d795e9baa7730a1a1d682
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189893"
---
# <a name="ad-fs-and-banned-ip-addresses"></a>AD FS 및 금지 된 IP 주소


Windows Server 2016에서 AD FS 2018 년 6 월에에서 도입 **Ip 차단** AD FS를 사용 하 여 2018 년 6 월 업데이트 합니다.  이 업데이트를 사용 하면 AD FS에서 IP 주소 집합을 전역적으로 구성 하려면 또는 해당 IP 주소에서 들어오는 요청 해당 IP 주소를 가질 수 있도록 합니다 **x-전달 기능에 대 한** 또는 **x-ms-전달-클라이언트-ip** 헤더를 AD FS에서 차단 됩니다.

## <a name="adding-banned-ips"></a>Ip 차단 추가
전역 목록에 금지 된 Ip를 추가 하려면 사용는 아래 Powershell cmdlet:

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

허용 된 형식

1.  IPv4
2.  IPv6
3.  IPv4 또는 v6을 사용 하 여 CIDR 형식

금지 된 IP 주소에 대 한 항목이 300 개의 제한이 있습니다. 단일 항목을 사용 하 여 항목의 큰 블록을 거부 하려면 CIDR 또는 범위 형식을 사용할 수 있습니다.

## <a name="removing-banned-ips"></a>Ip 차단 제거
전역 목록에서 금지 된 Ip를 제거 하려면 사용는 아래 Powershell cmdlet:

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>Ip를 차단 하는 읽기
금지 된 IP 주소의 현재 집합을 읽으려면 사용은 아래 Powershell cmdlet:

``` powershell
PS C:\ >Get-AdfsProperties 
```

출력의 예:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>추가 참조  
[Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
