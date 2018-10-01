# phpqrcode
```
1、png方法用法
png($frame, $filename = false, $pixelPerPoint = 4, $outerFrame = 4,$saveandprint=FALSE)

2、简单用法
<?php
include './phpqrcode.php';
QRcode::png('http://www.baidu.com'); 

3、复杂用法
<?php
include './phpqrcode.php';
QRcode::png('http://www.baidu.com','qrcode.png',2,10,true);
$logo = 'logo.jpg';//准备好的logo图片
$QR = 'qrcode.png';//已经生成的原始二维码图
if ($logo !== FALSE) {
    $QR = imagecreatefromstring(file_get_contents($QR));
    $logo = imagecreatefromstring(file_get_contents($logo));
    $QR_width = imagesx($QR);//二维码图片宽度
    $QR_height = imagesy($QR);//二维码图片高度
    $logo_width = imagesx($logo);//logo图片宽度
    $logo_height = imagesy($logo);//logo图片高度
    $logo_qr_width = $QR_width / 5;
    $scale = $logo_width/$logo_qr_width;
    $logo_qr_height = $logo_height/$scale;
    $from_width = ($QR_width - $logo_qr_width) / 2;
    //重新组合图片并调整大小
    imagecopyresampled($QR, $logo, $from_width, $from_width, 0, 0, $logo_qr_width,
    $logo_qr_height, $logo_width, $logo_height);
}
//输出图片
imagepng($QR, 'newcode.png');
echo '![](./newcode.png)';

```