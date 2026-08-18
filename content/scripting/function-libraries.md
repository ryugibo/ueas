+++
title = "함수 라이브러리"
weight = 30
sort_by = "weight"
+++

# 함수 라이브러리

스크립트에서 Unreal과 상호작용할 때 함수 라이브러리를 자주 사용합니다.
함수 라이브러리는 서로 관련된 함수 모음을 포함하는 네임스페이스로 스크립트에 노출됩니다.

예를 들어 타이머를 설정하려면 `System::SetTimer()`를 호출합니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">ATimerExample</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">BeginPlay</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #6a9955;">// Execute this.OnTimerExecuted() after 2 seconds</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #4ec9b0;">System</span><span style="color: #d4d4d4;">::</span><span style="color: #dcdcaa;">SetTimer</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">this</span><span style="color: #d4d4d4;">, n</span><span style="color: #ce9178;">"OnTimerExecuted"</span><span style="color: #d4d4d4;">, </span><span style="color: #b5cea8;">2.0</span><span style="color: #d4d4d4;">, bLooping = </span><span style="color: #569cd6;">false</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">private</span><span style="color: #d4d4d4;"> </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">OnTimerExecuted</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Timer executed!"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

## 일반적인 라이브러리

라이브러리를 클릭하면 사용할 수 있는 함수가 나열된 API 문서로 이동합니다.

- [Math::](http://angelscript.hazelight.se/api/index.html#CClass:Math) - 모든 표준 수학 기능
- [Gameplay::](http://angelscript.hazelight.se/api/index.html#CClass:Gameplay) - 스트리밍, 대미지, 플레이어 처리 등의 게임 기능
- [System::](http://angelscript.hazelight.se/api/index.html#CClass:System) - 타이머, 트레이스, 디버그 렌더링 등의 엔진 기능
- [Niagara::](http://angelscript.hazelight.se/api/index.html#CClass:Niagara) - 파티클 시스템 스폰 및 제어
- [Widget::](http://angelscript.hazelight.se/api/index.html#CClass:Widget) - UMG 위젯 기능

## 네임스페이스 단순화 {#namespace-simplification}

스크립트 함수 라이브러리의 함수는 C++의 블루프린트 함수 라이브러리 클래스에서 자동으로 가져옵니다.

바인딩하기 전에 Angelscript 플러그인은 클래스 이름을 단순화하여 더 짧은 네임스페이스를 만듭니다.
예를 들어 `System::` 네임스페이스의 함수는 C++의 `UKismetSystemLibrary` 클래스에서 자동으로 가져옵니다.

자동으로 제거되는 일반적인 접두사와 접미사는 다음과 같습니다.

- U...Statics
- U...Library
- U...FunctionLibrary
- UKismet...Library
- UKismet...FunctionLibrary
- UBlueprint...Library
- UBlueprint...FunctionLibrary

네임스페이스 단순화의 몇 가지 예는 다음과 같습니다.

- `UNiagaraFunctionLibrary`는 `Niagara::`가 됩니다.
- `UWidgetBlueprintLibrary`는 `Widget::`이 됩니다.
- `UKismetSystemLibrary`는 `System::`이 됩니다.
- `UGameplayStatics`는 `Gameplay::`가 됩니다.

# 수학 라이브러리

블루프린트와 C++의 수학 코드 작성 방식이 상당히 다르므로, 스크립트의 `Math::` 네임스페이스는 전반적으로 C++의 `FMath::` 네임스페이스에 가깝게 유지하기로 했습니다.

C++ 수학 기능과 유사하게 유지하면 숙련된 프로그래머가 쉽게 전환할 수 있고 두 환경 간에 코드를 옮기기도 더 편리합니다.

따라서 `UKismetMathLibrary`는 자동 바인딩에서 제외됩니다.
