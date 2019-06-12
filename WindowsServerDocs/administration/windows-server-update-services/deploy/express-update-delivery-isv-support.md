---
title: Express 업데이트 배달 ISV 지원
description: WSUS Windows Server Update Service () 항목-하는 방법을 소프트웨어 공급 업체 (ISV)는 WSUS를 사용 하 여 Express 업데이트 제공을 구성할 수 있습니다.
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 7331418c1926958da07c94bca9ff9f871134f3fa
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439874"
---
# <a name="express-update-delivery-isv-support"></a>Express 업데이트 배달 ISV 지원

>적용 대상: Windows 10, Windows Server 2016

Windows 10 업데이트 다운로드는 모든 패키지에는 일관성과 간결성을 위해 이전에 릴리스된 모든 수정 내용이 포함 되어 있으므로 클 수 있습니다.  

버전 7, Windows 라는 기능을 사용 하 여 Windows 업데이트 다운로드의 크기를 줄일 수 있게 되었습니다 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2), 및 Windows 10 enterprise 장치 필요 Windows Server Update 소비자 장치를 지원 하지만 기본적으로, Services (WSUS) Express를 활용할 수 있습니다.

## <a name="how-microsoft-supports-express"></a>Microsoft가 Express를 지원하는 방법

- **독립 실행형 WSUS express**

    Express 업데이트 배달 이미 [모든 지원 되는 버전의 WSUS에서 사용 가능한](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx)합니다.

- **Windows 업데이트에 직접 연결 하는 장치에서 express** 

    소비자 장치 Express 다운로드를 지원 합니다: 검색, 다운로드 및 업데이트를 설치 하려면 Windows Update (WU) 클라이언트를 사용 하 합니다. 다운로드 단계 중 WU 클라이언트 Express 패키지를 요청 하 고 적절 한 바이트 범위를 다운로드 합니다.

-  **[비즈니스용 Windows 업데이트](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** 를 사용하여 관리되는 엔터프라이즈 장치 또한 구성을 변경하지 않고 Express 업데이트 배달 지원의 이점을 얻을 수 있습니다.

## <a name="how-isvs-can-take-advantage-of-express"></a>Isv가 사용할 수 있는 방법을의 Express

Isv는 Express 업데이트 배달을 지원 하기 위해 WSUS와 WU 클라이언트를 사용할 수 있습니다. Microsoft는 다음 세 단계를 권장, 각 아래 섹션에서 자세히 설명 합니다.

1.  [**WSUS 구성**](#BKMK_1)

    WSUS 서버는 필요에 대 한 검색 및 업데이트 동기화 (추가 정보를 찾을 수 있습니다 [여기](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx))

2.  [**지정 하 고 ISV 파일 캐시를 채우기**](#BKMK_2)

    빠른 (.psf 파일)를 패키지 및 업데이트 캐비닛 파일 (.cab 파일)를 포함 하는 업데이트 콘텐츠를 호스트 하는 ISV 파일 캐시 것이 좋습니다.

3.  [**WU 클라이언트 작업을 보내기 위해 ISV 클라이언트 에이전트 설정**](#BKMK_3)

>[!NOTE]
>필요한 누적 업데이트에 대 한 Windows 10 버전 1607 릴리스 (또는 그 이후에) 2017 년 1 월 ([KB3213986 (OS 빌드 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693) 를 설치 해야 합니다.
    
   - ISV 클라이언트 에이전트 업데이트를 승인 하면 수행 다운로드 하 여 설치 하려면 업데이트 확인
   - WU 클라이언트 다운로드에 대 한 바이트 범위를 결정 하 고 다운로드 요청 시작

### <a name="BKMK_1"></a>1 단계: WSUS 구성

WSUS는 Windows Update로 인터페이스 역할을 하 고 다운로드 해야 하는 Express 패키지를 설명 하는 모든 메타 데이터를 관리 합니다. 배포 해야 하는 경우 참조 [ **개요의 Windows Server Update Services 3.0 SP2**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)합니다. WSUS을 배포한 후 주요 고려 사항은 WSUS 서버에서 업데이트 콘텐츠를 로컬로 저장할지 여부입니다. WSUS를 구성 하는 경우에 업데이트를 로컬에 저장 하지 않으므로 하는 것이 좋습니다. 이 환경에서 이러한 패키지의 배포를 전달 하는 소프트웨어를 이미가지고 있다고 가정 합니다. WSUS 로컬 저장소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요 [ **업데이트 저장 위치 결정**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx)합니다.

### <a name="BKMK_2"></a>2 단계: 지정 하 고 ISV 파일 캐시 채우기 

#### <a name="specify-the-isv-file-cache"></a>ISV 파일 캐시를 지정 합니다.

에 자세히 설명 된 새 클라이언트 쪽 그룹 정책 및 모바일 장치 관리 (MDM) 설정 합니다 [ **구성 서비스 공급자 참조** ](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) ISV 파일 캐시의 위치를 정의 합니다.

| **이름**                                              | **설명**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 업데이트에 대 한 대체 다운로드 위치를 구성 합니다. | Microsoft Update에서 업데이트를 호스트 하는 대체 인트라넷 서버를 지정합니다. 이 업데이트 서비스 네트워크에서 컴퓨터를 자동으로 업데이트를 사용할 수 있습니다. |

ISV 파일 캐시에 대 한 대체 다운로드 위치를 설정 하는 데 가지 두 가지 옵션이 있습니다.

1. **ISV HTTP 서버 호스트 이름을 지정**, ISV 파일 캐시는
    
    이 방법은 정책에 지정 된 HTTP 서버로 요청을 다운로드할 수 있도록 WU 클라이언트를 구성 합니다.

2. **Localhost를 지정 합니다.**
 
    이 방법은 로컬 호스트에 요청을 다운로드할 수 있도록 WU 클라이언트를 구성 합니다. 이렇게 하면 이러한 요청 및 다운로드 요청을 처리 하는 적절 한 경로 처리 하는 ISV 클라이언트 에이전트를 수 있습니다.

> [!IMPORTANT]
> ISV 파일 캐시에는 다음이 필요합니다.                                                          
> - 서버에는 HTTP 1.1 RFC 당 규정을 준수 해야 합니다. <http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
> 웹 서버를 지원 해야 하는 특히                                                                                                                                                                                                                                       [ **헤드** ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 하 고 [ **가져오기** ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm) 요청<br>                                                                                                                                                                                                                                                                                                  부분 범위 요청<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   -연결 유지<br>                                                                                                                                                                                                                                                                                                                                                                                                                            -대신 "Transfer-encoding: chunked"                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>ISV 파일 캐시 채우기

관리 되는 클라이언트에 설치할 업데이트와 관련 된 파일을 사용 하 여 ISV 파일 캐시를 채워야 합니다. 

**ISV 파일 캐시를 채우는:**

1. 사용 하 여 [WSUS Api](https://msdn.microsoft.com/en-us/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx) 업데이트의 파일 경로 및 파일 이름을 MU 서비스에 대 한 액세스.

    WSUS 서버에서 각 업데이트에 대 한 메타 데이터 업데이트의 파일 경로 및 Microsoft 업데이트에서 파일 이름 포함 같이 (Microsoft Update 호스트 이름에 굵게, 뒤에 파일 경로 및 파일 이름): **<http://download.windowsupdate.com>** /c msdownload/업데이트 / software/updt/2016/09/windows10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74.msu

2. Microsoft 업데이트에서 파일을 다운로드 하 고 이러한 두 가지 방법 중 하나를 사용 하 여 ISV 파일 캐시에 저장 합니다. 

   - 사용 하 여 파일을 저장 합니다 **MU 서비스와 동일한 폴더 경로**

   - 사용 하 여 파일을 저장 한 **ISV 정의 폴더 경로**

     가 HTTP 서버 (또는 localhost) 리디렉션 **HTTP GET** MU 폴더 경로 및 파일 이름, ISV 파일 위치를 참조 하는 요청을 합니다.

### <a name="BKMK_3"></a>3 단계: WU 클라이언트 작업을 보내기 위해 ISV 클라이언트 에이전트 설정

ISV 클라이언트 에이전트 다운로드 및 다음 권장된 워크플로 사용 하 여 승인 된 업데이트의 설치를 오케스트레이션 합니다.

1.  ISV 클라이언트 에이전트를 WSUS 서버에 대해 검색할 WU 클라이언트를 호출 합니다.

2.  검색 WU 클라이언트에 해당 하는 업데이트 집합을 반환합니다.

3.  ISV 클라이언트 업데이트를 승인, 다운로드 및 설치 확인

4.  승인 된 업데이트를 다운로드 하려면 ISV 클라이언트 에이전트 호출 WU 클라이언트

5.  업데이트를 다운로드 한 후 ISV 클라이언트 에이전트 승인 된 업데이트를 설치 하는 WU 클라이언트를 호출 하는

참조 [검색, 다운로드, 및 Installing Updates](https://msdn.microsoft.com/en-us/library/windows/desktop/aa387102(v=vs.85).aspx) WU 클라이언트를 사용 하 여 검색 하는 방법에 대 한 추가 정보에 대 한 업데이트 다운로드 및 설치 합니다.

### <a name="download-workflow-options"></a>워크플로 옵션 다운로드

다음은 두 그림은 ISV 파일 캐시에서 워크플로 옵션 다운로드 중입니다.

![워크플로 1](../../media/express-update-delivery-isv-support/image1.png)

![2 워크플로](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>Express 다운로드 작동 방식

- Express를 지원하는 OS 업데이트의 경우 다음과 같이 서비스에 저장된 파일 페이로드의 두 가지 버전이 있습니다.

  - **전체 파일 버전** -기본적으로 업데이트 이진 파일의 로컬 버전을 대체

  - **Express 버전** -장치에서 기존 이진 파일을 패치 하는 데 필요한 델타를 포함 합니다. 

    전체 파일 버전과 Express 버전 검사 단계의 일부분으로 클라이언트에 다운로드 된 업데이트의 메타 데이터에서 참조 됩니다. 

    **Express 다운로드 같이 작동합니다.**

    WU 클라이언트는 Express 먼저 및 특정 상황 fall에서 전체 파일에 다시 필요한 경우 다운로드 (예를 들어 경우 바이트 범위 요청을 지원 하지 않는 프록시를 거치지) 하려고 합니다.

  1. WU 클라이언트에서 Express 다운로드를 시작 하는 경우 **WU 클라이언트 스텁을 먼저 다운로드**, Express 패키지의 일부인 합니다.

  2. **WU 클라이언트 Windows 설치 관리자에이 스텁 전달**, 로컬 인벤토리를 사용 하 여 제공 되는 파일의 최신 버전을 이동 하는 데 필요한 사항을 장치에 있는 파일의 델타 비교를 위해 스텁을 사용 하는 합니다.

  3. 합니다 **Windows installer에는 다음 범위를 다운로드 하려면 WU 클라이언트 요청** 는 되었는지 여부를 결정 해야 합니다.

  4. **이러한 범위를 다운로드 하 고 Windows 설치 관리자에 전달 하는 WU 클라이언트**, 범위를 적용 하 고 그런 다음 추가 범위 필요한 경우를 결정 합니다. 이 Windows 설치 관리자는 필요한 모든 범위는 다운로드 한 WU 클라이언트 지시 될 때까지 반복 합니다.

  이 시점에서 다운로드가 완료되고 업데이트를 설치할 준비가 됩니다.

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>배달 최적화 대역폭 소비를 줄이는 방법

DO (배달 최적화)에 비즈니스를 운영 체제 업데이트, 운영 체제 업그레이드 및 응용 프로그램에 대 한 대역폭 소비를 줄이는 방안을 검토에 대 한 자체 구성 분산된 캐시 솔루션입니다. 수행 클라이언트가 지정 된 다운로드 위치 (이 시나리오에서는 ISV 파일 캐시)와 함께에서 대체 원본 (예: 네트워크에 있는 다른 피어)에서 이러한 요소를 다운로드 하도록 허용 합니다.

Windows 10 Enterprise 및 Education 기본적으로 조직의 자체 네트워크만 피어-투-피어 공유를 허용 수행 되지만 그룹 정책 및 모바일 장치 관리 (MDM) 설정을 사용 하 여 다르게 구성할 수 있습니다.

가리킵니다 [Windows 10에 대 한 배달 최적화 구성 업데이트](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization) 수행에 대 한 자세한 내용은 합니다.
