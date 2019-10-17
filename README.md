# test
假设我们现在有一个js的对象A，我们需要记录对象A自身属性的值中包含变量b的属性的出现位置，并已数组的形式返回,如果不包含直接返回[]：


    function someFunction(obj, val) {
        let arr = [];
        function find(obj, val, str) {
            return Object
                .keys(obj)
                .filter(s => {
                    if (Object.prototype.toString.call(obj[s]) === '[object Object]') {
                        // console.log(s)
                        return find(obj[s], val, s + '.');//利用了函数递归
                    } //运用ES6 的filter过滤器方法判断参数s中的key是否为对象
                    // console.log(s)
                    return obj[s].toString().indexOf(val) !== -1//找到对象中的值
                })
                .forEach(s => {
                    arr.push(str + s)
                })//遍历对象再组合为一个新数组
        }
        find(obj, val, '');
        return arr;
    }
    
    
## 然后再调用
    console.log(someFunction(
        {
            name: 'wang',
            age: 20,
        },
        20,
    ));// age

    console.log(someFunction(
        {
            name: 'wang',
            age: 20,
            address: {
                city: 'beiji',
                country: 'china',
            },
        },
        'i',
    ));// address.city address.country

    console.log(someFunction(
        {
            name: 'wang',
            age: 20,
        },
        40,
    ))// []
