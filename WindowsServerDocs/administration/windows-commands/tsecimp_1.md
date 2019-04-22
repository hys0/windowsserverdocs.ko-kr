---
title: tsecimp
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7488ec6-0eff-45ff-89ee-9cbe752416bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38582706dfa5db2b5069415b81dafc533c8a89b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822104"
---
# <a name="tsecimp"></a>tsecimp



TAPI 서버 보안 파일 (tsec.ini 로)에 Extensible Markup Language (XML) 파일에서 할당 정보를 가져옵니다. TAPI 공급자의 목록을 표시 하려면이 명령을 사용할 수도 있습니다 회선 장치 및 관련 된 각각의 XML 파일의 구조에서 콘텐츠를 가져오지 않고 유효성을 검사 도메인 구성원 자격을 확인 합니다.

## <a name="syntax"></a>구문

```
tsecimp /f <Filename> [{/v | /u}]
tsecimp /d
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/f \<Filename>|필수 사항입니다. 가져올 할당 정보를 포함 하는 XML 파일의 이름을 지정 합니다.|
|/v|Tsec.ini 파일에 정보를 가져오지 않고 XML 파일의 구조를 확인 합니다.|
|/u|각 사용자는 XML 파일에 지정 된 도메인의 구성원 인지 확인 합니다. 이 매개 변수를 사용 하는 컴퓨터는 네트워크에 연결 되어야 합니다. 이 매개 변수는 많은 양의 사용자 할당 정보를 처리 하는 경우 성능이 크게 저하 될 수 있습니다.|
|/d|설치 된 전화 통신 공급자의 목록이 표시 됩니다. 각 전화 통신 공급자에 대 한 관련된 된 회선 장치가 주소와 각 줄 장치와 연결 된 사용자가 나열 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   할당 정보를 가져오려면 원하는 XML 파일 아래에 설명 된 구조를 따라야 합니다.  
    -   **UserList** 요소

        **UserList** XML 파일의 최상위 요소입니다.
    -   **사용자** 요소

        각 **사용자** 요소는 도메인의 구성원 인 사용자에 대 한 정보를 포함 합니다. 각 사용자는 하나 이상의 줄 장치 할당 될 수 있습니다.

        또한 각 **사용자** 요소 라는 특성이 있을 수 **NoMerge**합니다. 이 특성을 지정 하는 경우 새로운 회선 전에 사용자에 대 한 모든 현재 줄 장치 할당 제거 됩니다. 원치 않는 사용자 할당을 쉽게 제거할이 특성을 사용할 수 있습니다. 기본적으로이 특성은 설정 하지.

        **사용자** 는 단일 요소를 포함 해야 **DomainUserName** 사용자의 도메인과 사용자 이름을 지정 하는 요소입니다. **사용자** 요소가 포함 될 수도 하나 **FriendlyName** 사용자에 대 한 이름을 지정 하는 요소입니다.

        **사용자** 요소가 하나 포함 될 수 있습니다 **LineList** 요소입니다. 경우에 **LineList** 요소가 없으면,이 사용자에 대 한 모든 줄 장치가 제거 됩니다.
    -   **LineList** 요소

        **LineList** 요소는 각 줄 또는 사용자에 게 할당 될 수 있는 장치에 대 한 정보를 포함 합니다. 각 **LineList** 요소를 하나 이상 포함할 수 **줄** 요소입니다.
    -   **줄** 요소

        각 **줄** 요소 줄 장치를 지정 합니다. 중 하나를 추가 하 여 각 줄 장치를 식별 해야는 **주소** 요소 또는 **PermanentID** 요소 아래에서 **줄** 요소입니다.

        각각에 대해 **줄** 설정할 수 있습니다 요소는 **제거** 특성. 이 특성을 설정 하는 경우 사용자가 더 이상 해당 회선 장치를 할당 합니다. 이 특성을 설정 하지 않으면 사용자는 해당 줄 장치에 대 한 액세스를 얻게 됩니다. 회선 장치 사용자에 게 사용할 수 없는 경우 오류가 지정 됩니다.

## <a name="examples"></a>예
-   다음 예제 XML 코드 세그먼트 위에 정의 된 요소의 올바른 사용법을 보여 줍니다.  
    -   다음 코드는 user1 계정에 할당 된 모든 줄 장치를 제거 합니다.  
        ```
        <UserList>
          <User NoMerge="1">
            <DomainUser>domain1\user1</DomainUser>
          </User>
        </UserList>
        ```  
    -   다음 코드는 99999 주소로 한 줄을 할당 하기 전에 user1 계정에 할당 된 모든 줄 장치를 제거 합니다. User1 회선 장치가 이전에 할당 되었는지 여부에 관계 없이 할당 된 다른 줄 장치 생깁니다.  
        ```
        <UserList>
          <User NoMerge="1">
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <Address>99999</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        ```  
    -   다음 코드 줄을 이전에 할당 된 장치를 삭제 하지 않고 User1에 대 한 한 줄 장치를 추가 합니다.  
        ```
        <UserList>
          <User>
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <Address>99999</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        ```  
    -   다음 코드 줄 주소 99999를 추가 하 고 회선 주소 88888 User1의 액세스 제거 합니다.  
        ```
        <UserList>
          <User>
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <Address>99999</Address>
              </Line>
              <Line Remove="1">
                <Address>88888</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        ```  
    -   다음 코드는 영구 장치 1000을 추가 하 고 회선 88888 User1의 액세스 제거 합니다.  
        ```
        <UserList>
          <User>
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <PermanentID>1000</PermanentID>
              </Line>
              <Line Remove="1">
                <Address>88888</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        
        ```  
-   뒤에 다음 예제 출력 표시는 **/d** 현재 TAPI 구성을 표시 하려면 명령줄 옵션을 지정 합니다. 각 전화 통신 공급자에 대 한 관련된 된 회선 장치가 주소와 각 줄 장치와 연결 된 사용자가 나열 됩니다.  
    ```
    NDIS Proxy TAPI Service Provider
            Line: "WAN Miniport (L2TP)"
                    Permanent ID: 12345678910
    
    NDIS Proxy TAPI Service Provider
            Line: "LPT1DOMAIN1\User1"
                    Permanent ID: 12345678910
    
    Microsoft H.323 Telephony Service Provider
            Line: "H323 Line"
                    Permanent ID: 123456
                    Addresses:
                            BLDG1-TAPI32
    
    ```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[명령 셸 개요](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)