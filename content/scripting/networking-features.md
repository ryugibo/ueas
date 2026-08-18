+++
title = "네트워킹 기능"
weight = 80
sort_by = "weight"
+++

# Unreal 네트워킹 기능
Unreal 네트워킹 기능은 블루프린트와 비슷한 수준으로 지원됩니다.

`UFUNCTION()` 지정자에 `NetMulticast`, `Client`, `Server`, `BlueprintAuthorityOnly` 중 하나 이상을 표시할 수 있으며 C++과 거의 동일하게 동작합니다. Angelscript나 블루프린트 어디에서 호출하든 함수 본문은 자동으로 RPC로 사용됩니다.

C++과 달리 Angelscript RPC 함수는 기본적으로 reliable입니다. unreliable RPC 메시지를 사용하려면 `UFUNCTION()` 선언에 `Unreliable` 지정자를 넣으세요.

`UPROPERTY()`는 `Replicated`로 표시할 수 있습니다. 블루프린트 프로퍼티의 드롭다운과 비슷하게 리플리케이션 조건도 선택적으로 설정할 수 있으며, `ReplicationCondition` 지정자를 사용합니다.

C++ 및 블루프린트 네트워킹과 마찬가지로 RPC와 리플리케이트된 프로퍼티가 작동하려면 액터와 컴포넌트가 리플리케이트되도록 설정해야 합니다. Angelscript에서는 `default` 문으로 설정할 수 있습니다.

예시:

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #569cd6;">class</span><span style="color: #d4d4d4;"> </span><span style="color: #4ec9b0;">AReplicatedActor</span><span style="color: #d4d4d4;"> : </span><span style="color: #4ec9b0;">AActor</span></div><div><span style="color: #d4d4d4;">{</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Set the actor's replicates property to default to true,</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// so its declared replicated properties work.</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">default</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">bReplicates</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">true</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Will always be replicated when it changes</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">Replicated</span><span style="color: #d4d4d4;">)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">bool</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">bReplicatedBool</span><span style="color: #d4d4d4;"> = </span><span style="color: #569cd6;">true</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Only replicates to the owner</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">Replicated</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">ReplicationCondition</span><span style="color: #d4d4d4;"> = OwnerOnly)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">int</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ReplicatedInt</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">0</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #6a9955;">// Calls OnRep_ReplicatedValue whenever it is replicated</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UPROPERTY</span><span style="color: #d4d4d4;">(</span><span style="color: #569cd6;">Replicated</span><span style="color: #d4d4d4;">, </span><span style="color: #569cd6;">ReplicatedUsing</span><span style="color: #d4d4d4;"> = OnRep_ReplicatedValue)</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">int</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">ReplicatedValue</span><span style="color: #d4d4d4;"> = </span><span style="color: #b5cea8;">0</span><span style="color: #d4d4d4;">;</span></div><br><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #4fc1ff;">UFUNCTION</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; </span><span style="color: #569cd6;">void</span><span style="color: #d4d4d4;"> </span><span style="color: #dcdcaa;">OnRep_ReplicatedValue</span><span style="color: #d4d4d4;">()</span></div><div><span style="color: #d4d4d4;">&#160; &#160; {</span></div><div><span style="color: #d4d4d4;">&#160; &#160; &#160; &#160; </span><span style="color: #dcdcaa;">Print</span><span style="color: #d4d4d4;">(</span><span style="color: #ce9178;">"Replicated Value has changed!"</span><span style="color: #d4d4d4;">);</span></div><div><span style="color: #d4d4d4;">&#160; &#160; }</span></div><div><span style="color: #d4d4d4;">}</span></div></div>

사용 가능한 `ReplicationCondition` 조건은 C++의 `ELifetimeCondition` 열거형과 일치하며 다음과 같습니다.

- None
- InitialOnly
- OwnerOnly
- SkipOwner
- SimulatedOnly
- AutonomousOnly
- SimulatedOrPhysics
- InitialOrOwner
- Custom
- ReplayOrOwner
- ReplayOnly
- SimulatedOnlyNoReplay
- SimulatedOrPhysicsNoReplay
- SkipReplay


리플리케이트된 `UPROPERTY`에 `ReplicatedUsing`을 지정하여 해당 프로퍼티 값이 리플리케이트될 때마다 함수를 호출할 수도 있습니다. `ReplicatedUsing`에 사용하는 함수는 Unreal에서 볼 수 있도록 반드시 `UFUNCTION()`으로 선언해야 합니다.
