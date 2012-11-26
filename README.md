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