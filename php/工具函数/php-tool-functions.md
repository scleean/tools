# PHP 工具函数 - 安全验证


## 安全处理

#### 检查mysql注入
~~~
/**
* 检查一个数据是否含有注入语句
* 
* 使用preg_match()搜索是否存在敏感字符, 存在返回匹配次数1,不存在返回匹配次数0
* 忽略大小写
* @param string $str 输入的字符串
* @return int
**/
function inject_check($str) 
{
    $check = preg_match('/select|insert|update|delete|\'|\/\*|\*|\.\.\/|\.\/|union|into|load_file|outfile/i', $str);
    return $check;
}
~~~
>使用 echo injCheck('1 or 1=1');

##环境以及客户端监测

### 浏览器检测 

#### 判断是不是微信
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

### 获取用户真实IP
~~~
/**
 * 获取客户端真实的ip地址
 * @return string
 */
function getIp()
{
    if (getenv("HTTP_CLIENT_IP") && strcasecmp(getenv("HTTP_CLIENT_IP"), "unknown")) {
        $ip = getenv("HTTP_CLIENT_IP");
    } else {
        if (getenv("HTTP_X_FORWARDED_FOR") && strcasecmp(getenv("HTTP_X_FORWARDED_FOR"), "unknown")) {
            $ip = getenv("HTTP_X_FORWARDED_FOR");
        } else {
            if (getenv("REMOTE_ADDR") && strcasecmp(getenv("REMOTE_ADDR"), "unknown")) {
                $ip = getenv("REMOTE_ADDR");
            } else {
                if (isset ($_SERVER['REMOTE_ADDR']) && $_SERVER['REMOTE_ADDR'] && strcasecmp($_SERVER['REMOTE_ADDR'], "unknown")) {
                    $ip = $_SERVER['REMOTE_ADDR'];
                } else {
                    $ip = "unknown";
                }
            }
        }
    }
    return ($ip);
}
~~~
> 使用 echo getIp();