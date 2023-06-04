# 모니터 주사율에 따른 requestAnimationFrame 셋팅

모니터의 주사율에따라 내가 의도치 않은 길이와 속도의 애니메이션이 나올 수 있다.

그러므로 이것 역시 균등하게 셋팅을 해줄 필요가 있음



만약

내 모니터 주사율이 60hz&#x20;

\= 1초에 60번 실행

\= 약 16ms(1초/60)마다 requestAnimationFrame이 실행



내 애니메이션의 목표 fps = 10

\= 1초에 10번 프레임을 찍어라

\= 100ms 마다 requestAnimationFrame을 실행시켜라



<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

위 표를 보면 delta가 16씩 계속 횟수에따라 증가한다.

노란색 라인들을 보면 여기에서 delta 값이 까여있다.

노란색 라인이 이제 애니메이션이 실행된 타이밍임. (100이 넘었을 상황이니까)

```javascript
if (delta > interval) {
    애니메이션 동작!
}
then = now - (delta % interval)
```

delta가 100(interval)이 넘어가버리면 100(interval)을 나눠서 나머지만 남겨서 delta를 100이하로 다시 돌려버린다.

이렇게 되면 애니메이션 실행주기가 일정하게 유지가 된다.

(맨 처음은 4ms 더 길고 100% 일정한건 아님)



최종 결론&#x20;

요즘 모니터들은 대부분 60hz임.

고로 이에 맞춰주려면 60FPS가 적절.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

아무튼 위와 같은 로직(delta)으로 최소 60hz\~240hz(고사양) 까지 내가 만든 컨텐츠를 같은 속도로 부드러움의 차이만 좀 있을뿐 작동시킬 수 있게됨.



이걸 코드로 보자&#x20;

```javascript
```
