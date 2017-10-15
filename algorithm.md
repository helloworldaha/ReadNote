# 算法

标签（空格分隔）： 未分类

---

国庆长假前，公司大佬出了道算法题给我和另一个同事，题目如下：
给一个int数组，一个目标值，封装成一个函数，返回值是存在在这个数组中的目标值减与数组元素的差。要求：时间复杂度为n

(￣▽￣)ノ
暗自窃喜

这么简单的算法题，对于世界上最好的语言PHP来说，简直So easy！

我和大佬说了下我的思路，大致是：用for循环，然后用目标值依次减去数组里的每一个元素，获得的差再用array_search()，大佬提示我：要求是时间复杂度为n，在for循环里用array_search()就不符合这个要求了，因为这个函数在实现的时候也用了for循环。

ლ(ಥ Д ಥ )ლ

不能在循环里用各种功能强大的array函数了！
༼☯﹏☯༽

黔驴技穷了！

_(：3 」∠ )_

然后我就觉得以自己的脑子是想不出来办法了

OTZ

于是去请教同事

果然聪明机智的同事很快就写完了，他告诉我可以用交集

┌(▀Ĺ̯▀)┐？？？

具体思路如下：
把计算出的差值放进一个数组里，然后把这个差值数组和原数组进行交集运算，那么这个交集就是我们需要的返回值啦！

୧༼ʘ̆ںʘ̆༽୨

代码如下：

    function calculate($arr, $target) {
    	$arr_length = count($arr);
    	$return = [];
    	for ($i = 0; $i < $arr_length; $i++) {
    		$subtraction[] = $target - $arr[$i];
    	}
    	$intersect = array_intersect($arr, $subtraction);
    	$return = array_keys($intersect);
    	return $return;
    }
    $arr = [1, 2, 3, 4, 5, 6];
    $target = 11;
    var_dump(calculate($arr, $target));













