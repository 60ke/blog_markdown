---
title: PHP常用类库
date: 2016-03-06 05:50:00
categories: php
tags: []
urlname: 22
---
PHP常用类库
<!--more-->
数组类

class libArray
{
    /**
     * 多维数组合并
     * @return array
     */
    public static function merge ()
    {
        $args = func_get_args();
        $array = [];
        foreach ( $args as $arg ) {
            if ( is_array($arg) ) {
                foreach ( $arg as $k => $v ) {
                    if ( is_array($v) ) {
                        $array[$k] = isset($array[$k]) ? $array[$k] : [];
                        $array[$k] = self::merge($array[$k], $v);
                    } else {
                        $array[$k] = $v;
                    }
                }
            }
        }
        return $array;
    }

    /**
     * 多维to一维
     * [1=>['a'=>'v1']] to ['1|a'=>'v1']
     * @param array $array
     * @param string $delimiter
     * @param string $key
     * @return array
     */
    public static function mTo1 (array $array, $delimiter = '|', $key = '')
    {
        $data = [];
        if ( !is_array($array) ) {
            return $data;
        }
        foreach ( $array as $k => $v ) {
            $keyNew = trim($key.$delimiter.$k, $delimiter);
            if ( is_array($v) ) {
                $data = array_merge($data, self::mTo1($v, $delimiter, $keyNew));
            } else {
                $data[$keyNew] = $v;
            }
        }
        return $data;
    }

    /**
     * 数组排序
     * @param array $array
     * @param $column
     * @param bool $reverse
     * @return bool
     */
    public static function sort (array &$array, $column, $reverse = FALSE)
    {
        $arrColumn = [];
        foreach ( $array as $key => $val ) {
            $arrColumn[$key] = $val[$column];
        }
        return array_multisort($arrColumn, $reverse ? SORT_DESC : SORT_ASC, $array);
    }

    /**
     * 添加索引
     * @param array $array
     * @param $key
     * @return array
     */
    public static function index (array $array, $key)
    {
        $ret = [];
        foreach ( $array as $val ) {
            $ret[$val[$key]] = $val;
        }
        return $ret;
    }

    /**
     * 添加前后缀
     * @param $array
     * @param null $pre
     * @param null $suf
     * @return array
     */
    public static function addFix (array $array, $pre = NULL, $suf = NULL)
    {
        $ret = [];
        foreach ( $array as $key => $val ) {
            $ret[$key] = $pre.$val.$suf;
        }
        return $ret;
    }
}
数据检查类

class libCheck
{
    /**
     * 是否为IP（IPv4）
     * @param $ip
     * @return bool
     */
    public static function isIP ($ip)
    {
        $isIP = filter_var($ip, FILTER_VALIDATE_IP) ? TRUE : FALSE;
        return $isIP;
    }

    /**
     * 是否为邮箱地址
     * @param $mail
     * @return bool
     */
    public static function isMail ($mail)
    {
        $isMail = filter_var($mail, FILTER_VALIDATE_EMAIL) ? TRUE : FALSE;
        return $isMail;
    }

    /**
     * 是否为URL
     * @param $url
     * @return bool
     */
    public static function isURL ($url)
    {
        $isMail = filter_var($url, FILTER_VALIDATE_URL) ? TRUE : FALSE;
        return $isMail;
    }

    /**
     * 是否为正整数
     * @param $num
     * @return bool
     */
    public static function isPosiInt ($num)
    {
        $isPosiInt = is_int($num) && $num > 0;
        return $isPosiInt;
    }

    /**
     * 是否在范围内
     * @param $num
     * @param int $min
     * @param null $max
     * @return bool
     */
    public static function isBetween ($num, $min = 0, $max = NULL)
    {
        $isBetween = $num >= $min;
        if ( $max ) {
            $isBetween = $isBetween && $num <= $max;
        }
        return $isBetween;
    }

    /**
     * 是否为有效长度
     * @param $str
     * @param int $min
     * @param null $max
     * @return bool
     */
    public static function isValidLen ($str, $min = 1, $max = NULL)
    {
        $length = mb_strlen($str);
        $isValidLen = self::isBetween($length, $min, $max);
        return $isValidLen;
    }
}
文件类

class libFile
{
    /**
     * 获取目录下所有文件
     * @param $path
     * @return array
     */
    public static function getFiles ($path)
    {
        $path = self::formatePath($path);
        if (!is_dir($path)) {
            return [];
        }
        $dh = opendir($path);
        $files = [];
        while ( ($filename = readdir($dh)) !== FALSE ) {
            if ( $filename != '.' && $filename != '..' ) {
                $files[] = implode('/', [$path, $filename]);
            }
        }
        closedir($dh);
        return $files;
    }

    /**
     * 按模式取目录下文件
     * @param $path
     * @param $pattern
     * @return array
     */
    public static function getFilesByPattern ($path, $pattern)
    {
        $path = self::formatePath($path);
        $filePattern = sprintf('%s/%s', $path, $pattern);
        return glob($filePattern);
    }

    /**
     * 递归删除文件夹
     * @param $dir
     * @return bool
     */
    public static function rmDir($dir)
    {
        $dir = self::formatePath($dir);
        $dh = opendir($dir);
        while ($filename = readdir($dh)) {
            if ($filename != '.' && $filename != '..') {
                $path = sprintf('%s/%s', $dir, $filename);
                is_dir($path) ? self::rmDir($path) : unlink($path);
            }
        }
        closedir($dh);
        return rmdir($dir);
    }

    /**
     * 获取最后修改时间
     * @param $path
     * @return int
     */
    public static function getModifiedTime ($path)
    {
        return filemtime($path);
    }

    /**
     * 格式化路径
     * @param $path
     * @return string
     */
    public static function formatePath ($path)
    {
        return rtrim($path, '/');
    }
}
HTTP类

class libHttp
{
    /**
     * GET方法
     * @param $url
     * @param array $options
     * @return bool|mixed
     */
    public static function get ($url, $options = [])
    {
        return self::send($url, NULL, NULL, $options);
    }

    /**
     * POST方法
     * @param $url
     * @param array $params
     * @param array $options
     * @return bool|mixed
     */
    public static function post ($url, $params = [], $options = [])
    {
        return self::send($url, 'POST', $params, $options);
    }

    /**
     * @param $url
     * @param string $method
     * @param array $params
     * @param array $options
     * @return mixed|string
     */
    public static function send ($url, $method = 'GET', $params = [], $options = [])
    {
        $ch = curl_init($url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
        curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 30);
        if ($method == 'POST') {
            $options[CURLOPT_POST] = TRUE;
            $options[CURLOPT_POSTFIELDS] = $params;
        }
        curl_setopt_array($ch, $options);
        $result = curl_exec($ch);
        return curl_errno($ch) ? curl_error($ch) : $result;
    }
}
字符串类

class libString
{
    /**
     * 随机字符串
     * @param int $length
     * @param bool $num
     * @param bool $lower
     * @param bool $upper
     * @return string
     */
    public static function rand ($length=5, $num=TRUE, $lower=TRUE, $upper=TRUE)
    {
        $str = '';
        $num && $str .= '0123456789';
        $lower && $str .= 'abcdefghijklmnopqrstuvwxyz';
        $upper && $str .= 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
        $rand = substr(str_shuffle($str), -$length);
        return $rand;
    }

    /**
     * 字符串截取（单次）
     * @param $ld
     * @param $rd
     * @param $str
     * @return string
     */
    public static function sub ($ld, $rd, $str)
    {
        $start = strpos($str, $ld) + strlen($ld);
        $end = strpos($str, $rd, $start);
        $data = substr($str, $start, $end - $start);
        return $data;
    }

    /**
     * 字符串截取（批量）
     * @param $ld
     * @param $rd
     * @param $str
     * @return array
     */
    public static function subs ($ld, $rd, $str)
    {
        $data = [];
        $lLen = strlen($ld);
        $rLen = strlen($rd);
        $offset = 0;
        while ( ($start = strpos($str, $ld, $offset)) !== FALSE ) {
            $start += $lLen;
            $end = strpos($str, $rd, $start);
            $data[] = substr($str, $start, $end - $start);
            $offset = $end + $rLen;
        }
        return $data;
    }

    /**
     * 生成唯一ID
     * @return string
     */
    public static function uniqid ()
    {
        return md5(uniqid(rand(), true));
    }
}
其它工具类

class libTool
{
    /**
     * ip->int
     * @param $ip
     * @return string
     */
    public static function ip2long ($ip)
    {
        $long = sprintf('%u', ip2long($ip));
        return $long;
    }

    /**
     * 系统负载
     * @return mixed
     */
    public static function loadAvg ()
    {
        $load = sys_getloadavg()[0];
        return $load;
    }

    /**
     * 写日志文件
     * @param $file
     * @param $msg
     * @param bool $newLine
     */
    public static function log ($file, $msg, $newLine = TRUE)
    {
        $newLine && $msg .= "\n";
        file_put_contents($file, $msg, FILE_APPEND);
    }

    /**
     * 内存使用峰值(M)
     * @return float
     */
    public static function memoryUsage ()
    {
        $memory = memory_get_peak_usage(TRUE) / pow(1024, 2);
        $memory = round($memory, 2);
        return $memery;
    }

    /**
     * 浏览器变量输出
     * @param $var
     * @param bool|FALSE $return
     * @param bool|TRUE $strict
     * @return bool|mixed|string
     */
    public static function dump ($var, $return = FALSE, $strict = TRUE)
    {
        if (!$strict) {
            if (ini_get('html_errors')) {
                $output = print_r($var, TRUE);
                $output = sprintf('<pre>%s</pre>', htmlspecialchars($output, ENT_QUOTES));
            } else {
                $output = print_r($var, TRUE);
            }
        } else {
            ob_start();
            var_dump($var);
            $output = ob_get_clean();
            if (!extension_loaded('xdebug')) {
                $output = preg_replace('/\]\=\>\n(\s+)/m', '] => ', $output);
                $output = sprintf('<pre>%s</pre>', htmlspecialchars($output, ENT_QUOTES));
            }
        }

        if ($return) {
            return $output;
        } else {
            echo $output;
            return TRUE;
        }
    }
}