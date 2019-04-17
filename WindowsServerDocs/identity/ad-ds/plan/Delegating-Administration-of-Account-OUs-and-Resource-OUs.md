---
ms.assetid: 19feca0e-a6d0-4d27-93b0-cb44f8c26484
title: "계정 Ou 및 리소스 Ou 관리 위임"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 56e69bffdf8ecc0f37f9f5159ae6bce7fcdc49f8
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="delegating-administration-of-account-ous-and-resource-ous"></a>계정 Ou 및 리소스 Ou 관리 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

계정 조직 (Ou) 사용자를 그룹과 컴퓨터 개체를 포함 합니다. 리소스 Ou 리소스 및 리소스를 관리 하는 계정 포함 됩니다. 숲 소유자는 OU 소유자에 게 해당 구조 제어 위임 및 OU 구조 이러한 물체 및 리소스를 만들기 위한 합니다.  
  
## <a name="delegating-administration-of-account-ous"></a>위임 Ou 계정 관리  
생성 하 고 사용자, 그룹과 컴퓨터 개체 수정 해야 하는 경우 데이터 관리자에 게 계정을 OU 구조 위임 합니다. 계정 OU 구조 하지 독립적으로 제어할 수 있어야 하는 계정 종류별로 ou 하위입니다. 예를 들어, OU 소유자 자녀가 Ou 사용자가, 컴퓨터, 그룹에 대 한 계정을 OU 및 계정 서비스에 대 다양 한 데이터 관리자에 게 특정 컨트롤 한 위임 수 있습니다.  
  
다음은 OU 구조 계정 중 한 가지 예입니다.  
  
![관리 위임](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/66d38fbe-e8eb-42d7-abab-9526243bf6d9.gif)  
  
다음 표에서 나열 하 고 가능한 하위 Ou OU 구조 계정에 만들 수 있는 설명 합니다.  
  
|OU|목적|  
|------|-----------|  
|사용자가|사용자 계정 일상적인 담당자 포함 되어 있습니다.|  
|서비스 계정|네트워크 리소스에 액세스 해야 하는 일부 서비스 사용자 계정으로 실행 합니다. 사용자가 OU에 포함 된 사용자 계정에서이 OU 별도 서비스 사용자 계정에 만들어집니다. 또한 다른 종류의 사용자 계정 별도 Ou 둠으로써 관리의 특정 요구에 따라 관리할 수 있습니다.|  
|컴퓨터|도메인 컨트롤러 아닌 다른 컴퓨터에 대 한 계정을 포함 되어 있습니다.|  
|그룹|개별적으로 관리 관리 그룹을 제외 하 고 모든 종류의 그룹에 포함 되어 있습니다.|  
|관리자|일반 사용자에 게 개별적으로 관리 수 있도록 하 데이터 관리자 OU 구조 계정에 대 한 사용자 및 그룹 계정을 포함 되어 있습니다. 설정 변경 사항을 관리 사용자 및 그룹 추적할 수 있도록이 OU에 대 한 감사 합니다.|  
  
다음은 OU 구조 계정에 대 한 관리 그룹 디자인 중 한 가지 예입니다.  
  
![관리 위임](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/be2cd2d2-6956-429c-a53a-369e6fe40b2b.gif)  
  
자녀가 Ou 관리 하는 그룹을 완전히 제어할만 개체 관리 하는 특정 클래스 부여 됩니다.  
  
제어 OU 구조 내 위임를 사용 하는 그룹 종류에는 계정이 있는 위치를 관리할 수 있는 OU 구조 기준으로 기반으로 합니다. 관리자 사용자 계정 및 OU 구조 단일 도메인에 있으면 위임에 사용 하 여 만드는 그룹 글로벌 그룹 여야 합니다. 조직에서 관리 하는 자체 사용자 계정 둘 이상의 지역에 존재 하는 부서, Ou 개 이상의 도메인에 있는 계정 관리 담당 하는 데이터 관리자가 그룹을 할 수도 있습니다. 모든 데이터 관리자 계정 단일 도메인의 존재 OU 구조 제어 위임 필요한 여러 도메인에 있는 경우 해당 관리자 계정 회원 글로벌 그룹의 확인 하 고 제어 OU 구조 글로벌 이러한 그룹 각 도메인에 위임. OU 구조를 제어 하는 위임 데이터 관리자 계정 여러 도메인의 제공, 유니버설 그룹을 사용 해야 합니다. 따라서 제어 여러 도메인에 위임를 사용할 수 및 유니버설 그룹 다른 도메인의 사용자가 포함 될 수 있습니다.  
  
## <a name="delegating-administration-of-resource-ous"></a>관리 Ou 리소스의 위임  
리소스 Ou 리소스에 대 한 액세스를 관리 하는 데 사용 합니다. 리소스 OU 소유자 리소스 파일 공유, 데이터베이스, 프린터 등을 포함 하는 도메인에 가입 하는 서버에 대 한 컴퓨터 계정을 만듭니다. 또한 리소스 OU 소유자 리소스에 대 한 액세스를 제어 하는 그룹을 만듭니다.  
  
다음 그림 가능한 두 OU 리소스에 대 한 위치를 보여 줍니다.  
  
![관리 위임](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/6667a5ce-34d6-48a9-9974-b823ba70e2af.gif)  
  
리소스 OU 도메인 루트 OU 관리 계층에서 해당 계정 OU OU 자식으로 있을 수 있습니다. 모든 자녀 표준 Ou 리소스 Ou 필요는 없습니다. 컴퓨터 및 그룹 직접 OU 리소스에에서 배치 됩니다.  
  
리소스 OU 소유자 OU 내 개체를 소유 하 고 하지만 자체 OU 컨테이너 소유 하 고 있지 않습니다. 컴퓨터 및 그룹 개체; 리소스 OU 소유자 관리 다른 유형의 OU, 내 개체를 만들 수 및 Ou 자녀를 만들 수 있습니다.  
  
> [!NOTE]  
> 작성자 또는 개체의 소유자 부모 컨테이너의 상속 권한 상관 없이 개체에 액세스 제어 목록 ACL ()를 설정 하는 기능을 있습니다. 리소스 OU 소유자 ACL OU에을 다시 수 있는 경우 해당 소유자 OU를 포함 하 여 사용자의 개체의 모든 클래스를 만들 수 있습니다. 이러한 이유로 리소스 OU 소유자 Ou 만드는 허용 되지 않습니다.  
  
도메인에 있는 OU 각 리소스에 대 한 데이터 관리자의 콘텐츠를 관리 하는 일을 전 세계 그룹을 만듭니다. 이 그룹 OU 컨테이너 자체 비롯해 하지 OU에 있는 그룹과 컴퓨터 개체를 통해 모든 권한을 가집니다.  
  
다음 그림에서는 OU 리소스에 대 한 관리 그룹 디자인을 보여 줍니다.  
  
![관리 위임](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/8a3f7714-a3bf-43f7-b999-6070543248b0.gif)  
  
컴퓨터 계정을 OU 리소스에 배치 OU 소유자 제어할 계정 개체 하지만 OU 소유자는 컴퓨터의 관리자 확인 하지 않습니다. 된 Active Directory 도메인에 도메인 관리자 그룹, 기본적으로에 있는 모든 컴퓨터에서 로컬 관리자가 그룹 합니다. 즉, 서비스 관리자는 컴퓨터에 대 한 제어 합니다. 리소스 OU 소유자가 Ou 컴퓨터 관리 제어를 요구 하는 경우 숲 소유자 하도록 리소스 OU 소유자 관리자가 그룹의 회원 OU 컴퓨터에서 제한 된 그룹 그룹 정책을 적용 수 있습니다.  
  


