+++
title = "구조체와 참조"
weight = 75
+++

# 구조체
스크립트에서 선언한 클래스는 항상 `UObject` 타입이며, Unreal의 일반 객체 시스템과 가비지 컬렉터에 포함됩니다.

스크립트에서 값 타입으로 동작하는 구조체도 만들 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">struct</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">FExampleStruct</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">/* Properties with UPROPERTY() in a struct will be accessible in blueprint. */</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ExampleNumber</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">4.0</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">FString</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ExampleString</span><span style="color: #d4d4d4;"> = </span><span style="color: #ce9178;">"Example String"</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">/* Properties without UPROPERTY() will still be in the struct, but cannot be seen by blueprint. */</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ExampleHiddenNumber</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">3.0</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">};</span></div></div>

> **참고:** 클래스와 달리 구조체는 `UFUNCTION()`을 가질 수 없습니다. 하지만 일반 스크립트 메서드는 가질 수 있으며, 블루프린트에서는 사용할 수 없습니다.

## 구조체 전달 및 반환
구조체는 일반적인 방식으로 스크립트 함수와 `UFUNCTION`에 전달하거나 반환할 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #4ec9b0;">FExampleStruct</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">CreateExampleStruct</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Number</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">FExampleStruct</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">ExampleNumber</span><span style="color: #d4d4d4;"> = </span><span style="color: #9cdcfe;">Number</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">ExampleString</span><span style="color: #d4d4d4;"> = </span><span style="color: #d7ba7d;">f"</span><span style="color: #569cd6;">{</span><span style="color: #9cdcfe;">Number</span><span style="color: #569cd6;">}</span><span style="color: #d7ba7d;">"</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">return</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">}</span></div><br><div><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintPure</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #569cd6;">bool</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">IsNumberInStructEqual</span><span style="color: #d4d4d4;">(</span><span style="color: #4ec9b0;">FExampleStruct</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Struct</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">float</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">TestNumber</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">return</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">Struct</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">ExampleNumber</span><span style="color: #d4d4d4;"> == </span><span style="color: #9cdcfe;">TestNumber</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

## 구조체 참조
기본적으로 스크립트 함수의 인수 값은 읽기 전용입니다.
따라서 구조체 매개변수의 프로퍼티를 변경하거나 `const`가 아닌 메서드를 호출할 수 없습니다.

필요하면 구조체의 참조를 받아 수정할 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #6a9955;">// Change the parameter struct so its number is randomized between 0.0 and 1.0</span></div><div><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">RandomizeNumberInStruct</span><span style="color: #d4d4d4;">(</span><span style="color: #4ec9b0;">FExampleStruct</span><span style="color: #d4d4d4;">&amp; </span><span style="color: #9cdcfe;">Struct</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">Struct</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">ExampleNumber</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">Math</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">RandRange</span><span style="color: #d4d4d4;">(</span><span style="color: #b5cea8;">0.0</span><span style="color: #d4d4d4;">, </span><span style="color: #b5cea8;">1.0</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

## 출력 매개변수 선언
구조체 참조를 받는 함수를 블루프린트 노드에서 호출하면 구조체가 입력값으로 전달됩니다.

{{ img(path="struct-input.png") }}

구조체 매개변수를 출력값으로만 사용하려면 스크립트에서 참조를 `&out`으로 선언합니다. 기본 타입의 출력 핀을 만들 때도 같은 방식을 사용할 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">OutputRandomizedStruct</span><span style="color: #d4d4d4;">(</span><span style="color: #4ec9b0;">FExampleStruct</span><span style="color: #d4d4d4;">&amp;out </span><span style="color: #9cdcfe;">OutputStruct</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">bool</span><span style="color: #d4d4d4;">&amp;out </span><span style="color: #9cdcfe;">bOutSuccessful</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4ec9b0;">FExampleStruct</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">.</span><span style="color: #9cdcfe;">ExampleNumber</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">Math</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">RandRange</span><span style="color: #d4d4d4;">(</span><span style="color: #b5cea8;">0.0</span><span style="color: #d4d4d4;">, </span><span style="color: #b5cea8;">1.0</span><span style="color: #d4d4d4;">);</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">OutputStruct</span><span style="color: #d4d4d4;"> = </span><span style="color: #9cdcfe;">ResultStruct</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #9cdcfe;">bOutSuccessful</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">true</span><span style="color: #d4d4d4;">;</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

{{ img(path="struct-multioutput.png") }}

## 함수 매개변수의 자동 참조
구현 세부 사항으로, 스크립트 함수는 구조체 매개변수를 값으로 받지 않습니다.
구조체 매개변수를 선언하면 `const &`를 추가한 것처럼 내부적으로 상수 참조로 구현됩니다.

따라서 `FVector` 매개변수와 `const FVector&` 매개변수 사이에는 차이가 없습니다. 성능과 의미 면에서 완전히 동일하게 동작합니다.

이는 스크립트 성능을 높이고 게임플레이 스크립터가 모든 매개변수에 `const &`를 작성해야 하는 불편을 피하기 위한 선택입니다.

## 필드 직렬화 및 리플리케이션
구조체 필드에 `UPROPERTY()`가 지정되지 않아도 Angelscript 내부에서는 프로퍼티로 등록됩니다. 따라서 `UPROPERTY(Transient)`와 `UPROPERTY(NotReplicated)`를 명시하지 않는 한, 구조체의 모든 필드는 기본적으로 직렬화되고 리플리케이트됩니다.
  
C++에서 `UPROPERTY()`가 없는 경우와 같은 동작을 구현하기 위해, 다음 두 프로젝트 설정으로 `UPROPERTY()`가 없는 구조체 필드의 동작을 제어할 수 있습니다.

* `Mark Non UProperty Properties as Transient`
* `Mark Non UProperty Properties as Not Replicated`
