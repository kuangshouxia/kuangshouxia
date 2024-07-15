狂收侠自助建站CMS程序的开发目的是为了帮助用户快速搭建、轻松管理、程序根据关键词和句子库自动生成内容，可以做影视站、文章站、以及泛站等等，操作很简单。 该程序没有后台，不需要数据库，安装php版本5.6就可以跑起来。降低建站成本的网站。为更多用户带来便利和价值。

搭建开始：
1、安装完宝塔后，继续安装Nginx和php5.6，然后禁用php里面的exec函数

2、新建站点

3、写上伪静态代码
location ~* (runtime|application)/{
  return 403;
}
location / {
  if (!-e $request_filename){
    rewrite  ^(.*)$  /index.php?s=$1  last;   break;
  }
}



3、将程序上传到新建的站点文件夹，根目录cache文件夹是缓存文件夹，如没有的话请自行右键新建文件夹。yjj.js可以放统计和跳转链接。static里面是js以及css的内容，一般不需要管。








3.需要修改的关键词库以及句子库都在这里。

date/fenlei 这里面是播放的视频链接，如果模板没有播放器可以不用管。
   date/gupiao 这是是放主关键词的。
   date/juzi  这里是放句子库的。
   date/keywords 这里放的是随机关键词。	
   date/lanmu 放的栏目词，不做站群可以不用理会。
   date/renming 随机调用的人名，不做站群可以不用理会。
   date/templates 这里是模板文件。
  date/yuming 这里放的站群域名，不做站群可以不用理会。
  date/zhangjie 文章章节，不是小说内容可以不用管。
  date/zhanming 这里是随机调用的网站名称，不做站群可以不用理会。
  Date/var.txt 这里放的是链轮，泛解析泛二级。不做泛二级可以不用理会。

4、date/templates这里是替换模板的地方，该程序仅首页index.html和内页show.html,两个页面，仿模板很快，一般仿一个模板一个小时就完成一套模板的改写。默认赠送一套模板，用户也可以自己写，关于模板的标签代码可以参考本手册底部。


站群操作手法：
1、宝塔站点管理域名管理批量添加域名

2、在date/yuming/yuming.txt 里批量添加域名。

3、data/var.txt这里是做链轮的也可以当蜘蛛池使用，把需要做蜘蛛池的域名丢进来即可。程序自动抽取生成


站群链轮代码，不做链轮请直接忽略。

<li><a href="http://<变量>/" target="_blank"><随机关键词></a></li>

<变量>标签调取的是Date/var.txt里的域名。

以下是写模板的标签，不写模板请直接忽略

        $html = preg_replace('/<当前链接>/','http://'.$_SERVER['HTTP_HOST'].$_SERVER['REQUEST_URI'],$html);
        $html = preg_replace('/<当前月日>/',date("m-d"),$html);
        $html = preg_replace('/<时间>/',date("Y-m-d H:i:s"),$html);
        $html = preg_replace('/<大写字母10>/',$this->randchar(10,3),$html);
        while(strstr($html,'<变量>'))
        {
            $html = preg_replace('/<变量>/',$this->var_(),$html,1);
        }
        while(strstr($html,'<随机名字>'))
        {
            $html = preg_replace('/<随机名字>/',$this->renming(),$html,1);
        }
        while(strstr($html,'<锁死名字2>'))
        {
            $html = preg_replace('/<锁死名字2>/',$this->renming(),$html,2);
        }
        while(strstr($html,'<锁死名字3>'))
        {
            $html = preg_replace('/<锁死名字3>/',$this->renming(),$html,3);
        }
        while(strstr($html,'<锁死名字1>'))
        {
            $html = preg_replace('/<锁死名字1>/',$this->renming(),$html);
        }
        while(strstr($html,'<锁死关键词2>'))
        {
            $html = preg_replace('/<锁死关键词2>/',$this->keyword(),$html,2);
        }
        while(strstr($html,'<随机关键词>'))
        {
            $html = preg_replace('/<随机关键词>/',$this->keyword(),$html,1);
        }
         while(strstr($html,'<随机章节模板>'))
        {
            $html = preg_replace('/<随机章节模板>/',$this->zhangjiemuban(),$html,1);
        }
        while(strstr($html,'<锁死随机数字3>'))
        {
            $html = preg_replace('/<锁死随机数字3>/',mt_rand(1,9).$this->randchar(4,2),$html,3);
        }
         while(strstr($html,'<内容数字锁死>'))
        {
            $html = preg_replace('/<内容数字锁死>/',mt_rand(2,9),$html);
        }
        
        while(strstr($html,'<锁死数字2>'))
        {
            $html = preg_replace('/<锁死数字2>/',mt_rand(1,3000),$html);
        }
        while(strstr($html,'<模板下>'))
        {
            $html = preg_replace('/<模板下>/',$this->mubanxia(),$html,1);
        }
        while(strstr($html,'<锁死数字1>'))
        {
            $html = preg_replace('/<锁死数字1>/',mt_rand(1,999),$html);
        }
        while(strstr($html,'<锁死数字3>'))
        {
            $html = preg_replace('/<锁死数字3>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字4>'))
        {
            $html = preg_replace('/<锁死数字4>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字5>'))
        {
            $html = preg_replace('/<锁死数字5>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字6>'))
        {
            $html = preg_replace('/<锁死数字6>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字7>'))
        {
            $html = preg_replace('/<锁死数字7>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字8>'))
        {
            $html = preg_replace('/<锁死数字8>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字9>'))
        {
            $html = preg_replace('/<锁死数字9>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字10>'))
        {
            $html = preg_replace('/<锁死数字10>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字11>'))
        {
            $html = preg_replace('/<锁死数字11>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字12>'))
        {
            $html = preg_replace('/<锁死数字12>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死数字13>'))
        {
            $html = preg_replace('/<锁死数字13>/',mt_rand(1,9).$this->randchar(4,2),$html);
        }
        while(strstr($html,'<锁死随机数字2>'))
        {
            $html = preg_replace('/<锁死随机数字2>/',mt_rand(1,9).$this->randchar(4,2),$html,2);
        }
        while(strstr($html,'<锁死章节1>'))
        {
            $html = preg_replace('/<锁死章节1>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节2>'))
        {
            $html = preg_replace('/<锁死章节2>/',$this->zhangjie(),$html,2);
        }
        while(strstr($html,'<锁死章节3>'))
        {
            $html = preg_replace('/<锁死章节3>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节4>'))
        {
            $html = preg_replace('/<锁死章节4>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节5>'))
        {
            $html = preg_replace('/<锁死章节5>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节6>'))
        {
            $html = preg_replace('/<锁死章节6>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节7>'))
        {
            $html = preg_replace('/<锁死章节7>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节8>'))
        {
            $html = preg_replace('/<锁死章节8>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节9>'))
        {
            $html = preg_replace('/<锁死章节9>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节10>'))
        {
            $html = preg_replace('/<锁死章节10>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节11>'))
        {
            $html = preg_replace('/<锁死章节11>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节12>'))
        {
            $html = preg_replace('/<锁死章节12>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<锁死章节13>'))
        {
            $html = preg_replace('/<锁死章节13>/',$this->zhangjie(),$html);
        }
        while(strstr($html,'<随机章节>'))
        {
            $html = preg_replace('/<随机章节>/',$this->zhangjie(),$html,1);
        }
        while(strstr($html,'<站名>'))
        {
            $html = preg_replace('/<站名>/',$this->zhanming(),$html);
        }
        while(strstr($html,'<域名>'))
        {
            $html = preg_replace('/<域名>/',$this->yuming(),$html);
        }
        while(strstr($html,'<随机数字2个>'))
        {
            $html = preg_replace('/<随机数字2个>/',mt_rand(1,99),$html,2);
        }
        while(strstr($html,'<随机栏目>'))
        {
            $html = preg_replace('/<随机栏目>/',$this->lanmu(),$html,1);
        }
        while(strstr($html,'<锁死栏目1>'))
        {
            $html = preg_replace('/<锁死栏目1>/',$this->lanmu(),$html);
        }
        while(strstr($html,'<随机分类>'))
        {
            $html = preg_replace('/<随机分类>/',$this->fenlei(),$html,1);
        }
        while(strstr($html,'<动态句子>'))
        {
            $html = preg_replace('/<动态句子>/',$this->juzi(),$html,1);
        }
        while(strstr($html,'<锁死句子1>'))
        {
            $html = preg_replace('/<锁死句子1>/',$this->juzi(),$html);
        }
        
        while(strstr($html,'<随机数字>'))
        {
            $html = preg_replace('/<随机数字>/',mt_rand(500,3000),$html,1);
        }
        while(strstr($html,'<干扰模板>'))
        {
            $html = preg_replace('/<干扰模板>/',$this->mubana(),$html,1);
        }
        while(strstr($html,'<当前域名>'))
        {
            $html = preg_replace('/<当前域名>/','http://'.$_SERVER['HTTP_HOST'],$html);
        }
        while(strstr($html,'<股票随机关键词>'))
        {
            $html = preg_replace('/<股票随机关键词>/',$this->gupiao(),$html,1);
        }
        
        while(strstr($html,'<随机变量>'))
        {
            $html = preg_replace('/<随机变量>/',$this->var_(),$html,1);
        }
        while(strstr($html,'<锁死图片3>'))
        {
            $html = preg_replace('/<锁死图片3>/','http://'.$_SERVER['HTTP_HOST'].'/static/img/'.$this->img(),$html,3);
        }
        while(strstr($html,'<动态随机图片>'))
        {
            $html = preg_replace('/<动态随机图片>/','http://'.$_SERVER['HTTP_HOST'].'/static/img/'.$this->img(),$html,1);
        }
        while(strstr($html,'<随机数字10>'))
        {
            $html = preg_replace('/<随机数字10>/',mt_rand(1,9).$this->randchar(9,2),$html,1);
        }
        while(strstr($html,'<随机小写字符5>'))
        {
            $html = preg_replace('/<随机小写字符5>/',$this->randchar(5,0),$html,1);
        }
        while(strstr($html,'<随机标题>'))
        {
            $html = preg_replace('/<随机标题>/',$this->biaoti(),$html,1);
        }
        
        $html = preg_replace('/<关键词>/',$this->gupiao(),$html);

        $html = preg_replace('/<动态时间>/',date("Y-m-d H:i:s"),$html);
