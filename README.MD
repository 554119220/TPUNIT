# PHP框架ThinkPHP单元测试库:TPUNIT
## 一、概述：
thinkphp本身并没有提供相应的单元测试支持，所以本库的目的是将thinkphp中的一些功能集合起来打包成一个库，
使大家可以通过只需导入本库，便可对thinkphp进行单元测试，从而保证软件的质量。
特点是：易用，方便，非入侵式(部分方法除外)
支持版本：ThinkPHP3.2.3

## 二、使用步骤
1. 定义TP_BASEPATH常量
2. 导入base.php库
3. 导入欲测试的文件
4. 使用phpunit运行单元测试

## 三、详细使用步骤

在Appcation下创建一个新的文件夹test，并新建一个测试类，命名为IndexTest.php。
其代码为：
<pre><code>
class IndexTest extends PHPUnit_Framework_TestCase{
    //构造函数
    function __construct(){
    	//定义目录路径，最好为绝对路径
    	define('TP_BASEPATH', 'E:/www/novel/');
		//导入base库
		include_once 'E:\www\novel\Application\test\base.php';
		//导入要测试的控制器
		include_once 'E:\www\novel\Application\Home\Controller\IndexController.php';
    }
	//测试index动作
    public function testIndex(){
    	//新建控制器
        $index=new \Home\Controller\IndexController();
		//调用控制器的方法
		$index->test();
		//断言
		$this->expectOutputString('123');
    }

}
</code></pre>
Index控制器为：
<pre><code>
namespace Home\Controller;
use Think\Controller;
class IndexController extends Controller {
    function test(){
    	echo 123;
	}
}
</code></pre>
然后运行phpunit进行单元测试：
phpunit E:\\www\\novel\\Application\\test\\IndexTest.php

## 四、使用注意
由于thinkphp代码中，ajaxReturn是使用exit进行处理的，所以导致了使用ajaxReturn的时候，会造成无法进行单元测试。
所以本库对ajaxReturn进行了一些修改，在使用的时候，需要加上return。
比如：
$this->ajaxReturn('abc');
现在需写为：
$this->ajaxReturn('abc');
return;

整个库中，目前只有该方法是入侵式的。


