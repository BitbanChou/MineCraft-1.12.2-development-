### 1.12.2Forge模组开发 配置ForgeMDK环境
#### 开发环境：eclipse
![ecl.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_214b3372ab-ecl.png) 
### 1. 我的世界模组开发首先需要配置Forge MDK环境
 1. 
    1. ##### 我们可以通过Forge官网进行下载:[minecraftforge官网](https://files.minecraftforge.net/net/minecraftforge/forge/index_1.12.2.html)
    2. #### 也可以通过国内网盘进行下载：[网盘链接](https://pan.baidu.com/s/1ZhHLFZ_i_0GHJ97kPt5ygQ) (网盘密码: MCNB)
    #### 下载1.12.2版本的Forgemdk即可(文件略大，需要耐心等待……)
    ![sav.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_08e8006aab-sav.png) 
### 2. 下载下来之后将文件解压，里面有两个文件夹。一个是.gradle文件夹，另一个是forge文件夹：
   ![grad.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_5b267e7bab-grad.png) 
#### 将第一个.gradle文件夹放在C:\User\用户名路径下：
   ![pu.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_d34505afab-pu.png) 
#### 第二个forge-1.12.2-14.23.5.2847-mdk文件夹作为之后的工程文件夹，即WorkSpace(做好备份)。
#### 我们可以将这个文件夹重命名为我们的模组名称(只能使用英文命名)
![rena.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_b433a7e2ab-rena.png) 
#### 将开发的文件夹放置到**纯英文**的文件路径中
![enus.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_86107d8aab-enus.png) 
### 3.cmd指令搭建gradlew环境
#### 在刚刚放置的NewMod(名字为自定义的)文件夹中运行cmd指令：
> gradlew setupDecompWorkspace
#### 之后耐心等待即可。
![stp.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_f4ae831aac-stp.png)  
![succ.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_bafa19e2ab-succ.png) 
#### 出现了BUILD SUCCESSFUL后再输入
> gradlew eclipse
### 4.如果之前的步骤都顺利进行，我们就可以将文件导入到eclipse中了：
#### 点击文件->导入(import)->Projects from Folder or Archive -> 下一步
![ip1.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_f0b9ee7aab-ip1.png) 
#### 点击Directory找到放置改名后的.forge工程文件夹目录 -> 完成
![ip2.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_49311b7fab-ip2.png) 
### 5.当我们出现下面的场景，说明我们的环境搭建成功了!
![ip.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_84562149ab-ip.png)
