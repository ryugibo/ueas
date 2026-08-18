+++
title = "스크립팅 입문"
weight = 20
+++

# 스크립팅 입문

이 입문서에서는 스크립트로 첫 액터 클래스를 만들고 Unreal 및 블루프린트에서 상호작용하는 방법을 설명합니다.

## 준비

다음 항목이 준비되어 있는지 확인하세요.

- UnrealEngine-Angelscript용 커스텀 엔진 빌드를 설치하거나 컴파일합니다.
- [Visual Studio Code](https://code.visualstudio.com/)를 설치합니다.
- Visual Studio Code용 [Unreal Angelscript 확장 프로그램](https://marketplace.visualstudio.com/items?itemName=Hazelight.unreal-angelscript)을 설치합니다.

> 자세한 내용은 [설치](@/getting-started/installation.md) 페이지를 참고하세요.

## 프로젝트 시작

- 커스텀 Unreal Editor를 실행하고 프로젝트를 엽니다.
  프로젝트를 열면 프로젝트 폴더 안에 빈 `Script/` 폴더가 자동으로 생성됩니다.
- Visual Studio Code를 실행하고 `File -> Open Folder` 메뉴에서 새 `MyProject/Script/` 폴더를 엽니다.

> **팁:** Tools 메뉴에서 "Open Angelscript workspace" 옵션을 클릭하면 Visual Studio Code에서 스크립트 폴더를 자동으로 열 수도 있습니다.
> {{ img(path="open-workspace.png") }}

## 액터 클래스 생성

Visual Studio Code에서 `IntroductionActor.as`라는 새 파일을 만듭니다.

프로젝트의 `Script/` 폴더 아래에 있는 `.as` 확장자 파일은 Angelscript 플러그인이 자동으로 불러옵니다.

`IntroductionActor.as` 안에 새 액터 클래스를 선언해 보겠습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">AIntroductionActor</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

첫 스크립트 액터를 만들었습니다!

## Unreal에 액터 배치

스크립트 파일을 저장하면 즉시 Unreal Editor에서 사용할 수 있게 됩니다.

- `Place Actors` 패널을 엽니다. 열려 있지 않다면 Unreal의 `Window` 메뉴에서 찾을 수 있습니다.
- "Introduction Actor"를 검색합니다. 새 스크립트 액터가 목록에 나타납니다.
- "Introduction Actor"를 레벨에 배치합니다.

{{ img(path="place-actors.png") }}

## 액터에 기능 추가

이제 레벨에는 아무 기능도 없는 완전히 빈 액터가 있습니다.
예제로 이 액터가 설정 가능한 카운트다운을 수행하도록 만들어 보겠습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">AIntroductionActor</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">CountdownDuration</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">5.0</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">0.0</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">bool</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">false</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">BeginPlay</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Start the countdown on beginplay with the configured duration</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> = </span><span style="color: #9cdcfe;">CountdownDuration</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">true</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">Tick</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">DeltaSeconds</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #569cd6;">if</span><span style="color: #d4d4d4;"> (</span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Count down the timer </span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> -= </span><span style="color: #9cdcfe;">DeltaSeconds</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #569cd6;">if</span><span style="color: #d4d4d4;"> (</span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> &lt;= </span><span style="color: #b5cea8;">0.0</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// The countdown was complete!</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Print a message to the screen</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Countdown was completed!"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">false</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; }</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; }</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

여기서 일어나는 주요 동작은 다음과 같습니다.

- `CountdownDuration` 변수를 `UPROPERTY()`로 선언하여 Unreal Editor에서 설정할 수 있게 했습니다. 레벨에서 액터를 선택하고 카운트다운 시간을 기본값인 5초보다 길거나 짧게 변경할 수 있습니다.
  _[프로퍼티와 접근자](@/scripting/properties-and-accessors.md) 문서를 참고하세요._
  {{ img(path="countdown-duration.png") }}
- `BeginPlay`와 `Tick` 이벤트를 오버라이드하여 액터 기능을 구현합니다.
  _[함수와 BlueprintEvent](@/scripting/functions-and-events.md) 문서를 참고하세요._
- BeginPlay가 발생하면 카운트다운을 시작합니다.
- Tick이 발생하면 남은 시간을 줄이고 완료되었는지 확인합니다.
- 카운트다운이 끝나면 `Print()`로 화면에 메시지를 표시합니다.

이제 액터가 배치된 레벨을 플레이하고 5초를 기다리면 메시지가 표시됩니다.
{{ img(path="countdown-print.png") }}

## 액터에 컴포넌트 추가

현재 액터에는 아직 컴포넌트가 없고 Tick 기능만 구현되어 있습니다.

컴포넌트를 추가해 보겠습니다. `Scene Component`를 루트로 사용하고 여기에 `Static Mesh Component`와 `Billboard Component`를 연결합니다.

액터 코드 위쪽에 다음 내용을 추가합니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">AIntroductionActor</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">DefaultComponent</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">RootComponent</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">USceneComponent</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">SceneRoot</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">DefaultComponent</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">Attach</span><span style="color: #d4d4d4;"> = SceneRoot)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">UStaticMeshComponent</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Mesh</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">DefaultComponent</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">Attach</span><span style="color: #d4d4d4;"> = SceneRoot)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">UBillboardComponent</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Billboard</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">....</span></div></div>

스크립트 파일을 저장하면 레벨에 배치한 Introduction Actor에 새 컴포넌트가 나타납니다.

컴포넌트 추가에 관한 자세한 내용은 [액터와 컴포넌트](@/scripting/actors-components.md) 페이지를 참고하세요.

{{ img(path="intro-components.png") }}

> **팁:** 컴포넌트 메뉴의 _"Edit in C++"_ 링크를 클릭하면 Visual Studio Code에서 해당 컴포넌트를 추가한 스크립트 위치로 이동합니다.
> Angelscript 플러그인은 Unreal의 일반 C++ 기능과 연동하는 경우가 많아 스크립트 클래스도 여러 면에서 C++ 클래스처럼 동작합니다.

## 블루프린트 액터 생성

이제 액터에 Static Mesh Component가 있지만 스태틱 메시를 선택하지 않았기 때문에 보이지 않습니다.

레벨에서 액터를 선택해 메시를 지정할 수도 있지만, 배치하는 액터마다 이 작업을 반복하고 싶지는 않습니다.

대신 새 Introduction Actor의 블루프린트를 만들어 보겠습니다.

- 콘텐츠 브라우저를 열고 `Add -> Blueprint Class`를 클릭해 일반적인 방식으로 새 블루프린트를 만듭니다.
- 부모 클래스를 선택하라는 메시지가 나타나면 "Introduction Actor"를 검색해 선택합니다.
  {{ img(path="bp-pickparent.png") }}
- 액터 블루프린트임을 알 수 있도록 새 블루프린트 이름을 `BP_IntroductionActor`로 지정합니다.
- 새 블루프린트를 열고 Static Mesh Component의 메시를 선택합니다.
  여기서는 엔진의 표준 `SM_Cube` 메시를 선택하지만 원하는 메시를 사용해도 됩니다.
  {{ img(path="choose-staticmesh.png") }}
- 레벨에서 기존 `IntroductionActor`를 제거하고 새 `BP_IntroductionActor`를 배치해 보세요.

## 블루프린트 안팎으로 호출

이제 블루프린트가 있으므로 노드 그래프와 함께 작동하도록 스크립트를 변경할 수 있습니다.

- 카운트다운이 즉시 시작되지 않고 함수를 호출해야 시작되도록 액터를 변경합니다.
- 카운트다운이 끝났을 때 액터 블루프린트가 알림을 받도록 오버라이드 가능한 블루프린트 이벤트도 추가합니다.

`IntroductionActor.as`에서 BeginPlay 및 Tick 함수의 스크립트 코드를 다음과 같이 변경합니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">BeginPlay</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// We no longer start the countdown on BeginPlay automatically</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">StartCountdown</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Start the countdown when StartCountdown() is called </span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> = </span><span style="color: #9cdcfe;">CountdownDuration</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">true</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">/**</span></div><div><span style="color: #6a9955;">&#160; &#160; &#160;* Declare an overridable event so the actor blueprint can</span></div><div><span style="color: #6a9955;">&#160; &#160; &#160;* respond when the countdown finishes</span></div><div><span style="color: #6a9955;">&#160; &#160; &#160;*/</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintEvent</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">FinishedCountdown</span><span style="color: #d4d4d4;">() {}</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">Tick</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">DeltaSeconds</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #569cd6;">if</span><span style="color: #d4d4d4;"> (</span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Count down the timer </span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> -= </span><span style="color: #9cdcfe;">DeltaSeconds</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #569cd6;">if</span><span style="color: #d4d4d4;"> (</span><span style="color: #9cdcfe;">CurrentTimer</span><span style="color: #d4d4d4;"> &lt;= </span><span style="color: #b5cea8;">0.0</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// The countdown was complete!</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Print a message to the screen</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Countdown was completed!"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Also: trigger a blueprint event</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">FinishedCountdown</span><span style="color: #d4d4d4;">();</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; &#160; &#160; </span><span style="color: #9cdcfe;">bCountdownActive</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">false</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; &#160; &#160; }</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; }</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div></div>

변경 사항을 저장한 뒤 `BP_IntroductionActor`를 열어 다음과 같이 노드를 추가합니다.

{{ img(path="intro-bpnodes.png") }}

이제 블루프린트에서 카운트다운을 명시적으로 시작해야 하며, 카운트다운이 끝나면 블루프린트가 액터를 자동으로 제거합니다.

블루프린트를 배치한 레벨을 플레이하면 5초 후 액터가 사라지는 것을 볼 수 있습니다.

# 스크립트 예제

`UnrealEngine-Angelscript` 프로젝트에는 `Script-Examples/` 폴더가 있습니다.
여기에서 더 자세한 예제 스크립트를 읽거나 프로젝트로 복사할 수 있습니다.

- [Example_MovingObject.as](https://github.com/Hazelight/UnrealEngine-Angelscript/blob/angelscript-master/Script-Examples/Examples/Example_MovingObject.as) 액터 예제부터 살펴보는 것이 좋습니다.

- [GitHub의 Examples 폴더](https://github.com/Hazelight/UnrealEngine-Angelscript/tree/angelscript-master/Script-Examples/Examples)도 살펴볼 수 있습니다.

# 더 읽어보기

이 웹사이트 왼쪽 사이드바에서 더 많은 문서를 찾을 수 있습니다.

스크립트에서 할 수 있는 작업을 파악하려면 최소한 "스크립트 기능" 페이지를 읽어보는 것이 좋습니다.

다음 문서부터 시작해 보세요.

- [함수와 BlueprintEvent](@/scripting/functions-and-events.md)
- [함수 라이브러리](@/scripting/function-libraries.md)
- [Unreal C++과의 차이점](@/scripting/cpp-differences.md)
