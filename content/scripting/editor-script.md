+++
title = "에디터 전용 스크립트"
weight = 110
sort_by = "weight"
+++

# 에디터 전용 스크립트
C++의 일부 프로퍼티, 함수 또는 클래스는 에디터에서만 사용할 수 있습니다.
쿠킹된 게임에서 이를 사용하려 하면 스크립트 컴파일에 실패합니다.

액터 레이블, 에디터 서브시스템, 비주얼라이저 등이 여기에 해당합니다.

## 전처리기 블록
클래스 안에서 에디터 전용 코드를 사용해야 한다면 코드 주위에 `#if EDITOR` 전처리기 문을 사용할 수 있습니다.
이 블록 안의 코드는 에디터 외부에서 컴파일되지 않으므로 에디터 전용 기능을 안전하게 사용할 수 있습니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">AExampleActor</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #569cd6;">#if EDITOR</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">default</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">PivotOffset</span><span style="color: #d4d4d4;"> = </span><span style="color: #4ec9b0;">FVector</span><span style="color: #d4d4d4;">(</span><span style="color: #b5cea8;">0</span><span style="color: #d4d4d4;">, </span><span style="color: #b5cea8;">0</span><span style="color: #d4d4d4;">, </span><span style="color: #b5cea8;">10</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #569cd6;">#endif</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">BlueprintOverride</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">ConstructionScript</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #569cd6;">#if EDITOR</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">SetActorLabel</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Example Actor Label"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #569cd6;">#endif</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

> **팁:** 그 밖의 유용한 매크로 조건은 다음과 같습니다.
> `EDITORONLY_DATA` - 에디터에만 관련된 프로퍼티를 읽을 수 있는지 여부
> `RELEASE` - 게임이 Shipping 또는 Test 빌드 구성으로 빌드되었는지 여부
> `TEST` - 게임이 Debug, Development 또는 Test 빌드 구성으로 빌드되었는지 여부

## 에디터 전용 디렉터리
에디터 외부에서 스크립트 파일 전체를 제외할 수도 있습니다.
이름이 `Editor`인 폴더는 쿠킹된 빌드에서 스크립트 컴파일러가 완전히 무시합니다.
예를 들어 에디터 비주얼라이저나 서브시스템 클래스를 `Editor` 폴더 아래에 둘 때 유용합니다.

`Editor` 폴더뿐 아니라 `Examples`와 `Dev`라는 이름의 폴더도 쿠킹된 빌드에서 무시됩니다.

# 쿠킹 시뮬레이션 모드로 테스트
에디터 전용 스크립트 때문에 에디터에서는 작동하고 컴파일되지만 게임을 쿠킹하면 실패하는 스크립트가 생길 수 있습니다.
CI 작업 등에서 이러한 오류를 쉽게 감지하려면 `-as-simulate-cooked` 명령줄 매개변수를 사용할 수 있습니다.

쿠킹 시뮬레이션 모드가 활성화되면 에디터 전용 프로퍼티와 클래스를 스크립트에서 사용할 수 없으며 `#if EDITOR` 블록도 컴파일에서 제외됩니다.

`AngelscriptTest` 커맨드릿과 함께 사용하여 모든 항목이 컴파일되는지 확인할 수 있습니다.
스크립트 컴파일 여부를 테스트하는 Unreal 명령줄은 다음과 같습니다.
```sh
UnrealEditor-Cmd.exe "MyProject.uproject" -as-simulate-cooked -run=AngelscriptTest
```
