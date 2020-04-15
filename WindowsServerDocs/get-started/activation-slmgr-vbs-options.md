---
title: 볼륨 정품 인증 정보를 가져오는 Slmgr.vbs 옵션
description: Slmgr.vbs 스크립트에 사용할 수 있는 옵션을 나열하고, 이를 사용하는 방법을 설명합니다.
ms.date: 09/24/2019
ms.technology: server-general
ms.topic: article
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
appliesto:
- Windows Server 2012 R2
- Windows 10
- Windows 8.1
ms.openlocfilehash: e3e4b4d236672ce310c8a0eb038d0e19f936a5d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826346"
---
# <a name="slmgrvbs-options-for-obtaining-volume-activation-information"></a>볼륨 정품 인증 정보를 가져오는 Slmgr.vbs 옵션

여기서는 Slmgr.vbs 스크립트의 구문에 대해 설명하고, 이 문서의 표에는 각 명령줄 옵션에 대한 설명이 나와 있습니다.

```cmd
slmgr.vbs [<ComputerName> [<User> <Password>]] [<Options>]
```

> [!NOTE]
> 이 문서에서 \[] 대괄호는 선택적 인수를 묶고, \<> 꺾쇠 괄호는 자리 표시자를 묶습니다. 이러한 명령문을 입력하는 경우 괄호를 생략하고 해당 값을 사용하여 자리 표시자를 바꿉니다.

> [!NOTE]
> 볼륨 정품 인증을 사용하는 다른 소프트웨어 제품에 대한 자세한 내용은 해당 애플리케이션에 맞게 특별히 작성된 문서를 참조하세요.

## <a name="using-slmgr-on-remote-computers"></a>원격 컴퓨터에서 Slmgr 사용

원격 클라이언트를 관리하려면 VAMT(볼륨 정품 인증 관리 도구) 버전 1.2 이상을 사용하거나 플랫폼 간의 차이점을 인식하는 사용자 지정 WMI 스크립트를 만들어야 합니다. 볼륨 정품 인증용 WMI 속성 및 메서드에 대한 자세한 내용은 [볼륨 정품 인증용 WMI 속성 및 메서드](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502536(v=ws.11))를 참조하세요.

> [!IMPORTANT]
> Windows 7 및 Windows Server 2008 R2의 WMI 변경 내용으로 인해 Slmgr.vbs 스크립트는 플랫폼 간에 작동하지 않습니다. Slmgr.vbs를 사용하여 Windows Vista&reg; 운영 체제에서 Windows 7 또는 Windows Server 2008 R2 시스템을 관리하는 것은 지원되지 않습니다. Windows 7 또는 Windows Server 2008 R2에서 이전 시스템을 관리하려고 하면 특정 버전 불일치 오류가 생성됩니다. 예를 들어 **cscript slmgr.vbs \<vista\_machine\_name\> /dlv**를 실행하면 생성되는 출력은 다음과 같습니다.
>  
>> Microsoft (R) Windows Script Host Version 5.8 Copyright (C) Microsoft Corporation. All rights reserved.
>>  
>> 원격 머신에서 이 버전의 SLMgr.vbs를 지원하지 않습니다.

## <a name="general-slmgrvbs-options"></a>일반 Slmgr.vbs 옵션

|옵션 |설명 |
| - | - |
|\[\<ComputerName\>] |원격 컴퓨터의 이름입니다(기본값은 로컬 컴퓨터). |
|\[\<User\>] |원격 컴퓨터에 필요한 권한이 있는 계정 |
|\[\<Password\>] |원격 컴퓨터에 필요한 권한이 있는 계정의 암호 |

## <a name="global-options"></a>글로벌 옵션

|옵션 |설명 |
| - | - |
|\/ipk&nbsp;&lt;ProductKey&gt; |5×5 제품 키를 설치하려고 합니다. 이 매개 변수에서 제공되는 제품 키는 설치된 운영 체제에 유효하며 적용 가능한 것으로 확인된 것입니다.<br />그렇지 않으면 오류가 반환됩니다.<br />키가 유효하고 적용 가능하면 키가 설치됩니다. 키가 이미 설치되어 있으면 자동으로 대체됩니다.<br />라이선스 서비스에서 안정성 문제를 방지하려면 시스템을 다시 시작하거나 소프트웨어 보호 서비스가 다시 시작해야 합니다.<br />관리자 권한으로 실행되는 명령 프롬프트 창에서 이 작업을 실행하거나, 권한이 없는 사용자가 소프트웨어 보호 서비스에 추가로 액세스할 수 있도록 표준 사용자 작업 레지스트리 값을 설정해야 합니다. |
|/ato&nbsp;\[\<Activation&nbsp;ID\>] |KMS 호스트 키 또는 MAK(복수 정품 인증 키)가 설치되어 있는 정품 버전 및 볼륨 시스템의 경우 **/ato**는 Windows에서 온라인 정품 인증을 시도하라는 메시지를 표시합니다.<br />GVLK(일반 볼륨 라이선스 키)가 설치되어 있는 시스템의 경우 KMS 정품 인증을 시도하라는 메시지를 표시합니다. 자동 KMS 정품 인증 시도( **/stao**)를 일시 중단하도록 설정된 시스템의 경우 **/ato**가 실행되는 경우에도 KMS 정품 인증을 시도합니다.<br />**참고:** Windows 8(및 Windows Server 2012)부터 **/stao** 옵션은 더 이상 사용되지 않습니다. 대신 **/act-type** 옵션을 사용합니다.<br />\<**Activation ID**\> 매개 변수는 컴퓨터에 설치된 Windows 버전을 식별하도록 **/ato** 지원을 확장합니다. \<**Activation ID**\> 매개 변수를 지정하면 옵션의 효과를 해당 정품 인증 ID와 연결된 버전으로 격리합니다. 설치된 Windows 버전의 정품 인증 ID를 가져오려면 **slmgr.vbs /dlv all**을 실행합니다. 다른 애플리케이션을 지원해야 하는 경우 추가 지침은 해당 애플리케이션에서 제공하는 지침을 참조하세요.<br />KMS 정품 인증에는 상승된 권한이 필요하지 않습니다. 그러나 온라인 정품 인증에는 권한 상승이 필요하거나, 소프트웨어 보호 서비스에 대한 권한 없는 사용자의 추가 액세스를 허용하도록 표준 사용자 작업 레지스트리 값을 설정해야 합니다. |
|\/dli&nbsp;\[<Activation&nbsp;ID\>&nbsp;\|&nbsp;All\] |라이선스 정보를 표시합니다.<br />기본적으로 **/dli**는 설치된 활성 Windows 에디션에 대한 라이선스 정보를 표시합니다. \<**Activation ID**\> 매개 변수를 지정하면 해당 정품 인증 ID와 연결된 특정 버전의 라이선스 정보가 표시됩니다. **All**을 매개 변수로 지정하면 해당하는 모든 설치된 제품의 라이선스 정보가 표시됩니다.<br />이 작업에는 상승된 권한이 필요하지 않습니다. |
|\/dlv&nbsp;\[<Activation&nbsp;ID\>&nbsp;\|&nbsp;All\] |자세한 라이선스 정보를 표시합니다.<br />기본적으로 **/dlv**는 설치된 운영 체제에 대한 라이선스 정보를 표시합니다. \<**Activation ID**\> 매개 변수를 지정하면 해당 정품 인증 ID와 연결된 특정 버전의 라이선스 정보가 표시됩니다. **All** 매개 변수를 지정하면 해당하는 모든 설치된 제품의 라이선스 정보가 표시됩니다.<br />이 작업에는 상승된 권한이 필요하지 않습니다. |
|\/xpr \[\<Activation&nbsp;ID\>] |제품의 정품 인증 만료 날짜를 표시합니다. 기본적으로 현재 Windows 에디션을 나타내며, MAK와 일반 정품 인증은 영구적이므로 주로 KMS 클라이언트에 유용합니다.<br />\<**Activation ID**\> 매개 변수를 지정하면 해당 정품 인증 ID와 연결된 특정 버전의 정품 인증 만료 날짜가 표시됩니다. 이 작업에는 상승된 권한이 필요하지 않습니다. |

## <a name="advanced-options"></a>고급 옵션

|옵션 |설명 |
| - | - |
|\/cpky |일부 서비스 작업의 경우 OOBE(첫 실행 경험) 작업 중에 레지스트리에서 제품 키를 사용할 수 있어야 합니다. **/cpky** 옵션은 악성 코드에 의한 제품 키 도난을 방지하기 위해 레지스트리에서 제품 키를 제거합니다.<br />키를 배포하는 일반 정품 설치의 경우 이 작업을 실행하는 것이 좋습니다. MAK 및 KMS 호스트 키에는 이 옵션이 필요하지 않습니다. 이러한 키에는 기본 동작으로 제공되기 때문입니다. 이 옵션은 기본 동작에서 레지스트리의 키를 지우지 않는 다른 유형의 키에만 필요합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/ilc&nbsp;&lt;license_file&gt; |이 옵션은 필수 매개 변수에 지정된 라이선스 파일을 설치합니다. 이러한 라이선스는 문제 해결, 토큰 기반 정품 인증 지원 또는 등록된 애플리케이션의 수동 설치 요소로 설치될 수 있습니다.<br />이 프로세스 중에는 라이선스의 유효성이 검사되지 않습니다. 라이선스 유효성 검사가 Slmgr.vbs의 범위를 벗어나기 때문입니다. 대신 소프트웨어 보호 서비스에서 런타임으로 유효성 검사를 처리합니다.<br />관리자 권한으로 실행되는 명령 프롬프트 창에서 이 작업을 실행하거나, 권한이 없는 사용자가 소프트웨어 보호 서비스에 추가로 액세스할 수 있도록 **표준 사용자 작업** 레지스트리 값을 설정해야 합니다. |
|\/rilc |이 옵션은 %SystemRoot%\system32\oem 및 %SystemRoot%\System32\spp\tokens에 저장된 모든 라이선스를 다시 설치합니다. 이러한 라이선스는 설치 중에 저장된 "유효한 것으로 알려진" 복사본입니다.<br />신뢰할 수 있는 저장소에 있는 일치하는 모든 라이선스가 대체됩니다. 추가 라이선스(예: TA(신뢰할 수 있는 기관) IL(발급 라이선스), 애플리케이션 라이선스)는 영향을 받지 않습니다.<br />관리자 권한으로 실행되는 명령 프롬프트 창에서 이 작업을 실행하거나, 권한이 없는 사용자가 소프트웨어 보호 서비스에 추가로 액세스할 수 있도록 **표준 사용자 작업** 레지스트리 값을 설정해야 합니다. |
|\/rearm |이 옵션은 정품 인증 타이머를 다시 설정합니다. **/rearm** 프로세스는 **sysprep /generalize**에 의해서도 호출됩니다.<br />**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform\SkipRearm** 레지스트리 항목이 **1**로 설정된 경우 이 작업은 수행되지 않습니다. 이 레지스트리 항목에 대한 자세한 내용은 [볼륨 정품 인증에 대한 레지스트리 설정](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502532(v=ws.11))을 참조하세요.<br />관리자 권한으로 실행되는 명령 프롬프트 창에서 이 작업을 실행하거나, 권한이 없는 사용자가 소프트웨어 보호 서비스에 추가로 액세스할 수 있도록 **표준 사용자 작업** 레지스트리 값을 설정해야 합니다. |
|\/rearm-app &lt;Application&nbsp;ID&gt; |지정된 응용 프로그램의 라이선스 상태를 다시 설정합니다. |
|\/rearm-sku &lt;Application&nbsp;ID&gt; |지정된 SKU의 라이선스 상태를 다시 설정합니다. |
|\/upk&nbsp;\[&lt;Application&nbsp;ID&gt;] |이 옵션은 현재 Windows 에디션의 제품 키를 제거합니다. 다시 시작 후 새 제품 키를 설치하지 않으면 시스템이 사용 허가되지 않음 상태가 됩니다.<br />필요에 따라 \<**Activation ID**\> 매개 변수를 사용하여 설치된 다른 제품을 지정할 수 있습니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/dti&nbsp;\[\<Activation&nbsp;ID\>] |오프라인 정품 인증에 대한 설치 ID를 표시합니다. |
|\/atp &lt;Confirmation&nbsp;ID&gt; |사용자가 제공한 확인 ID를 사용하여 제품을 정품 인증합니다. |

## <a name="kms-client-options"></a>KMS 클라이언트 옵션

|옵션 |설명 |
| - | - |
|\/skms \<Name\[:Port]&nbsp;\|&nbsp;\:&nbsp;port\> \[\<Activation&nbsp;ID\>] |이 옵션을 이름을 지정하며, 필요에 따라 연결할 KMS 호스트 컴퓨터의 포트를 지정합니다. 이 값을 설정하면 KMS 호스트의 자동 검색이 비활성화됩니다.<br />KMS 호스트에서 IPv6(인터넷 프로토콜 버전 6)만 사용하는 경우 주소는 \<hostname\>:\<port\> 형식으로 지정해야 합니다. IPv6 주소에는 Slmgr.vbs 스크립트에서 올바르게 구문 분석하지 않는 콜론(:)이 포함되어 있습니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/skms-domain&nbsp;&lt;FQDN&gt; \[\<Activation&nbsp;ID\>] |모든 KMS SRV 레코드를 찾을 수 있는 특정 DNS 도메인을 설정합니다. **/skms** 옵션을 사용하여 특정 단일 KMS 호스트를 설정한 경우 이 설정이 적용되지 않습니다. 특히 비연속 네임스페이스 환경에서 KMS가 DNS 접미사 검색 목록을 무시하고 대신 지정된 DNS 도메인에서 KMS 호스트 레코드를 찾도록 강제로 실행하려는 경우 이 옵션을 사용합니다. |
|\/ckms&nbsp;\[\<Activation&nbsp;ID\>] |이 옵션은 레지스트리에서 지정된 KMS 호스트 이름, 주소 및 포트 정보를 제거하고 KMS 자동 검색 동작을 복원합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/skhc |이 옵션은 KMS 호스트 캐싱을 사용하도록 설정합니다(기본값). 클라이언트에서 작동하는 KMS 호스트를 검색한 후에 이 설정을 사용하면 DNS(Domain Name System) 우선 순위 및 가중치가 호스트와의 추가 통신에 영향을 주지 않습니다. 시스템에서 작동하는 KMS 호스트에 더 이상 연결할 수 없는 경우 클라이언트는 새 호스트를 검색하려고 시도합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/ckhc |이 옵션은 KMS 호스트 캐싱을 사용하지 않도록 설정합니다. 이 설정은 클라이언트에서 KMS 정품 인증을 시도할 때마다 DNS 자동 검색을 사용하도록 명령합니다(우선 순위 및 가중치를 사용하는 경우 추천됨).<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |

## <a name="kms-host-configuration-options"></a>KMS 호스트 구성 옵션

|옵션 |설명 |
| - | - |
|\/sai&nbsp;&lt;Interval&gt; |이 옵션은 정품 인증되지 않은 클라이언트에서 KMS에 연결하려고 시도하는 간격(분)을 설정합니다. 정품 인증 간격은 15분에서 30일 사이여야 하며, 기본값(2시간)이 추천됩니다.<br />KMS 클라이언트는 초기에 레지스트리에서 이 간격을 선택하지만 첫 번째 KMS 응답을 받은 후에는 KMS 설정으로 전환합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/sri &lt;Interval&gt; |이 옵션은 정품 인증된 클라이언트에서 KMS에 연결하려고 시도하는 갱신 간격(분)을 설정합니다. 갱신 간격은 15분에서 30일 사이여야 합니다. 이 옵션은 초기에 KMS 서버 쪽과 클라이언트 쪽 모두에 설정됩니다. 기본값은 10,080분(7일)입니다.<br />KMS 클라이언트는 초기에 레지스트리에서 이 간격을 선택하지만 첫 번째 KMS 응답을 받은 후에는 KMS 설정으로 전환합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/sprt&nbsp;&lt;Port&gt; |이 옵션은 KMS 호스트에서 클라이언트 정품 인증 요청을 수신 대기하는 포트를 설정합니다. 기본 TCP 포트는 1688입니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/sdns |KMS 호스트의 DNS 게시를 사용하도록 설정합니다(기본값).<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/cdns |KMS 호스트의 DNS 게시를 사용하지 않도록 설정합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/spri |KMS 우선 순위를 보통(기본값)으로 설정합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/cpri |KMS 우선 순위를 낮음(기본값)으로 설정합니다.<br />공동 호스팅 환경에서 KMS의 경합을 최소화하는 경우 이 옵션을 사용합니다. 이로 인해 다른 애플리케이션 또는 서버 역할이 활성 상태인지 여부에 따라 KMS가 고갈될 수 있습니다. 주의해서 사용해야 합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/act-type \[\<Activation-Type\>] \[\<Activation&nbsp;ID\>] |이 옵션은 볼륨 정품 인증을 단일 유형으로 제한하는 레지스트리 값을 설정합니다. 정품 인증 유형 **1**은 정품 인증을 Active Directory로만 제한하고, **2**는 KMS 정품 인증으로 제한하며, **3**은 토큰 기반 정품 인증으로 제한합니다. **0** 옵션은 모든 정품 인증 유형을 허용하며, 이것이 기본값입니다. |

## <a name="token-based-activation-configuration-options"></a>토큰 기반 정품 인증 구성 옵션

|옵션 |설명 |
| - | - |
|/lil |설치된 토큰 기반 정품 인증 발급 라이선스를 나열합니다. |
|\/ril&nbsp;&lt;ILID&gt;&nbsp;&lt;ILvID&gt; |설치된 토큰 기반 정품 인증 발급 라이선스를 제거합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다. |
|\/stao |**Token-based Activation Only** 플래그를 설정하여 자동 KMS 정품 인증을 비활성화합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다.<br />이 옵션은 Windows Server 2012 R2 및 Windows 8.1에서 제거되었습니다. 대신 **/act–type** 옵션을 사용합니다. |
|\/ctao |**Token-based Activation Only** 플래그를 지워(기본값) 자동 KMS 정품 인증을 활성화합니다.<br />이 작업은 관리자 권한으로 실행되는 명령 프롬프트 창에서 실행해야 합니다.<br />이 옵션은 Windows Server 2012 R2 및 Windows 8.1에서 제거되었습니다. 대신 **/act–type**</strong> 옵션을 사용합니다. |
|\/ltc |설치된 소프트웨어를 활성화할 수 있는 유효한 토큰 기반 정품 인증 인증서를 나열합니다. |
|\/fta &lt;Certificate&nbsp;Thumbprint&gt; \[&lt;PIN&gt;] |식별된 인증서를 사용하여 토큰 기반 정품 인증을 강제로 적용합니다. 하드웨어(예: 스마트 카드)로 보호되는 인증서를 사용하는 경우 PIN(개인 식별 번호) 프롬프트 없이 프라이빗 키의 잠금을 해제하기 위해 선택적 PIN이 제공됩니다. |

## <a name="active-directory-based-activation-configuration-options"></a>Active Directory 기반 정품 인증 구성 옵션

|옵션 |설명 |
| - | - |
|\/ad-activation-online &lt;Product&nbsp;Key&gt; \[\<Activation&nbsp;Object&nbsp;name\>] |명령 프롬프트에서 실행하는 자격 증명을 사용하여 Active Directory 데이터를 수집하고 Active Directory 포리스트 정품 인증을 시작합니다. 로컬 관리자 액세스 권한은 필요하지 않습니다. 그러나 포리스트의 루트 도메인에 있는 정품 인증 개체 컨테이너에 대한 읽기/쓰기 액세스 권한이 필요합니다. |
|\/ad-activation-get-IID &lt;Product&nbsp;Key&gt; |이 옵션은 전화 모드로 Active Directory 포리스트 정품 인증을 시작합니다. 인터넷 연결을 사용할 수 없는 경우 전화를 통해 포리스트를 정품 인증하는 데 사용할 수 있는 IID(설치 ID)가 출력됩니다. 정품 인증 전화 통화에서 이 IID를 제공하면 정품 인증을 완료하는 데 사용되는 CID가 반환됩니다. |
|\/ad-activation-apply-cid &lt;Product&nbsp;Key&gt; &lt;Confirmation&nbsp;ID&gt; \[\<Activation&nbsp;Object&nbsp;name>] |이 옵션을 사용하는 경우 정품 인증 전화 통화에서 제공된 CID를 입력하여 정품 인증을 완료합니다. |
|\[/name: &lt;AO_Name&gt;] |필요한 경우 이러한 명령 에 **/name** 옵션을 추가하여 Active Directory에 저장된 정품 인증 개체의 이름을 지정할 수 있습니다. 이름은 40자의 유니코드 문자를 초과할 수 없습니다. 큰따옴표를 사용하여 이름 문자열을 명시적으로 정의합니다.<br />Windows Server 2012 R2 및 Windows 8.1에서는 **/name** 옵션을 사용할 필요 없이 **/ad-activation-online &lt;Product&nbsp;Key&gt;** 및 **/ad-activation-apply-cid** 바로 뒤에 이름을 추가할 수 있습니다. |
|\/ao-list |로컬 컴퓨터에서 사용할 수 있는 모든 정품 인증 개체를 표시합니다. |
|\/del-ao &lt;AO_DN&gt;<br />\/del-ao &lt;AO_RDN&gt; |지정된 정품 인증 개체를 포리스트에서 삭제합니다. |

## <a name="see-also"></a>참고 항목

- [볼륨 정품 인증 기술 참조](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502529%28v%3dws.11%29)
- [볼륨 정품 인증 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831612%28v%3dws.11%29)

