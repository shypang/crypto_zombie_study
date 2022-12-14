# crypto_zombie_study

## solidity study

```
private은 컨트랙트 내부의 다른 함수들에서만 호출될 수 있음을 의미
internal은 private과 비슷하지만, 해당 컨트랙트를 상속하는 컨트랙트에서도 호출
external은 오직 컨트랙트 외부에서만 호출될 수 있네
public은 내외부 모두에서, 어디서든 호출될 수 있네.

state modifier
view는 해당 함수를 실행해도 어떤 데이터도 저장/변경되지 않음
pure는 해당 함수가 어떤 데이터도 블록체인에 저장하지 않을 뿐만 아니라, 블록체인으로부터 어떤 데이터도 읽지 않음
이들 모두는 컨트랙트 외부에서 불렸을 때 가스를 전혀 소모하지 않네(하지만 다른 함수에 의해 내부적으로 호출됐을 경우에는 가스를 소모하지).

사용자 정의 제어자
onlyOwner
aboveLevel

함수 제어자
payable

require : 함수실행이 실패하면 남은 가스를 사용자에게 되돌려줌
assert  : 함수실행이 실패해도 남은 가스를 사용자에게 되돌려 주지 않음


call은 view와 pure 함수를 위해 사용하네. 로컬 노드에서만 실행하고, 블록체인에 트랜잭션을 만들지 않지.
    복습: view와 pure 함수는 읽기 전용이고 블록체인에서 상태를 변경하지 않네. 가스를 전혀 소모하지 않고, 메타마스크에서 트랜잭션에 서명하라고 사용자에게 창을 띄우지도 않지.

Web3.js를 사용하여, 다음과 같이 123을 매개 변수로 myMethod라는 이름의 함수를 call할 수 있네:

myContract.methods.myMethod(123).call()


send는 트랜잭션을 만들고 블록체인 상의 데이터를 변경하네. view와 pure가 아닌 모든 함수에 대해 send를 사용해야 하는 것이지.

    참고: 트랜잭션을 send하는 것은 사용자에게 가스를 지불하도록 하고, 메타마스크에서 트랜잭션에 서명하라고 창을 띄울 것이네. Web3 프로바이더로 메타마스크를 사용할 때, send()를 호출하면 자동으로 이 모든 것이 이루어지고, 우리의 코드에 어떤 특별한 것도 추가할 필요가 없지. 꽤나 훌륭하지!?

Web3.js를 사용하여, 다음과 같이 123을 매개 변수로 myMethod라는 이름의 함수를 호출하는 트랜잭션을 send할 수 있네:

myContract.methods.myMethod(123).send()

receipt는 트랜잭션이 이더리움의 블록에 포함될 때, 즉 좀비가 생성되고 우리의 컨트랙트에 저장되었을 때 발생하게 되네.
error는 트랜잭션이 블럭에 포함되지 못했을 때, 예를 들어 사용자가 충분한 가스를 전송하지 않았을 때 발생하게 되네. 우리는 우리의 UI를 통해 사용자에게 트랜잭션이 전송되지 않았음을 알리고, 다시 시도할 수 있도록 할 것이네.


```

## natspec 표준 - 주석참고

```
/// @title 기본적인 산수를 위한 컨트랙트
/// @author H4XF13LD MORRIS 💯💯😎💯💯
/// @notice 지금은 곱하기 함수만 추가한다.
contract Math {
  /// @notice 2개의 숫자를 곱한다.
  /// @param x 첫 번쨰 uint.
  /// @param y 두 번째 uint.
  /// @return z (x * y) 곱의 값
  /// @dev 이 함수는 현재 오버플로우를 확인하지 않는다.
  function multiply(uint x, uint y) returns (uint z) {
    // 이것은 일반적인 주석으로, natspec에 포함되지 않는다.
    z = x * y;
  }
}
@title과 @author는 따로 설명이 필요 없을 것 같군.

@notice는 사용자에게 컨트랙트/함수가 무엇을 하는지 설명하네. @dev는 개발자에게 추가적인 상세 정보를 설명하기 위해 사용하지.

@param과 @return은 함수에서 어떤 매개 변수와 반환값을 가지는지 설명하네.

```
