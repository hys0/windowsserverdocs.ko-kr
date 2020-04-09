---
title: -DriverPackage 제거
description: 서버에서 드라이버 패키지를 제거 하는 DriverPackage의 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9eeebd0fd560f18aa49ac46f7eea30d8a9cc958
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830406"
---
# <a name="remove-driverpackage"></a>-DriverPackage 제거

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 

서버에서 드라이버 패키지를 제거합니다.

## <a name="syntax"></a>구문
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>매개 변수

|        매개 변수        |                                                                            설명                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:<Server name>] |              서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.              |
| [/ DriverPackage:<Name>] |                                                        제거할 드라이버 패키지의 이름을 지정 합니다.                                                         |
|    [/ 패키지 Id:<ID>]    | 제거할 드라이버 패키지의 Windows 배포 서비스 ID를 지정 합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우에 ID를 지정 해야 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와
이미지에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[제거 DriverPackages 명령을 사용 하 여](using-the-remove-driverpackages-command.md)
