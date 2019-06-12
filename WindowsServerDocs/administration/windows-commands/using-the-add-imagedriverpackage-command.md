---
title: 추가 ImageDriverPackage 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c2a4833-6427-47f8-9ffb-20b3786cb406
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38d6c032f347f9945701f17b9289f3e3ff474031
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440626"
---
# <a name="using-the-add-imagedriverpackage-command"></a>추가 ImageDriverPackage 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 기존 부팅 이미지에 드라이버 저장소에 있는 드라이버 패키지를 추가 합니다. Windows 7 또는 Windows Server 2008 R2 이미지 버전 이어야 합니다. 이상.
## <a name="syntax"></a>구문
```
wdsutil /add-ImageDriverPackage [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} 
```
```
[/Filename:<File name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>매개 변수

|                 매개 변수                  |                                                                                                                                                                                                            설명                                                                                                                                                                                                             |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           [/Server:<Server name>           |                                                                                                                                               서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.                                                                                                                                                |
|             미디어:<Image name>             |                                                                                                                                                                                       드라이버를 추가 하는 이미지의 이름을 지정 합니다.                                                                                                                                                                                        |
|               mediatype:Boot               |                                                                                                                                                                드라이버를 추가 하는 이미지의 유형을 지정 합니다. 드라이버 패키지는 부팅 이미지에만 추가할 수 있습니다.                                                                                                                                                                 |
| / 아키텍처: {x86 &#124;ia64 &#124; x64} |                                                                                                       부팅 이미지의 아키텍처를 지정합니다. 다른 아키텍처에서 부팅 이미지에 동일한 이미지 이름을 가질 수 있기 때문에 올바른 이미지를 사용 하도록 아키텍처를 지정 해야 합니다.                                                                                                        |
|           / 파일 이름:<File name>]           |                                                                                                                                                        파일의 이름을 지정합니다. 이미지 이름으로 고유 하 게 식별할 수 없으면, 파일 이름을 지정 해야 합니다.                                                                                                                                                        |
|           [/DriverPackage:<Name>           |                                                                                                                                                                                   이미지에 추가할 드라이버 패키지의 이름을 지정 합니다.                                                                                                                                                                                    |
|             [/ 패키지 Id:<ID>]              | 드라이버 패키지의 Windows 배포 서비스 ID를 지정합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우이 옵션을 지정 해야 합니다. 패키지 ID를 찾으려면 패키지가 드라이버 그룹을 클릭 합니다 (또는 **모든 패키지** 노드)에서 패키지를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다. 패키지 ID가 나열 된 **일반** 탭 합니다. 예를 들어: {dd098d20-1850-4fc8-8e35-ea24a1beff5e}. |

## <a name="BKMK_examples"></a>예제
부팅 이미지에 드라이버 패키지를 추가 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /add-ImageDriverPackagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /DriverPackage:XYZ
```
```
wdsutil /verbose /add-ImageDriverPackagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[추가 ImageDriverPackages 명령을 사용 하 여](using-the-add-imagedriverpackages-command.md)
