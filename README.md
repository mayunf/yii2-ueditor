# yii2-ueditor
ueditor for yii，upload local or aliyunoss

## 安装

- run
```bash
composer require mayunfeng/yii2-ueditor -vvv
```

- or add

```bash
"mayunfeng/yii2-ueditor":"*"
```
then run

```bash
composer update
```

## 应用

参考:
[https://github.com/BigKuCha/yii2-ueditor-widget](https://github.com/BigKuCha/yii2-ueditor-widget)


- controller

```bash
public function actions()
{
    return [
        'upload' => [
            'class' => 'yii2\ueditor\UEditorAction',
        ]
    ];
}
```

- view
```bash
echo \yii2\ueditor\UEditor::widget(['name' => 'xxxx']);
```
or

```bash
echo $form->field($model,'colum')->widget('yii2\ueditor\UEditor',[]);
```

## 说明

> ueditor只支持2种语言，en-us和zh-cn,默认跟随系统语言 Yii::$app->language,可以通过2种方式设置，1.修改系统语言，在main.php(高级版) 或者web.php(基础版)添加'language' => 'zh-CN',。2.实例化的时候配置语言选项，见下边配置


## 配置相关
编辑器相关配置，请在view 中配置，参数为clientOptions，比如定制菜单，编辑器大小等等，具体参数请查看[UEditor官网文档](http://fex.baidu.com/ueditor/)。

简单实例：
```bash
use \yii2\ueditor\UEditor;
echo UEditor::widget([
    'clientOptions' => [
        //编辑区域大小
        'initialFrameHeight' => '200',
        //设置语言
        'lang' =>'en', //中文为 zh-cn
        //定制菜单
        'toolbars' => [
            [
                'fullscreen', 'source', 'undo', 'redo', '|',
                'fontsize',
                'bold', 'italic', 'underline', 'fontborder', 'strikethrough', 'removeformat',
                'formatmatch', 'autotypeset', 'blockquote', 'pasteplain', '|',
                'forecolor', 'backcolor', '|',
                'lineheight', '|',
                'indent', '|'
            ],
        ]
]);
```

文件上传相关配置，请在controller中配置，参数为config,例如文件上传路径等；更多参数请参照 config.php (跟UEditor提供的config.json一样)

简单实例:


```bash
public function actions()
{
    return [
        'upload' => [
            'class' => 'kucha\ueditor\UEditorAction',
            'config' => [
                "imageUrlPrefix"  => "http://www.baidu.com",//图片访问路径前缀
                "imagePathFormat" => "/upload/image/{yyyy}{mm}{dd}/{time}{rand:6}" //上传保存路径
                "imageRoot" => Yii::getAlias("@webroot"),
                "disk" => "oss" // 需要上传至阿里云oss，填写此项。否则会上传至本地
            ],
        ]
    ];
}
```

## 上传至阿里云

1. 需要安装`mayunfeng/aliyunoss`扩展。详见文档：[传送门](https://github.com/mayunf/yii2-aliyunoss)
2. config 中不要配置 `imageUrlPrefix` 参数。
3. config 中指定`disk` 值为 `oss`
3. 暂不支持查看oss中的文件列表



