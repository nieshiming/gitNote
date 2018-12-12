git 教学文章： https://gitbook.tw/  
              https://backlog.com/git-tutorial/tw/stepup/stepup2_8.html  

初始化连接git相关： 
    git clone xxx(远程仓库名)            ---克隆项目  
    git remote add origin xxx           ---本地仓库连接到远程  

配置账号密码:     
    git config --local user.name xxx  
    git config --local user.email 'xxx@xx.com'  

    git配置推送时自动保存账号密码： git config credential.helper store            
    参考文章: --https://cloud.tencent.com/developer/ask/131910  

单个分支相关：  
    创建本地分支: git branch dev/nsm  
    删除本地分支： git branch -D dev/nsm  
    切换到本地分支： git checkout dev/nsm  
    创建并切换到改分支： git checkout -b xxx  
    查看本地分支： git branch  
    查看远程分支： git branch -r  
    查看本地分支和远程分支： git branch -a  
    推送本地分支到远程： git push origin dev/nsm  
    删除远程git 分支： git push origin -d dev/nsm  or  git push origin :dev/nsm  
    合并分支: git merge xxx  ???  
    更新远程分支 git fetch origin  
    基于远程分支新建一个本地分支： git checkout -b xxx origin/xxxx  

分支操作：   
    修改分支名： git branch -m 旧分支名  新分支名    （这里只是把本地分支重命名， 后续还需要把 远程旧分支删除，然后push新分支名）  
    刷新远程分支： git remote update origin -p  

日志相关：  
    查看提交日志： git log                  (q: 快速退出)
    查看简化日期: git log --oneline  
    查看分支提交树： git log --graph  
    查看提交日志最新 x 次： git log -number  
    查看log差异： git log -p -number  .
    查看提交明细： git show
    查看指定commit 修改：git show xxx(commit号)

    查看本地提交状态： git status  
    查看简化版状态： git status -s   
    查看未加入暂存区(缓冲区)文件的变化： git diff  
    查看已加入暂存区(缓冲区)文件的变化： git diff staged  
    移除文件： git rm 文件名      ( 不在暂存区的文件 )  
              git rm -f 强制删除 ( 已在暂存区的文件 )  

查看文件：  
    git blame xxx(文件名)   查看文件提交信息  
    cat xxx(文件名)         查看文件  
    git reflog              获取全部版本号  


commit 相关：  
    本地仓库：  
        修改上一次commit信息(已commit)  
            git commit --amend -m "备注"  
    
    
    实际应用中，当完成一次提交之后，可能会发现此次提交有些文件需要修改，当然我们可以在下一次提交中修改此文件  
        解决思路：   
            思路2: git add .  
                  git commit --amend -m 'new remark'        2次提交合在一起，并且只有共用新的提交备注  


提交代码代码相关：  
    拉取远程代码： git fetch origin xxxx  
    git merge origin/xxx  
    git add . (将文件加入到缓冲区,加入缓冲区后，发p现文件名变成绿色)   --暂存区  
    git reset HEAD .                                              --撤离暂存区  
    git commit -m "这里是备注".                                    --提交更新  
    git push -u origin master(分支名) 推送到远程分支(第一次提交)     ---推送到远程  
    git push origin master(分支名)    推送到远程分支   

文件回退：  
    修改文件未 git add., 那么直接 git checkout 文件名  
    加入到缓存区后 git add .  =>    撤销暂存区更新： git reset HEAD fileName    => 然后git checkout  

    回退本地仓库：  
        解决：    
            1、回退版本： git reset --hard head~number  
            2、选中任意版本： git reset --hard xxxx(版本号eg: 8e8fbe8 )    
            注意： 这里仅仅回退的本地仓库的  
        强制推送远程仓库  
                1、选中任意版本： git reset --hard xxxx(版本号eg: 8e8fbe8 )    
                2、git push -f origin xx(远程仓库名)        强制push到远程仓库  

        git reflog              获取全部版本号  

    
    回退远程仓库：  
        git reset --hard origin/master   强制远程master 覆盖本地master  


远程更新本地仓库：  
    git checkout xxx  
    git fetch origin xxx   更新远程仓库同步到本地（不会merge）  
    git merge origin/xxx   本地仓库merge远程仓库，本地commit 同步  


删除文件：  
    commit后恢复文件=》删除文件》恢复文件 || add.  
        1、git checkout -- 文件名  
    查看工作区要被删除的文件 git clean -n  
    删除工作区文件： git clean -f  

版本回退：  



远程相关  
    git remote          查看远程信息  
    git remote -v       查看远程库详细信息  
    

/**************************************/  
工作区： 就是电脑上看到的目录，日常所建的目录都是属于工作区的范畴  
版本库： 工作区有一个隐藏目录.git, 这个不属于工作区，这是版本库，版本库存在了很多东西，其他最重要的  
         就是暂存区，还有git为我们自动创建的master分支，以及只想master分支的head  
        
head: 指向工作所在的分支  

git提交文件到版本库有2步  
1、使用 git add . 把文件添加进去，实际就是把文件添加到暂存区  
2、使用 git commit 把暂存区的内容提交到当前本地仓库的分支上去   


rebase 实例： {  
    git checkout master  
    git fetch origin  
    git merge origin/master  

    git checkout development  
    git fetch origin  
    git merge origin/development  

    git rebase origin/master  
    git checkout master  
    git merge development  
}  


git rebase 原理：  
基于远程 origin/nsm  拉出来一个nsm本地分支：  
对应文章： https://www.cnblogs.com/kevingrace/p/5896706.html  
条件：  
    1、origin/nsm 有提交  
    2、nsm本地分支有提交  
生成条件：  
    git fetch origin nsm      
    git rebase  origin/nie  以远程复位基底   
    git push origin nsm  


git rebase 基于同一分支有修改有冲突  
条件：   
    1、origin/nsm 有提交  
    2、nsm本地分支有提交  
生成条件：   
    git fetch origin nsm  
    git rebase origin/nsm  
    /****解决冲突****/  
    查看冲突文件个数： git status --uno  
    /****解决冲突****/  
    git add .  
    git rebase --continue     
    git push origin nsm  

不同分支：  
    基于 relase1.3 开分支nsm分支  
    git rabase origin/release1.0  
    nsm 分支提交  
    checkout release1.3  
    git merge nsm  
    git fetch origin/relase1.3  
    git rebase origin/releasa1.3  
    git push origin release1.3  

fast forward： 分支间快速推进； A分支没有commit , B分支是基于A 分支切出来的分支， 并有commit   
               执行 A merge B ;        => A 分支快速合并B的commit， 不会产生新的commit   

三方合并：A 分支上切分支B， A B各有新的commit, A merge B 会形成新的commit 来链接2个commit  

git rebase原理： 条件：A 分支上切分支B， A B各有新的commit  
                    1、A rebase B,   A将除去共有祖先上的commit 全部以B为基底嫁接到分支B上去   => 这样A分全部B分支commit为基点，嫁接自身新增的commit   
                    2、回到B分支，直接merge A 分支，执行快速推荐  

参考文章：   
    1、https://www.jianshu.com/p/ca76937b174f  

