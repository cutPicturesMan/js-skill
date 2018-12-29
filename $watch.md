## $watch

### new Vue()中的watch
```javascript
var vm = new Vue({
  methods: {
    handleB: function(){}
  },
  watch: {
    // 【路径】'e.f': function (val, oldVal) {}
    a: function (val, oldVal) {},
    // 方法名
    b: 'handleB',
    c: {
      handler: function (val, oldVal) {},
      // 在侦听开始之后立即调用handler函数
      immediate: true
      // 深度 watcher
      deep: true
    },
    d: [
      function handle1 (val, oldVal) {},
      function handle2 (val, oldVal) {}
    ],
  }
})
```

## vm.$watch()
```javascript
/**
 * vm.$watch( expOrFn, callback, [options] )
 * @param expOrFn {string | Function}
 * @param cb {Function | Object}
 * @param [options] {Object}
 *    {
 *       immediate {boolean},      // 在侦听开始之后立即调用handler函数
 *       deep {boolean}            // 深度watcher
 *    }
 * 
 * @returns {Function} unwatch
 */
vm.$watch('a.b.c', function (newVal, oldVal) {}, {
    immediate: true
    deep: true
})

vm.$watch(
    function () {
        return this.a + this.b
    }, {
        handler: function (val, oldVal) {},
        // 在侦听开始之后立即调用handler函数
        immediate: true
        // 深度watcher
        deep: true
    }
)
```

