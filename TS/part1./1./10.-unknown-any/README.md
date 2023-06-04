# 10. unknown과 any(그리고 타입 대입가능표)



> any는 ts에게 타입을 포기시킨다.

> unknown은 그 이후에 타입을 추가로 시켜야한다.(지금 당장 모르겠다. 나중에 쓰면서 알게되면 쓰겠다.)

\=> 주로 try, catch할때 err에서 쓰임.

```typescript
try {

} catch (error) {
    (error as Error).message
    //AxiosError 도 있
}
```

위의 Error 타입은 ts에서 제공하는 타입 중 하나임.

왜냐하면 나중에 err가 어떤 타입의 정보가 나올지 모름.



이전 히스토리를 좀 보자면 처음에는 ts에 error는 any 였는데 unknown으로 바뀜.



왜울 필요 없음 왜?&#x20;

코딩할때 어차피 ts가 다 에러 만들어줌.

아래의 표에서 초록색 체크도 x 로 보면 됨 strict 여부에 따른 것임.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>











