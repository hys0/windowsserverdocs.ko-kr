---
title: Windows server에서 AD FS에 대 한 사용자 지정 인증 방법 구축
description: 이 시나리오에는 Windows server에서 AD FS에 대 한 사용자 지정 인증 방법 구축 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f28458ed9e781df6eca2478b02fb667d9240ca48
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445306"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Windows server에서 AD FS에 대 한 사용자 지정 인증 방법 구축

이 연습에서는 Windows Server 2012 R2에서 AD FS에 대 한 사용자 지정 인증 메서드를 구현 하는 것에 대 한 지침을 제공 합니다. 자세한 내용은 [추가 인증 방법](https://msdn.microsoft.com/en-us/library/dn758113\(v=msdn.10\))합니다.


> [!WARNING]
> 여기 빌드할 수 있는 예제는&nbsp;교육 목적에 대 한 합니다. &nbsp;이러한 지침은 모델의 필수 요소를 노출할 수 가장 간단 하 고 가장 최소한의 구현에 대 한 것입니다.&nbsp; 백 엔드 인증, 오류 처리 또는 구성 데이터가 필요 하지 않습니다. 
> <P></P>



## <a name="setting-up-the-development-box"></a>개발 상자를 설정합니다.

이 연습에서는 Visual Studio 2012를 사용합니다.  Windows에 대 한.NET 클래스를 만들 수 있는 모든 개발 환경을 사용 하 여 프로젝트를 빌드할 수 있습니다. 프로젝트 때문에.NET 4.5를 대상으로 해야 합니다는 **BeginAuthentication** 하 고 **TryEndAuthentication** 메서드 유형을 사용 하 여 **System.Security.Claims.Claim**.NET의 일부로, 프레임 워크 버전 4.5.There 하나의 참조를 프로젝트에 필요한 같습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>참조 dll</strong></p></td>
<td><p><strong>찾는 위치</strong></p></td>
<td><p><strong>에 필요한</strong></p></td>
</tr>
<tr class="even">
<td><p>Microsoft.IdentityServer.Web.dll</p></td>
<td><p>Dll은 AD FS를 설치한 Windows Server 2012 R2 서버의 %windir%\ADFS에 있습니다.</p>
<p></p>
<p>개발 컴퓨터에서 프로젝트에서 작성 하는 명시적 참조를이 dll은 복사 해야 합니다.</p></td>
<td><p>IAuthenticationContext, IProofData를 포함 하는 인터페이스 형식</p></td>
</tr>
</tbody>
</table>


## <a name="create-the-provider"></a>공급자 만들기

1.  In Visual Studio 2012: 선택 하 고 파일 기반\>New-\>프로젝트...

2.  클래스 라이브러리를 선택 하 고.NET 4.5를 대상으로 해야 합니다.

    ![공급자를 만듭니다](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "공급자 만들기")

3.  복사본을 만듭니다 **Microsoft.IdentityServer.Web.dll** %windir%에서\\ADFS에서 Windows Server 2012 R2 서버를 AD FS 설치가 완료 된 후 개발 컴퓨터에서 프로젝트 폴더에 붙여 넣습니다.

4.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **참조가** 및 **참조 추가...**

5.  로컬 복사본을 이동할 **Microsoft.IdentityServer.Web.dll** 고 **추가...**

6.  클릭 **확인** 새 참조를 확인 하려면:

    ![공급자를 만듭니다](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "공급자 만들기")

    이제 수 설정한 모든 공급자에 필요한 형식을 확인 하려면. 

7.  프로젝트에 새 클래스 추가 (프로젝트를 마우스 오른쪽 단추로 클릭 **추가.... 클래스...** )와 같은 이름을 지정 하 고 **MyAdapter**다음과 같이 합니다.

    ![공급자를 만듭니다](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "공급자 만들기")

8.  MyAdapter.cs 새 파일에서 기존 코드를 다음으로 바꿉니다.

        using System;
         using System.Collections.Generic;
         using System.Linq;
         using System.Text;
         using System.Threading.Tasks;
         using System.Globalization;
         using System.IO;
         using System.Net;
         using System.Xml.Serialization;
         using Microsoft.IdentityServer.Web.Authentication.External;
         using Claim = System.Security.Claims.Claim;

         namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {

         }
         }

    이제 F12를 수 있습니다 (마우스 오른쪽 단추로 클릭-정의로 이동)에서 필요한 인터페이스 멤버의 집합을 확인할 IAuthenticationAdapter 합니다. 

    다음으로, 다음의 간단한 구현을 수행할 수 있습니다.

9.  클래스의 전체 내용을 다음으로 바꿉니다.

        namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {
         public IAuthenticationAdapterMetadata Metadata
         {
         //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
         }

         public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
         {
         return true; //its all available for now

         }

         public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
         {
         //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

         }

         public void OnAuthenticationPipelineUnload()
         {

         }

         public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         }
         }

10. 아직 빌드할 준비가 되지... 두 가지 자세한 인터페이스가 이동 합니다.

    두 개의 추가 클래스인 프로젝트에 추가 합니다: 하나는 메타 데이터 및 프레젠테이션 폼에 대 한 다른 합니다.  위의 클래스와 동일한 파일 내에서이 추가할 수 있습니다.

        class MyMetadata : IAuthenticationAdapterMetadata
         {

         }

         class MyPresentationForm : IAdapterPresentationForm
         {

         }

11. 다음으로, 각각에 대 한 필수 멤버를 추가할 수 있습니다. 첫 번째, 메타 데이터 (유용한 인라인 주석 포함)

        class MyMetadata : IAuthenticationAdapterMetadata
         {
         //Returns the name of the provider that will be shown in the AD FS management UI (not visible to end users)
         public string AdminName
         {
         get { return "My Example MFA Adapter"; }
         }

         //Returns an array of strings containing URIs indicating the set of authentication methods implemented by the adapter 
         /// AD FS requires that, if authentication is successful, the method actually employed will be returned by the
         /// final call to TryEndAuthentication(). If no authentication method is returned, or the method returned is not
         /// one of the methods listed in this property, the authentication attempt will fail.
         public virtual string[] AuthenticationMethods 
         {
         get { return new[] { "http://example.com/myauthenticationmethod1", "http://example.com/myauthenticationmethod2" }; }
         }

         /// Returns an array indicating which languages are supported by the provider. AD FS uses this information
         /// to determine the best language\locale to display to the user.
         public int[] AvailableLcids
         {
         get
         {
         return new[] { new CultureInfo("en-us").LCID, new CultureInfo("fr").LCID};
         }
         }

         /// Returns a Dictionary containing the set of localized friendly names of the provider, indexed by lcid. 
         /// These Friendly Names are displayed in the "choice page" offered to the user when there is more than 
         /// one secondary authentication provider available.
         public Dictionary<int, string> FriendlyNames
         {
         get
         {
         Dictionary<int, string> _friendlyNames = new Dictionary<int, string>();
         _friendlyNames.Add(new CultureInfo("en-us").LCID, "Friendly name of My Example MFA Adapter for end users (en)");
         _friendlyNames.Add(new CultureInfo("fr").LCID, "Friendly name translated to fr locale");
         return _friendlyNames;
         }
         }

         /// Returns a Dictionary containing the set of localized descriptions (hover over help) of the provider, indexed by lcid. 
         /// These descriptions are displayed in the "choice page" offered to the user when there is more than one 
         /// secondary authentication provider available.
         public Dictionary<int, string> Descriptions
         {
         get 
         {
         Dictionary<int, string> _descriptions = new Dictionary<int, string>();
         _descriptions.Add(new CultureInfo("en-us").LCID, "Description of My Example MFA Adapter for end users (en)");
         _descriptions.Add(new CultureInfo("fr").LCID, "Description translated to fr locale");
         return _descriptions; 
         }
         }

         /// Returns an array indicating the type of claim that that the adapter uses to identify the user being authenticated.
         /// Note that although the property is an array, only the first element is currently used.
         /// MUST BE ONE OF THE FOLLOWING
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
         public string[] IdentityClaims
         {
         get { return new[] { "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" }; }
         }

         //All external providers must return a value of "true" for this property.
         public bool RequiresIdentity
         {
         get { return true; }
         }
        }

    다음, 표시 형식:

        class MyPresentationForm : IAdapterPresentationForm
         {
         /// Returns the HTML Form fragment that contains the adapter user interface. This data will be included in the web page that is presented
         /// to the cient.
         public string GetFormHtml(int lcid)
         {
         string htmlTemplate = Resources.FormPageHtml; //todo we will implement this
         return htmlTemplate;
         }

         /// Return any external resources, ie references to libraries etc., that should be included in 
         /// the HEAD section of the presentation form html. 
         public string GetFormPreRenderHtml(int lcid)
         {
         return null;
         }

         //returns the title string for the web page which presents the HTML form content to the end user
         public string GetPageTitle(int lcid)
         {
         return "MFA Adapter";
         }


~~~
     }
~~~

12. '일'에 대 한 참고 합니다 **Resources.FormPageHtml** 위의 요소입니다. 

   수정할 수 있습니다 분 있지만 첫 번째 보겠습니다 초기 MyAdapter 클래스에는 새롭게 구현된 된 형식을 기반으로 최종 필요한 반환 명령문을 추가 합니다.  이렇게 하려면 항목을 추가 *기울임꼴* 아래 기존 IAuthenticationAdapter 구현에:

       MyAdapter 클래스: IAuthenticationAdapter     {     public IAuthenticationAdapterMetadata Metadata     {     //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }     get { return new MyMetadata(); }     }

        public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
        {
        //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
        }

        public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
        {
        return true; //its all available for now
        }

        public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
        {
        //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

        }

        public void OnAuthenticationPipelineUnload()
        {

        }

        public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
        {
        //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
        }

        public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
        {
        //return new instance of IAdapterPresentationForm derived class
        outgoingClaims = new Claim[0];
        return new MyPresentationForm();
        }

        }

13. 리소스 파일에 포함 된 html 조각입니다. 다음 콘텐츠를 사용 하 여 프로젝트 폴더에 새 텍스트 파일을 만듭니다.

       <div id="loginArea">
        <form method="post" id="loginForm" >
        <!-- These inputs are required by the presentation framework. Do not modify or remove -->
        <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
        <input id="context" type="hidden" name="Context" value="%Context%"/>
        <!-- End inputs are required by the presentation framework. -->
        <p id="pageIntroductionText">이 콘텐츠는 MFA 샘플 어댑터에 의해 제공 됩니다. 질문 입력 아래 표시 됩니다.</p>
        <label for="challengeQuestionInput" class="block">질문 텍스트</label>
        <input id="challengeQuestionInput" name="ChallengeQuestionAnswer" type="text" value="" class="text" placeholder="Answer placeholder" />
        <div id="submissionArea" class="submitMargin">
        <input id="submitButton" type="submit" name="Submit" value="Submit" onclick="return AuthPage.submitAnswer()"/>
        </div>
        </form>
        <div id="intro" class="groupMargin">
        <p id="supportEmail">지원 정보</p>
        </div>
        <script type="text/javascript" language="JavaScript">
        //<![CDATA[
        function AuthPage() { }
        AuthPage.submitAnswer = function () { return true; };
        //]]>
        </script></div>

14. 그런 다음 선택 **프로젝트-\>구성 요소를 추가 하는 중... 리소스** 파일 및 파일 이름을 **리소스**를 클릭 하 고 **추가:**

   ![공급자를 만듭니다](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "공급자 만들기")

15. 그런 다음 내에서 **Resources.resx** 파일을 선택 **추가 리소스... 기존 파일 추가**합니다.  텍스트 파일로 이동 (html 조각을 포함) 위에 저장 합니다.

   GetFormHtml 코드 새 리소스의 이름을 올바르게 확인 리소스 자체의 이름 뒤에 리소스 파일 (.resx) 이름 접두사로 확인 합니다.

       public string GetFormHtml(int lcid)    {     string htmlTemplate = Resources.MfaFormHtml; //Resxfilename.resourcename     return htmlTemplate;    }

   이제 빌드에 있어야 합니다.

## <a name="build-the-adapter"></a>어댑터를 작성 합니다.

어댑터는 Windows에서 GAC에 설치할 수 있는 강력한 이름이 지정 된.NET 어셈블리에 빌드해야 합니다.  Visual Studio 프로젝트에서 이렇게 하려면 다음 단계를 수행 합니다.

1.  솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.

2.  에 **서명** 탭 **어셈블리에 서명할** 선택한 **\<새로 만들기... \>** 아래에서 **강력한 이름 키 파일 선택:**  키 파일 이름 및 암호를 입력 하 고 클릭 **확인**합니다.  그런 다음 **어셈블리 서명** 확인란이 선택 되어 및 **서명만 연기** 선택 하지 않으면.  속성을 **서명** 페이지는 다음과 같습니다.

    ![공급자 빌드](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "공급자 빌드")

3.  그런 다음 솔루션을 빌드하십시오.

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>AD FS 테스트 컴퓨터에 어댑터 배포

AD FS에서 외부 공급자를 호출할 수 있습니다, 전에 시스템에 등록 되어야 합니다.  어댑터 공급자는 GAC에 설치를 포함 하는 데 필요한 설치 작업을 수행 하는 설치 관리자를 제공 해야 하 고 설치 관리자는 AD FS에서 등록을 지원 해야 합니다.  그렇지 않은 경우 관리자는 아래 Windows PowerShell 단계를 실행 해야 합니다.  이러한 단계 테스트 및 디버깅을 사용 하도록 설정 하려면 랩에서 사용할 수 있습니다.

### <a name="prepare-the-test-ad-fs-machine"></a>AD FS 테스트 컴퓨터 준비

파일을 복사 하 고 GAC에 추가 합니다.

1.  Windows Server 2012 R2 컴퓨터 또는 가상 컴퓨터를 확인 합니다.

2.  AD FS 역할 서비스를 설치 하 고 하나 이상의 노드를 사용 하 여 팜을 구성 합니다.

    랩 환경에서 페더레이션 서버를 설치 하는 자세한 단계에 대해서는 [Windows Server 2012 R2 AD FS 배포 가이드](https://msdn.microsoft.com/en-us/library/dn486820\(v=msdn.10\))합니다.

3.  서버에 Gacutil.exe 도구를 복사 합니다.

    Gacutil.exe는에서 확인할 수 있습니다 **%homedrive%\\프로그램 파일 (x86)\\Microsoft SDKs\\Windows\\v8.0A\\bin\\NETFX 4.0 도구\\** Windows 8 컴퓨터에서.  해야 합니다 **gacutil.exe** 파일 자체 뿐만 **1033**를 **EN-US**, 및 기타 지역화 된 리소스 아래에 폴더를 **NETFX 4.0 도구** 위치입니다.

4.  공급자 파일을 복사 (하나 이상의 강력한 이름 서명 된.dll 파일)와 같은 폴더 위치로 **gacutil.exe** (위치는 단지 편의 위한)

5.  Gac에 팜의 각 AD FS 페더레이션 서버에.dll 파일을 추가 합니다.

    예: 명령줄 도구 GACutil.exe를 사용 하 여 dll을 GAC에 추가 하려면: `C:\>.\gacutil.exe /if .\<yourdllname>.dll`

    GAC에서 결과 항목을 보려면:`C:\>.\gacutil.exe /l <yourassemblyname>`

6.  

### <a name="register-your-provider-in-ad-fs"></a>AD FS에서 공급자 등록

위의 필수 조건을 충족 되 면 페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 입력 합니다 (Windows 내부 데이터베이스를 사용 하는 페더레이션 서버 팜을 사용 하는 경우 있습니다 해야 실행할 이러한 명령에는 기본 페더레이션 서버 팜의):

1.  `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    여기서 YourTypeName은.NET 강력한 형식 이름: "YourDefaultNamespace.YourIAuthenticationAdapterImplementationClassName, 이름, 버전 YourAssemblyVersion, Culture = neutral, PublicKeyToken = = YourPublicKeyTokenValue, processorArchitecture = MSIL"

    그러면 위의 AnyNameYouWish로 제공한 이름 사용 하 여 AD FS에서 외부 공급자가 등록 됩니다.

2.  (사용 하 여 Windows 서비스 스냅인 예를 들어) AD FS 서비스를 다시 시작 합니다.

3.  다음 명령을 실행: `Get-AdfsAuthenticationProvider`합니다.

    이 공급자에 게 시스템에서 공급자 중으로 표시합니다.

    예:

        PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
        PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
        PS C:\>net stop adfssrv
        PS C:\>net start adfssrv

    장치 등록 서비스를 AD FS 환경의 사용할 경우 다음 실행할 수도 있습니다.  `PS C:\>net start drs`

    등록 된 공급자를 확인 하려면 다음 명령을 사용 하 여:`PS C:\>Get-AdfsAuthenticationProvider`합니다.

    이 공급자에 게 시스템에서 공급자 중으로 표시합니다.

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>어댑터를 호출 하는 AD FS 인증 정책 만들기

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 관리 스냅인을 사용 하 여 인증 정책 만들기

1.  AD FS 관리 스냅인을 엽니다 (서버 관리자에서 **도구** 메뉴).

2.  클릭 **인증 정책**합니다.

3.  가운데 창에서 아래 **Multi-factor Authentication**를 클릭 합니다 **편집** 오른쪽의 링크를 **전역 설정**합니다.

4.  아래 **추가 인증 방법을 선택** 페이지의 맨 아래에 해당 공급자의 AdminName에 대 한 상자를 선택 합니다. **적용**을 클릭합니다.

5.  "트리거" 아래에서 해당 어댑터를 사용 하 여 MFA를 호출할 수 있도록 **위치** 모두 선택 **엑스트라넷** 하 고 **인트라넷**예를 들어 있습니다. **확인**을 클릭합니다. (트리거를 구성 하려면 신뢰 당사자 별 파티, 아래 "Windows PowerShell을 사용 하 여 인증 정책 만들기"를 참조 하세요.)

6.  다음 명령을 사용 하 여 결과 확인 합니다.

    먼저 사용 하 여 `Get-AdfsGlobalAuthenticationPolicy`입니다. 공급자 이름 AdditionalAuthenticationProvider 값 중 하나로 표시 됩니다.

    사용 하 여 `Get-AdfsAdditionalAuthenticationRule`입니다. 엑스트라넷 및 인트라넷 관리자 UI의에서 정책 선택의 결과로 구성에 대 한 규칙이 표시 됩니다.

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 인증 정책 만들기

1.  먼저, 글로벌 정책에서 공급자를 사용 하도록 설정:

    `PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`


~~~
> [!NOTE]
> Note that the value provided for the AdditionalAuthenticationProvider parameter corresponds to the value you provided for the “Name” parameter in the Register-AdfsAuthenticationProvider cmdlet above and to the “Name” property from Get-AdfsAuthenticationProvider cmdlet output. 
> <P></P>


Example:`PS C:\>Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
~~~

2. 다음을 트리거하고 MFA 전역 또는 신뢰 당사자-특정 규칙을 구성 합니다.

   예제 1: 외부 요청에 대 한 MFA를 요구 하는 전역 규칙을 만듭니다.`PS C:\>Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'`

   예제 2: MFA를 만들려면 특정 신뢰에 대 한 외부 요청에 대 한 MFA를 요구 하는 규칙 당사자입니다.  (Note: Windows Server 2012 R2의 AD FS에서 개별 신뢰 당사자에 개별 공급자를 연결할 수 없음).

       PS C:\>$rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
       PS C:\>Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'

### <a name="authenticate-with-mfa-using-your-adapter"></a>어댑터를 사용 하 여 MFA를 사용 하 여 인증

마지막으로 어댑터를 테스트 하려면 다음 단계를 수행 합니다.

1.  엑스트라넷 및 인트라넷 (이 쉽게 데모 하는 특정 사용자로 인증)에 대 한 AD FS 전역 기본 인증 유형을 폼 인증으로 구성 되어 있는지 확인

    1.  AD FS에서 스냅인을 **인증 정책**를 **기본 인증** 영역에서 클릭 **편집** 옆에 **전역 설정**.

        1.  클릭 또는 **주** 에서 탭의 **다단계 인증 정책을** UI.

2.  확인 **폼 인증** 는 엑스트라넷 및 인트라넷 인증 방법에 대 한 옵션만 선택 됩니다.  **확인**을 클릭합니다.

3.  IDP 시작 로그온 html 페이지 열기 (https://\<fsname\>/adfs/ls/idpinitiatedsignon.htm) 및 테스트 환경에서 유효한 AD 사용자로 로그인 합니다.

4.  기본 인증에 대 한 자격 증명을 입력 합니다.

5.  예에서는 챌린지 질문을 사용 하 여 페이지가 표시 MFA 폼이 표시 됩니다. 

    구성 된 어댑터가 둘 이상인 경우 MFA 선택 페이지를 위쪽에서 친숙 한 이름으로 나타납니다.

    ![어댑터를 사용 하 여 인증](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "어댑터를 사용 하 여 인증")

    ![어댑터를 사용 하 여 인증](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "어댑터를 사용 하 여 인증")

이제 인터페이스의 실제 구현이 있고 모델의 작동 방식에 대 한 지식을 합니다. TryEndAuthentication 뿐만 아니라는 BeginAuthentication 중단점을 설정 하는 추가 예제로 trym 할 수 있습니다.  BeginAuthentication 실행 되는 방식을 사용자 MFA 폼에 먼저 들어가면 TryEndAuthentication 폼의 각 전송에서 트리거되지만 알 수 있습니다.

## <a name="update-the-adapter-for-successful-authentication"></a>성공적인 인증을 위해 어댑터 업데이트

대기 – 예제 어댑터 인증이 실패 하지만\!  이 코드의 경우 nothing TryEndAuthentication에 대 한 null 반환 합니다.

위의 절차를 완료 하 여 기본 어댑터 구현을 생성 하 고 AD FS 서버에 추가 합니다.  MFA forms 페이지를 가져올 수는 있지만 아직 올바른 논리 TryEndAuthentication 구현에서 아직 두지가 없어를 인증할 수 없습니다.  추가 해 보겠습니다.

TryEndAuthentication 구현을 회수 합니다.

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     //return new instance of IAdapterPresentationForm derived class
     outgoingClaims = new Claim[0];
     return new MyPresentationForm();

     }

보겠습니다 있도록 업데이트 메서드 MyPresentationForm() 항상 반환 하지 않습니다.  이 클래스 내에서 하나의 간단한 유틸리티 메서드를 만들 수 있습니다.

    static bool ValidateProofData(IProofData proofData, IAuthenticationContext authContext)
     {
     if (proofData == null || proofData.Properties == null || !proofData.Properties.ContainsKey("ChallengeQuestionAnswer"))
     {
     throw new ExternalAuthenticationException("Error - no answer found", authContext);
     }

     if ((string)proofData.Properties["ChallengeQuestionAnswer"] == "adfabric")
     {
     return true;
     }
     else
     {
     return false;
     }
     }

그런 다음 아래와 같이 TryEndAuthentication를 업데이트 합니다.

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     outgoingClaims = new Claim[0];
     if (ValidateProofData(proofData, authContext))
     {
     //authn complete - return authn method
     outgoingClaims = new[] 
     {
     // Return the required authentication method claim, indicating the particulate authentication method used.
     new Claim( "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", 
     "http://example.com/myauthenticationmethod1" )
     };
     return null;
     }
     else
     {
     //authentication not complete - return new instance of IAdapterPresentationForm derived class
     return new MyPresentationForm();
     }
     }

이제 테스트 상자에서 어댑터를 업데이트 해야 합니다.  먼저 다음 등록을 취소 AD FS에서 AD FS 정책 실행 취소 및 AD FS를 다시 시작 후.dll GAC에서 제거 다음 GAC에 새.dll을 추가 다음 AD FS에서 등록, AD FS를 다시 시작 하 고 AD FS 정책을 다시 구성 합니다.

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>배포 및 테스트 AD FS 컴퓨터에 업데이트 된 어댑터를 구성 합니다.

### <a name="clear-ad-fs-policy"></a>AD FS 정책 지우기

지우기 모든 MFA 확인란 아래에 나와 있는 MFA ui와 관련 된 다음 확인을 클릭 합니다.

![정책 지우기](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "정책 지우기")

### <a name="unregister-provider-windows-powershell"></a>(Windows PowerShell) 공급자를 등록 취소

`PS C:\> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

예:`PS C:\> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

Note 등록 AdfsAuthenticationProvider cmdlet에 제공 "Name"은 "Name"와 같은 값을 전달 하는 값입니다.  Get-AdfsAuthenticationProvider에서 출력 되는 "Name" 속성 이기도 합니다.

공급자 등록을 취소 하면 전에 제거 해야 한다는 공급자 (또는 AD FS 관리 스냅인에서 선택한 확인란 선택을 취소 하 여 Windows PowerShell을 사용 하 여.) AdfsGlobalAuthenticationPolicy에서 note

이 작업 후 AD FS 서비스를 다시 시작 해야 있는지 note 합니다.

### <a name="remove-assembly-from-gac"></a>GAC에서 어셈블리 제거

1.  먼저 다음 명령을 사용 하 여 항목의 정규화 된 강력한 이름을 찾으려면:`C:\>.\gacutil.exe /l <yourAdapterAssemblyName>`

    예:`C:\>.\gacutil.exe /l mfaadapter`

2.  그런 다음 명령을 사용 하 여 다음 GAC에서 제거 합니다.`.\gacutil /u “<output from the above command>”`

    예:`C:\>.\gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>업데이트 된 어셈블리를 GAC에 추가

먼저 로컬로 업데이트 된.dll을 붙여 넣으면 있는지 확인 합니다. `C:\>.\gacutil.exe /if .\MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>(명령줄) GAC에 어셈블리 보기

`C:\> .\gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>AD FS에서 공급자 등록

1.  `PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2.  `PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3.  AD FS 서비스를 다시 시작 합니다.

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 관리 스냅인을 사용 하 여 인증 정책 만들기

1.  AD FS 관리 스냅인을 엽니다 (서버 관리자에서 **도구** 메뉴).

2.  클릭 **인증 정책**합니다.

3.  아래 **Multi-factor Authentication**를 클릭 합니다 **편집** 오른쪽의 링크를 **전역 설정**합니다.

4.  아래 **추가 인증 방법을 선택**, 공급자의 AdminName에 대 한 상자를 선택 합니다. **적용**을 클릭합니다.

5.  MFA 어댑터를 사용 하 여 호출 하는 "트리거"를 제공 하려면 위치에서 모두 선택 **엑스트라넷** 하 고 **인트라넷**예를 들어 있습니다. **확인**을 클릭합니다.

### <a name="authenticate-with-mfa-using-your-adapter"></a>어댑터를 사용 하 여 MFA를 사용 하 여 인증

마지막으로 어댑터를 테스트 하려면 다음 단계를 수행 합니다.

1.  AD FS 전역 기본 인증 유형으로 구성 되었는지 확인 하십시오 **폼 인증** 엑스트라넷 및 인트라넷 (이렇게 하면 쉽게 특정 사용자로 인증)에 대 한 합니다.

    1.  AD FS 관리에서 스냅인에서 **인증 정책**를 **기본 인증** 영역 클릭 **편집** 옆에 **전역설정**.

        1.  클릭 또는 합니다 **기본** 다단계 인증 정책 UI에서에서 탭 합니다.

2.  확인 **폼 인증** 옵션만 확인란이 둘 다에 대해 합니다 **엑스트라넷** 하며 **인트라넷** 인증 방법.  **확인**을 클릭합니다.

3.  IDP 시작 로그온 html 페이지 열기 (https://\<fsname\>/adfs/ls/idpinitiatedsignon.htm) 및 테스트 환경에서 유효한 AD 사용자로 로그인 합니다.

4.  기본 인증 자격 증명을 입력 합니다.

5.  예제 문제 텍스트를 사용 하 여 페이지가 표시 MFA 폼이 표시 됩니다.

    1.  구성 된 어댑터가 둘 이상인 경우 MFA 선택 페이지에 친숙 한 이름으로 나타납니다.

MFA 인증 페이지에서 "adfabric"를 입력 하는 경우 성공적인 로그인에 표시 됩니다.

![어댑터로 로그인](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "어댑터로 로그인")

![어댑터로 로그인](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "어댑터로 로그인")

## <a name="see-also"></a>관련 항목

#### <a name="other-resources"></a>관련 자료

[추가 인증 방법](https://msdn.microsoft.com/en-us/library/dn758113\(v=msdn.10\))  
[추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](https://msdn.microsoft.com/en-us/library/dn280949\(v=msdn.10\))

