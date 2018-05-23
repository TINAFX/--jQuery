#####  本项目是由jquery编写的PC端小项目，实现了登录 评论  首页详情页的跳转
###  登录 
######  页面写的简单 但是实现了登录的功能
###  通过ajax调用接口："http://192.168.199.249:8080/index.php?c=api&a=doLogin
  
**请求方式：**
- POST

**参数：** 

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|email |是  |string |邮箱|
|password |是  |string |密码|
######  通过
localStorage.setItem("user_id",result.data.id);
localStorage.setItem("user_name",result.data.name)来存储用户名和用户ID

### 首页
######  由于接口不是线上的 我自己写了假数据 并且用jquery用拼接字符串的方法渲染数据，并实现了首页跳转详情页的功能
######  部分代码实现： 
for(var i=0; i<result.data.lists.length;i++){			   	
			    str += "<li class='time-box clearfix'><div>><div class='timer'><p>"+result.data.lists[i].month+"</p><p class='year'>"+result.data.lists[i].year+"</p></div><div class='icon'></div><div class='timed'><div class='timed-title'><h2><a href='#'>"+result.data.lists[i].title+"</a></h2></div><div class='time-img'><a href='#'><img src='./images/1.jpg' alt=''></a></div><div class='time-info'><p>"+result.data.lists[i].content+"</p><span><a href='./xiangqing.html?id="+result.data.lists[i].id+"'>阅读全文>></a></span></div></div></div</li>";
			   
		   };
		   $(".time-content").html(str);
###  详情页
**请求URL：** 
- ` http://192.168.199.249:8080/index.php?c=api&a=info 

 `
  
**请求方式：**
- get

**参数：** 

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|id |是  |string |博客id|
######  通过var nowId=window.location.search.split("=")[1]; 获取到博客的id来实现跳转，并且用拼接字符串的方法来渲染数据
######  部分代码实现：
$(function(){
		var nowId=window.location.search.split("=")[1];
		$.ajax({
			url:"http://192.168.199.249:8080/index.php?c=api&a=info",
			dataType:"json",
            type:"get",
            data:{
            	id:nowId ,
            },
            success:function(result){
            	var str='<div class="title clearfix"><h2>'+result.data.info.title+'</h2><p>'+result.data.info.content+'</p></div>'
		       $(".about").html(str)
		       var rStr="";
		       for(var i=0;i<result.data.commentList.length;i++){
		       	 rStr+="<li class='clearfix'><div class='author'><div class='author-img'><img src='./images/555.jpg'alt=''></div><div class='name'><a href='#'>"+result.data.commentList[i].author.name+"</a></div><div class='address'><p>[山西省太原市网友]</p></div><div class='time clearfix'><p>"+result.data.commentList[i].createtime+"</p></div><div class='saying'><p>"+result.data.commentList[i].content+"</p></div><div class='tip'><ul><li class='inform'><a href='#'>举报</a></li><li class='replay'><a href='#'>回复</a></li><li class='zan'><a href='#'>2</a></li><li class='unzan'><a href='#'></a></li><li class='ying'><a href='#'></a></li></ul></div></div><div class='box1'><textarea name='' id='' cols='30' rows='10'></textarea></div></li>"
		       }
		       $(".item").html(rStr);	
		    }
		});
       
	}
  ### 评论
  **请求URL：** 
- ` http://192.168.199.249:8080/index.php?c=api&a=doComment 

 `
  
**请求方式：**
- get

**参数：** 

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|content |是  |string |评论内容|
|user_id|是  |string |用户id|
|blog_id |是  |string |博客的id|
######  通过
      var blogId=window.location.search.split("=")[1];
			var userId=localStorage.getItem("user_id");
			var userName=localStorage.getItem("user_name")方法来获得博客id 用户id 以及用户名
 ######  用字符串拼接的方法将发布的内容等拼接进去，并且将评论的内容插入到最后一条
 ##### 部分代码的实现
 f(result.status){
						alert("发布成功");
					  var cStr="<li class='clearfix'><div class='author'><div class='author-img'><img src='./images/555.jpg'alt=''></div><div class='name'><a href='#'>"+userName+"</a></div><div class='address'><p>[山西省太原市网友]</p></div><div class='time clearfix'><p>"+result.data.createtime+"</p></div><div class='saying'><p>"+contentText+"</p></div><div class='tip'><ul><li class='inform'><a href='#'>举报</a></li><li class='replay'><a href='#'>回复</a></li><li class='zan'><a href='#'>2</a></li><li class='unzan'><a href='#'></a></li><li class='ying'><a href='#'></a></li></ul></div></div><div class='box1'><textarea name='' id='' cols='30' rows='10'></textarea></div></li>"
					    $(".item").append(cStr)	
					}

