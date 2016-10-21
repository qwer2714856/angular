控制器
======
    dom 和 数据操作 都不要放在控制器外处理。
    {{persion}} 这里如果是对象直接输出对象的 toString();
    作用域指令内部创建的有自己的作用域。

表达式
======
    $parse("对象的key名").val(目标对象);
    如果在这个里面有完全包含对象的key名，将打印对象key对应的值
    例如
    $parse("admin").({admin:1});将打印1
    
    $interpolate 相比要灵活许多
    $interpolate("{{admin}} is {{hello}}")({admin:1,hello:2}) 将打印 1 is 2 这个可以打印多个key对应的值
    
    修改默认表达式的{{}}
    $interpolateProvider.startSymbol("__"); //前
    $interplateProvider.endSymbol("__"); //后
    
