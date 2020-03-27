---
title: 다중 포리스트 배포 계획
description: 이 항목은 Windows Server 2016의 다중 포리스트 환경에 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8acc260f-d6d1-4d32-9e3a-1fd0b2a71586
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8e483f5986a5a23123495e3a13440ddc57a6c521
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314048"
---
# <a name="plan-a-multi-forest-deployment"></a>다중 포리스트 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 다중 포리스트 배포에서 원격 액세스를 구성할 때 필요한 계획 단계에 대해 설명합니다.  
  
## <a name="prerequisites"></a>필수 조건  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  
  
-   양방향 트러스트가 필요합니다.  
  
## <a name="plan-trust-between-forests"></a>포리스트 간 트러스트 계획  
새로운 포리스트의 리소스에 대한 액세스를 허용하고, 클라이언트가 새로운 포리스트에서 DirectAccess를 사용하거나 새 포리스트의 원격 액세스 서버를 진입점으로 원격 액세스 배포에 추가하도록 허용하기로 결정한 경우 두 포리스트 간 완전한 트러스트 관계 즉, 양방향 전이적 트러스트 관계가 설정되어야 합니다. [트러스트 종류](https://technet.microsoft.com/library/cc775736.aspx)를 참조하세요. 포리스트 간의 완전한 트러스트는 다중 포리스트 배포에서 관리자가 새 포리스트에서 GPO 편집, 새 포리스트에서 클라이언트 보안 그룹으로 보안 그룹 사용, 새 포리스트의 컴퓨터에 대한 원격 호출(WinRM, RPC) 수행, 새 포리스트로부터 원격 클라이언트 인증과 같은 작업을 수행하기 위한 사전 요구 사항입니다.  
  
## <a name="plan-remote-access-administrator-permissions"></a>원격 액세스 관리자 권한 계획  
원격 액세스를 구성하면 원격 액세스 서버나 클라이언트가 포함된 각 도메인에서 GPO가 업데이트되거나 새로 만들어집니다. 다중 포리스트 환경에서도 단일 포리스트 환경과 마찬가지로 원격 액세스 관리자는 DirectAccess GPO와 해당 보안 필터를 작성하고 수정할 수 있는 권한이 있어야 하며, 경우에 따라 관련된 모든 포리스트에 대해 DirectAccess GPO의 링크를 만들 수 있는 권한이 있어야 합니다. 이러한 권한은 원격 액세스 관리자가 속한 포리스트에 관계없이 필요합니다.  
  
또한 원격 액세스 관리자는 원래 원격 액세스 배포에 대한 진입점으로 추가된 새 포리스트의 원격 액세스 서버를 비롯하여 모든 원격 액세스 서버에 대한 로컬 관리자여야 합니다.  
  
## <a name="plan-client-security-groups"></a><a name="ClientSG"></a>클라이언트 보안 그룹 계획  
새 포리스트에서 DirectAccess 클라이언트 컴퓨터에 대해 하나 이상의 보안 그룹을 구성해야 합니다. 단일 보안 그룹은 여러 포리스트의 계정을 포함할 수 없기 때문입니다.  
  
> [!NOTE]  
> -   DirectAccess를 사용 하려면 각 포리스트에 대해 Windows 10&reg; 또는 Windows&reg; 8 클라이언트 보안 그룹이 하나 이상 필요 합니다. 그러나 Windows 10 또는 Windows 8 클라이언트를 포함 하는 각 도메인에 대해 Windows 10 또는 Windows 8 클라이언트 보안 그룹을 하나 포함 하는 것이 좋습니다.  
> -   멀티 사이트가 사용 하도록 설정 된 경우 DirectAccess를 사용 하려면 Windows 7 클라이언트 컴퓨터가 지원 되는 각 DirectAccess 진입점에 대해 포리스트 당 Windows 7&reg; 클라이언트 보안 그룹이 하나 이상 있어야 합니다. 그러나 Windows 7 클라이언트를 포함 하는 각 도메인의 진입점 마다 별도의 Windows 7 클라이언트 보안 그룹을 지정 하는 것이 좋습니다.  
>   
> DirectAccess가 추가 도메인의 클라이언트 컴퓨터에 적용되도록 하려면 해당 도메인에서 클라이언트 GPO가 만들어져야 합니다. 보안 그룹을 추가하면 새 도메인에 해당하는 새 클라이언트 GPO가 작성됩니다. 따라서 새 도메인의 새 보안 그룹을 DirectAccess 클라이언트 보안 그룹 목록에 추가하면 새 도메인에서 클라이언트 GPO가 자동으로 만들어지고 이 클라이언트 GPO를 통해 새 도메인의 클라이언트 컴퓨터가 DirectAccess 보안 설정을 가져오게 됩니다.  
>   
> 이미 DirectAccess 클라이언트 보안 그룹으로 구성된 기존의 보안 그룹에 새 도메인의 클라이언트를 추가할 경우에는 DirectAccess에 의해 새 도메인에서 클라이언트 GPO가 자동으로 만들어지지 않습니다. 이 경우 새 도메인의 클라이언트는 DirectAccess 설정을 수신하지 않으므로 DirectAccess를 사용하여 연결할 수 없습니다.  
  
## <a name="plan-certification-authorities"></a>인증 기관 계획  
OTP(일회용 암호) 인증을 사용하도록 DirectAccess 배포가 구성된 경우 각 포리스트에는 동일한 서명 인증 템플릿이 포함되지만 Oid 값은 다릅니다. 이 때문에 포리스트를 단일 구성 단위로 구성할 수 없습니다. 이 문제를 해결 하 고 다중 포리스트 환경에서 OTP를 구성 하려면 [다중 포리스트 배포 구성](Configure-a-Multi-Forest-Deployment.md)항목의 "다중 포리스트 배포에서 otp 구성" 섹션을 참조 하세요.  
  
IPsec 컴퓨터 인증서 인증을 사용할 경우에는 모든 클라이언트 컴퓨터 및 서버 컴퓨터가 속한 포리스트에 관계없이 이러한 컴퓨터에 동일한 루트 또는 중간 인증 기관에서 발급한 컴퓨터 인증서가 있어야 합니다.  
  
## <a name="plan-otp-exemptions"></a>OTP 예외 계획  
DirectAccess OTP 인증을 사용할 경우 OTP 예외 보안 그룹이 단일 포리스트의 사용자로 제한됩니다. 각 보안 그룹에는 단일 포리스트의 사용자만 포함될 수 있으며, 이러한 보안 그룹은 하나만 구성할 수 있기 때문입니다.  
  


