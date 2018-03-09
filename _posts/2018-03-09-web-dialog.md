---
layout: post
title:  "confirm&alert弹框"
date:   2018-03-09
categories: 前端
tags: 交互
---

> #### 效果图

![Alt text](/images/object/20180309-1.png "confirm弹框效果图")

---
> 使用方法
{% highlight ruby %}
//confirm弹框  回调函数可以直接填写方法
 $("#del").bind("click", function () {  
    pop.Confirm(
        "来自火星的温馨提示", 
        "准备删除喽，确定继续吗？", 
        function () { console.log("居然真的删除了...") },
        a);  
 });  
 function a(){
    console.log("你点击了取消")
 } 
 //alert弹框
 $("#add").bind("click", function () {  
    pop.Alert("消息", "哈哈，添加成功！");  
 }); 
      
{% endhighlight %}
>子框架调用弹框 `window.parent` window可以省略~~~
弹框支持i8+,但是需注意jq版本问题，否则会报`$`相关的错,demo的jq版本 v1.7.1 亲测有效。
{% highlight ruby %}
parent.pop.alert(
    "来自火星的提示",
    "我被子框架召唤而来"
)
{% endhighlight %}

> css
{% highlight ruby %}
#popBg{width:100%;height:100%;z-index:99999;position:fixed;filter:Alpha(opacity=60);background-color:#000;top:0;left:0;opacity:.6}
#popContent{z-index:999999;width:400px;position:fixed;background-color:#fff;border-radius:15px}
#popTitle{font-size:20px;color:#444;padding:10px 15px 0;border-radius:15px 15px 0 0;text-align:center}
#popMsg{padding:20px;line-height:20px;font-size:14px;text-align:center}
#popBtnDiv{margin:15px 0 10px 0;text-align:center}
#popBtnN,#popBtnY{width:85px;height:30px;color:#fff;border:none}
#popBtnY{background-color:#168bbb}
#popBtnN{background-color:gray;margin-left:20px}
{% endhighlight %}
> javascript
{% highlight ruby %}
<script>
(function () {  
    pop = {  
        Alert: function (title, msg) {  
            setHtml("alert", title, msg);  
            btnY();  
        },  
        Confirm: function (title, msg, callback,callback2) {  
            setHtml("confirm", title, msg);  
            btnY(callback);  
            btnN(callback2);  
        }  
    }  
    //Html  
    var setHtml = function (type, title, msg) {  
        var _html = "";  
        _html += '<div id="popBg"></div><div id="popContent" class="md-show md-content"><div id="popTitle">' + title + '</div>';  
        _html += '<div id="popMsg">' + msg + '</div><div id="popBtnDiv">';  
        if (type == "alert") {  
            _html += '<input id="popBtnY" type="button" value="确定" />';  
        }  
        if (type == "confirm") {  
            _html += '<input id="popBtnY" type="button" value="确定" />';  
            _html += '<input id="popBtnN" type="button" value="取消" />';  
        }  
        _html += '</div></div>';           
        $("body").append(_html);   
         //适应浏览器位置 
         setCss();  
    }  
  
    //自适应浏览器位置  
    var setCss = function () { 
        //获取浏览器窗口文档显示区域的宽高，不包括滚动条 
        var _widht = document.documentElement.clientWidth;   
        var _height = document.documentElement.clientHeight; 
        var boxWidth = $("#popContent").width();  
        var boxHeight = $("#popContent").height();  
        //让提示框居中  
        $("#popContent").css({ 
        	top: (_height - boxHeight) / 2 + "px", 
        	left: (_widht - boxWidth) / 2 + "px" 
        });  
    }  
    //确定按钮事件  
    var btnY = function (callback) {  
        $("#popBtnY").click(function () {  
            $("#popBg,#popContent").remove();  
            if (typeof (callback) == 'function') {  
                callback();  
            }  
        });  
    }  
    //取消按钮事件  
    var btnN = function (callback2) {  
        $("#popBtnN").click(function () {
          	$("#popBg,#popContent").remove();
          	if (typeof (callback2) == 'function') {  
                callback2();  
            } 
        })
    }  
})();  
</script>
{% endhighlight %}

---



