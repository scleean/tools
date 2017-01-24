# PHP 工具函数 - 安全验证


#### 检查mysql注入

~~~
/**
* 检查一个get或者post数据是否含有注入语句
* @param string $str 输入的字符串
* @return bool
**/
function inject_check($str) 
{
    $check = preg_match('/select|insert|update|delete|\'|\/\*|\*|\.\.\/|\.\/|union|into|load_file|outfile/i', $str);
    return $check;
}
~~~

#### 浏览器检测 
> 判断是不是微信
~~~
/**
* 检查判断是不是微信浏览器
* @param string $str 输入的字符串
* @return bool
**/
function is_weixin()
{
if ( strpos($_SERVER['HTTP_USER_AGENT'], 'MicroMessenger') !== false ) {
        return true;
    }
        return false;
}
~~~
