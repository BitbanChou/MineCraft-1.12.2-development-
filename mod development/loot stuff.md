## 我们本次对击杀怪物掉落战利品进行设置
### 1.在 util.handler 包中新建 LootTableHandler 类
![cr1.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_762bbdd5b7-cr1.png) 
#### 在LootTableHandler.java中进行编辑:
```
package com.Joy187.newmod.util.handlers;

import com.Joy187.newmod.util.Reference;

import net.minecraft.util.ResourceLocation;
import net.minecraft.world.storage.loot.LootTableList;

public class LootTableHandler {
    //添加你想要产生掉落物的生物
	public static final ResourceLocation RA3 = LootTableList.register(new ResourceLocation(Reference.Mod_ID ,"ra3"));
}
```
### 2.在 EntityRA3.java (第7讲中创建) 中添加注册表函数
```
	@Override
    protected ResourceLocation getLootTable()
    {
    	return LootTableHandler.RA3;
    }
```
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_5a7083c7b7-cr2.png) 
### 3.在resource中新建 loot_table 包
![cr3.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_556440d7b7-cr3.png) 

### 4.打开 战利品制作网站进行掉落物的相关设置：
[战利品（掉落物）制作网站](https://amaury.carrade.eu/minecraft/loot_tables)
### 自定义你的战利品信息
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_f6ccd2eab7-cr4.png) 
### 将自动生成的代码全部复制
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_0b78f974b7-cr5.png) 
### 在loot_table 下新建.json文件，把代码全部放进去
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_2ea9f8a3b7-cr6.png) 

### 保存文件 -> 运行游戏
![cr7.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_5681053bb7-cr7.png) 
### 击杀怪物后，怪物掉落腐肉
![cr8.png](https://cdn.acwing.com/media/article/image/2021/05/18/39383_623351c9b7-cr8.png) 
#### 你可以通过修改json文件中"weight"的大小来增加各种物品的掉率~
