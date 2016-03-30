1. uploadify3.1以后的版本
   'swf'参数和'uploader'参数是有改变的，一开始不知道跟着别的教程走，连上传按钮都出不来！
   
   关于302报错：
   我用的是session传值，首先在前端模板页面的JS代码里定义：
   var sid = '{:session_id()}';
   然后实例化uploadify时，formDate参数设置为：
   formData : {'session_id' : sid},
   
   'session_id'是PHP模板定义好的session名，和<? echo session_name(); ?>是一样的。
