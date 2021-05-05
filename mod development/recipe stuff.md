### 方块创建好了之后就需要进行合成来增加游戏的趣味性了，我们本次对合成配方进行讲解
### 解释：有序合成 & 无序合成
#### 钻石镐必须按照这样的次序进行摆放，为有序合成
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505131928665.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)

#### 钻石锄只要材料够，这两种摆法都可以合成，为无序合成![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505132302695.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)

### 1.在src/main/resources文件夹下新建一个包 -> 命名为 assets.joymod(你的modid).recipes -> 完成
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505131214570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 2.在新建的recipes包下 -> 新建一无标题的文本文件(进行有序合成配方) 
#### 在该文件中进行编辑： 
```
{
    "type": "minecraft:crafting_shaped",
    
    //你在合成台中的3×3方格中的摆放图案
    "pattern":
    [
        "RRR",
        "RRQ",
        "RRX"
    ],
    
    //进行键值对映射(合成的材料)
    "key":
    {
    	//此处的R代表modid中的object物品(原版的modid为minecraft)
        "R":
        {
            "item": "modid:object"
            		//modid    方块名称
        },	//要加","
        "Q":
        {
            "item": "modid:object"
            		//modid    方块名称        
        },	//要加","
        "X":
        {
            "item": "modid:object"
            		//modid    方块名称        
        }
        //X是最后一项，不用加","(json经典语法)
    },
    
    //合成结果
    "result":
    {
            "item": "modid:object"
            		//modid    方块名称
           	"count": 1
           	//合成几个出来
    }
}
```
#### 假如我们要用zs_block合成一个黑曜石，就可以写成这样：
```
{
    "type": "minecraft:crafting_shaped",
    
    //将工作台摆满
    "pattern":
    [
        "ZZZ",
        "ZZZ",
        "ZZZ"
    ],
    
    //合成材料映射
    "key":
    {
    	//Z代表joymod(我的modid)中的zs_block(第四讲中创作的方块)
        "Z":
        {
            "item": "joymod:zs_block"
        }
    },
    
    //合成结果
    "result":
    {
  		//合成结果为minecraft:黑曜石
        "item": "minecraft:obsidian",
        "count": 9
      	//设置可以合成出9个黑曜石
    }
}
```
关于Minecraft中的物品名称可以在我的世界Wiki中进行查找：
[我的世界中文Wiki百科](https://minecraft.fandom.com/zh/wiki/Minecraft_Wiki)
### 将文件命名为合成结果.json -> 保存到recipes里
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505134032906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 3. 如果我们在有序合成中不想将合成台填满(比如钻石镐的配方)，可以这样编辑:
```
{
    "type": "minecraft:crafting_shaped",

    // 用空格代替即可
    "pattern":
    [
        "ZZZ",
        "Z Z",
        "ZZZ"
    ],
    
    "key":
    {
        "Z":
        {
            "item": "joymod:zs_block"
        }
    },
    
    "result":
    {
        "item": "minecraft:obsidian",
        "count": 9
    }
}
```
### 4. 下面进行无序合成 -> 新建 -> 无标题的文本文件 
#### 在文件中进行编辑
```
{
	"type" : "minecraft:crafting_shapeless",
	
	//所有所需材料
	"ingredients":
	[
	
	{
		"item": "modid:object"
	},
	
	{
        "item": "modid:object"
	},
	
	{
        "item": "modid:object"
	}
	
	],
	//结果生成
	"result":
	{
        "item": "modid:object"
		"count": 1
	}
}
```
#### 假如我们要用原版的两个铁锭和一个青金石合成一个模组中的labor_shovel(第3讲中创作的物品)，就可以写成这样：
```
{
	"type" : "minecraft:crafting_shapeless",
	
	"ingredients":
	[
	//第一个铁锭
	{
		"item" : "minecraft:iron_ingot"
	},
	//第二个铁锭
	{
		"item" : "minecraft:iron_ingot"
	},
	//一个青金石(染料dye中的第4号元素)
	{
		"item": "minecraft:dye",
		"data": 4
	}
	
	],
	//结果
	"result":
	{
		"item" :"joymod:labor_shovel",
		"count": 1
		//生成1个
	}
}
```
### 同样的，将文件命名为合成结果.json -> 保存到recipes里![在这里插入图片描述](https://img-blog.csdnimg.cn/2021050513571842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 5. 保存所有文件 -> 刷新项目 -> 启动游戏进行调试：
#### 有序合成(有空位版)
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/05/39383_7f28d5d0ad-cr5.png) 
#### 无序合成
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/05/39383_adb27542ad-cr6.png) 
#### 成功合成
![cr7.png](https://cdn.acwing.com/media/article/image/2021/05/05/39383_fccfb8cbad-cr7.png) 
## 游戏中成功出现配方，并合成了相应物品，至此有序合成和无序合成工作顺利完成！
