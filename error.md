# 工作上的失误

标签（空格分隔）： 未分类

公元2017年9月29日
--------------

版本比较
----

PHP有版本比较函数，不能将版本号直接进行字符串的比较。

公元2017年9月29日这天，因为我昨日无视公司大佬的嘱咐！执意参考错误的代码，导致错误的判断，把两个版本号直接进行字符串比较，导致APP线上的图标集体消失......ლ(ಥ Д ಥ )ლ

OTZ

以下是正确的代码：

    if (($os === $equipment::Android && version_compare($version, '3.5.8', '<=')) ||
            ($os === $equipment::iOS && version_compare($version, '4.0.2', '<'))) {
            $icons = [
                [
                    'id' => 1,
                    'path' => '/event',
                    'title' => '活动',
                    'normal' => 'd8465fd27e5914f9a4d8d4a2bbdfbbca',
                    'dark' => 'b750043bd845ec90e54fe19d3d0c5a5c',
                ],
                [
                    'id' => 6,
                    'path' => '/rank',
                    'title' => '排行',
                    'normal' => '72827cefa44e1f8eb523c6f9406b26fb',
                    'dark' => '972e5b890698d361e841e01d39c6e5dd',
                ],
                [
                    'id' => 3,
                    'path' => '/drama',
                    'title' => '广播剧',
                    'normal' => '5c92910140371717659819a8cf652543',
                    'dark' => 'fef6840b7a80a826b25bb7da5b2ac128',
                ],
                [
                    'id' => 5,
                    'path' => 'https://m.missevan.com/summerdrama',
                    'title' => '精品周更',
                    'normal' => '675ba333d46d35d452a05b2bab746290',
                    'dark' => 'dfd93afe5ab72d91ebfc3869ea60b928',
                ],
            ];
        } else {
            $icons = Yii::$app->memcache->get('ICON_LIST') ?: [];
        }


谨记版本号的判断要使用版本判断函数version_compare()！

以下是错误代码

OTZ

ლ(ಥ Д ಥ )ლლ(ಥ Д ಥ )ლლ(ಥ Д ಥ )ლლ(ಥ Д ಥ )ლლ(ಥ Д ಥ )ლ

千万不要学我！！！
千万不要再犯！！！

    $version < '3.5.8'
$version < '4.0.2'

公元2017年10月20日
------------

我又来记录了......

ᕕ(ಥʖ̯ಥ)ᕗ

今天的失误是由于想看发送验证码到邮箱的文案模板样式，结果改了一个获取模板的变量的值，

忘了改回来！！！！

༼ つ ˵ ╥ ͟ʖ ╥ ˵༽つ

结果就上线了！！！！


导致线上发邮件验证码的功能崩了！

还好测试及时发现！

希望以后能做到不更新这个笔记！

┌(▀Ĺ̯▀)┐
