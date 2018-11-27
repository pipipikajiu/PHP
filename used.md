## 1 . yii2.0
```php
- 1.1 .request组件(很多命令):
isGet
userIP
$request = \Yii::$app->request;
$id = $request->get('id',1);(post);

合成一个数组
compact('数组名','数组名');

- 1.2 .视图分配:
return $this->render('index',$data);(渲染父模板)
return $this->renderPartial('index',$data);(不渲染父模板)

yii处理字符串方法:
use \yii\helpers\Html
use \yii\helpers\HtmlPurifier::process();(把标签处理掉)

<?= Html::encode();?>
<?= HtmlPurifier::process();( ?>


- 1.3 . 定义父模板
controller中:
public $layout = 'home';// 用属性的方法定义父模板

在父模板中 <?$content;?>


两个view 要相互调用
<?php echo $this->render('about')  ?>

- 1.4 . 操作model
继承基类:
use \yii\db\ActiveRecord
extends ActiveRecord



在c层 use app\models\文件名
文件名::findBySql($sql)->all();

- 1.5 . 预防sql注入(添加占位符)
$id = 1;
$sql="select * from user where id=:id";
文件名::findBySql($sql,[:id=>$id])->all();

- 1.6 . where表单查询
文件名::find()->where(['id'=>5])->all();
文件名::find()->where(['>','id',3)->all();
文件名::find()->where(['between','id',2,5])->all();
文件名::find()->where(['like','title','巴菲特'])->all();

->one();

文件名::findOne (findAll)

- 1.6 . yii大数据节省内存处理
文件名::find()->asArray()->all();(对象转化为数组)

foreach(文件名::find()->batch(2) as $arr){
    $data[] = $arr;
}

- 1.7 . 插入数据
save()
insert()

获取插入数据id:
文件名->attributes['id'];

- 1.8 . 
update
save
更新单个字段:
文件名:: updateAllCounters(['num'=>1],[],'id'=>10]);(把id为10的数据num加1)
```
## 2 . 常用
```php
ajax:

function checkUser(user_info,obj){
	$.ajax({
		url:'/Bank/Task/checkUser',
		type:'post',
		data:user_info,
		dataType:'json',
		success:function(re){
			obj.html(re.tips);
			if(re.flag==1){
				$('#user_pwd').css('display','block');
				$('#userName').html($('input[name="id_code"]').val());
				if(tag){
					$('input[name="name"]').val('').prop('readonly',false).css('background','#fff');
					tag=true;
				}
				$('input[name="tel"]').prop('readonly',false).val('').css('background','#fff');
			}else{
				tag=true;
				$('#user_pwd').css('display','block');
				$('#userName').html(re.user_name);
				$('#pw').css('display','none');
				$('input[name="name"]').val(re.name).prop('readonly',true).css('background','#eee');
				$('input[name="tel"]').val(re.tel).prop('readonly',true).css('background','#eee');
			}
		}
	});
}

```

