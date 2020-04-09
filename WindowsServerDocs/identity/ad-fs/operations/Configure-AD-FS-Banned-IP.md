---
title: 금지 AD FS IP Addesses 구성
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/28/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1a1e8a9e668caa0c766f6fe3012d5ae6ecaddb50
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859926"
---
# <a name="ad-fs-and-banned-ip-addresses"></a>AD FS 및 금지 IP 주소


6 월 2018에 Windows Server 2016의 AD FS에는 AD FS 6 월 2018 업데이트를 사용 하 여 **금지 된 ip** 가 도입 되었습니다.  이 업데이트를 사용 하면 AD FS에서 전역적으로 IP 주소 집합을 구성 하 여 해당 IP 주소에서 오는 요청이 나 **x로 전달** 된 (또는 x-AD FS **m** ---------------------------------------

## <a name="adding-banned-ips"></a>금지 Ip 추가
전역 목록에 금지 된 Ip를 추가 하려면 아래 Powershell cmdlet을 사용 합니다.

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

허용 되는 형식

1.  IPv4
2.  IPv6
3.  IPv4 또는 v6를 사용 하는 CIDR 형식

금지 된 IP 주소에 대 한 항목 수는 300 개로 제한 됩니다. CIDR 또는 range 형식을 사용 하 여 단일 항목으로 많은 항목 블록을 거부할 수 있습니다.

## <a name="removing-banned-ips"></a>금지 Ip 제거
전역 목록에서 금지 된 Ip를 제거 하려면 아래 Powershell cmdlet을 사용 합니다.

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>금지 Ip 읽기
현재 금지 된 IP 주소 집합을 읽으려면 아래 Powershell cmdlet을 사용 합니다.

``` powershell
PS C:\ >Get-AdfsProperties 
```

출력의 예:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>추가 참조  
[Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
