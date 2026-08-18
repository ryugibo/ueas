+++
title = "서브시스템"
weight = 140
+++

# 서브시스템

서브시스템은 공통 기능을 접근하기 쉬운 싱글턴으로 모으는 Unreal의 방법 중 하나입니다.
자세한 내용은 [서브시스템 프로그래밍 Unreal 문서](https://docs.unrealengine.com/5.1/en-US/programming-subsystems-in-unreal-engine/)를 참고하세요.

## 서브시스템 사용

스크립트에서는 `USubsystemClass::Get()`을 사용해 서브시스템을 가져올 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">TestCreateNewLevel</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">auto</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">LevelEditorSubsystem</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">ULevelEditorSubsystem</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">Get</span><span style="color: #d4d4d4;">();</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">LevelEditorSubsystem</span><span style="color: #d4d4d4;">.</span><span style="color: #dcdcaa;">NewLevel</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"/Game/NewLevel"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

> **참고:** 많은 서브시스템은 _에디터 서브시스템_ 이므로 패키징된 게임에서 사용할 수 없습니다.
> 에디터 서브시스템은 반드시 [에디터 전용 스크립트](@/scripting/editor-script.md) 안에서만 사용하세요.

## 서브시스템 생성

스크립트에서 서브시스템을 만들 수 있도록 오버라이드 가능한 함수를 노출하는 헬퍼 부모 클래스가 제공됩니다.
다음 클래스를 상속할 수 있습니다.

- 월드 서브시스템: `UScriptWorldSubsystem`
- 게임 인스턴스 서브시스템: `UScriptGameInstanceSubsystem`
- 로컬 플레이어 서브시스템: `UScriptLocalPlayerSubsystem`
- 에디터 서브시스템: `UScriptEditorSubsystem`
- 엔진 서브시스템: `UScriptEngineSubsystem`

예를 들어 스크립트 월드 서브시스템은 다음과 같이 작성할 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">UMyGameWorldSubsystem</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">UScriptWorldSubsystem</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">Initialize</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"MyGame World Subsystem Initialized!"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">Tick</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">DeltaTime</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Tick"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Create functions on the subsystem to expose functionality</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">LookAtMyActor</span><span style="color: #d4d4d4;">(</span><span style="color: #4ec9b0;">AActor</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Actor</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><div><span style="color: #d4d4d4;">}</span></div><br><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">UseMyGameWorldSubsystem</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">auto</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">MySubsystem</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">UMyGameWorldSubsystem</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">Get</span><span style="color: #d4d4d4;">();</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">MySubsystem</span><span style="color: #d4d4d4;">.</span><span style="color: #dcdcaa;">LookAtMyActor</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">nullptr</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

선언한 모든 `UFUNCTION`은 서브시스템의 블루프린트에서도 접근할 수 있습니다.

{{ img(path="scripted-subsystem.png") }}

## 로컬 플레이어 서브시스템

로컬 플레이어 서브시스템에서는 서브시스템을 가져올 대상 `ULocalPlayer`를 `::Get()` 함수에 전달해야 합니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">UMyPlayerSubsystem</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">UScriptLocalPlayerSubsystem</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">}</span></div><br><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">UseScriptedPlayerSubsystem</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">ULocalPlayer</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">RelevantPlayer</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">Gameplay</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">GetPlayerController</span><span style="color: #d4d4d4;">(</span><span style="color: #b5cea8;">0</span><span style="color: #d4d4d4;">).</span><span style="color: #9cdcfe;">LocalPlayer</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">auto</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">MySubsystem</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">UMyPlayerSubsystem</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">Get</span><span style="color: #d4d4d4;">(</span><span style="color: #9cdcfe;">RelevantPlayer</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

> **참고:** 로컬 플레이어 서브시스템을 가져올 때 `APlayerController`를 직접 전달할 수도 있습니다.
