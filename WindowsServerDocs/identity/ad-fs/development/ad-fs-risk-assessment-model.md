---
title: AD FS 2019 위험 평가 모델을 사용 하 여 플러그 인 빌드
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: af7a565fb5b3745531497ed9119976418eb6dcd7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857526"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>AD FS 2019 위험 평가 모델을 사용 하 여 플러그 인 빌드

이제 다양 한 단계 (요청 수신, 사전 인증 및 사후 인증) 중에 인증 요청에 대 한 위험 점수를 차단 하거나 할당 하기 위해 고유한 플러그 인을 빌드할 수 있습니다. AD FS 2019에서 도입 된 새로운 위험 평가 모델을 사용 하 여이를 수행할 수 있습니다. 

## <a name="what-is-the-risk-assessment-model"></a>위험 평가 모델은 무엇 인가요?

위험 평가 모델은 개발자가 인증 요청 헤더를 읽고 자신의 위험 평가 논리를 구현 하는 데 사용할 수 있는 인터페이스 및 클래스 집합입니다. 그러면 구현 된 코드 (플러그 인)가 AD FS 인증 프로세스와 함께 실행 됩니다. 예를 들어 모델에 포함 된 인터페이스와 클래스를 사용 하 여 요청 헤더에 포함 된 클라이언트 IP 주소에 따라 인증 요청을 차단 하거나 허용 하는 코드를 구현할 수 있습니다. AD FS는 각 인증 요청에 대해 코드를 실행 하 고 구현 된 논리에 따라 적절 한 작업을 수행 합니다. 

이 모델은 아래와 같이 AD FS 인증 파이프라인의 3 단계 중 하나에서 플러그 인 코드를 사용할 수 있습니다.

![모델](media/ad-fs-risk-assessment-model/risk1.png)

1.    **수신 요청 단계** – AD FS 인증 요청을 받을 때 (예: 사용자가 자격 증명을 입력 하기 전에) 요청을 허용 하거나 차단할 플러그 인을 빌드할 수 있습니다. 이 단계에서 사용 가능한 요청 컨텍스트 (예: 클라이언트 IP, Http 메서드, 프록시 서버 DNS 등)를 사용 하 여 위험 평가를 수행할 수 있습니다. 예를 들어 요청 컨텍스트에서 IP를 읽을 플러그 인을 빌드하고 IP가 미리 정의 된 위험한 ip 목록에 있는 경우 인증 요청을 차단할 수 있습니다. 

2.    **사전 인증 단계** – 사용자가 자격 증명을 제공 하 고 AD FS 평가 하기 전에 요청을 허용 하거나 차단 하는 플러그 인을 빌드할 수 있습니다. 이 단계에서는 요청 컨텍스트 외에도 보안 컨텍스트 (예: 사용자 토큰, 사용자 id 등)와 프로토콜 컨텍스트 (예: 인증 프로토콜, clientid, resourceid 등)에 대 한 정보를 사용 하 여 위험 평가 논리에 사용할 수 있습니다. 예를 들어 사용자 토큰에서 사용자 암호를 읽고 암호가 미리 정의 된 위험한 암호 목록에 있는 경우 인증 요청을 차단 하 여 암호 스프레이 공격을 방지 하기 위해 플러그 인을 빌드할 수 있습니다. 

3.    **사후 인증** -사용자가 자격 증명 AD FS을 제공 하 고 인증을 수행한 후 위험을 평가 하기 위해 플러그 인을 빌드할 수 있습니다. 이 단계에서 요청 컨텍스트, 보안 컨텍스트 및 프로토콜 컨텍스트 외에도 인증 결과 (성공 또는 실패)에 대 한 정보가 있습니다. 플러그인은 사용 가능한 정보에 따라 위험 점수를 평가 하 고 추가 평가를 위해 위험 점수를 클레임 및 정책 규칙에 전달할 수 있습니다. 

위험 평가 플러그 인을 작성 하 고 AD FS 프로세스를 통해 실행 하는 방법을 더 잘 이해 하려면 위험한 것으로 식별 된 특정 **엑스트라넷** ip에서 들어오는 요청을 차단 하는 샘플 플러그 인을 만들어 AD FS에 플러그 인을 등록 하 고 마지막으로 기능을 테스트 합니다. 

>[!NOTE]
>이 연습은 샘플 플러그 인을 만드는 방법을 보여 주기 위한 것입니다. 아니요를 사용 하는 경우 솔루션이 준비 된 솔루션을 만드는 것입니다.  

## <a name="building-a-sample-plug-in"></a>샘플 플러그 인 빌드

### <a name="pre-requisites"></a>필수 구성 요소
이 샘플 플러그 인을 빌드하는 데 필요한 필수 구성 요소 목록은 다음과 같습니다.

- AD FS 2019 설치 및 구성 됨
- .NET Framework 4.7 이상
- Visual Studio

### <a name="build-plug-in-dll"></a>빌드 플러그 인 dll
다음 절차에서는 샘플 플러그 인 dll을 빌드하는 과정을 안내 합니다.

1. 샘플 플러그 인을 다운로드 하 고, Git Bash를 사용 하 고, 다음을 입력 합니다. 

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

2. AD FS 서버의 모든 위치에 **.csv** 파일을 만들고 (이 경우 **C:\ca 확장**에서 **authconfigdb .csv** 파일을 만듦)이 파일에 차단 하려는 ip를 추가 합니다. 

   샘플 플러그 인은이 파일에 나열 된 **엑스트라넷 ip** 에서 들어오는 모든 인증 요청을 차단 합니다. 

   >{! 참고] AD FS 팜이 있는 경우 또는 모든 AD FS 서버에 파일을 만들 수 있습니다. 모든 파일을 사용 하 여 위험한 Ip를 AD FS으로 가져올 수 있습니다. 위의 [AD FS에 플러그 인 Dll 등록](#register-the-plug-in-dll-with-ad-fs) 섹션에서 가져오기 프로세스를 자세히 설명 합니다. 

3. Visual Studio를 사용 하 여 프로젝트 `ThreatDetectionModule.sln` 열기

4. 아래와 같이 솔루션 탐색기에서 `Microsoft.IdentityServer.dll`을 제거 합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk2.png)

5. 아래와 같이 AD FS의 `Microsoft.IdentityServer.dll`에 대 한 참조를 추가 합니다.

   a.    **솔루션 탐색기** 에서 **참조** 를 마우스 오른쪽 단추로 클릭 하 고 **참조 추가** ...를 선택 합니다.</br> 
   ![모델](media/ad-fs-risk-assessment-model/risk3.png)
   
   b.    **참조 관리자** 창에서 **찾아보기**를 선택 합니다. **참조할 파일 선택** ... 대화 상자에서 `Microsoft.IdentityServer.dll`를 선택 하 AD FS 설치 폴더 (이 경우에는 **c:\kd**)에서를 선택 하 고 **추가**를 클릭 합니다.
   
   >[!NOTE]
   >이 경우 AD FS 서버 자체에서 플러그 인을 작성 합니다. 개발 환경이 다른 서버에 있는 경우 AD FS 서버의 AD FS 설치 폴더에 있는 `Microsoft.IdentityServer.dll`를 개발 상자에 복사 합니다.</br> 
   
   ![모델](media/ad-fs-risk-assessment-model/risk4.png)
   
   c.    `Microsoft.IdentityServer.dll` 확인란이 선택 되었는지 확인 한 후 **참조 관리자** 창에서 **확인을** 클릭 합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk5.png)
 
6. 이제 모든 클래스와 참조가 빌드를 수행 하기 위해 준비 되었습니다.   그러나이 프로젝트의 출력은 dll 이므로 AD FS 서버의 GAC ( **전역 어셈블리 캐시**)에 설치 해야 하 고 dll을 먼저 서명 해야 합니다. 다음과 같이이 작업을 수행할 수 있습니다.

   a.    ThreatDetectionModule 프로젝트의 이름을 **마우스 오른쪽 단추로 클릭** 합니다. 메뉴에서 **속성**을 클릭 합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk6.png)
   
   b.    **속성** 페이지의 왼쪽에서 **서명**을 클릭 한 다음 **어셈블리 서명**표시 확인란을 선택 합니다. **강력한 이름 키 파일 선택**: 풀 다운 메뉴에서 **< 새로 만들기 ...를 선택 합니다. >**</br>
   ![모델](media/ad-fs-risk-assessment-model/risk7.png)

   c.    **강력한 이름 키 만들기 대화 상자**에서 키의 이름을 입력할 수 있습니다. 확인란을 선택 취소 하 고 **암호를 사용 하 여 내 키 파일 보호**확인란의 선택을 취소 합니다. 그런 다음 **확인**을 클릭합니다.
   ![모델](media/ad-fs-risk-assessment-model/risk8.png)</br>
 
   .    아래와 같이 프로젝트를 저장 합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk9.png)

7. **빌드** 를 클릭 하 고 아래와 같이 **솔루션 다시** 빌드를 클릭 하 여 프로젝트를 빌드합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk10.png)
 
   화면 맨 아래에 있는 **출력 창을**확인 하 여 오류가 발생 했는지 확인 합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk11.png)


이제 플러그 인 (dll)을 사용할 준비가 되었으며 프로젝트 폴더의 **\bin\debug** 폴더 (이 경우에는 **C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**)에 있습니다. 

다음 단계는이 dll을 AD FS에 등록 하 여 AD FS 인증 프로세스의 줄에서 실행 되도록 하는 것입니다. 

### <a name="register-the-plug-in-dll-with-ad-fs"></a>AD FS를 사용 하 여 플러그 인 dll 등록

AD FS 서버에서 `Register-AdfsThreatDetectionModule` PowerShell 명령을 사용 하 여 AD FS에 dll을 등록 해야 하지만 등록 하기 전에 공개 키 토큰을 가져와야 합니다. 이 공개 키 토큰은 키를 만들고 해당 키를 사용 하 여 dll에 서명 했을 때 만들어졌습니다. Dll에 대 한 공개 키 토큰을 알아보려면 다음과 같이 Sn.exe를 사용할 수 있습니다 **.**

1. **\Bin\debug** 폴더의 dll 파일을 다른 위치로 복사 합니다 (이 경우 **c:\extensions**로 복사).

2. Visual Studio에 대 한 **개발자 명령 프롬프트** 를 시작 하 고 **sn.exe** 를 포함 하는 디렉터리로 이동 합니다 (이 경우 디렉터리가 **C:\Program files (X86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**) ![모델](media/ad-fs-risk-assessment-model/risk12.png)

3. **-T** 매개 변수 및 파일 위치 (이 경우 `SN -T "C:\extensions\ThreatDetectionModule.dll"`) ![모델을 사용 하 여 **SN** 명령을 실행](media/ad-fs-risk-assessment-model/risk13.png)</br>
   이 명령은 공개 키 토큰을 제공 합니다. **공개 키 토큰은 714697626ef96b35입니다**.

4. AD FS 서버의 **전역 어셈블리 캐시** 에 dll을 추가 하는 것이 가장 좋습니다. 가장 좋은 방법은 프로젝트에 대 한 적절 한 설치 관리자를 만들고 설치 관리자를 사용 하 여 GAC에 파일을 추가 하는 것입니다. 다른 솔루션은 개발 컴퓨터에서 **gacutil.exe** ( [여기](https://docs.microsoft.com/dotnet/framework/tools/gacutil-exe-gac-tool)에 제공 되는 **gacutil.exe** 에 대 한 자세한 정보)를 사용 하는 것입니다.  AD FS와 동일한 서버에 visual studio가 있으므로 다음과 같이 Gacutil.exe를 사용 합니다 **.**

   a.    Visual Studio 개발자 명령 프롬프트에서 Gacutil.exe를 포함 하는 디렉터리로 이동 합니다 (이 경우 디렉터리가 **C:\Program files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**) **.**

   b.    **Gacutil.exe** 명령 (내 사례 `Gacutil /IF C:\extensions\ThreatDetectionModule.dll`) ![모델을 실행](media/ad-fs-risk-assessment-model/risk14.png)
 
   >[!NOTE]
   >AD FS 팜이 있는 경우 팜에 있는 각 AD FS 서버에서 위의를 실행 해야 합니다. 

5. **Windows PowerShell** 을 열고 다음 명령을 실행 하 여 dll을 등록 합니다.
   ```
   Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>"
   ```
   이 경우 명령은 다음과 같습니다. 
   ```
   Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv"
   ```
 
   >[!NOTE]
   >AD FS 팜이 있는 경우에도 dll을 한 번만 등록 해야 합니다. 

6. Dll을 등록 한 후 AD FS 서비스를 다시 시작 합니다.

이제 dll이 AD FS에 등록 되어 사용할 준비가 되었습니다.

 >[!NOTE]
 > 플러그 인을 변경 하 고 프로젝트를 다시 작성 하면 업데이트 된 dll을 다시 등록 해야 합니다. 등록 하기 전에 다음 명령을 사용 하 여 현재 dll의 등록을 취소 해야 합니다.</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br> 이 경우 명령은 다음과 같습니다.
 >``` 
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>플러그 인 테스트

1. 이전에 만든 **authconfig** 파일 (여기서는 **c:\extensions**위치)을 열고 차단할 **엑스트라넷 ip** 를 추가 합니다. 모든 IP는 별도의 줄에 있어야 하며 끝에 공백이 없어야 합니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk18.png)
 
2. 파일을 저장하고 닫습니다.

3. 다음 PowerShell 명령을 실행 하 여 AD FS에서 업데이트 된 파일을 가져옵니다. 

   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
   ```
 
   이 경우 명령은 다음과 같습니다. 
   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
   ```
 
4. 인증 요청을 인증 하는 서버에서 동일한 IP를 사용 하 여 **authconfig**.

   이 데모에서는 요청을 시작 하는 [데 도움이 되는 AD FS 도움말 클레임 도구](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) 를 사용 합니다. X 광선 도구를 사용 하려면 다음 지침을 따르세요. 

   페더레이션 서버 인스턴스를 입력 하 고 **테스트 인증** 단추를 누릅니다.</br> 
   ![모델](media/ad-fs-risk-assessment-model/risk15.png) 

5. 인증은 아래와 같이 차단 됩니다.</br>
   ![모델](media/ad-fs-risk-assessment-model/risk16.png)
 
이제 플러그 인을 빌드 및 등록 하는 방법을 배웠으므로 모델에 도입 된 새 인터페이스 및 클래스를 사용 하 여 구현을 이해 하는 플러그 인 코드를 연습 하겠습니다. 

## <a name="plug-in-code-walkthrough"></a>플러그 인 코드 연습

Visual Studio를 사용 하 여 프로젝트 `ThreatDetectionModule.sln`를 열고 화면 오른쪽의 **솔루션 탐색기** 에서 주 파일 **UserRiskAnalyzer.cs** 을 엽니다.</br>
![모델](media/ad-fs-risk-assessment-model/risk17.png)
 
이 파일에는 추상 클래스 [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) 및 interface [IRequestReceivedThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) 를 구현 하는 주 클래스 UserRiskAnalyzer이 포함 되어 있습니다 .이 클래스는 요청 컨텍스트에서 ip를 읽고, 가져온 ip를 AD FS DB에서 로드 된 ip와 비교 하 고, IP가 일치 하는 경우 요청을 차단 합니다. 이러한 형식에 대해 자세히 살펴보겠습니다.

### <a name="threatdetectionmodule-abstract-class"></a>ThreatDetectionModule 추상 클래스

이 추상 클래스는 플러그 인을 AD FS 파이프라인으로 로드 하 여 AD FS 프로세스에서 플러그 인 코드를 실행할 수 있도록 합니다. 

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
클래스에는 다음 메서드와 속성이 포함 됩니다.

|메서드 |형식|정의|
|-----|-----|-----| 
|[OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) |Void|플러그 인이 해당 파이프라인으로 로드 될 때 AD FS에 의해 호출 됩니다.| 
|[OnAuthenticationPipelineUnload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload?view=adfs-2019) |Void|플러그 인이 파이프라인에서 언로드될 때 AD FS에 의해 호출 됩니다.| 
|[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)| Void|구성 업데이트 시 AD FS에 의해 호출 됩니다. |
|**속성** |**Type** |**정의**|
|[이름의](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname?view=adfs-2019)|String |플러그 인을 소유 하는 공급 업체의 이름을 가져옵니다.|
|[ModuleIdentifier](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier?view=adfs-2019)|String |플러그 인의 식별자를 가져옵니다.|

이 샘플 플러그인에서는 [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) 및 [onconfigurationupdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) 메서드를 사용 하 여 AD FS DB에서 미리 정의 된 ip를 읽습니다. [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) 는 AD FS에 플러그 인을 등록할 때 호출 되며, `Import-AdfsThreatDetectionModuleConfiguration` cmdlet을 사용 하 여 .csv를 가져올 때 [onconfigurationupdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) 가 호출 됩니다. 

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>IRequestReceivedThreatDetectionModule 인터페이스

이 [인터페이스](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) 를 사용 하면 AD FS 인증 요청을 수신 하 고 사용자가 자격 증명을 입력 하기 전에 (예: 인증 프로세스의 수신 요청 단계) 위험 평가를 구현할 수 있습니다. 
 
```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger, 
RequestContext requestContext );
}
```

인터페이스에는 requestContext 입력 매개 변수에 전달 되는 인증 요청의 컨텍스트를 사용 하 여 위험 평가 논리를 작성할 수 있는 [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) 메서드가 포함 되어 있습니다. RequestContext 매개 변수는 [requestcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)유형입니다. 

전달 된 다른 입력 매개 변수는 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)형식의로 거입니다. 매개 변수를 사용 하 여 오류, 감사 및/또는 디버그 메시지를 AD FS 로그에 쓸 수 있습니다. 

메서드는 [ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (0 인 경우 0을 반환 하 고, 1에서 Block로, 2를 허용 하는 경우)을 반환 하 여 요청을 차단 하거나 허용 하는 AD FS 합니다.

샘플 플러그 인에서 [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) 메서드 구현은 [requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019) 매개 변수에서 [clientIpAddress](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses?view=adfs-2019#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses) 를 구문 분석 하 고이를 AD FS DB에서 로드 된 모든 ip와 비교 합니다. 일치 항목이 발견 되 면 메서드는 **블록**에 대해 2를 반환 하 고, 다른 하나는 **허용**에 대해 1을 반환 합니다. 반환 된 값에 따라 요청을 차단 하거나 허용 하는 AD FS 합니다. 

>[!NOTE]
>위에서 설명한 샘플 플러그 인은 IRequestReceivedThreatDetectionModule 인터페이스만 구현 합니다. 그러나 위험 평가 모델은 IPreAuthenticationThreatDetectionModule (위험 평가 논리 중 사전 인증 단계를 구현 하기 위해) 및 IPostAuthenticationThreatDetectionModule (인증 후 단계에서 위험 평가 논리를 구현 하기 위해)의 두 가지 추가 인터페이스를 제공 합니다. 두 인터페이스에 대 한 세부 정보는 아래에 나와 있습니다. 

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>IPreAuthenticationThreatDetectionModule 인터페이스 

이 [인터페이스](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule?view=adfs-2019) 를 사용 하면 사용자가 자격 증명을 제공 하는 지점에서 위험 평가 논리를 구현할 수 있습니다. 즉, 사전 인증 단계를 AD FS 평가 합니다. 

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
인터페이스에는 [requestContext requestcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), [ProtocolContext ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)및 [IList<Claim> additionalclams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) 입력 매개 변수에 전달 된 정보를 사용 하 여 사전 인증 위험 평가 논리를 작성할 수 있는 [EvaluatePreAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication?view=adfs-2019) 메서드가 포함 되어 있습니다. 

>[!NOTE]
>각 컨텍스트 형식과 함께 전달 되는 속성 목록은 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)및 [ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) 클래스 정의를 참조 하세요. 

전달 된 다른 입력 매개 변수는 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)형식의로 거입니다. 매개 변수를 사용 하 여 오류, 감사 및/또는 디버그 메시지를 AD FS 로그에 쓸 수 있습니다.

메서드는 [ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (0 인 경우 0을 반환 하 고, 1에서 Block로, 2를 허용 하는 경우)을 반환 하 여 요청을 차단 하거나 허용 하는 AD FS 합니다. 

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>IPostAuthenticationThreatDetectionModule 인터페이스

이 [인터페이스](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule?view=adfs-2019) 를 사용 하면 사용자가 자격 증명을 제공 하 고 인증을 수행한 AD FS (예: 인증 후 단계) 위험 평가 논리를 구현할 수 있습니다. 

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

인터페이스에는 [requestContext requestcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), [ProtocolContext ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)및 [IList<Claim> additionalclams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) 입력 매개 변수에 전달 된 정보를 사용 하 여 인증 후 위험 평가 논리를 작성할 수 있도록 하는 [EvaluatePostAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication?view=adfs-2019) 메서드가 포함 되어 있습니다. 

>[!NOTE]
> 각 컨텍스트 형식과 함께 전달 되는 속성의 전체 목록은 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)및 [ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) 클래스 정의를 참조 하세요. 

전달 된 다른 입력 매개 변수는 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)형식의로 거입니다. 매개 변수를 사용 하 여 오류, 감사 및/또는 디버그 메시지를 AD FS 로그에 쓸 수 있습니다. 

메서드는 AD FS 정책 및 클레임 규칙에 사용할 수 있는 [위험 점수](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants?view=adfs-2019) 를 반환 합니다. 

>[!NOTE]
>플러그 인이 작동 하려면 주 클래스 (이 경우 UserRiskAnalyzer)가 [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) abstract 클래스를 파생 시켜야 하며 위에서 설명한 세 가지 인터페이스 중 하나 이상을 구현 해야 합니다. Dll이 등록 되 면 구현 된 인터페이스를 확인 하 고 파이프라인의 적절 한 단계에서 해당 인터페이스를 호출 AD FS 합니다.

### <a name="faqs"></a>FAQ

**이러한 플러그 인을 빌드하는 이유는 무엇 인가요?**</br>
**A:** 이러한 플러그 인은 암호 스프레이 공격과 같은 공격 으로부터 환경을 보호 하는 추가 기능을 제공할 뿐만 아니라 사용자의 요구 사항에 따라 고유한 위험 평가 논리를 유연 하 게 작성할 수 있는 기능도 제공 합니다. 

**로그가 캡처되는 위치는 어디 인가요?**</br>
**A:** WriteAdminLogErrorMessage 메서드를 사용 하 여 "AD FS/Admin" 이벤트 로그에 오류 로그를 작성 하 고, WriteAuditMessage 메서드를 사용 하 여 "AD FS 감사" 보안 로그에 대 한 감사 로그를 작성 하 고, WriteDebugMessage 메서드를 사용 하 여 디버그 로그를 "AD FS 추적" 

**이러한 플러그 인을 추가 하면 인증 프로세스 대기 시간 AD FS 증가 하나요?**</br>
**A:** 대기 시간 영향은 구현 하는 위험 평가 논리를 실행 하는 데 걸리는 시간에 따라 결정 됩니다. 프로덕션 환경에서 플러그 인을 배포 하기 전에 대기 시간 영향을 평가 하는 것이 좋습니다. 

**위험한 Ip, 사용자 등의 목록을 제안 AD FS 수 없는 이유는 무엇입니까?**</br>
**A:** 현재 사용할 수는 없지만 플러그형 위험 평가 모델에서 위험한 Ip, 사용자 등을 제안 하는 인텔리전스를 구축 하기 위해 노력 하 고 있습니다. 시작 날짜는 곧 공유 될 예정입니다. 
