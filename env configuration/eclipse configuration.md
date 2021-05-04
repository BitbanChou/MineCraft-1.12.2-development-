### MDK环境搭建完成后，我们需要对eclipse内的模组开发进行基础设置

### 1. 右键src/main/java -> 新建 -> 包 -> 名称为com.你的游戏名(英文).模组名称(纯小写字母无空格) -> 完成
## 演示名称：com.Joy187.newmod (之后操作一直要用到这个包的名字，根据个人喜好修改)
![creat1.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_4fa9e0d7ac-creat1.png) 
### 2. 对着刚刚创建的包右键 -> 新建 -> 类 -> 命名为Main -> 完成
![cr.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_ef889249ac-cr.png) 
### 3. 建立一个新的包 -> 名称为com.Joy187.newmod.util (com.你的游戏名.模组名称.util)-> 完成
### 4. 对着刚刚创建的util包右键 -> 新建 -> 类 -> 命名为Reference -> 完成
![cr1.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_cb740d36ac-cr1.png) 
### 5. 建立一个新的包 -> 名称为com.Joy187.newmod.proxy (com.你的游戏名.模组名称.proxy)-> 完成 
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_37c9381fac-cr2.png) 
### 6. 在刚刚创建的proxy包下创建两个类：ClientProxy 和 CommonProxy
![cr3.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_c516e45dac-cr3.png) 
#### 对ClientProxy类进行 继承 操作 -> ctrl + s 保存文件:
#### Java代码
```
package com.Joy187.newmod.proxy;

public class ClientProxy extends CommonProxy{   //只需要加上这两个单词,其他不要改extends CommonProxy

}
```
### 7.在Reference.java文件中输入如下的代码：
#### Java代码
```
package com.Joy187.newmod.util; //包会自动或手动导入,不用写

public class Reference {

	    //Mod_ID的字符串要全部是小写！小写！小写！
		public static final String Mod_ID = ""; //模组ID(全世界的每一个模组的ID都不能相同,所以要起一个独特的ID)
		public static final String NAME = "";   //你的模组名称
		public static final String VERSION = "1.0"; //模组版本
		public static final String ACCEPTED_VERSIONS = "[1.12.2]";  //模组适用的游戏版本(1.12.2开发就填1.12.2)
		public static final String CLIENT_PROXY_CLASS = "com.Joy187.newmod.proxy.ClientProxy";  //(com.你的游戏名.模组名称.proxy.ClientProxy)
		public static final String COMMON_PROXY_CLASS = "com.Joy187.newmod,proxy.CommonProxy";//(com.你的游戏名.模组名称.proxy.CommonProxy)
}
```
#### 示例:
![exp.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_28fe23feac-exp.png)

### 8.对Main.java进行编辑：(出现红色波浪线就自动导入包)
```
//包可以自动导入
package com.Joy187.newmod;

import com.Joy187.newmod.proxy.CommonProxy;
import com.Joy187.newmod.util.Reference;

import net.minecraftforge.fml.common.Mod;
import net.minecraftforge.fml.common.Mod.EventHandler;
import net.minecraftforge.fml.common.Mod.Instance;
import net.minecraftforge.fml.common.SidedProxy;
import net.minecraftforge.fml.common.event.FMLInitializationEvent;
import net.minecraftforge.fml.common.event.FMLPostInitializationEvent;
import net.minecraftforge.fml.common.event.FMLPreInitializationEvent;

@Mod(modid = Reference.Mod_ID, name = Reference.NAME, version=Reference.VERSION)    
public class Main {
	
	
	@Instance
	public static Main instance;
	
	@SidedProxy(clientSide = Reference.CLIENT_PROXY_CLASS, serverSide = Reference.COMMON_PROXY_CLASS)
	public static CommonProxy proxy;
	
	@EventHandler
	public static void PreInit(FMLPreInitializationEvent event)
	{
		
	}
	
	@EventHandler
	public static void Init(FMLInitializationEvent event)
	{
		
	}
	
	@EventHandler
	public static void PostInit(FMLPostInitializationEvent event)
	{
		
	}
	
}
```
### 9.找到src/main/resources文件夹-> 打开mcmod.info -> 对模组信息进行编辑：
```
[
{
  "modid": "joymod",    //和第7步的命名保持一致
  "name": "newMod",     //和第7步的命名保持一致
  "description": "This is Joy's First Mod.",    //可以添加你对模组的个人描述
  "version": "1.0",     //和第7步的命名保持一致
  "mcversion": "1.12.2",    //和第7步的命名保持一致
  "url": "",
  "updateUrl": "",
  "authorList": ["Joy187"],  //作者名单,可以是个人也可以是团队
  "credits": "The Forge and FML guys, for making this example",
  "logoFile": "",
  "screenshots": [],
  "dependencies": []
}
]
```
#### 示例：
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_1f0b7c95ac-cr4.png) 
### 10.回到Main文件,点击绿色运行按钮旁边的黑色三角 -> 运行配置 -> 找到Java应用程序 -> (模组名).Client -> 点击运行按钮
![r5.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_50f336beac-r5.png) 
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_47e3d793ac-cr6.png) 

## 11.MineCraft 成功运行！！！
![cr7.png](https://cdn.acwing.com/media/article/image/2021/05/03/39383_9406a9c0ac-cr7.png) 
