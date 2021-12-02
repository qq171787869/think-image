# think-image
thinkphp5.1 图像处理类库

参考文档地址：https://www.kancloud.cn/manual/thinkphp5_1/354123

## 安装
> composer require qq171787869/think-image


## 使用open方法打开图像文件进行相关操作
~~~
$image = \think\Image::open('./image.png');
~~~

## 也可以从直接获取当前请求中的文件上传对象
~~~
$image = \think\Image::open(request()->file('image'));
~~~

## 获取图像信息
~~~
$image = \think\Image::open('./image.png');
// 返回图片的宽度
$width = $image->width(); 
// 返回图片的高度
$height = $image->height(); 
// 返回图片的类型
$type = $image->type(); 
// 返回图片的mime类型
$mime = $image->mime(); 
// 返回图片的尺寸数组 0 图片宽度 1 图片高度
$size = $image->size(); 
~~~

## 使用crop和save方法完成裁剪图片功能
~~~
$image = \think\Image::open('./image.png');
// 将图片裁剪为300x300并保存为crop.png
$image->crop(300, 300)->save('./crop.png');
// 支持从某个坐标开始裁剪，例如下面从（100，30）开始裁剪
$image->crop(300, 300,100,30)->save('./crop.png');
~~~

## 使用thumb方法生成缩略图
~~~
$image = \think\Image::open('./image.png');
// 按照原图的比例生成一个最大为150*150的缩略图并保存为thumb.png
$image->thumb(150, 150)->save('./thumb.png');
// 居中裁剪
$image->thumb(150,150, \think\Image::THUMB_CENTER)->save('./thumb.png');
// 右下角剪裁
$image->thumb(150,150,\think\Image::THUMB_SOUTHEAST)->save('./thumb.png');
~~~

## 使用flip可以对图像进行翻转操作，默认是以x轴进行翻转
~~~
$image = \think\Image::open('./image.png');
// 对图像进行以x轴进行翻转操作
$image->flip()->save('./filp_image.png');
// 对图像进行以y轴进行翻转操作
$image->flip(\think\image::FLIP_Y)->save('./filp_image.png');
~~~

## 使用rotate可以对图像进行旋转操作（默认是顺时针旋转90度）
~~~
$image = \think\Image::open('./image.png');
// 对图像使用默认的顺时针旋转90度操作
$image->rotate()->save('./rotate_image.png');
~~~

## 系统支持添加图片及文字水印
~~~
$image = \think\Image::open('./image.png');
// 给原图左上角添加水印并保存water_image.png
$image->water('./logo.png')->save('water_image.png'); 
// 给原图左上角添加水印并保存water_image.png
$image->water('./logo.png', \think\Image::WATER_NORTHWEST)->save('water_image.png');
// 给原图左上角添加透明度为50的水印并保存alpha_image.png
$image->water('./logo.png', \think\Image::WATER_NORTHWEST, 50)->save('alpha_image.png');
// 给图片添加文字水印（我们复制一个字体文件HYQingKongTiJ.ttf到入口目录）生成一个像素20px，颜色为#ffffff的水印效果
$image->text('为API开发设计的高性能框架', 'HYQingKongTiJ.ttf', 20, '#ffffff')->save('text_image.png');
~~~
