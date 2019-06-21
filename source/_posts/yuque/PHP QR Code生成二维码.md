
---

title: PHP QR Code生成二维码

date: 2016-07-04 10:32:16 +0800

tags: [PHP,二维码]

categories: PHP

---

首先，我们去官网下载：[http://sourceforge.net/projects/phpqrcode/](http://sourceforge.net/projects/phpqrcode/)

然后解压缩，把整个文件夹放到项目目录下

新建demo.php

```
<?php 
    include('./phpqrcode/phpqrcode.php'); 
    // 二维码数据 
    $data = '产、范';
    // 纠错级别：L、M、Q、H 
    $errorCorrectionLevel = 'H';  
    // 点的大小：1到10 
    $matrixPointSize = 4;  
     // 生成的文件名 
    $filename = $errorCorrectionLevel.$matrixPointSize.'.png'; 
     // 生成二维码图片
    QRcode::png($data, $filename, $errorCorrectionLevel, $matrixPointSize, 2); 
     // 输出二维码图片 
    echo '<img src="'.$filename.'">';
 ?>
```

关于QRcode::png方法参数说明：<br />  1.第一个参数$text，就是上面代码里的URL网址参数，

2. 第二个参数$outfile默认为否，不生成文件，只将二维码图片返回，否则需要给出存放生成二维码图片的路径
2. 第三个参数$level默认为L，这个参数可传递的值分别是L(QR_ECLEVEL_L，7%)，M(QR_ECLEVEL_M，15%)，Q(QR_ECLEVEL_Q，25%)，H(QR_ECLEVEL_H，30%)。这个参数控制二维码容错率，不同的参数表示二维码可被覆盖的区域百分比。利用二维维码的容错率，我们可以将头像放置在生成的二维码图片任何区域。
2. 第四个参数$size，控制生成图片的大小，默认为4
2. 第五个参数$margin，控制生成二维码的空白区域大小
2. 第六个参数$saveandprint，保存二维码图片并显示出来，$outfile必须传递图片路径。

那么实际应用中，我们会在二维码的中间加上自己的LOGO，以增强宣传效果。那如何生成含有logo的二维码呢？其实原理很简单，先使用PHP QR Code生成一张二维码图片，然后再利用php的image相关函数，将事先准备好的logo图片加入到刚生成的原始二维码图片中间，然后重新生成一张新 的二维码图片。

```php
<?php
    include('./phpqrcode/phpqrcode.php');
    $value = 'http://blog.csdn.net/luoshengkim?viewmode=contents'; //二维码内容     
    $errorCorrectionLevel = 'L'; //容错级别     
    $matrixPointSize = 6; //生成图片大小  
  
    // 生成二维码图片     
    QRcode::png($value, 'qrcode.png', $errorCorrectionLevel, $matrixPointSize, 2);  
  
    //生成中间带logo的二维码       
    $logo = 'dirk.jpg'; // logo图片是你自己放到文件夹里的    
    $QR = 'qrcode.png';    
     
    if($logo !== FALSE)    
    {    
     
        $QR = imagecreatefromstring(file_get_contents($QR));    
        $logo = imagecreatefromstring(file_get_contents($logo));    
        $QR_width = imagesx($QR); //二维码图片宽度   
        $QR_height = imagesy($QR);//二维码图片高度     
        $logo_width = imagesx($logo);//logo图片宽度    
        $logo_height = imagesy($logo);//logo图片高度    
        $logo_qr_width = $QR_width / 5;    
        $scale = $logo_width / $logo_qr_width;    
        $logo_qr_height = $logo_height / $scale;    
        $from_width = ($QR_width - $logo_qr_width) / 2;    
         //重新组合图片并调整大小
        imagecopyresampled($QR, $logo, $from_width, $from_width, 0, 0, $logo_qr_width, $logo_qr_height, $logo_width, $logo_height);    
    } 
    
    //输出图片   
    imagepng($QR,'qrWithLogo.png');   
  
    echo '<img src="qrWithLogo.png">';
```

由于二维码允许有一定的容错性，一般的二维码即使在遮住部分但仍然能够解码，经常我们扫描二维码的时候扫描到甚至不到一半时就能解码扫描结果，这是因为生成器会将部分信息重复表示来提高其容错度，这就是为什么我们在二维码中间加个LOGO图片并不影响解码结果的原因。

