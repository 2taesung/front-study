# React가 두 번 실행되는 문제

\<React.StrictMode>

\<React.StrictMode>로 컴포넌트 전체를 감쌀 경우, 예상치 못한 Side Effect를 찾으려고 Effect 등을 두 번씩 실행함. (거의 모든 것들을 두번 실행시킨다고 보면 됨 console.log 도)



평소에는 큰 문제가 없지만, API 등을 사용하면 이상하다고 느낄 수 있으니 참고할 것.

dev 상태에서는 이러지만 build 하면 사라짐.



* [**예상치 못한 부작용 검사**](https://www.notion.so/0bf5a58a76714573946be792e38f53d5)
