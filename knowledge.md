控制器
======
    dom 和 数据操作 都不要放在控制器外处理。
    {{persion}} 这里如果是对象直接输出对象的 toString();
    作用域指令内部，ng-model 创建的有自己的作用域。

表达式
======
    $parse("字符串值") 返回的是一个函数
    $parse("字符串值")(对象) 如果字符串是对象的key 返回key对应的值
    如果 字符串是检测返回的newValue
    $watch("aaa", function($newvalue, $oldvalue, scope){})
    $parse(newValue)(scope) 返回的还是newvalue
    说白了就是
    $parse("字符串")(放到哪个作用域中去) 解析这个表达式在作用域上的值
    $parse
    http://www.thinksaas.cn/topics/0/401/401879.html
    $interpolate
    http://www.thinksaas.cn/topics/0/401/401878.html
    都有切换作用域的作用。
    
