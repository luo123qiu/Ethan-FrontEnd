Ethan-FrontEnd
==============

CSS3 UI库：http://css3lib.alloyteam.com/

webAPP化的写法，precomposed表示图标无高光

    <link rel="apple-touch-icon-precomposed" size="57x57" href="images/apple-touch-icon-precomposed.png" />
    <link rel="apple-touch-icon-precomposed" size="72x72" href="images/apple-touch-icon-72x72-precomposed.png" />
    <link rel="apple-touch-icon-precomposed" size="114x114" href="images/apple-touch-icon-114x114-precomposed.png" />

CSS3实现三角箭头

    .arrow1 {width:20px; height:20px; overflow:hidden; position:relative;}
    .arrow2 {-webkit-transform:rotate(45deg); background:#3a272d; width:8px; height:8px; position:absolute;}
    <div class="arrow1"><div class="arrow2"></div></div>
    
Ajax类

    function Ajax(recvType){
        var aj=new Object();
        aj.recvType=recvType ? recvType.toUpperCase() : 'HTML';  //向形参中传递的文件类型
        aj.targetUrl='';
        aj.sendString='';
        aj.resultHandle=null;
        /*创建XMLHttpRequest对象*/
        aj.createXMLHttpRequest=function(){
            var xmlHttp = false;
            if(window.XMLHttpRequest){ //在非IE中创建XMLHttpRequest对象
                xmlHttp = new XMLHttpRequest();
            }else if(window.ActiveXObject){
                try{
                    xmlHttp = new ActiveXObject("Msxml2.XMLHTTP"); //按新版IE创建
                }catch(error1){ //创建失败
                    try{
                        xmlHttp = new ActiveXobject("Microsoft.XMLHttp"); //按老版IE创建
                    }catch(error2){ //创建失败
                        xmlHttp = false;
                    }
                }
            }
            return xmlHttp;
        }
        aj.XMLHttpRequest=aj.createXMLHttpRequest();
        /*处理服务器的响应*/
        aj.processHandle=function(){
            if(aj.XMLHttpRequest.readyState == 4){
                if(aj.XMLHttpRequest.status == 200){
                    if(aj.recvType=="HTML")
                    aj.resultHandle(aj.XMLHttpRequest.responseText);
                    else if(aj.recvType=="XML")
                    aj.resultHandle(aj.XMLHttpRequest.responseXML);
                }
            }
        }
        /*定义使用get方法传递的方法*/
        aj.get=function(targetUrl, resultHandle){
            aj.targetUrl=targetUrl;    
            if(resultHandle!=null){
                aj.XMLHttpRequest.onreadystatechange=aj.processHandle;    
                aj.resultHandle=resultHandle;    
            }
            if(window.XMLHttpRequest){
                aj.XMLHttpRequest.open("get", aj.targetUrl);
                aj.XMLHttpRequest.send(null);
            }else{
                aj.XMLHttpRequest.open("get", aj.targetUrl, true);
                aj.XMLHttpRequest.send();
            }
        }
        /*定义使用post方法传递的方法*/
        aj.post=function(targetUrl, sendString, resultHandle){
            aj.targetUrl=targetUrl;
            if(typeof(sendString)=="object"){
                var str="";
                for(var pro in sendString){
                    str+=pro+"="+sendString[pro]+"&";    
                }
                aj.sendString=str.substr(0, str.length-1);
            }else{
                aj.sendString=sendString;
            }
            if(resultHandle!=null){
                aj.XMLHttpRequest.onreadystatechange=aj.processHandle;    
                aj.resultHandle=resultHandle;    
            }
            aj.XMLHttpRequest.open("post", targetUrl);
            aj.XMLHttpRequest.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
            aj.XMLHttpRequest.send(aj.sendString);  
        }
        return aj;
    }
    
    //调用ajax类
    var ajax=Ajax();
    /*get使用方式*/
    ajax.get("server.php?name=zhangsan&phone=778", function(data){                
        alert(data); //data为从服务器端读取的数据
    });
    /*第一种post使用方式*/
    ajax.post("server.php", "name=ligang&phone=222", function(data){
        alert(data);
    });
    /*第二种post使用方式*/
    ajax.post("server.php", {name:"tom",phone:"456"},function(data){
        alert(data);
    });