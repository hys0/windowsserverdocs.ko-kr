---
title: KMS 클라이언트 설정 키
description: KMS 서버에서 Windows 제품을 정품 인증하는 데 필요한 키
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 11/12/2019
ms.topic: get-started-article
ms.openlocfilehash: f2320b80fb372a227098f952dc8e7f0758420f34
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947824"
---
# <a name="kms-client-setup-keys"></a>KMS 클라이언트 설정 키

>적용 대상: Windows Server 2019, Windows Server 반기 채널, Windows Server 2016, Windows 10

Windows Server, Windows 10, Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, Windows Server 2008 R2, Windows Vista 및 Windows Server 2008의 볼륨 라이선스 버전을 실행하는 컴퓨터는 기본적으로 추가 구성이 필요하지 않은 KMS 클라이언트입니다.

> [!NOTE]
> 다음 표에서 "LTSC"는 "장기 서비스 채널"을 의미하지만 "LTSB"는 "장기 서비스 분기"를 의미합니다. 

**여기에 나열된 키(GVLK)를 사용하려면 먼저 배포에서 실행되는 KMS 호스트가 있어야 합니다.** KMS 호스트를 아직 구성하지 않은 경우 설정 단계는 [KMS 정품 인증 배포](https://technet.microsoft.com/library/dn502531(v=ws.11).aspx)를 참조하세요.

컴퓨터를 KMS 호스트, MAK 또는 Windows 정품 버전에서 KMS 클라이언트로 변환하는 경우 다음 표에서 해당하는 설정 키(GVLK)를 설치합니다. 클라이언트 설정 키를 설치하려면 클라이언트에서 관리 명령 프롬프트를 열고 **slmgr /ipk \<setup key\>** 를 입력한 다음, **Enter** 키를 누릅니다.

| 수행할 작업…    | …사용할 리소스   |
|--------------------|------------------------|
| 볼륨 활성화 시나리오 외부에서 Windows를 활성화하면(Windows 일반 정품 버전을 활성화하려고 시도) **이러한 키가 작동하지 않습니다**. | Windows 일반 정품 버전에 다음 링크를 사용합니다. |
| Windows 8.1, Windows Server 2012 R2 또는 최신 시스템을 정품 인증할 때 표시되는 다음 오류를 해결합니다. “오류: 0xC004F050 소프트웨어 라이선스 서비스에서 제품 키가 잘못되었다고 보고했습니다.”… | Windows 8.1, Windows Server 2012 R2, Windows 8 또는 Windows Server 2012를 실행하고 있으면 KMS 호스트에[이 업데이트를 설치합니다](https://support.microsoft.com/help/3172614/july-2016-update-rollup-for-windows-8-1-and-windows-server-2012-r2) . |

-   [Windows 10 다운로드](https://www.microsoft.com/windows/get-windows-10)

-   [새 Windows 제품 키 얻기](https://support.microsoft.com/help/10749/windows-product-key)

-   [정품 Windows 도움말 및 방법](https://support.microsoft.com/help/15087/windows-genuine)


>   Windows Server 2008 R2 또는 Windows 7을 실행하고 있으면 이 운영 체제를 Windows 10 클라이언트용 KMS 호스트로 사용하도록 지원하는 업데이트가 있는지 자세히 살펴보세요.

## <a name="windows-server-semi-annual-channel-versions"></a>Windows Server 반기 채널 버전

### <a name="windows-server-version-1909-version-1903-and-version-1809"></a>Windows Server, 버전 1909, 버전 1903 및 버전 1809

| 운영 체제 버전  | KMS 클라이언트 설정 키          |
|---------------------------|-------------------------------|
| Windows Server Datacenter | 6NMRW-2C8FM-D24W7-TQWMY-CWH2D |
| Windows Server Standard   | N2KJX-J94YW-TQVFB-DG9YT-724CC |

## <a name="windows-server-ltscltsb-versions"></a>Windows Server LTSC/LTSB 버전

### <a name="windows-server-2019"></a>시작
| 운영 체제 버전       | KMS 클라이언트 설정 키          |
|--------------------------------|-------------------------------|
| Windows Server 2019 Datacenter | WMDGN-G9PQG-XVVXX-R3X43-63DFG  | 
| Windows Server 2019 Standard   | N69G4-B89J2-4G8F4-WWYCC-J464C  |
| Windows Server 2019 Essentials|WVDHN-86M7X-466P6-VHXV7-YY726|

### <a name="windows-server-2016"></a>Windows Server 2016

| 운영 체제 버전       | KMS 클라이언트 설정 키          |
|--------------------------------|-------------------------------|
| Windows Server 2016 Datacenter | CB7KF-BWN84-R7R2Y-793K2-8XDDG |
| Windows Server 2016 Standard   | WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY |
| Windows Server 2016 Essentials | JCKRF-N37P4-C2D82-9YXRT-4M63B |

## <a name="windows-10-all-supported-semi-annual-channel-versions"></a>Windows 10, 지원되는 모든 반기 채널 버전

지원되는 버전 및 서비스 종료 날짜에 대한 내용은 [Windows 수명 주기 팩트 시트](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)를 참조하세요.

| 운영 체제 버전          | KMS 클라이언트 설정 키          |
|-----------------------------------|-------------------------------|
|Windows 10 Pro|W269N-WFGWX-YVC9B-4J6C9-T83GX|
|Windows 10 Pro N|MH37W-N47XK-V7XM9-C7227-GCQG9|
|Windows 10 Pro for Workstations|NRG8B-VKK3Q-CXVCJ-9G2XF-6Q84J|
|Windows 10 Pro for Workstations N|9FNHH-K3HBT-3W4TD-6383H-6XYWF|
|Windows 10 Pro Education|6TP4R-GNPTD-KYYHQ-7B7DP-J447Y|
|Windows 10 Pro Education N|YVWGF-BXNMC-HTQYQ-CPQ99-66QFC|
|Windows 10 Education|NW6C2-QMPVW-D7KKK-3GKT6-VCFB2|
|Windows 10 Education KN |2WH4N-8QGBV-H22JP-CT43Q-MDWWJ|
|Windows 10 Enterprise  |NPPR9-FWDCX-D2C8J-H872K-2YT43|
|Windows 10 Enterprise KN    |DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4|
|Windows 10 Enterprise G|YYVX9-NTFWV-6MDM3-9PT4T-4M68B|
|Windows 10 Enterprise G N|44RPN-FTY23-9VTTB-MP9BX-T84FV|

## <a name="windows-10-ltscltsb-versions"></a>Windows 10 LTSC/LTSB 버전

### <a name="windows-10-ltsc-2019"></a>Windows 10 LTSC 2019

|운영 체제 버전|KMS 클라이언트 설정 키|
|-|-|
|Windows 10 Enterprise LTSC 2019|M7XTQ-FN8P6-TTKYV-9D4CC-J462D|
|Windows 10 Enterprise N LTSC 2019|92NFX-8DJQP-P6BBQ-THF9C-7CG2H|

### <a name="windows-10-ltsb-2016"></a>Windows 10 LTSB 2016

|운영 체제 버전|KMS 클라이언트 설정 키|
|-|-|
|Windows 10 Enterprise LTSB 2016|DCPHK-NFMTC-H88MJ-PFHPY-QJ4BJ|
|Windows 10 Enterprise N LTSB 2016|QFFDN-GRT3P-VKWWX-X7T3R-8B639|

### <a name="windows-10-ltsb-2015"></a>Windows 10 LTSB 2015 

| 운영 체제 버전          | KMS 클라이언트 설정 키          |
|-----------------------------------|-------------------------------|
| Windows 10 Enterprise 2015 LTSB   | WNMTR-4C88C-JK8YV-HQ7T2-76DF9 |
| Windows 10 Enterprise 2015 LTSB KN | 2F77B-TNFGY-69QQF-B8YKP-D69TJ |

## <a name="earlier-versions-of-windows-server"></a>이전 버전의 Windows Server

### <a name="windows-server-version-1803"></a>Windows Server, 버전 1803

| 운영 체제 버전       | KMS 클라이언트 설정 키          |
|--------------------------------|-------------------------------|
| Windows Server Datacenter | 2HXDN-KRXHB-GPYC7-YCKFJ-7FVDG  | 
| Windows Server Standard   | PTXN8-JFHJM-4WC78-MPCBR-9W4KR  |

### <a name="windows-server-version-1709"></a>Windows Server, 버전 1709

| 운영 체제 버전       | KMS 클라이언트 설정 키          |
|--------------------------------|-------------------------------|
| Windows Server Datacenter | 6Y6KB-N82V8-D8CQV-23MJW-BWTG6  | 
| Windows Server Standard   | DPCNP-XQFKJ-BJF7R-FRC8D-GF6G4  |

### <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

| 운영 체제 버전               | KMS 클라이언트 설정 키          |
|----------------------------------------|-------------------------------|
| Windows Server 2012 R2 Server Standard | D2N9P-3P6X9-2R39C-7RTCD-MDVJX |
| Windows Server 2012 R2 Datacenter      | W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9 |
| Windows Server 2012 R2 Essentials      | KNC87-3J2TX-XB4WP-VCPJV-M4FWM |

### <a name="windows-server-2012"></a>Windows Server 2012

| 운영 체제 버전                | KMS 클라이언트 설정 키          |
|-----------------------------------------|-------------------------------|
| Windows Server 2012                     | BN3D2-R7TKB-3YPBD-8DRP2-27GG4 |
| Windows Server 2012 N                   | 8N2M2-HWPGY-7PGT9-HGDD8-GVGGY |
| Windows Server 2012 Single Language     | 2WN2H-YGCQR-KFX6K-CD6TF-84YXQ |
| Windows Server 2012 Country Specific    | 4K36P-JN4VD-GDC6V-KDT89-DYFKP |
| Windows Server 2012 Server Standard     | XC9B7-NBPP2-83J2H-RHMBY-92BT4 |
| Windows Server 2012 MultiPoint Standard | HM7DN-YVMH3-46JC3-XYTG7-CYQJJ |
| Windows Server 2012 MultiPoint Premium  | XNH6W-2V9GX-RGJ4K-Y8X6F-QGJ2G |
| Windows Server 2012 Datacenter          | 48HP8-DN98B-MYWDG-T2DCC-8W83P |


### <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

| 운영 체제 버전                         | KMS 클라이언트 설정 키          |
|--------------------------------------------------|-------------------------------|
| Windows Server 2008 R2 Web                       | 6TPJF-RBVHG-WBW2R-86QPH-6RTM4 |
| Windows Server 2008 R2 HPC 버전               | TT8MH-CG224-D3D7Q-498W2-9QCTX |
| Windows Server 2008 R2 Standard                  | YC6KT-GKW9T-YTKYR-T4X34-R7VHC |
| Windows Server 2008 R2 Enterprise                | 489J6-VHDMP-X63PK-3K798-CPX3Y |
| Windows Server 2008 R2 Datacenter                | 74YFP-3QFB3-KQT8W-PMXWJ-7M648 |
| Windows Server 2008 R2 for Itanium-based Systems | GT63C-RJFQ3-4GMB6-BRFB9-CB83V |

### <a name="windows-server-2008"></a>Windows Server 2008

| 운영 체제 버전                       | KMS 클라이언트 설정 키          |
|------------------------------------------------|-------------------------------|
| Windows Web Server 2008                        | WYR28-R7TFJ-3X2YQ-YCY4H-M249D |
| Windows Server 2008 Standard                   | TM24T-X9RMF-VWXK6-X8JC9-BFGM2 |
| Windows Server 2008 Standard(Hyper-V 불포함)   | W7VD6-7JFBR-RX26B-YKQ3Y-6FFFJ |
| Windows Server 2008 Enterprise                 | YQGMW-MPWTJ-34KDK-48M3W-X4Q6V |
| Windows Server 2008 Enterprise(Hyper-V 불포함) | 39BXF-X8Q23-P2WWT-38T2F-G3FPG |
| Windows Server 2008 HPC                        | RCTX3-KWVHP-BR6TB-RB6DM-6X7HP |
| Windows Server 2008 Datacenter                 | 7M67G-PC374-GR742-YH8V4-TCBY3 |
| Windows Server 2008 Datacenter(Hyper-V 불포함) | 22XQ2-VRXRG-P8D42-K34TD-G3QQC |
| Windows Server 2008 for Itanium-Based Systems  | 4DWFP-JF3DJ-B7DTH-78FJB-PDRHK |

## <a name="earlier-versions-of-windows"></a>이전 버전 Windows

### <a name="windows-81"></a>Windows 8.1

| 운영 체제 버전               | KMS 클라이언트 설정 키          |
|----------------------------------------|-------------------------------|
| Windows 8.1 Pro               | GCRJD-8NW9H-F2CDX-CCM8D-9D6T9 |
| Windows 8.1 Pro N             | HMCNV-VVBFX-7HMBH-CTY9B-B4FXY |
| Windows 8.1 Enterprise                 | MHF9N-XY6XB-WVXMC-BTDCT-MKKG7 |
| Windows 8.1 Enterprise KN               | TT4HM-HN7YT-62K67-RGRQJ-JFFXW |

### <a name="windows-8"></a>Windows 8

| 운영 체제 버전                | KMS 클라이언트 설정 키          |
|-----------------------------------------|-------------------------------|
| Windows 8 Pro                  | NG4HW-VH26C-733KW-K6F98-J8CK4 |
| Windows 8 Pro N                | XCVCF-2NXM9-723PB-MHCB7-2RYQQ |
| Windows 8 Enterprise                    | 32JNW-9KQ84-P47T8-D8GGY-CWCK7 |
| Windows 8 Enterprise N                  | JMNMF-RHW7P-DMY6X-RF3DR-X2BQT |


### <a name="windows-7"></a>Windows 7 

| 운영 체제 버전                         | KMS 클라이언트 설정 키          |
|--------------------------------------------------|-------------------------------|
| Windows 7 Professional                           | FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4 |
| Windows 7 Professional KN                         | MRPKT-YTG23-K7D7T-X2JMM-QY7MG |
| Windows 7 Professional E                         | W82YF-2Q76Y-63HXB-FGJG9-GF7QX |
| Windows 7 Enterprise                             | 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH |
| Windows 7 Enterprise N                           | YDRBP-3D83W-TY26F-D46B2-XCKRJ |
| Windows 7 Enterprise E                           | C29WB-22CC8-VJ326-GHFJW-H9DH4 |


참고 항목

• [볼륨 정품 인증 계획](https://technet.microsoft.com/library/jj134042(v=ws.11).aspx)


