```php
//控制器内使用,组装列表
//$list反正就是个数组列表
$query = $model->find();
$list  = $query->asArray()->all();
//列标题
$header = ['登录名','昵称','角色','级别','状态','最后登录时间','创建时间','交易账号','姓名','消息开关状态','用户积分','房间名称','房间ID','是否VIP'];
$datas = [];
foreach ($list as $k => $v) {
    // $excel->HandleLarge($times);
    $datas[$k]['登录名'] = $v['user_loginname'];
    $datas[$k]['昵称'] = $v['user_nickname'];
}
$name = '用户导出';
$this->ExcelPull($name, $header, $datas);


    //XLS导出
    /**
    $name  string 文件名称
    $header array 列标题
    $dataResult  数组
    **/
    public  function ExcelPull($name, $header, $dataResult)
    {
        //这一行没啥用,根据具体情况优化下
        $headTitle = "xx详情";
        $headtitle= "<tr style='height:50px;border-style:none;><td border=\"0\" style='height:90px;width:470px;font-size:22px;' colspan='11' >{$headTitle}</th></tr>";
        $titlename = "<tr>";
        foreach ($header as $v) {
            $titlename .= "<td>$v</td>";
        }
        $titlename .= "</tr>";
        $fileName = date("Y-m-d") . "-" . $name . ".xls";
        $this->excelData($dataResult, $titlename, $headtitle, $fileName);
    }


   public  function excelData($data, $titlename, $title, $filename)
    {
        $str = "<html xmlns:o=\"urn:schemas-microsoft-com:office:office\"\r\nxmlns:x=\"urn:schemas-microsoft-com:office:excel\"\r\nxmlns=\"http://www.w3.org/TR/REC-html40\">\r\n<head>\r\n<meta http-equiv=Content-Type content=\"text/html; charset=utf-8\">\r\n</head>\r\n<body>";
        $str .="<table border=1>" . $titlename;
        $str .= '';
        foreach ($data as $key => $rt) {
            $str .= "<tr>";
            foreach ($rt as $v) {
                $str .= "<td >{$v}</td>";
            }
            $str .= "</tr>\n";
        }
        $str .= "</table></body></html>";
        $str .= "<span>creator:".yii::$app->user->identity->user_loginname."</span>";
        header("Content-Type: application/vnd.ms-excel; name='excel'");
        header("Content-type: application/octet-stream");
        header("Content-Disposition: attachment; filename=" . $filename);
        header("Cache-Control: must-revalidate, post-check=0, pre-check=0");
        header("Pragma: no-cache");
        header("Expires: 0");
        exit($str);
    }



```
快速导出excel
```php
//导出excel格式表

function exportData($filename,$title,$data){
	header("Content-type: application/vnd.ms-excel");
	header("Content-disposition: attachment; filename="  . $filename . ".xls");
	if (is_array($title)){
		foreach ($title as $key => $value){
			echo $value."\t";
		}
	}
	echo "\n";
	if (is_array($data)){
		foreach ($data as $key => $value){
			foreach ($value as $_key => $_value){
				echo $_value."\t";
			}
			echo "\n";
		}
	}
}

```