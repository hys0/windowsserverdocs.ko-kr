---
title: 2 단계 DirectAccess-VPN 서버 구성
description: 이 항목은 Windows Server 2016에 대 한 기존 원격 액세스 (VPN) 배포에 DirectAccess 추가 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe221fc9-c7d9-4508-b8a1-000d2515283c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c26f1fbcfa2d94c001579aabd6794c6537bd06f8
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314738"
---
#  <a name="step-2-configure-the-directaccess-vpn-server"></a>2 단계 DirectAccess-VPN 서버 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 DirectAccess 사용 마법사를 사용하여 기본 원격 액세스 배포에 필요한 클라이언트 및 서버 설정을 구성하는 방법에 대해 설명합니다.

다음 표에서는이 항목을 사용 하 여 완료할 수 있는 단계에 대 한 개요를 제공 합니다.

|작업       |설명|
|-----------|-----------|
|DirectAccess 클라이언트 구성|DirectAccess 클라이언트가 포함된 보안 그룹으로 원격 액세스 서버를 구성합니다.|
|네트워크 토폴로지 구성|원격 액세스 서버 설정을 구성합니다.|
|DNS 접미사 검색 목록 구성|필요한 경우 접미사 검색 목록을 수정합니다.|
|GPO 구성|필요한 경우 GPO를 수정합니다.|

## <a name="to-start-the-enable-directacces-wizard"></a>DirectAcces 사용 마법사를 시작하려면

1. 서버 관리자에서 **도구**를 클릭 한 다음 **원격 액세스**를 클릭 합니다. **이 화면을 다시 표시 안 함**을 선택 하지 않으면 DirectAccess 사용 마법사가 자동으로 시작 됩니다. 

2. 마법사가 자동으로 시작 되지 않으면 라우팅 및 원격 액세스 트리에서 서버 노드를 마우스 오른쪽 단추로 클릭 하 고 **DirectAccess 사용**을 클릭 합니다.

3. **다음**을 클릭합니다.

## <a name="configure-directaccess-clients"></a>DirectAccess 클라이언트 구성

DirectAccess를 사용하여 클라이언트 컴퓨터를 프로비전하려면 클라이언트 컴퓨터가 선택한 보안 그룹에 속해 있어야 합니다. DirectAccess를 구성한 후 해당 보안 그룹의 클라이언트 컴퓨터는 DirectAccess 그룹 정책을 수신하도록 프로비전됩니다.

1. **그룹 선택** 페이지에서 **추가**를 클릭합니다.

2. **그룹 선택** 대화 상자에서 DirectAccess 클라이언트 컴퓨터를 포함한 보안 그룹을 선택합니다.

3. **이동 컴퓨터에만 DirectAccess 사용** 확인란을 선택하여 이동 컴퓨터에서만 내부 네트워크에 액세스할 수 있도록 허용합니다.

4. **강제 터널링 사용** 확인란을 선택하여 모든 클라이언트 트래픽(내부 네트워크 및 인터넷으로의 트래픽)을 원격 액세스 서버를 통해 라우팅합니다.

5. **다음**을 클릭합니다.

## <a name="configure-the-network-topology"></a>네트워크 토폴로지 구성

원격 액세스를 배포하려면 올바른 네트워크 어댑터, 클라이언트 컴퓨터에서 연결할 수 있는 원격 액세스 서버의 공용 URL(ConnectTo 주소) 및 주체가 ConnectTo 주소와 일치하는 IP-HTTPS 인증서로 원격 액세스 서버를 구성해야 합니다.

1. **네트워크 토폴로지** 페이지에서 조직에서 사용할 배포 토폴로지를 클릭합니다. **클라이언트가 원격 액세스 서버에 연결하는 데 사용할 공개 이름 또는 IPv4 주소 입력**에 배포의 공개 이름(이 이름이 IP-HTTPS 인증서의 주체 이름(예: edge1.contoso.com)과 일치)을 입력하고 **다음**을 클릭합니다.

## <a name="configure-the-dns-suffix-search-list"></a>DNS 접미사 검색 목록 구성

DNS 클라이언트의 경우 DNS 검색 기능을 확장하거나 수정하는 DNS 도메인 접미사 검색 목록을 구성할 수 있습니다. 목록에 접미사를 추가하면 둘 이상의 지정된 DNS 도메인에서 정규화되지 않은 짧은 컴퓨터 이름을 검색할 수 있습니다. 그러면 dns 쿼리가 실패 하는 경우 DNS 클라이언트 서비스는이 목록을 사용 하 여 다른 이름 접미사 끝을 원래 이름에 추가 하 고 이러한 대체 Fqdn에 대해 dns 쿼리를 DNS 서버로 반복할 수 있습니다.

1. **DNS 클라이언트 접미사 검색 목록을 사용하여 DirectAccess 클라이언트 구성**을 선택하여 클라이언트 이름 검색을 위한 추가 접미사를 추가합니다.

2. **새** 접미사에 새 접미사 이름을 입력 한 다음 **추가**를 클릭 합니다. 또한 검색 순서를 변경 하 고 **도메인 접미사에서 사용할**접미사를 제거할 수 있습니다.

>두고 연결 되지 않은 이름 공간 시나리오에서 하나 이상의 도메인 컴퓨터에 컴퓨터가\)속한 Active Directory 도메인과 일치 하지 않는 DNS 접미사가 있는 경우 필요한 모든 접미사를 포함 하도록 검색 목록을 사용자 지정 해야 \(합니다. 원격 액세스 마법사는 기본적으로 Active Directory DNS 이름을 클라이언트의 주 DNS 접미사로 구성합니다. 관리자는 이름 확인을 위해 클라이언트에서 사용하는 DNS 접미사를 추가해야 합니다.

컴퓨터 및 서버의 경우 다음과 같은 기본 DNS 검색 동작을 미리 결정 하 고 정규화 되지 않은 약식 이름을 완료 하 고 해결할 때 사용 합니다. 접미사 검색 목록이 비어 있거나 지정 되지 않은 경우 컴퓨터의 주 DNS 접미사가 정규화 되지 않은 짧은 이름에 추가 되 고 결과 FQDN을 확인 하는 데 DNS 쿼리가 사용 됩니다. 

이 쿼리가 실패 하면 컴퓨터는 네트워크 연결에 대해 구성 된 연결별 DNS 접미사를 추가 하 여 대체 Fqdn에 대 한 추가 쿼리를 시도할 수 있습니다. 연결 관련 접미사가 구성 되어 있지 않거나 이러한 결과 연결별 Fqdn에 대 한 쿼리가 실패 한 경우 클라이언트는 기본 접미사 (계승이 라고도 함)의 체계적인 감소에 따라 쿼리를 다시 시도할 수 있습니다.

예를 들어 주 접미사가 "example.microsoft.com" 인 경우 "microsoft.com" 및 "com" 도메인에서 검색 하 여 약식 이름에 대해 쿼리를 다시 시도할 수 있습니다.

접미사 검색 목록이 비어 있지 않고 하나 이상의 DNS 접미사를 지정 하는 경우에는 지정 된 접미사 목록에서 가능한 Fqdn만 검색 하는 것으로 제한 됩니다. 

목록에 각 접미사를 추가한 결과로 형성된 모든 FQDN에 대한 쿼리가 확인되지 않으면 쿼리 프로세스에 실패하고 "이름을 찾을 수 없음" 결과가 생성됩니다. 

> [!WARNING]
> 도메인 접미사 목록을 사용하는 경우 클라이언트는 쿼리가 응답하지 않거나 확인되지 않으면 다른 DNS 도메인 이름을 기반으로 추가 대체 쿼리를 계속 보냅니다. 접미사 목록의 항목을 사용하여 이름이 확인되고 나면 사용되지 않은 목록 항목은 시도되지 않습니다. 따라서 가장 자주 사용하는 도메인 접미사부터 목록을 정렬하는 것이 가장 효율적입니다.
> 
> 도메인 이름 접미사 검색은 DNS 이름 항목이 정규화되지 않은 경우에만 사용됩니다. DNS 이름을 정규화하려면 이름 끝에 마침표(.)를 입력합니다.

## <a name="gpo-configuration"></a>GPO 구성

원격 액세스를 구성할 때 DirectAccess 설정은 GPO (그룹 정책 Objects)로 수집 됩니다. 

**Gpo 설정**에서는 DIRECTACCESS 서버 gpo 이름 및 클라이언트 gpo 이름이 나열 됩니다. 또한 GPO 선택 설정을 수정할 수 있습니다.

두 Gpo가 DirectAccess 설정으로 자동으로 채워지며 다음과 같은 방식으로 배포 됩니다.

1. **DirectAccess 클라이언트 GPO**. 이 GPO는 IPv6 전환 기술 설정, NRPT 항목, 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙 등의 클라이언트 설정을 포함하며, 클라이언트 컴퓨터에 지정된 보안 그룹에 적용됩니다.

2. **DirectAccess 서버 GPO**. 이 GPO는 배포에서 원격 액세스 서버로 구성 된 모든 서버에 적용 되는 DirectAccess 구성 설정을 포함 합니다. 또한 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙을 포함합니다.

## <a name="summary"></a>요약

원격 액세스 구성이 완료 되 면 **요약이** 표시 됩니다. 구성 된 설정을 변경 하거나 **마침** 을 클릭 하 여 구성을 적용할 수 있습니다.
