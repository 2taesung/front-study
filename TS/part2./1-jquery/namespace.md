# 네임스페이스(namespace)

```typescript
export = jQuery;
```

type ->

```typescript
declare const jQuery: JQueryStatic;
declare const $: JQueryStatic;
```

이걸 보고 우리가 알 수 있는것은

1. declare&#x20;

구현부는 따로 있고 선언부에 해당.



2. jQuery와 $가 같구나.



\->

```typescript
<TElement extends HTMLElement = HTMLElement>(html: JQuery.htmlString, ownerDocument_attributes?: Document | JQuery.PlainObject): JQuery<TElement>;
```

여기서 또 JQuery.htmlString는 뭐냐&#x20;



```typescript
declare namespace JQuery {
    type TypeOrArray<T> = T | T[];
    type Node = Element | Text | Comment | Document | DocumentFragment;

    /**
     * A string is designated htmlString in jQuery documentation when it is used to represent one or more DOM elements, typically to be created and inserted in the document. When passed as an argument of the jQuery() function, the string is identified as HTML if it starts with <tag ... >) and is parsed as such until the final > character. Prior to jQuery 1.9, a string was considered to be HTML if it contained <tag ... > anywhere within the string.
     */
    type htmlString = string;
```



여기서 namespace는 같은 type 구현이 다른 라이브러리들에서 겹칠 여지를 막아주는 것



```typescript
ownerDocument_attributes?: Document | JQuery.PlainObject
```

이건 안씀.



```typescript
JQuery<TElement>
```

이게 결국 중요한데&#x20;

이게 뭐냐 맨 앞에 있던 제네릭

```typescript
<TElement extends HTMLElement = HTMLElement>
```

HTMLElement



고로 약TElement == HTMLElement

오케이 이제 제네릭은 찾았음.



그럼 이제 jQuery로 들어가보려고 하는데

두가지가 존재한다.

\-> type



우리가 처음에 봤던 jQuery 타입과

또 다른건&#x20;

```typescript
interface JQuery<TElement = HTMLElement> extends Iterable<TElement> {
```

처음에 봤던 애는 제네릭이 없었다.

그런데 얘는 제네릭이 대놓고 존재.
