---
date: 2024-7-20
category:
  - vue
tag:
  - tag Vue3设计原理
sticky: true
excerpt: <p>A sticky article demo.</p>
---

# 5.8 代理Set和Map

- 集合类型数据操作与普通对象存在很大的不同
  
| 集合类型 |
| --- |
| Map |  
| Set |  
| WeakMap |
| Weakset |

## 一.第一小节

### set和map

| API对比 | Map | Set |
| --- | --- |--- |
| 添加元素 | set(key,value) | add(value)|
| 获取方法 | get(key) | |

```js
const s = new Set();
const proxyTest = new Proxy(s, {});
console.log(proxyTest.size); //TypeError: Method get Set.prototype.size called on incompatible receiver #<Set>
```

**由报错可知size是访问器属性，会被当成方法调用** 代理中不存在setData这个内部槽，所以会跑出错误，通过修正访问器属性的getter函数执行时this的指向来修正

```js

const s = new Set([1, 2]);
const p = new Proxy(s, {
  get(target, key, receiver) {
    if (key === "size") {
      // 修正this指向，指定第三个参数receiver为原始set对象target，不是代理对象从而进行修复
      return Reflect.get(target, key, target);
    }
    // 正常执行，读取其他属性的默认行为
    return Reflect.get(target, key, receiver);
  }
});
console.log(p.size);
console.log(s.size);

```

### delete处理

```js
console.log(p.delete(1));
//TypeError: Method Set.prototype.delete called on incompatible receiver #<Set>
```

| proxy Set |  size| delete|
| --- | --- | --- |
|  类型  |访问属性 |方法 |
| 执行时间 |立即执行 |调用时执行 |
| 处理方法 | 修正访问属性getter函数执行时的this |将delete与原始数据对象标定 |

```js

const s = new Set([1, 2]);
const p = new Proxy(s, {
  get(target, key, receiver) {
    if (key === "size") {
      return Reflect.get(target, key, target);
    }
    // 将方法与原始对象绑定返回
    return target[key].bind(target);
  }
});

console.log(p.delete(1));//true
console.log(p.size);//1
console.log(s.size);//1
```

### 第一部分小结

```js
const reactiveMap = new Map();
function reactive(obj) {
  const proxy = createReactive(obj);
  const existionProxy = reactiveMap.get(obj);
  if (existionProxy) {
    return existionProxy;
  }
  reactiveMap.set(obj, proxy);
  return proxy;
}
function createReactive(obj, isShallow = false, isReadonly = false) {
  return new Proxy(obj, {
    get(target, key, receiver) {
      if (key === "size") {
        return Reflect.get(target, key, target);
      }
      return target[key].bind(target);
    }
  });
}
const proxy1 = reactive(new Set([1, 2]));
console.log(proxy1);
proxy1.delete(1);
console.log(proxy1);
```

## 二.建立响应联系
