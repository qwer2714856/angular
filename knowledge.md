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

过滤器
======
表单验证
<!DOCTYPE html>

<html ng-app="myTest">
    <head>
        <meta name="viewport" content="width=device-width" />
        <title>Index</title>
        <link href="~/Content/css/bootstrap.min.css" rel="stylesheet" />
        <script src="~/Javascript/angular.min.js"> </script>
        <style type="text/css">
            body { padding-top: 30px; }
        </style>
    </head>
    <body  ng-Controller="MyController">
        <div class="col-md-6">
            <form role="form" name="myForm" ng-submit="submitForm(myForm.$valid)" class="form-horizontal" novalidate>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="name">1.必填项</label>
                    </div>
                    <div class="col-md-8">
                        <input class="form-control" id="name" name="name" type="text" required ng-model='user.name' />
                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.name.$dirty && myForm.name.$valid"></span>
                    </div>
                </div>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="minlength">2.最小长度=5</label>
                    </div>
                    <div class="col-md-8">
                        <input type="text" id="minlength" name="minlength" ng-minlength="5" ng-model="user.minlength" class="form-control" />
                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.minlength.$dirty && myForm.minlength.$valid"></span>
                    </div>
                </div>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="maxlength">3.最大长度=20</label>
                    </div>
                    <div class="col-md-8">
                        <input type="text" id="maxlength" name="maxlength" ng-model="user.maxlength" ng-maxlength="20" class="form-control" />
                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.maxlength.$dirty && myForm.maxlength.$valid"></span>
                    </div>
                </div>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="pattern">4. 模式匹配</label>
                    </div>
                    <div class="col-md-8">
                        <input type="text" id="pattern" name="pattern" ng-model="user.pattern" ng-pattern="/^[a-zA-Z]*\d$/" class="form-control" />
                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.pattern.$dirty && myForm.pattern.$valid"></span>
                    </div>
                </div>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="email">5. 电子邮件</label>
                    </div>
                    <div class="col-md-8">
                        <input type="email" id="email" name="email" ng-model="user.email" class="form-control" />
                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.email.$dirty && myForm.email.$valid"></span>
                    </div>
                </div>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="age">6. 数字</label>
                    </div>
                    <div class="col-md-8">
                        <input type="number" id="age" name="age" ng-model="user.age" class="form-control" />

                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.age.$dirty && myForm.age.$valid"></span>
                    </div>
                </div>
                <div class="form-group  has-feedback">
                    <div class="col-md-4">
                        <label for="url"> 7. URL</label>
                    </div>
                    <div class="col-md-8">
                        <input type="url" id="url" name="url" ng-model="user.url" class="form-control" />
                        <span class="glyphicon glyphicon-ok form-control-feedback"
                              ng-show="myForm.url.$dirty && myForm.url.$valid"></span>
                    </div>
                </div>
                <div class="form-group  text-center">
                    <input class="btn btn-primary btn-lg" ng-disabled="myForm.$invalid" type="submit" value="提交" />
                </div>
            </form>       
        </div>
        <div class="col-md-12">
            1.必填项:{{user.name}}&nbsp;&nbsp;
            $pristine 【没修改】：{{myForm.name.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.name.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.name.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.name.$valid}}&nbsp;&nbsp;
            required：{{myForm.name.$error.required}}&nbsp;&nbsp;
            <br>
            2.最小长度=5:{{user.minlength}}
            $pristine 【没修改】：{{myForm.minlength.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.minlength.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.minlength.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.minlength.$valid}}&nbsp;&nbsp;
            $error【错误详情】：{{myForm.minlength.$error}}&nbsp;&nbsp;<br>
            3.最大长度=20:{{user.maxlength}}
            $pristine 【没修改】：{{myForm.maxlength.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.maxlength.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.maxlength.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.maxlength.$valid}}&nbsp;&nbsp;
            $error【错误详情】：{{myForm.maxlength.$error}}&nbsp;&nbsp;<br>
            4.模式匹配:{{user.pattern}}
            $pristine 【没修改】：{{myForm.pattern.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.pattern.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.pattern.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.pattern.$valid}}&nbsp;&nbsp;
            $error【错误详情】：{{myForm.pattern.$error}}&nbsp;&nbsp;<br>
            5.电子邮件:{{user.email}}
            $pristine 【没修改】：{{myForm.email.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.email.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.email.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.email.$valid}}&nbsp;&nbsp;
            $error【错误详情】：{{myForm.email.$error}}&nbsp;&nbsp;<br>
            6.数字:{{user.age}}
            $pristine 【没修改】：{{myForm.age.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.age.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.age.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.age.$valid}}&nbsp;&nbsp;
            $error【错误详情】：{{myForm.age.$error}}&nbsp;&nbsp;<br>
            7.URL:{{user.url}}
            $pristine 【没修改】：{{myForm.url.$pristine }}&nbsp;&nbsp;
            $dirty【修改过】：{{myForm.url.$dirty}}&nbsp;&nbsp;
            $invalid【验证失败】：{{myForm.url.$invalid}}&nbsp;&nbsp;
            $invalid【验证成功】：{{myForm.url.$valid}}&nbsp;&nbsp;
            $error【错误详情】：{{myForm.url.$error}}&nbsp;&nbsp;<br>
        </div>
    </body>
</html>
<script type="text/javascript">
    angular.module('myTest', [])
        .controller('myController', function($scope) {
            $scope.submitForm = function(isValid) {
                if (!isValid) {
                    alert('验证失败');
                }
            };
        }
        );
</script>
    
http://www.cnblogs.com/rohelm/p/4033513.html

$parsers
<!DOCTYPE html>
<html lang="en" ng-app="myApp">
<head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script src='https://code.angularjs.org/1.2.0/angular.js'></script>
</head>
<body>
<form name="mainform">
<input type="text" ng-model="text" name="text"  one-to-tocken="" />
<span ng-show="!mainform.text.$error.oneToTocken">error</span>

</form>


<script>
var app = angular.module('myApp', []);
app.directive('tk', function(){
    return{
        require : '?ngModel',
        link : function(scpe, ele, attrs, ngModel, $filter){
            if(!ngModel) return ;
            
            ngModel.$parsers.unshift(function(v){
                
                ngModel.$setValidity('tk', false);
                return v + 999;

            });
        
           ngModel.$formatters.unshift(function(v){
                console.log($filter);
                return v + '';
           })           

        }

    }

});
</script>
</body>
</html>


$formatters
当自定义指令一加载就会对ng-model 里面的值进行修改

使用ng-submit 提交的时候form不需要action 使用$http post
