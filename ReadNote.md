# 读书笔记

标签（空格分隔）： 

7月10号
=====

学习使用到的git命令：
------------

    （1）git撤销commit但未push的内容：git reset <commit id>
    （2）git查看commit但未push的内容：git log master ^origin/master
    （3）git提交指定文件到暂存区：git commit -m "文件路径"
            eg:git commit -m "protected\modules\backend\views\malbum\_form.php"
    （4）git 解决pull冲突：
            先将本地修改暂时存储起来：git stash
            然后pull：git pull
            最后还原暂存的内容：git stash pop stash@{0}
    （5）查看远程分支：git branch -a
    （6）创建本地相应远程分支：git checkout -b mobile origin/mobile
    （7）切换分支：git checkout 分支名
    （9）查看状态：git status
    (10) 添加modifed文件：git add -u
    (11) 添加add文件： git add -a
    （12）添加指定文件： git add 文件路径

----------

7月21号
=====

??的用法
------------
举例：
$a = [];
$b = $a['b'] ?? '';
$a['b']是不存在的，用??
$c = $a ?: '';
$a存在，所以用?:

----------
8月11号
----------

static关键字
---------
一、介绍
Static方法属于整个类，即使不用创建对象也能直接调用，
静态方法的原理，共享代码段；静态变量的原理，共享数据段，
静态方法和静态变量会使用同一块内存，而实例化则会创建不同的内存，
所以静态方法的效率比实例化高，但静态方法不能做到自动销毁，实例化可以，
静态方法内部只能出现Static变量和Static方法，不能使用this，因为属于整个类，静态成员不能访问非静态成员，而非静态成员可以访问静态成员。
二、使用
PHP中访问类的方法和用户有两种方法：
1、创建对象，$object = new model(),使用"->"调用
2、直接调用，Model::方法名/变量，静态，非静态都可以，前提条件：
A. 如果是变量，需要该变量可访问。
B. 如果是方法，除了该方法可访问外，还需要满足：
b1) 如果是静态方法，没有特殊条件；
b2) 如果是非静态方法，需要该方法中没有使用$this，即没有调用非静态的变量/方法，当然，调用静态的变量/方法没有问题。 
4，$object->… 和Model::…的区别：
a.使用$object->… ，需要执行构造函数创建对象；
b.使用class::… 调用静态方法/变量，不需要执行构造函数创建对象；
c.使用class::… 调用非静态方法/变量，也不需要执行构造函数创建对象。

Yii框架
-----
一、YII2.0中，使用updateCounter/updateAllCounter（['字段' => 加量]）更新字段增加对应加量

二、save，load，validate方法
1、load()加载数据，validate()验证数据
2、更新和添加都可以用save()
因为save会先调用validate()再执行insert或者update，
Yii会通过$model->isNewRecord来判断是否是一条新记录，然后调用insert或者update，

    public function save($runValidation = true, $attributeNames = null)
    {
        if ($this->getIsNewRecord()) {
            return $this->insert($runValidation, $attributeNames);
        } else {
            return $this->update($runValidation, $attributeNames) !== false;
        }
    }

3、当你调用save，insert，update方法的时候都会先调用validate

三、一般Gii生成的Model最后一行的字段都是safe（用户输入什么内容都是安全的，不需要规则）

