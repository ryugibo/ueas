+++
title = "Unreal C++과의 차이점"
weight = 300
sort_by = "weight"
+++

# Unreal C++ 개발자를 위한 차이점 개요
Unreal C++에 익숙한 개발자라면 스크립트 파일이 친숙하게 느껴지겠지만 여러 차이점이 있습니다.
대부분의 차이는 블루프린트 사용자가 쉽게 접근할 수 있도록 스크립트 언어를 단순화하기 위한 것입니다.

흔히 마주칠 만한 차이점을 여기에서 설명합니다.

## 포인터 대신 객체
`UObject` 타입으로 선언한 변수는 자동으로 객체 참조가 됩니다. 스크립트 언어에는 포인터가 없습니다.
이는 블루프린트의 객체 참조 변수와 비슷합니다.
스크립트에는 `->` 화살표 연산자가 없으며 모든 접근에 `.`을 사용합니다.

> **참고:** C++과 달리 프로퍼티가 가비지 컬렉션되는 것을 막기 위해 `UPROPERTY()`로 선언할 필요가 **없습니다**. 스크립트의 모든 객체 참조는 GC에 자동으로 추가됩니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">TeleportActorToOtherActor</span><span style="color: #d4d4d4;">(</span><span style="color: #4ec9b0;">AActor</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ActorReference</span><span style="color: #d4d4d4;">, </span><span style="color: #4ec9b0;">AActor</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">TeleportToActor</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">FTransform</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">TeleportToTransform</span><span style="color: #d4d4d4;"> = </span><span style="color: #9cdcfe;">TeleportToActor</span><span style="color: #d4d4d4;">.</span><span style="color: #dcdcaa;">GetActorTransform</span><span style="color: #d4d4d4;">();</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">ActorReference</span><span style="color: #d4d4d4;">.</span><span style="color: #dcdcaa;">SetActorTransform</span><span style="color: #d4d4d4;">(</span><span style="color: #9cdcfe;">TeleportToTransform</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

## 프로퍼티의 기본 접근성
`UPROPERTY()` 변수에는 기본적으로 `EditAnywhere`와 `BlueprintReadWrite`가 적용됩니다. `NotBlueprintCallable` 또는 `NotEditable`을 지정해 이 동작을 변경할 수 있습니다.

스크립트 프로퍼티의 기본 접근 지정자는 프로젝트 설정에서 구성할 수 있습니다.

이는 프로퍼티 지정자를 단순화하기 위한 것입니다. 올바른 가비지 컬렉션에 `UPROPERTY()`가 필요하지 않으므로 에디터나 블루프린트에서 접근해야 할 때만 지정하세요.

## 함수의 기본 호출 가능 여부
`UFUNCTION()`으로 선언한 함수에는 명시하지 않아도 기본적으로 `BlueprintCallable`이 적용됩니다.
스크립트 함수를 `UFUNCTION()`으로 만드는 것 자체가 일반적으로 블루프린트에서 호출하려는 의도를 나타내므로 함수 선언을 단순화하기 위한 동작입니다.

`BlueprintCallable`을 명시하도록 강제하려면 프로젝트 설정에서 이 동작을 끌 수 있습니다.

## 생성자 대신 `default` 키워드 사용
핫 리로드 중 예측하기 어려운 시점에 실행될 수 있는 객체 생성자 대신, 프로퍼티의 모든 기본값을 클래스 본문에서 지정해야 합니다.

하위 객체의 값을 설정하려면 `default` 키워드를 사용합니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">AExampleActor</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Set default values for class properties in the class body</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ConfigurableValue</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">5.0</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Set default values for subobjects with `default` statements</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">DefaultComponent</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">UCapsuleComponent</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">CapsuleComponent</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">default</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">CapsuleComponent</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">CapsuleHalfHeight</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">88.0</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">default</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">CapsuleComponent</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">CapsuleRadius</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">40.0</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">default</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">CapsuleComponent</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">bGenerateOverlapEvents</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">true</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

## 부동소수점 너비
Unreal 5.0부터 Epic은 모든 게임플레이 관련 벡터, 로테이터 등에 `double`을 사용하기 시작했습니다.
블루프린트에서 `float`에 익숙한 사용자의 혼란을 피하기 위해, 에디터에서는 이전처럼 이러한 double을 계속 `float`이라고 부릅니다.

Angelscript 통합도 이 방식을 따르므로 스크립트에서 선언한 `float`은 실제로 64비트 double 값입니다.
특정 너비의 부동소수점 변수를 만들려면 `float32` 또는 `float64` 타입을 명시적으로 사용하세요.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ValueDouble</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">1.0</span><span style="color: #d4d4d4;">; </span><span style="color: #6a9955;">// &lt;-- This is a 64-bit double-precision float</span></div><div><span style="color: #569cd6;">float32</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ValueSingle</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">1.f</span><span style="color: #d4d4d4;">; </span><span style="color: #6a9955;">// &lt;-- This is a 32-bit single-precision float</span></div><div><span style="color: #569cd6;">float64</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ValueAlsoDouble</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">1.0</span><span style="color: #d4d4d4;">; </span><span style="color: #6a9955;">// &lt;-- This is *also* a 64-bit double-precision float</span></div></div>
