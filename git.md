# git

一个项目组,建一个master,建一个dev

有需求可以建多条分支,专人进行merge

## merge

比如:我处在master,鼠标悬停dev,点击Merge into Current,就把dev合并到master了



![image-20220513093907779](\git.assets\image-20220513093907779.png)

多人在同一个分支开发,可能修改同一个类.

所以push时,先update.中间可能需要merge一些代码



## merge和accept

如果你确定除了你以外,没人动过这部分代码,你可以用accept,accept可以简单粗暴的决定,全按我的来,还是全按remote的来.

如果你不确定这些代码的构成,用merge,merge是手动进行代码整合,在其中你可能看到同一段代码中,有多人进行了修改,这时需要你找这个人确定一下,代码的顺序.



## bug

如果某人push上去的代码有bug,之后又有其他人push.之后导致项目起不来之类的问题

最好的解决方法,找到bug,让提交人本地修改然后再提交.

而如果bug的人如果修改量很大,可以在本地进行版本回退(不会影响remote的),然后重写代码,然后update(update下来的代码有他自己以前提交上去的bug代码),所以他update时需要进行一下merge.



![image-20220513100638702](C:\Users\ly-yangst\Desktop\常用工具\my学习\git.assets\image-20220513100638702.png)

## 小妙招

拉两份代码到本地,自己push了一些代码之后,可以用备用代码update,然后运行一下看会不会报错(以免影响别人开发)

push前先update一下,push完之后,跑一下,这时候你拉的别人的代码可能导致你的项目报错.这时候有两个办法

1.本地回退(这样可能导致你自己push的代码,在本地也没了)

2.备用代码出场,反应bug,但不影响我的开发



