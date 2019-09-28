---
title: Microsoft Server 정품 인증
description: Windows Server 2016을 정품 인증하는 방법.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 09/19/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a45d5cc7a54
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 9dd12a7858a24457251d8354a2df49632b5960c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391608"
---
# <a name="windows-server-2016-activation"></a>Windows Server 2016 정품 인증

다음 정보는 Windows Server 2016과 관련된 KMS(키 관리 서비스) 정품 인증을 확인해야 할 때 고려해야 하는 초기 계획 사항에 대한 요약입니다. 이 목록에 나온 것보다 오래된 운영 체제 관련 KMS 정품 인증에 대한 내용은 [1단계: 정품 인증 방법 확인 및 선택](https://technet.microsoft.com/library/jj134256(WS.11).aspx)을 참조하세요.

KMS는 클라이언트 서버 모델을 사용하여 클라이언트를 정품 인증합니다. KMS 클라이언트는 정품 인증을 위해 KMS 호스트라고 불리는 KMS 서버에 연결됩니다. KMS 호스트는 로컬 네트워크에 상주해야 합니다.

KMS 호스트는 서버 전용일 필요가 없으며 KMS는 다른 서비스와 함께 공동 호스트될 수 있습니다. Windows 10, Windows Server 2016, Windows Server 2012 R2, Windows 8.1 또는 Windows Server 2012를 실행하는 물리적 또는 가상 시스템에서 KMS 호스트를 실행할 수 있습니다.

Windows 10 또는 Windows 8.1에서 실행되는 KMS 호스트는 클라이언트 운영 체제를 실행하는 컴퓨터만을 정품 인증할 수 있습니다.
다음 표에서는 Windows Server 2016 및 Windows 10 클라이언트를 포함하는 네트워크에 대한 KMS 호스트 및 클라이언트 요구 사항을 요약합니다.

> [!NOTE]
> **참고:**  업데이트는 이러한 최신 클라이언트의 활성화를 지원하도록 KMS 서버가 필요할 수 있습니다. 활성화 오류가 발생하면 이 테이블에 나열된 적합한 업데이트가 있는지 확인합니다.

|제품 키 그룹|KMS가 호스트될 수 있는 Windows 버전|이 KMS 호스트에 의해 정품 인증되는 Windows 버전|  
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|  
|Windows Server 2016용 볼륨 라이선스|Windows Server 2012<br /><br />Windows Server 2012 R2<br /><br />Windows Server 2016<br /><br />|Windows Server 반기 채널 <br><br>Windows Server 2016(모든 버전)<br /><br />Windows 10 LTSB(2015 및 2016)<br /><br />Windows 10 Professional<br /><br />Windows 10 Enterprise<br /><br />Windows 10 Pro for Workstations<br><br>Windows 10 Education<br><br>Windows Server 2012 R2(모든 버전)<br /><br />Windows 8.1 Professional<br /><br />Windows 8.1 Enterprise<br /><br />Windows Server 2012(모든 버전)<br /><br />Windows Server 2008 R2(모든 버전)<br /><br />Windows Server 2008(모든 버전)<br /><br />Windows 7 Professional<br /><br />Windows 7 Enterprise| 
|Windows 10용 볼륨 라이선스|Windows 7<br /><br />Windows 8.1<br /><br /> Windows 10|Windows 10 Professional<br /><br /> Windows 10 Professional KN<br /><br /> Windows 10 Enterprise<br /><br /> Windows 10 Enterprise KN<br /><br /> Windows 10 Education<br /><br /> Windows 10 Education KN<br /><br /> Windows 10 Enterprise LTSB(2015)<br /><br /> Windows 10 Enterprise LTSB N(2015)<br /><br /> Windows 10 Pro for Workstations<br><br>Windows 8.1 Professional<br /><br /> Windows 8.1 Enterprise<br /><br /> Windows 7 Professional<br /><br /> Windows 7 Enterprise<br /><br />|  
|"Windows 10용 Windows Server 2012 R2"에 대한 볼륨 라이선스|Windows Server 2008 R2<br /><br /> Windows Server2012 Standard<br /><br /> Windows Server2012 Datacenter<br /><br /> Windows Server 2012 R2 Standard<br /><br />Windows Server 2012 R2 Datacenter|Windows 10 Professional<br /><br /> Windows 10 Enterprise<br /><br />Windows 10 Enterprise LTSB(2015)<br><br>Windows 10 Pro for Workstations<br><br>Windows 10 Education<br><br> Windows Server 2012 R2(모든 버전)<br /><br /> Windows 8.1 Professional<br /><br /> Windows 8.1 Enterprise<br /><br /> Windows Server 2012(모든 버전)<br /><br /> Windows Server 2008 R2(모든 버전)<br /><br />Windows Server 2008(모든 버전)<br /><br /> Windows 7 Professional<br /><br /> Windows 7 Enterprise|

> [!NOTE]  
> KMS 서버에서 실행하는 운영 체제 또는 활성화하려는 운영 체제에 따라 다음 업데이트 중 하나 이상을 설치해야 할 수 있습니다.
> - Windows 10을 실행하는 클라이언트의 정품 인증을 지원하려면 Windows 7 또는 Windows Server 2008 R2에 KMS를 설치해야 합니다. 자세한 내용은  [Windows 7 및 Windows Server 2008 R2 KMS 호스트가 Windows 10을 정품 인증할 수 있도록 업데이트](https://support.microsoft.com/help/3079821/update-that-enables-windows-7-and-windows-server-2008-r2-kms-hosts-to-activate-windows-10)를 참조하세요.  
> - Windows 10 및 Windows Server 2016 이상의 클라이언트 또는 서버 운영 체제를 실행하는 클라이언트의 정품 인증을 지원하려면 Windows Server 2012에 KMS 설치가 업데이트되어야 합니다. 자세한 내용은  [Windows Server 2012용 2016년 7월 업데이트 롤업](https://support.microsoft.com/help/3172615/july-2016-update-rollup-for-windows-server-2012)을 참조하세요. 
> - Windows 10 및 Windows Server 2016 이상의 클라이언트 또는 서버 운영 체제를 실행하는 클라이언트의 정품 인증을 지원하려면 Windows 8.1 또는 Windows Server 2012 R2에 KMS 설치가 업데이트되어야 합니다. 자세한 내용은  [Windows 8.1 및 Windows Server 2012 R2용 2016년 7월 업데이트 롤업](https://support.microsoft.com/help/3172614/july-2016-update-rollup-for-windows-8.1-and-windows-server-2012-r2)을 참조하세요.  
> - Windows Server 2008 R2는 Windows Server 2016 이상의 운영 체제를 실행하는 클라이언트의 정품 인증을 지원도록 업데이트될 수 없습니다. 

KMS 호스트는 단 한 개로도 무한히 많은 KMS 클라이언트를 지원할 수 있습니다. 클라이언트가 50개를 초과한다면 KMS 호스트 중 하나를 사용할 수 없게 될 경우를 대비하여 KMS 호스트를 두 개 이상 보유할 것을 권장합니다. 대부분의 조직에서는 KMS 호스트 두 개만으로 전체 인프라를 호스트할 수 있습니다.

# <a name="addressing-kms-operational-requirements"></a>KMS 운영 요구 사항 충족
KMS는 물리적 및 가상 컴퓨터를 정품 인증할 수 있지만 KMS 정품 인증을 정규화하려면 네트워크는 컴퓨터를 최소 수량으로 갖추어야 합니다(정품 인증 임계값이라 불림). KMS 클라이언트는 이 임계값이 충족된 다음에만 정품 인증됩니다. 정품 인증 임계값이 충족되었는지 확인하기 위해 KMS 호스트는 네트워크에서 정품 인증을 요청하는 컴퓨터의 수량을 셉니다.

KMS 호스트는 가장 최근의 연결 수를 셉니다. 클라이언트 또는 서버가 KMS 호스트에 연결되면 호스트는 컴퓨터 ID를 해당 개수에 추가한 다음 해당 응답에서 현재 개수 값을 반환합니다. 개수가 충분히 크면 클라이언트 또는 서버가 정품 인증됩니다. 클라이언트의 수가 25 이상이면 정품 인증됩니다. Microsoft Office 제품의 서버 및 볼륨 버전 개수가 5 이상이면 정품 인증됩니다. KMS는 지난 30일간의 고유한 연결 수만을 세고 최근 50개의 연락처만 저장합니다.

KMS 정품 인증은 정품 인증 유효 간격으로 알려진 180일 동안 유효합니다. KMS 클라이언트는 정품 인증 상태를 유지하기 위해 최소 180일에 한 번씩 KMS 호스트에 연결하여 정품 인증을 갱신해야 합니다. 기본적으로 KMS 클라이언트 컴퓨터는 7일마다 정품 인증 갱신을 수행합니다. 클라이언트의 정품 인증이 갱신되면 정품 인증 유효 기간 간격이 다시 시작됩니다.

# <a name="addressing-kms-functional-requirements"></a>KMS 기능 요구 사항 충족

KMS 정품 인증에는 TCP/IP 연결이 필요합니다. KMS 호스트 및 클라이언트는 기본적으로 DNS(Domain Name System)을 사용하도록 구성됩니다. 기본적으로 KMS 호스트는 KMS 클라이언트가 검색 및 연결해야 하는 정보를 자동으로 게시하기 위해 DNS 동적 업데이트를 사용합니다. 기본 설정을 수락하거나 네트워크 및 보안 구성 요구 사항이 특별히 있는 경우 KMS 호스트와 클라이언트를 수동으로 구성할 수 있습니다.

첫 KMS 호스트가 정품 인증된 후 첫 호스트에서 사용된 KMS 키는 네트워크에서 KMS 호스트를 최대 5개까지 더 정품 인증하는 데 사용될 수 있습니다. KMS 호스트가 정품 인증된 다음에는 관리자가 같은 호스트를 동일한 키로 최대 9번까지 다시 정품 인증할 수 있습니다.

조직에서 6개가 넘는 KMS 호스트를 필요로 한다면 조직의 KMS 키에 추가 정품 인증을 요구해야 합니다. 예를 들어 한 볼륨 라이선스 계약에 물리적 위치가 10개 있으며 각 위치에 로컬 KMS 호스트를 하나씩 배치하고자 할 수 있습니다.

> [!NOTE] 
> 이 예외 사항을 요구하려면 정품 인증 콜 센터에 연락하실 수 있습니다. 자세한 내용은 [Microsoft 볼륨 라이선스]( https://www.microsoft.com/licensing)를 참조하세요.

Windows 10, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 7, Windows Server 2008 R2의 볼륨 라이선스 버전을 실행하는 컴퓨터는 기본적으로 추가 구성이 필요 없는 KMS 클라이언트입니다.

컴퓨터를 KMS 호스트, MAK 또는 Windows 정품 버전에서 KMS 클라이언트로 변환하는 경우 해당하는 KMS 클라이언트 설정 키를 설치합니다. 자세한 내용은 [KMS 클라이언트 설정 키](KMSclientkeys.md)를 참조하세요. 
