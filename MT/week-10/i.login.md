# 주문 목록-I.login()

login 이후 e2e 테스트를 위해 login 모듈화하기

logout\_test.ts

```typescript
Feature("Log out");

Before(({ backdoor, I }) => {
  backdoor.setupDatabase();

  I.login();
});

Scenario("Logout success", ({ I }) => {
  I.amOnPage("/");

  I.see("Cart");

  I.click("Logout");

  I.waitForText("Login");

  I.dontSee("Cart");
});
```

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

당연히 아직 아무것도 안했기 때문에 I.login function이 없다.

고로 e2e test에 세팅으로 넣어주는 파일에 함수를 넣어주어야함



./test/steps\_file.ts

```typescript
const { I } = inject();

export = () =>
  actor({
    async login() {
      I.amOnPage("/");
      I.click("Login");
      I.fillField("E-mail", "tester@example.com");
      I.fillField("Password", "password");
      I.click("로그인", { css: "form" });
    },
  });


```
