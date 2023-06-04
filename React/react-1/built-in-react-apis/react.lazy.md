---
description: https://ko.reactjs.org/docs/code-splitting.html
---

# React.lazy

[https://velog.io/@ansrjsdn/React.lazy-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0](https://velog.io/@ansrjsdn/React.lazy-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0)



실제 사용 예시&#x20;

if 로 component를 일일히 분기 처리하다가&#x20;

이게 안티 패턴이라는 정보를 확인했고&#x20;

\=> good

componentMap을 만들어 component를 import 하는 것

\=> better

componentMap 은 동일하지만 lazy를 통해 다이나믹 import 하는 것 까지 추가



기왕 하는거 better를 한다고 했으나 에러를 발생.

docs를 읽고 확인해보니 lazy는 react의 suspense가 적용되어있을때 가능했다.



```javascript
const componentMap = {
  hvac: lazy(() => import('../Hvac/components/AppliedDiv')),
  uc: lazy(() => import('../UnitCooler/components/AppliedDiv')),
  lighting: lazy(() => import('../Lighting/components/AppliedDiv')),
  nutrient: lazy(() => import('../Nutrient/components/AppliedDiv')),
};
```

```jsx
        <Suspense>
          <Component
            appName={appName}
            data={appliedScheduleData?.schedule}
            setValue={setValue}
            isImmediateControlLoading={isImmediateControlLoading}
            scheduleSettingMode={scheduleSettingMode}
          />
        </Suspense>
```



