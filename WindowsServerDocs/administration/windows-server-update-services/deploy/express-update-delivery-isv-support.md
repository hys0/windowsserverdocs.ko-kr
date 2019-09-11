---
title: Express 업데이트 배달 ISV 지원
description: WSUS (Windows Server Update Service) 토픽-ISV (독립 소프트웨어 공급 업체)에서 WSUS를 사용 하 여 빠른 업데이트 배달을 구성할 수 있는 방법
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
ms.openlocfilehash: 0f5893d47219e9263ed7f35bee472848a47c6164
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868742"
---
# <a name="express-update-delivery-isv-support"></a>Express 업데이트 배달 ISV 지원

>적용 대상: Windows 10, Windows Server 2016

모든 패키지에는 일관성과 단순성을 보장 하기 위해 이전에 릴리스된 모든 수정 프로그램이 포함 되어 있으므로 Windows 10 업데이트 다운로드는 클 수 있습니다.  

버전 7부터 Windows는 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)라는 기능을 사용 하 여 Windows 업데이트 다운로드 크기를 줄일 수 있으며, 소비자 장치는 기본적으로이 기능을 지원 하지만, windows 10 enterprise 장치에는 WINDOWS SERVER UPDATE SERVICES (WSUS)를 사용 해야 합니다. Express의 장점입니다.

## <a name="how-microsoft-supports-express"></a>Microsoft가 Express를 지원하는 방법

- **WSUS 독립 실행형 Express**

    지원 되는 [모든 버전의 WSUS에서](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx)Express 업데이트 배달이 이미 제공 됩니다.

- **Windows 업데이트에 직접 연결 된 장치에 대 한 Express** 

    소비자 장치에서 빠른 다운로드 지원: WU (Windows 업데이트) 클라이언트를 사용 하 여 업데이트를 검색, 다운로드 및 설치 합니다. 다운로드 단계 중에 WU 클라이언트는 Express 패키지를 요청 하 고 적절 한 바이트 범위를 다운로드 합니다.

-  **[비즈니스용 Windows 업데이트](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** 를 사용하여 관리되는 엔터프라이즈 장치 또한 구성을 변경하지 않고 Express 업데이트 배달 지원의 이점을 얻을 수 있습니다.

## <a name="how-isvs-can-take-advantage-of-express"></a>Isv에서 Express를 활용 하는 방법

Isv는 WSUS 및 WU 클라이언트를 사용 하 여 빠른 업데이트 배달을 지원할 수 있습니다. 다음 세 단계를 수행 하는 것이 좋습니다. 각 단계에 대해서는 아래 섹션에서 자세히 설명 합니다.

1.  [**WSUS 구성**](#BKMK_1)

    WSUS 서버는 검색 & 업데이트 동기화에 필요 합니다 (자세한 내용은 [여기](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx)참조).

2.  [**ISV 파일 캐시 지정 및 채우기**](#BKMK_2)

    업데이트 캐비닛 파일 (.cab 파일) 및 Express 패키지 (psf 파일)를 포함 하는 업데이트 콘텐츠를 호스트 하는 데 ISV 파일 캐시가 권장 됩니다.

3.  [**WU 클라이언트 작업을 보내도록 ISV 클라이언트 에이전트 설정**](#BKMK_3)

>[!NOTE]
>설치 하려면[KB3213986 (OS 빌드 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693) 2017의 Windows 10 버전 1607 버전에 대 한 누적 업데이트가 필요 합니다.
    
   - ISV 클라이언트 에이전트는 승인할 업데이트를 결정 하 고 업데이트를 다운로드 하 여 설치 하는 경우를 결정 합니다.
   - WU 클라이언트는 다운로드 요청을 다운로드 하 고 시작 하기 위한 바이트 범위를 결정 합니다.

### <a name="BKMK_1"></a>1 단계: WSUS 구성

WSUS는 Windows 업데이트 하는 인터페이스로 사용 되며 다운로드 해야 하는 Express 패키지를 설명 하는 모든 메타 데이터를 관리 합니다. 배포 해야 하 [**는 경우 Windows Server Update Services 3.0**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)s p 2의 개요를 참조 하세요. WSUS가 배포 되 면 기본 고려 사항은 업데이트 콘텐츠를 WSUS 서버에 로컬로 저장할지 여부입니다. WSUS를 구성 하는 경우 업데이트를 로컬에 저장 하지 않는 것이 좋습니다. 사용자 환경에 이러한 패키지를 배포 하는 소프트웨어가 이미 있다고 가정 합니다. WSUS 로컬 저장소를 구성 하는 방법에 대 한 자세한 내용은 [**업데이트를 저장할 위치 결정**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx)을 참조 하십시오.

### <a name="BKMK_2"></a>2 단계: ISV 파일 캐시 지정 및 채우기 

#### <a name="specify-the-isv-file-cache"></a>ISV 파일 캐시 지정

[**구성 서비스 공급자 참조**](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) 에 자세히 설명 된 새로운 클라이언트 쪽 그룹 정책 및 MDM (모바일 장치 관리) 설정은 ISV 파일 캐시의 위치를 정의 합니다.

| **이름**                                              | **설명**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 업데이트에 대 한 대체 다운로드 위치를 구성 합니다. | Microsoft 업데이트에서 업데이트를 호스트할 대체 인트라넷 서버를 지정 합니다. 그런 다음이 업데이트 서비스를 사용 하 여 네트워크에 있는 컴퓨터를 자동으로 업데이트할 수 있습니다. |

ISV 파일 캐시에 대 한 대체 다운로드 위치를 설정 하는 경우 두 가지 옵션이 있습니다.

1. Isv 파일 캐시용 **ISV HTTP 서버 호스트 이름 지정**
    
    이 방법은 정책에 지정 된 HTTP 서버에 다운로드 요청을 만들도록 WU 클라이언트를 구성 합니다.

2. **Localhost 지정**
 
    이 방법은 localhost에 다운로드 요청을 만들도록 WU 클라이언트를 구성 합니다. 따라서 ISV 클라이언트 에이전트는 이러한 요청을 처리 하 고 다운로드 요청을 수행할 수 있도록 적절 하 게 라우팅할 수 있습니다.

> [!IMPORTANT]
> ISV 파일 캐시에는 다음이 필요 합니다.                                                          
> - 서버는 RFC에 따라 HTTP 1.1을 준수 해야 합니다.<http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
> 특히 웹 서버에서 다음을 지원 해야 합니다.                                                                                                                                                                                                                                       [**HEAD**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 및 [**GET**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm) 요청<br>                                                                                                                                                                                                                                                                                                  -부분 범위 요청<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   -Keep-alive<br>                                                                                                                                                                                                                                                                                                                                                                                                                            -"전송-인코딩: 청크 분할"을 사용 하지 마십시오.                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>ISV 파일 캐시 채우기

ISV 파일 캐시는 관리 되는 클라이언트에 설치할 업데이트와 연결 된 파일로 채워야 합니다. 

**ISV 파일 캐시를 채우려면 다음을 수행 합니다.**

1. [WSUS api](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx) 를 사용 하 여 MU 서비스의 업데이트 파일 경로 및 파일 이름에 액세스 합니다.

    WSUS 서버의 각 업데이트에 대 한 메타 데이터에는 다음과 같이 Microsoft 업데이트에 대 한 업데이트의 파일 경로와 파일 이름이 포함 되어 있습니다. **<http://download.windowsupdate.com>** Microsoft 업데이트 hostname은 굵게 표시 되 고 파일 경로와 파일 이름에는/c/msdownload/update/software/updt/2016/09/ windows 10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74

2. Microsoft 업데이트에서 파일을 다운로드 하 여 다음 두 가지 방법 중 하나를 사용 하 여 ISV 파일 캐시에 저장 합니다. 

   - **MU 서비스와 동일한 폴더 경로** 를 사용 하 여 파일 저장

   - **ISV 정의 폴더 경로** 를 사용 하 여 파일 저장

     HTTP 서버 (또는 localhost)가 MU 폴더 경로 및 파일 이름을 참조 하는 **HTTP GET** 요청을 ISV 파일 위치로 리디렉션하도록 합니다.

### <a name="BKMK_3"></a>3 단계: WU 클라이언트 작업을 보내도록 ISV 클라이언트 에이전트 설정

ISV 클라이언트 에이전트는 다음과 같은 권장 워크플로를 사용 하 여 승인 된 업데이트의 다운로드 및 설치를 오케스트레이션 합니다.

1.  ISV 클라이언트 에이전트는 WU 클라이언트를 호출 하 여 WSUS 서버를 검색 합니다.

2.  검색은 WU 클라이언트에 적용 가능한 업데이트 집합을 반환 합니다.

3.  ISV 클라이언트에서 승인, 다운로드 및 설치할 업데이트를 결정 합니다.

4.  ISV 클라이언트 에이전트는 WU 클라이언트를 호출 하 여 승인 된 업데이트를 다운로드 합니다.

5.  업데이트가 다운로드 되 면 ISV 클라이언트 에이전트는 WU 클라이언트를 호출 하 여 승인 된 업데이트를 설치 합니다.

WU 클라이언트를 사용 하 여 업데이트를 검색, 다운로드 및 설치 하는 방법에 대 한 자세한 내용은 [업데이트 검색, 다운로드 및 설치](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx) 를 참조 하세요.

### <a name="download-workflow-options"></a>워크플로 옵션 다운로드

ISV 파일 캐시에서 워크플로 옵션을 다운로드 하는 두 가지 그림은 다음과 같습니다.

![워크플로 1](../../media/express-update-delivery-isv-support/image1.png)

![워크플로 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>Express 다운로드 작동 방식

- Express를 지원하는 OS 업데이트의 경우 다음과 같이 서비스에 저장된 파일 페이로드의 두 가지 버전이 있습니다.

  - **전체 파일 버전** -기본적으로 업데이트 이진 파일의 로컬 버전 바꾸기

  - **Express version** -장치에서 기존 이진 파일을 패치 하는 데 필요한 델타를 포함 합니다. 

    전체 파일 버전과 Express 버전은 모두 업데이트의 메타 데이터에서 참조 되며, 검색 단계의 일부로 클라이언트에 다운로드 됩니다. 

    **빠른 다운로드는 다음과 같이 작동 합니다.**

    WU 클라이언트는 Express first를 다운로드 하려고 시도 하 고, 특정 상황에서는 필요한 경우 (예: 바이트 범위 요청을 지원 하지 않는 프록시를 통해 이동 하는 경우) 전체 파일로 대체 됩니다.

  1. WU 클라이언트에서 빠른 다운로드를 시작 하면 **wu 클라이언트는 먼저**express 패키지의 일부인 스텁을 다운로드 합니다.

  2. WU 클라이언트는 스텁을 사용 하 여 로컬 인벤토리를 수행 하 고, 장치에 있는 파일의 델타와 제공 되는 파일의 최신 버전을 가져오는 데 필요한 항목을 비교 하는 **Windows installer로이 스텁을 전달**합니다.

  3. 그러면 Windows installer는 필요한 것으로 확인 된 **범위를 다운로드 하도록 WU 클라이언트에 요청** 합니다.

  4. **WU 클라이언트는 이러한 범위를 다운로드 하 고 Windows installer에 전달**하 여 범위를 적용 한 다음 추가 범위가 필요한 지 여부를 결정 합니다. 이는 Windows installer가 필요한 모든 범위가 다운로드 되었음을 WU 클라이언트에 지시할 때까지 반복 됩니다.

  이 시점에서 다운로드가 완료되고 업데이트를 설치할 준비가 됩니다.

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>배달 최적화에서 대역폭 사용량을 줄이는 방법

배달 최적화 (DO)는 운영 체제 업데이트, 운영 체제 업그레이드 및 응용 프로그램에 대 한 대역폭 사용량을 줄일 수 있는 비즈니스를 위한 자체 구성 분산 캐시 솔루션입니다. 를 사용 하면 클라이언트가 지정 된 다운로드 위치 (이 시나리오의 ISV 파일 캐시)와 함께 대체 원본 (예: 네트워크의 다른 피어)에서 해당 요소를 다운로드할 수 있습니다.

기본적으로 Windows 10 Enterprise 및 교육용에서는 조직의 자체 네트워크 에서만 피어 투 피어 공유를 허용 하지만 그룹 정책 및 MDM (모바일 장치 관리) 설정을 사용 하 여 다르게 구성할 수 있습니다.

이에 대 한 자세한 내용은 [Windows 10 업데이트에 대 한 배달 최적화 구성](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization) 을 참조 하세요.
