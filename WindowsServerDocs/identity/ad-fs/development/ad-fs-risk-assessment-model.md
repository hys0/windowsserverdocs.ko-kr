---
title: AD FS 2019 위험 평가 모델을 사용 하 여 플러그 인 빌드
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: ''
ms.date: 04/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e43f505a02ec2241a84f74ff57e217c2fb95157b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445350"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>AD FS 2019 위험 평가 모델을 사용 하 여 플러그 인 빌드

이제 차단 또는 요청 받은, 사전 인증 및 사후 인증 – 다양 한 단계 인증 요청에 위험 점수를 할당 하도록 사용자 고유의 플러그 인을 빌드할 수 있습니다. 이 AD FS 2019에 도입 된 새 위험 평가 모델을 사용 하 여 수행할 수 있습니다. 

## <a name="what-is-the-risk-assessment-model"></a>위험 평가 모델 이란?

위험 평가 모델은 개발자가 인증 요청 헤더를 읽고 고유한 위험 평가 논리를 구현할 수 있도록 하는 클래스와 인터페이스의 집합입니다. AD FS 인증 프로세스에 따라 (플러그 인) 구현된 코드를 실행합니다. 예를 들어 인터페이스 및 모델에 포함 된 클래스를 사용 하 여, 있습니다 수 하거나 블록에 코드를 구현 또는 요청 헤더에 포함 된 클라이언트 IP 주소를 기반으로 하는 인증 요청을 허용 합니다. AD FS 각 인증 요청에 대 한 코드를 실행 하 고 구현된 논리에 따라 적절 한 조치 됩니다. 

아래 표시 된 대로 AD FS 인증 파이프라인의 세 단계 중 하나에서 플러그 인 코드를 사용 하면 모델

![모델](media/ad-fs-risk-assessment-model/risk1.png)

1.  **요청 받은 단계** – 빌드할 수 있습니다 플러그 인 허용 하거나 AD FS 인증 요청 받으면 즉, 사용자가 자격 증명을 입력 하기 전에 요청을 차단 하도록 합니다. 요청 컨텍스트 (예를 들어 클라이언트 IP, Http 메서드, 프록시 서버 DNS 등)를 사용할 수는 위험 평가 수행 하려면이 단계에서 사용할 수 있습니다. 예를 들어 IP 요청 컨텍스트를 읽고 위험한 Ip 미리 정의 된 목록에서 IP가 인증 요청을 차단 플러그 인을 빌드할 수 있습니다에 대 한. 

2.  **사전 인증 단계** – 빌드할 수 있습니다 플러그 인 허용 하거나 되었으나 AD FS를 평가 하 고 사용자 자격 증명을 제공 하는 경우 지점에 대 한 요청을 차단 합니다. 이 단계에서 요청 컨텍스트 외에도 수도 있습니다 (예: 사용자 토큰, 사용자 id, 등)는 보안 컨텍스트 및 위험 평가 논리에 사용할 프로토콜 컨텍스트 (예: 인증 프로토콜, clientid, resourceid, 등)에 대 한 정보. 예를 들어 사용자 토큰에서 사용자 암호를 읽고 암호는 위험한 암호 목록을 미리 정의 된 경우 인증 요청을 차단 하 여 암호 스프레이 공격을 방지 하기 위해 플러그 인을 빌드할 수 있습니다에 대 한. 

3.  **사후 인증** – 사용자가 자격 증명을 제공 하 고 AD FS 인증을 수행한 후 위험을 평가 하는 플러그 인을 빌드할 수 있습니다. 이 단계에서는 요청 컨텍스트, 보안 컨텍스트 및 컨텍스트 프로토콜 외에도 인증 결과 (성공 또는 실패)에 대 한 정보 또한 있습니다. 플러그 인 사용 가능한 정보를 기반으로 위험 점수를 평가 요청할 위험 점수 및 추가 평가 대 한 정책 규칙을 전달 됩니다. 

플러그 인 위험 평가 빌드 및 AD FS 프로세스에 따라 실행 하는 방법, 더 잘 이해 하려면 특정에서 들어오는 요청을 차단 하는 플러그 인 예제를 빌드 해 보겠습니다 **엑스트라넷** Ip로 식별 위험, 등록 플러그 인 AD FS를 사용 하 여 고 마지막으로 기능을 테스트 합니다. 

>[!NOTE]
>이 연습은 소개를 만드는 방법을 샘플 플러그 인입니다. 엔터프라이즈 준비 솔루션을 만들고 솔루션을 결코입니다.  

## <a name="building-a-sample-plug-in"></a>플러그 인 샘플을 빌드하면

### <a name="pre-requisites"></a>필수 구성 요소
다음은 플러그 인이 샘플을 빌드하는 데 필요한 필수 조건 목록

- AD FS 2019 설치 및 구성
- .NET framework 4.7 이상
- Visual Studio

### <a name="build-plug-in-dll"></a>플러그 인 dll 빌드
다음 절차를 안내 샘플 플러그 인 dll을 작성 합니다.

1. 플러그 인 샘플을 다운로드 하 고 Git Bash를 사용 하 여 다음을 입력 합니다. 

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

2. 만들기를 **.csv** AD FS 서버의 모든 위치에서 파일 (만들었습니다 필자의 경우 합니다 **authconfigdb.csv** 파일을 **C:\extensions**)이 파일을 차단 하려면 Ip를 추가 합니다. 

   플러그 인 샘플에서 들어오는 모든 인증 요청을 차단 합니다는 **엑스트라넷 Ip** 이 파일에 나열 합니다. 

   >{! 참고] AD FS 팜, 있는 경우에 모든 AD FS 서버에서 파일을 만들 수 있습니다. AD FS에 위험한 Ip를 가져오는 데 사용할 수 있습니다 파일 중 하나입니다. 가져오기 프로세스에서 자세히 설명 합니다 [AD FS를 사용 하 여 플러그 인 dll을 등록](#register-the-plug-in-dll-with-ad-fs) 아래의 섹션입니다. 

3. 프로젝트를 열고 `ThreatDetectionModule.sln` Visual Studio를 사용 하 여

4. 제거 된 `Microsoft.IdentityServer.dll` 아래와 같이 솔루션 탐색기에서:</br>
   ![model](media/ad-fs-risk-assessment-model/risk2.png)

5. 에 대 한 참조를 추가 합니다 `Microsoft.IdentityServer.dll` 아래 표시 된 대로 AD FS의

   a.   마우스 오른쪽 단추로 클릭 **참조가** 에 **솔루션 탐색기** 선택한 **참조 추가...**</br> 
   ![모델](media/ad-fs-risk-assessment-model/risk3.png)
   
   b.   에 **참조 관리자** 창 선택 **찾아보기**합니다. 에 **참조할 파일 선택...** 대화 상자에서 선택 `Microsoft.IdentityServer.dll` AD FS 설치 폴더에서 (여기서에서 **C:\Windows\ADFS**)를 클릭 하 고 **추가**합니다.
   
   >[!NOTE]
   >여기서에서 작성 플러그 인 자체 AD FS 서버에서. 개발 환경의 다른 서버에 있으면 복사는 `Microsoft.IdentityServer.dll` 에 개발 상자에 AD FS 서버에서 AD FS 설치 폴더에서.</br> 
   
   ![모델](media/ad-fs-risk-assessment-model/risk4.png)
   
   c.   클릭 **확인** 에 **참조 관리자** 확인 한 후에 창 `Microsoft.IdentityServer.dll` 확인란을 선택</br>
   ![model](media/ad-fs-risk-assessment-model/risk5.png)
 
6. 모든 클래스 및 참조는 이제 빌드를 수행 하기.   단,이 프로젝트의 출력 dll 이므로 됩니다 하는 것에 설치할 수는 **전역 어셈블리 캐시**, 또는 AD FS 서버 dll을 GAC에 먼저 서명 해야 합니다. 이 다음과 같이 수행할 수 있습니다.

   a.   **마우스 오른쪽 단추로 클릭** ThreatDetectionModule 프로젝트의 이름입니다. 메뉴에서 클릭 **속성**합니다.</br>
   ![model](media/ad-fs-risk-assessment-model/risk6.png)
   
   b.   **속성** 페이지에서 **서명**, 왼쪽의 확인란을 표시 한 다음 확인 **어셈블리에 서명**. **강력한 이름 키 파일 선택**: 풀 다운 메뉴에서 **< 새로 만들기... >**</br>
   ![model](media/ad-fs-risk-assessment-model/risk7.png)

   c.   에 **강력한 이름 키 만들기 대화 상자**키에 대 한 (이름을 임의로 선택할 수 있습니다) 이름을 입력 하 고 확인란을 선택 취소 **암호로 내 키 파일 보호**합니다. 클릭 **확인**합니다.
   ![model](media/ad-fs-risk-assessment-model/risk8.png)</br>
 
   d.   아래와 같이 프로젝트를 저장 합니다.</br>
   ![model](media/ad-fs-risk-assessment-model/risk9.png)

7. 클릭 하 여 프로젝트를 빌드할 **빌드합니다** 차례로 **솔루션 다시 빌드** 아래와 같이</br>
   ![model](media/ad-fs-risk-assessment-model/risk10.png)
 
   확인 합니다 **출력 창**, 오류가 발생 하는 경우를 확인 하려면 화면 맨 아래에</br>
   ![model](media/ad-fs-risk-assessment-model/risk11.png)


플러그 인 (dll)를 사용할 준비가 이제 요소 이며 합니다 **\bin\Debug** 프로젝트 폴더의 폴더 (필자의 경우에는 **C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**). 

다음 단계는 ADFS 인증 프로세스에 따라 실행 되도록 AD FS를 사용 하 여이 dll을 등록 하는 것입니다. 

### <a name="register-the-plug-in-dll-with-ad-fs"></a>AD FS를 사용 하 여 플러그 인 dll을 등록 합니다.

그러나 AD FS에서 사용 하 여 dll을 등록 해야 합니다 `Register-AdfsThreatDetectionModule` AD FS 서버에서 PowerShell 명령을 등록 하기 전에 해야 공개 키 토큰을 가져옵니다. 키를 생성 하 고 해당 키를 사용 하 여 dll을 서명 하는 경우이 공개 키 토큰을 만들었습니다. 공개 키 토큰 dll에 대 한 소식 알아보기에 사용할 수 있습니다 합니다 **SN.exe** 같이

1. dll 파일을 복사 합니다 **\bin\Debug** 폴더를 다른 위치 (필자의 경우에 복사 **C:\extensions**)

2. 시작 합니다 **개발자 명령 프롬프트** Visual Studio에 들어 있는 디렉터리로 이동 합니다 **sn.exe** (여기서에서 디렉터리는 **C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A 4.7.2 \bin\NETFX 도구**) ![모델](media/ad-fs-risk-assessment-model/risk12.png)

3. 실행 합니다 **SN** 명령에 **-T** 매개 변수 및 파일의 위치 (여기서에서 `SN -T “C:\extensions\ThreatDetectionModule.dll”`) ![모델](media/ad-fs-risk-assessment-model/risk13.png)</br>
   명령이 공개 키 토큰을 제공 합니다 (중요 한, 합니다 **공개 키 토큰은 714697626ef96b35**)

4. Dll을 추가 합니다 **전역 어셈블리 캐시** AD FS 서버의 프로젝트에 대 한 적절 한 설치 관리자를 만든 파일을 GAC에 추가할 설치 관리자를 사용 하는 모범 사례 수는 있습니다. 다른 솔루션을 사용 하는 것 **Gacutil.exe** (대 한 자세한 내용은 **Gacutil.exe** 사용할 수 있습니다 [여기](https://docs.microsoft.com/dotnet/framework/tools/gacutil-exe-gac-tool)) 개발 컴퓨터에 있습니다.  사용할 AD FS와 동일한 서버에서 내 visual studio를 수 있기 때문 **Gacutil.exe** 같이

   a.   들어 있는 디렉터리로 이동 하 고 Visual Studio 용 개발자 명령 프롬프트에는 **Gacutil.exe** (여기서에서 디렉터리는 **C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**)

   b.   실행 합니다 **Gacutil** 명령 (여기서에서 `Gacutil /IF C:\extensions\ThreatDetectionModule.dll`) ![모델](media/ad-fs-risk-assessment-model/risk14.png)
 
   >[!NOTE]
   >위의 AD FS 팜이 있는 경우 팜의 각 AD FS 서버에서 실행 해야 합니다. 

5. 오픈 **Windows PowerShell** dll을 등록 하려면 다음 명령을 실행 합니다.
   ```
   Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>”
   ```
   여기서는 명령이입니다. 
   ```
   Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv”
   ```
 
   >[!NOTE]
   >AD FS 팜에 있는 경우에 dll을 한 번만 등록 해야 합니다. 

6. Dll을 등록 한 후 AD FS 서비스를 다시 시작

이것이, dll이 이제 AD FS 및 사용에 대 한 준비를 사용 하 여 등록 됩니다.

 >[!NOTE]
 > 플러그 인에 모든 변경 내용이 프로젝트를 다시 작성 하 고 경우에 업데이트 된 dll을 다시 등록 해야 합니다. 를 등록 하기 전에 다음 명령을 사용 하 여 현재 dll의 등록을 취소 해야 합니다.</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br> 여기서는 명령이입니다.
 >``` 
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>테스트 플러그 인

1. 열기는 **authconfig.csv** 이전에 만든 파일 (위치 여기서에서 **C:\extensions**) 추가 합니다 **엑스트라넷 Ip** 차단 하려는. 모든 IP 별도 줄에 있어야 하 고 끝에 공백이 있어야 합니다.</br>
   ![model](media/ad-fs-risk-assessment-model/risk18.png)
 
2. 파일을 닫고 저장

3. 다음 PowerShell 명령을 실행 하 여 AD FS에서 업데이트 된 파일 가져오기 

   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
   ```
 
   여기서는 명령이입니다. 
   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
   ```
 
4. 추가한 동일한 IP 사용 하 여 서버에서 시작 인증 요청 **authconfig.csv**합니다.

   이 데모를 보려면 사용 하겠습니다 [AD FS 도움말 클레임 x-레이 도구](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) 는 요청을 시작 합니다. 지침을 따르세요 x-레이 도구를 사용 하려는 경우 

   페더레이션 서버 인스턴스를 입력 하 고 적중 **인증 테스트** 단추입니다.</br> 
   ![모델](media/ad-fs-risk-assessment-model/risk15.png) 

5. 인증에는 아래와 같이 차단 됩니다.</br>
   ![model](media/ad-fs-risk-assessment-model/risk16.png)
 
빌드 플러그 인을 등록 하는 방법을 알았으므로 보겠습니다 연습 새로운 인터페이스 및 클래스를 사용 하 여 구현을 이해 하기 위한 플러그 인 코드 도입 모델. 

## <a name="plug-in-code-walkthrough"></a>플러그 인 코드 연습

프로젝트를 엽니다 `ThreatDetectionModule.sln` Visual Studio를 사용 하 고 주 파일을 엽니다 **UserRiskAnalyzer.cs** 에서 합니다 **솔루션 탐색기** 화면의 오른쪽</br>
![model](media/ad-fs-risk-assessment-model/risk17.png)
 
UserRiskAnalyzer 추상 클래스를 구현 하는 기본 클래스를 포함 하는 파일 [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) 및 인터페이스 [IRequestReceivedThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) 요청에서 IP를 읽을 수 컨텍스트를 AD FS DB에서 로드 된 Ip 사용 하 여 얻은 IP를 비교 하 고 IP와 일치 하는 경우 요청을 차단 합니다. 이러한 형식을 좀 더 자세히 검토해 보겠습니다.

### <a name="threatdetectionmodule-abstract-class"></a>ThreatDetectionModule 추상 클래스

AD FS 프로세스에 따라 플러그 인 코드를 실행할 수 있도록 하는 AD FS 파이프라인에 플러그 인 로드 하는이 추상 클래스입니다. 

```
public abstract class ThreatDetectionModule 
{ 
    protected ThreatDetectionModule(); 
 
    public abstract string VendorName { get; } 
    public abstract string ModuleIdentifier { get; } 
 
 public abstract void OnAuthenticationPipelineLoad(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData); 
 public abstract void OnAuthenticationPipelineUnload(ThreatDetectionLogger logger); 
  public abstract void OnConfigurationUpdate(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData); 
 }   
```
클래스는 다음 메서드 및 속성 포함 되어 있습니다.

|메서드 |형식|정의|
|-----|-----|-----| 
|[OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) |void|플러그 인이 해당 파이프라인에 로드 되 면 AD FS에서 호출| 
|[OnAuthenticationPipelineUnload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload?view=adfs-2019) |void|플러그 인 해당 파이프라인에서 로드 되지 경우 AD FS에서 호출| 
|[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)| void|AD FS 구성 업데이트 하 여 호출합니다. |
|**속성** |**형식** |**정의**|
|[VendorName](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname?view=adfs-2019)|문자열 |플러그 인을 소유한 공급 업체의 이름을 가져옵니다.|
|[ModuleIdentifier](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier?view=adfs-2019)|문자열 |플러그 인의 식별자를 가져옵니다.|

우리의 샘플 플러그 인에서 사용 하 여 [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) 하 고 [OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) AD FS DB에서 미리 정의 된 Ip를 읽을 수 있는 메서드입니다. [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) 하는 동안 AD FS를 사용 하 여 플러그 인이 등록 될 때 호출 됩니다 [OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) 사용 하 여.csv를 가져올 때 호출 되는 `Import-AdfsThreatDetectionModuleConfiguration` cmdlet. 

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>IRequestReceivedThreatDetectionModule 인터페이스

이렇게 [인터페이스](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) 되었으나 사용자 자격 증명을 입력 예: 인증 프로세스의 요청 받은 단계에서 AD FS 인증 요청을 수신 하는 경우 지점에서 위험 평가 구현할 수 있습니다. 
 
```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger, 
RequestContext requestContext );
}
```

인터페이스를 포함 [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) requestContext 입력 매개 변수의 위험 평가 논리를 작성 하면 인증 요청의 컨텍스트를 사용 하는 메서드에 전달 합니다. RequestContext 매개 변수는 형식 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)합니다. 

다른 입력된 매개 변수가 전달 되는 형식인로 거 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)합니다. 매개 변수를 사용 하 여 오류를 쓸 수 감사 및/또는 AD FS 로그에 메시지를 디버그 합니다. 

메서드는 반환 [ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (인 경우 0 NotEvaluated, 블록 1 및 허용 하는 2) AD FS에는 차단 또는 요청을 허용 합니다.

플러그 인 샘플 [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) 메서드 구현 구문 분석 합니다 [clientIpAddress](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses?view=adfs-2019#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses) 에서 합니다 [requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019) 매개 변수 모든 Ip와 비교 AD FS DB에서 로드 합니다. 일치 하는 항목이 없으면 반환에 대 한 2 **블록**, 그렇지 않으면 1을 반환 합니다 **허용**합니다. 반환된 된 값에 따라 AD FS를 차단 또는 요청을 허용 합니다. 

>[!NOTE]
>샘플 플러그 인 구현만 IRequestReceivedThreatDetectionModule 인터페이스 위에서 설명한 것입니다. 그러나 위험 평가 모델에서는 두 개의 추가 – IPreAuthenticationThreatDetectionModule (위험 평가 논리 중 사전 인증 단계를 구현)를 및 위험을 구현 하는 것 (하 IPostAuthenticationThreatDetectionModule 인터페이스 평가 논리 사후 인증 단계 중). 두 인터페이스에 대 한 세부 정보 아래에 나와 있습니다. 

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>IPreAuthenticationThreatDetectionModule 인터페이스 

이렇게 [인터페이스](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule?view=adfs-2019) 사용자 자격 증명을 제공 하는 경우 있지만 해당 AD FS 사전 인증, 즉 단계를 제공 하는 계산 전에 시점 위험 평가 논리를 구현할 수 있습니다. 

```
public interface IPreAuthenticationThreatDetectionModule
{
Task<ThrottleStatus> EvaluatePreAuthentication (
ThreatDetectionLogger logger, 
RequestContext requestContext, 
SecurityContext securityContext, 
ProtocolContext protocolContext, 
IList<Claim> additionalClams
);
}
```
인터페이스를 포함 [EvaluatePreAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication?view=adfs-2019) 전달 된 정보를 사용할 수 있는 메서드는 [RequestContext requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext securityContext ](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)하십시오 [ProtocolContext protocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019), 및 [IList<Claim> additionalClams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) 입력 매개 변수 사전 인증 위험 평가 논리를 작성 합니다. 

>[!NOTE]
>각 상황에 맞는 형식으로 전달 하는 속성 목록에 대 한 방문 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)를 [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), 및 [ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) 클래스 정의 합니다. 

다른 입력된 매개 변수가 전달 되는 형식인로 거 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)합니다. 매개 변수를 사용 하 여 오류를 쓸 수 감사 및/또는 AD FS 로그에 메시지를 디버그 합니다.

메서드는 반환 [ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (인 경우 0 NotEvaluated, 블록 1 및 허용 하는 2) AD FS에는 차단 또는 요청을 허용 합니다. 

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>IPostAuthenticationThreatDetectionModule 인터페이스

이렇게 [인터페이스](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule?view=adfs-2019) 사용자가 자격 증명을 제공 하 고 AD FS 인증, 즉 사후 인증 단계를 수행한 후 위험 평가 논리를 구현할 수 있습니다. 

```
public interface IPostAuthenticationThreatDetectionModule
{
Task<RiskScore> EvaluatePostAuthentication (
ThreatDetectionLogger logger, 
RequestContext requestContext, 
SecurityContext securityContext, 
ProtocolContext protocolContext, 
AuthenticationResult authenticationResult, 
IList<Claim> additionalClams
);
}
```

인터페이스를 포함 [EvaluatePostAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication?view=adfs-2019) 전달 된 정보를 사용할 수 있는 메서드는 [RequestContext requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext securityContext ](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)하십시오 [ProtocolContext protocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019), 및 [IList<Claim> additionalClams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) 입력 매개 변수 사후 인증 위험 평가 논리를 작성 합니다. 

>[!NOTE]
> 각 상황에 맞는 형식으로 전달 하는 속성의 전체 목록은 참조 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)를 [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), 및 [ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) 클래스 정의 합니다. 

다른 입력된 매개 변수가 전달 되는 형식인로 거 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)합니다. 매개 변수를 사용 하 여 오류를 쓸 수 감사 및/또는 AD FS 로그에 메시지를 디버그 합니다. 

메서드는 반환 된 [위험 점수](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants?view=adfs-2019) AD FS 정책에서 사용할 수 있으며 클레임 규칙입니다. 

>[!NOTE]
>에 대 한 플러그 인 작동 합니다 (이 경우 UserRiskAnalyzer)의 기본 클래스 파생 되어야 [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) 추상 클래스 및 위에서 설명한 세 가지 인터페이스 중 하나 이상 구현 해야 합니다. Dll 등록 되 면 AD FS 구현 된 인터페이스 검사 하 고 파이프라인의 적절 한 단계에서 호출.

### <a name="faqs"></a>FAQ

**이러한 플러그 인을 구축 해야 하는 이유**</br>
**A:** 이러한 플러그 인 뿐만 아니라 암호 스프레이 공격과 같은 공격 으로부터 환경을 보호 하려면 추가 기능을 제공 하지만 또한 요구 사항에 따라 고유한 위험 평가 논리를 작성 하는 데 유연성을 제공 합니다. 

**로그가 캡처됩니다.**</br>
**A:** WriteAdminLogErrorMessage 메서드를 사용 하 여 "AD FS/Admin" 이벤트 로그에 오류 로그를 쓸 수 있습니다, "AD FS 감사" 보안 감사 로그 WriteAuditMessage 메서드를 사용 하 여 로그 및 디버그 WriteDebugMessage 메서드를 사용 하 여 "AD FS 추적" 디버그 로그에 기록 합니다. 

**이러한 플러그 인 추가 AD FS 인증 프로세스 대기 시간 늘릴 수 있습니까?**</br>
**A:** 대기 시간이 영향 구현 하는 위험 평가 논리를 실행 하는 데 걸리는 시간에 의해 결정 됩니다. 프로덕션 환경에서 플러그 인을 배포 하기 전에 대기 시간 영향을 평가 하는 것이 좋습니다. 

**AD FS 없습니다 등 사용자가 위험한 Ip 목록을 제안 하는 이유**</br>
**A:** 현재 사용할 수 없습니다, 있지만 노력 하 고 제안 플러그형 위험 평가 모델에서 등 사용자가 위험한 Ip에 인텔리전스를 구축 합니다. 시작 날짜를 곧 공유 됩니다. 
