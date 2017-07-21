拦截`getter`和`setter`等等操作进行拦截
```javascript
var obj = new Proxy({}, {
    get(tartget, key, receiver) {

    },
    set(tartget, key, value, receiver) {

    },
    apply(tartget, thisBinding, args) {

    },
    construct(tartget, args) {

    }
});

```

`Proxy`和`Object.defineproperty()`??
