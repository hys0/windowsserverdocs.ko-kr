---
title: Express 업데이트 배달 ISV 지원
description: WSUS(Windows Server Update Service) 항목 - ISV(독립 소프트웨어 공급업체)가 WSUS를 사용하여 Express 업데이트 배달을 구성하는 방법
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: a4880a1a66d9c722cfda9e194c4eff38c5058674
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361717"
---
# <a name="express-update-delivery-isv-support"></a>Express 업데이트 배달 ISV 지원

>적용 대상: Windows 10, Windows Server 2016

모든 패키지에는 일관성과 단순성을 보장하기 위해 이전에 사용된 수정 사항이 포함되어 있으므로 Windows 10 업데이트 다운로드의 규모가 커질 수 있습니다.  

버전 7부터 Windows에는 Windows 업데이트 다운로드 크기를 줄일 수 있는 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)라는 기능이 지원됩니다. 소비자 디바이스에서 기본적으로 지원되더라도 Express 기능을 이용하기 위해서는 Windows 10 Enterprise 디바이스에 WSUS(Windows Server Update Services)가 필요합니다.

## <a name="how-microsoft-supports-express"></a>Microsoft가 Express를 지원하는 방법

- **독립 실행형 WSUS의 Express**

    Express 업데이트 배달은 이미 [WSUS의 모든 지원 버전](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx)에서 사용할 수 있습니다.

- **Windows 업데이트에 직접 연결된 디바이스의 Express** 

    소비자 디바이스의 Express 다운로드 지원: WU(Windows 업데이트) 클라이언트를 사용하여 업데이트 스캔, 다운로드 및 설치를 수행합니다. 다운로드 단계 중에 WU 클라이언트가 Express 패키지를 요청하고 적합한 바이트 범위를 다운로드합니다.

-  **[비즈니스용 Windows 업데이트](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)를 사용하여 관리되는 Enterprise 디바이스**도 구성 변경 없이 Express 업데이트 배달 지원 이점을 얻을 수 있습니다.

## <a name="how-isvs-can-take-advantage-of-express"></a>ISV의 Express 활용 방법

ISV는 WSUS 및 WU 클라이언트를 사용하여 Express 업데이트 배달을 지원할 수 있습니다. 아래 섹션에서 자세히 설명되는 다음 세 단계를 수행하는 것이 좋습니다.

1.  [**WSUS 구성**](#BKMK_1)

    스캔 및 업데이트 동기화를 위해서는 WSUS 서버가 필요합니다(추가 정보는 [여기](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx)를 참조).

2.  [**ISV 파일 캐시 지정 및 채우기**](#BKMK_2)

    ISV 파일 캐시는 업데이트 캐비닛 파일(.cab 파일) 및 Express 패키지(.psf 파일)가 포함된 업데이트 콘텐츠를 호스팅하기 위해 권장됩니다.

3.  [**WU 클라이언트 작업 지시를 위한 ISV 클라이언트 에이전트 설정**](#BKMK_3)

>[!NOTE]
>2017 1월 또는 그 이후의 Windows 10 버전 1607 릴리스용 누적 업데이트([KB3213986 (OS Build 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693)를 설치해야 합니다.
    
   - ISV 클라이언트 에이전트가 승인할 업데이트 및 업데이트 다운로드/설치 시간을 결정합니다.
   - WU 클라이언트는 다운로드할 바이트 범위를 결정하고 다운로드 요청을 시작합니다.

### <a name="BKMK_1"></a>1단계: WSUS 구성

WSUS는 Windows 업데이트 인터페이스로 사용되며, 다운로드해야 하는 Express 패키지를 기술하는 모든 메타 데이터를 관리합니다. 배포가 필요하면 [**Windows Server Update Services 3.0 SP2 개요**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)를 참조하세요. WSUS가 배포된 후에는 기본적으로 업데이트 콘텐츠를 WSUS 서버에 로컬로 저장할지 여부를 고려해야 합니다. WSUS를 구성할 때 업데이트가 로컬로 저장되지 않도록 하는 것이 좋습니다. 이 경우 해당 환경에서 이러한 패키지의 배포를 지시하는 소프트웨어가 있다고 가정합니다. WSUS 로컬 스토리지 구성 방법은 [**업데이트 저장 위치 결정**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx)을 참조하세요.

### <a name="BKMK_2"></a>2단계: ISV 파일 캐시 지정 및 채우기 

#### <a name="specify-the-isv-file-cache"></a>ISV 파일 캐시 지정

[**구성 서비스 공급자 참조**](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference)에 설명된 새로운 클라이언트 쪽 그룹 정책 및 MDM(모바일 디바이스 관리) 설정에 따라 ISV 파일 캐시의 위치가 정의됩니다.

| **이름**                                              | **설명**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 업데이트의 대체 다운로드 위치를 구성합니다. | Microsoft 업데이트에서 제공되는 업데이트를 호스팅하기 위한 대체 인트라넷 서버를 지정합니다. 그런 다음 이 업데이트 서비스를 사용하여 네트워크의 컴퓨터를 자동으로 업데이트할 수 있습니다. |

ISV 파일 캐시의 대체 다운로드 위치를 설정할 때는 두 가지 옵션이 있습니다.

1. ISV 파일 캐시인 **ISV HTTP 서버 호스트 이름 지정**
    
    이 방법은 정책에 지정된 HTTP 서버에 다운로드 요청을 수행하도록 WU 클라이언트를 구성합니다.

2. **localhost 지정**
 
    이 방법은 localhost에 다운로드 요청을 수행하도록 WU 클라이언트를 구성합니다. 이렇게 하면 ISV 클라이언트 에이전트가 해당 요청을 처리하고 경로를 적절하게 지정하여 다운로드 요청을 수행할 수 있습니다.

> [!IMPORTANT]
> ISV 파일 캐시에는 다음이 필요합니다.                                                          
> - RFC: <http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                              에 따라 서버가 HTTP 1.1과 호환되어야 합니다.  
> 특히 웹 서버가 [**HEAD**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 및 [**GET**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm) 요청을 지원해야 합니다.<br>                                                                                                                                                                                                                                                                                                  - 부분 범위 요청<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   - Keep-alive<br>                                                                                                                                                                                                                                                                                                                                                                                                                            - "Transfer-Encoding:chunked" 사용 불가                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>ISV 파일 캐시 채우기

ISV 파일 캐시는 관리되는 클라이언트에 설치할 업데이트와 연관된 파일로 채워야 합니다. 

**ISV 파일 캐시를 채우려면:**

1. [WSUS API](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx)를 사용하여 MU 서비스에 대한 업데이트의 파일 경로 및 파일 이름에 액세스합니다.

    WSUS 서버의 각 업데이트에 대한 메타 데이터에는 다음과 같이 Microsoft 업데이트에 대한 업데이트의 파일 경로 및 파일 이름이 포함됩니다. (굵게 표시된 Microsoft 업데이트 호스트 이름에 이어 파일 경로 및 파일 이름이 표시됨): **<http://download.windowsupdate.com>** /c/msdownload/update/software/updt/2016/09/windows10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74.msu

2. Microsoft 업데이트에서 파일을 다운로드하고 다음 두 가지 방법 중 하나를 사용하여 ISV 파일 캐시에 파일을 저장합니다. 

   - **MU 서비스와 동일한 경로**를 사용하여 파일 저장

   - **ISV에 정의된 폴더 경로**를 사용하여 파일 저장

     ISV 파일 위치로 MU 폴더 경로 및 파일 이름을 참조하는 HTTP 서버(또는 localhost) 리디렉션 **HTTP GET** 요청을 수행합니다.

### <a name="BKMK_3"></a>3단계: WU 클라이언트 작업 지시를 위한 ISV 클라이언트 에이전트 설정

ISV 클라이언트 에이전트는 다음과 같은 권장 워크플로를 사용하여 승인된 업데이트의 다운로드 및 설치를 오케스트레이션합니다.

1.  ISV 클라이언트 에이전트는 WSUS 서버에 대해 스캔을 수행하도록 WU 클라이언트를 호출합니다.

2.  스캔은 적용 가능한 업데이트 집합을 WU 클라이언트에 반환합니다.

3.  ISV 클라이언트가 승인, 다운로드 및 설치할 업데이트를 결정합니다.

4.  ISV 클라이언트 에이전트가 승인된 업데이트를 다운로드하도록 WU 클라이언트를 호출합니다.

5.  업데이트가 다운로드된 다음 ISV 클라이언트 에이전트가 승인된 업데이트를 설치하도록 WU 클라이언트를 호출합니다.

WU 클라이언트를 사용하여 업데이트를 스캔, 다운로드 및 설치하는 방법에 대한 자세한 내용은 [업데이트 검색, 다운로드 및 설치](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx)를 참조하세요.

### <a name="download-workflow-options"></a>다운로드 워크플로 옵션

다음은 ISV 파일 캐시의 다운로드 워크플로 옵션에 대한 두 가지 설명입니다.

![워크플로 1](../../media/express-update-delivery-isv-support/image1.png)

![워크플로 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>Express 다운로드 작동 방식

- Express를 지원하는 OS 업데이트의 경우 다음과 같이 서비스에 저장된 파일 페이로드의 두 가지 버전이 있습니다.

  - **전체 파일 버전** - 기본적으로 업데이트 바이너리의 로컬 버전을 교체합니다.

  - **Express 버전** - 디바이스의 기존 바이너리를 패치하는 데 필요한 델타가 포함되어 있습니다. 

    전체 파일 버전과 Express 버전은 스캔 단계의 일부로 클라이언트에 다운로드된 업데이트의 메타 데이터에서 참조됩니다. 

    **Express 다운로드는 다음과 같이 작동합니다.**

    WU 클라이언트는 먼저 Express를 다운로드하려고 시도하며 특정 상황에서는 필요한 경우 전체 파일로 대체합니다(예: 바이트 범위 요청을 지원하지 않는 프록시를 통과하는 경우).

  1. WU 클라이언트가 Express 다운로드를 시작할 때 **WU 클라이언트는 스텁을 먼저 다운로드**합니다(Express 패키지에 포함되어 있음).

  2. **WU 클라이언트는 Windows Installer에 이 스텁을 전달**합니다. Windows Installer는 스텁을 사용하여 로컬 인벤토리를 수행하며 제공되는 파일의 최신 버전을 얻는 데 필요한 파일과 디바이스의 델타를 비교합니다.

  3. **그 다음에 Windows Installer는 필수로 확인된 범위를 다운로드하도록 WU 클라이언트에 요청**합니다.

  4. **클라이언트가 이 범위를 다운로드하여 Windows Installer로 전달**하면 Windows Installer가 범위를 적용한 다음, 추가 범위가 필요한지 여부를 결정합니다. 이 작업은 Windows Installer가 WU 클라이언트에 필요한 모든 범위가 다운로드되었다는 것을 알릴 때까지 반복됩니다.

  이 시점에서 다운로드가 완료되고 업데이트를 설치할 준비가 됩니다.

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>배달 최적화로 대역폭 소비를 줄이는 방법

DO(배달 최적화)는 운영 체제 업데이트, 운영 체제 업그레이드 및 애플리케이션의 대역폭 소비 감소를 원하는 기업들을 위한 자체 구성된 분산형 캐시 솔루션입니다. DO를 통해 클라이언트는 지정된 다운로드 위치(이 시나리오에서는 ISV 파일 캐시)와 함께 대체 원본(예: 네트워크의 다른 피어)으로부터 해당 요소를 다운로드할 수 있습니다.

기본적으로 Windows 10 Enterprise 및 Education에서는 조직 고유의 네트워크에서만 DO를 통한 피어 투 피어 공유가 허용되지만, 그룹 정책 및 MDM(모바일 디바이스 관리) 설정을 사용해서 이를 다르게 구성할 수 있습니다.

DO에 대한 자세한 내용은 [Windows 10 업데이트를 위한 배달 최적화 구성](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization)을 참조하세요.
