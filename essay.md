##1 . 乱码问题
```php
iconv("UTF-8","gbk",$new);(linux上需安装libiconv才支持iconv函数)

php页面为utf编码 
header("Content-type: text/html; charset=utf-8"); 

php页面为gbk编码 
header("Content-type: text/html; charset=gb2312"); 

```
##2 . php更改文件名称
```php
rename('oldfilename','newfilename')
```
##4 . php对象转数组
```php
$array = get_object_vars($obj);
```
##5 . yii header下载文件
```php
public function actionImages() {
        $path = User::get_url();
        $filename = $path["path"];
//        var_dump($filename);die();
        $out_filename = $path["name"];
        if( ! file_exists($filename)){
            echo 'Not Fond';exit();
        } else {
            header('Accept-Ranges:bytes');
            header('Accept-Length:'.filesize($filename));
            header('Content-Transfer-Encoding:binary');
            header('Content-type:application/octet-stream');
            header('Content-Disposition: attachment; filename='.$out_filename);
            header('Content-Type: application/octet-stream;name='.$out_filename);
            if(is_file($filename) && is_readable($filename)){
                $file = fopen($filename,'r');
                echo fread($file,filesize($filename));
                fclose($file);
            }
        }
```
## 6 . HTML中设置多个class属性的优先级
```php
css样式的优先级 是在加载css文件的时候就确定下来的,和后来html里class属性位置前后无关。

```
## 7 . yii打印最后一条sql
```php
echo $query->createCommand()->getRawSql()
```
## 8 . php.ini修改php上传文件大小限制
```php
打开php.ini，首先找到
file_uploads = on ;是否允许通过HTTP上传文件的开关。默认为ON即是开
upload_tmp_dir ;文件上传至服务器上存储临时文件的地方，如果没指定就会用系统默认的临时文件夹
upload_max_filesize = 8m ;望文生意，即允许上传文件大小的最大值。默认为2M
post_max_size = 8m ;指通过表单POST给PHP的所能接收的最大值，包括表单里的所有值。默认为8M
一般地，设置好上述四个参数后，上传<=8M的文件是不成问题，在网络正常的情况下。
但如果要上传>8M的大体积文件，只设置上述四项还一定能行的通。

进一步配置以下的参数
max_execution_time = 600 ;每个PHP页面运行的最大时间值(秒)，默认30秒
max_input_time = 600 ;每个PHP页面接收数据所需的最大时间，默认60秒
memory_limit = 8m ;每个PHP页面所吃掉的最大内存，默认8M
把上述参数修改后，在网络所允许的正常情况下，就可以上传大体积文件了
max_execution_time = 600
max_input_time = 600
memory_limit = 32m
file_uploads = on
upload_tmp_dir = /tmp
upload_max_filesize = 32m
post_max_size = 32m

```

## 9 . yii2.0 goback跳转问题
```php
goback()要先设置一下返回地址,代码:
 Yii::$app->user->setReturnUrl(Yii::$app->request->referrer); 
```
## 10 . 提取链接中的数字
```php
function findNum($str=''){
        $str=trim($str);
        if(empty($str)){return '';}
        $temp=array('1','2','3','4','5','6','7','8','9','0');
        $result='';
        for($i=0;$i<strlen($str);$i++){
            if(in_array($str[$i],$temp)){
                $result.=$str[$i];
            }
        }
        return $result;
    }
```
## 11 . yii框架 不加在jq
```php
在/config/web.php中:
components数组中 添加;

        'assetManager'=>[
            'bundles'=>[
                'yii\web\JqueryAsset'=>[
                    'jsOptions'=>[
                        'position'=>\yii\web\View::POS_HEAD,
                    ]
                ]
            ]
        ],

```
## 12 . 前台if判断
```php
<?php if(!empty($name[1])){?>
         		<h3><?php echo $name[1]?></h3>
                    <?php }else{?>
         		<h3>用户名</h3>
     			<?php }?>

```

## 13 . jquery操作select下拉框：取值，赋值，删除
```php
-13.1.jquery对select的取值
        <select id="test">  
        <option value ="1">测试1</option>  
        <option value ="2">测试2</option>  
        <option value="3" >测试3</option>  
        <option value="4" >测试4</option>  
        </select>
        用上面的select举例说明：
        取得value: var value=$("#test").val();
        取得text:    var text=$("#test").find("option:selected").text();
        获取Select选择的索引值: var checkIndex=$("#test ").get(0).selectedIndex;
        获取Select最大的索引值: var maxIndex=$("#test  option:last").attr("index");

-13.2.jquery对select的赋值
        jquery对select的动态赋值，动态赋值是实际项目中用的最多的,往往和下拉框的二级联动用在一起。
        //获得收费单位动态赋值给下拉框
                function getCityList(){
                    var provCd=$("#provList").val();
                    var billStyle=$("#billStyle").val();
                    if(provCd==""||billStyle=="")
                        return;
                    var optionstring="";
                    $("#cityList").empty();
                    $.ajax({
                    url:'<%=root%>/employ/bmfwAction!getBillCompanyBilProvCdAndType',   
                    type:'post', 
                    data:'billStyle='+billStyle+'&provCd='+provCd,
                    success:function(data){
                        $.each(data,function(key,value){  //循环遍历后台传过来的json数据
                            optionstring += "<option value=\"" + value.billMchntCd + "\" >" + value.billNm + "</option>";
                        });
                        $("#cityList").html("<option value=''>请选收费单位</option> "+optionstring); //获得要赋值的select的id，进行赋值
                    }
                });
                }


        -13.2.1下面的追加option
           $("#test").append("<option value='5'>测试5</option>");   //为Select追加一个Option(下拉项)
           $("#test").prepend("<option value='0'>测试6</option>");   //为Select插入一个Option(第一个位置)


-13.3.jquery对select的删除

         $("#test").empty();用的最多 
         $("#test  option:last").remove();   //删除Select中索引值最大Option(最后一个)
         $("#test  option[index='0']").remove();   //删除Select中索引值为0的Option(第一个)
         $("#test  option[value='3']").remove();   //删除Select中Value='3'的Option
         $("#test  option[text='4']").remove();   //删除Select中Text='4'的Option

```

## 14 . PHP中设置error_reporting错误报告级别(例如 foerach 下标报错)
```php
error_reporting = E_ALL & ~E_NOTICE
```

## 15. jq动态加载表格和分页
```javascript
 $(function(){
        var sign = 'exhibition';
        $.ajax({
            url:'/default/exhibition',
            dataType:"json",
            type:'post',
            data:{sign:sign},
            success:function(data) {
                var s_data =data.s_data;
                if (data.code == 1) {
                    var exhibition = $("#exhibition");
                    exhibition.empty();
					for(var i=0;i<s_data.length;i++) {
						var option = $("<option>").text(s_data[i].hui_nickname).val(s_data[i].checkin_id);
						exhibition.append(option);
					}
                    var exh = $("#exhibition").val();
                    $.ajax({
                        url:'/default/change-show',
                        dataType:"json",
                        type:'post',
                        data:{exh:exh},
                        success:function(data) {
                            var title = data.final;
                            var name = data.new;
                            var xb = data.data1;


                            //分页
                            var test = data.page;
                            $('.M-box3').pagination({
                                pageCount: test,
                                jump: true,
                                coping: true,
                                homePage: '首页',
                                endPage: '末页',
                                prevContent: '上页',
                                nextContent: '下页',
                                callback: function (api) {
                                    $.ajax({
                                        type: "POST",
                                        dataType: "json",
                                        url: '/default/change-show',
                                        data: {
                                            "num": api.getCurrent(),
                                            "exh": exh,
                                        },
                                        success: function(res) {
                                            var li_new = res.li_new;
                                            // console.log(li_new);return false;
                                            var str = "<tr style='background: lightgrey'>";
                                            $.each(title,function(i){
                                                str += "<th>"+title[i]+"</th>";
                                            });
                                            str += "</tr>";
                                            $.each(li_new,function(s){
                                                str += "<tr>";
                                                for(var m=0;m<title.length;m++ ){
                                                    if(li_new[s][title[m]] == null || li_new[s][title[m]] == ''){
                                                        if(title[m] == '操作'){
                                                            str += "<td>"+
                                                                '<a class="layui-btn layui-btn-danger layui-btn-xs edit delete" id="">删除</a>'
                                                                // "<a class='layui-btn layui-btn-danger layui-btn-xs edit delete' edit='edit' id='data3[s].czz_id' lay-event='del'>删除</a>"
                                                                + "</td>";
                                                        }else {
                                                            str += "<td>" +
                                                                '-'
                                                                + "</td>";
                                                        }

                                                    }else {
                                                        str += "<td>" +
                                                            li_new[s][title[m]]
                                                            + "</td>";
                                                    }
                                                }

                                                str += "</tr>";
                                            });
                                            $("#te_table").html(str);


                                        }
                                    });

                                }
                            });

                            //加载table

                            var str = "<tr style='background: lightgrey'>";
                            $.each(title,function(i){
                                str += "<th>"+title[i]+"</th>";
                            });
                            str += "</tr>";
                            $.each(name,function(s){
                                str += "<tr>";
                                for(var m=0;m<title.length;m++ ){
                                    if(name[s][title[m]] == null || name[s][title[m]] == ''){
                                        if(title[m] == '操作'){
                                            str += "<td>" +
                                                '<a class="layui-btn layui-btn-danger layui-btn-xs edit delete" edit="edit" id="" lay-event="del">删除</a>'
                                                + "</td>";
                                        }else {
                                            str += "<td>" +
                                                '-'
                                                + "</td>";
                                        }
                                    }else {
                                        str += "<td>" +
                                            name[s][title[m]]
                                            + "</td>";
                                    }
                                }
                                str += "</tr>";
                            });
                            $("#te_table").html(str);
                        }
                    });

                }
            }
        });
    });

```

## 16 . php开启短标签(yii2 前台写php代码报错 } )
```
在php.ini（配置文件）中设置为on: 
short_open_tag = On
```

## 17 . 搜索引擎选择： Elasticsearch与Solr
```php

```

## 18 . a连接提交form表单

```javascript

<a href="javascript:document.form1.submit();" type="submit" class="info-btn-c">确认信息</a>

```

## 19 . 二维数组去重
```php
 function array_unset_tt($arr,$key){
        //建立一个目标数组
        $res = array();
        foreach ($arr as $value) {
            //查看有没有重复项
            if(isset($res[$value[0][$key]])){
                unset($value[0][$key]);  //有：销毁
            }else{
                $res[$value[0][$key]] = $value;
            }
        }
        return $res;
    }
```
## 20. yii 更改字段+1
```php
User::updateAllCounters(['total'=>5], ['status'=>1])
翻译为sql语句大概就是：
UPDATE User SET total=total+5 WHERE status=1
```

## 21. jq判断checkbox是否被选中
```javascript
//jq判断checkbox是否被选中
$('#checkbox9').is(':checked')
//移除数组最后一位
shopid.pop();
//jq像数组插入值
array.push()
```

## 22. php获取字符串中的数字
```php
$patterns = "/\d+/";//结合正则获取字符串中数字
preg_match_all($patterns,$specifications,$arr);




 public static function price($hui_id,$type_name,$area){

        $query = BaoJia::find();
        $query->select("h.unit_yu_price,from_unixtime(h.create_time,'%Y-%m-%d %H:%i:%s') `create_time`");
        $query->from('hui_goods as h');
        $query->innerJoin('goods_type as ty','ty.goods_type_id=h.type_id');
        $query->where('status = 0');
        if(!empty($hui_id)){
            $query->andWhere(['h.hui_id'=>$hui_id]);
        }
        $query->andWhere(['ty.type_name'=>$type_name]);
        $query->andWhere(['h.goods_name'=>$area]);
        $res =$query->asArray()->all();
//        echo $query->createCommand()->getRawSql();die();
        return $res;
    }
```
## 23. yii更新操作
```php
 return GoodsShopcar::updateAll(['num'=> $num], ['id'=>$goods_id]);

$sql1 ="UPDATE goods_shopcar SET num = " .$num.',specifications='."'".$spec."'".',update_time='.$create_time.',money='.$money ." where czs_number =".$czs_number." and name ="."'".$entry;
$res = \Yii::$app->db->createCommand($sql1)->queryAll();
```

## 24. 微信登陆相关
```php
$code = $_GET['code'];
$url = "https://api.weixin.qq.com/sns/oauth2/access_token?appid=wx37c8063768cbe505&secret=e597ad28b7637165c4d700605e506787&code={$code}&grant_type=authorization_code";
$str= file_get_contents($url);
$access = json_decode($str,true);
$token = $access['access_token'];
$openid = $access['openid'];
$userUrl = "https://api.weixin.qq.com/sns/userinfo?access_token={$token}&openid={$openid}&lang=zh_CN ";
$user = file_get_contents($userUrl);
$open = json_decode($user);
```
```php
微信网页授权access_token和普通access_token区别:

有效期：两者有效时间都是7200s。
使用范围：通过网页授权获得的access_token，只能获取到对应的微信用户信息，与微信用户是一对一关系；而普通的access_token在有效期内可以使用，可以获取所有用户信息。
次数限制：普通access_token每天获取最多次数为2000次，而网页授权的access_token获取次数没有限制。

获取网页授权access_token(返回token和openid):
$url = "https://api.weixin.qq.com/sns/oauth2/access_token?appid=wx37c8063768cbe505&secret=e597ad28b7637165c4d700605e506787&code={$code}&grant_type=authorization_code";

获取普通access_token(只返回token):
$url =  "https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=wx37c8063768cbe505&secret=e597ad28b7637165c4d700605e506787";
           
获取微信用户基本信息           
$userUrl = "https://api.weixin.qq.com/sns/userinfo?access_token={$token}&openid={$openid}&lang=zh_CN ";           
```