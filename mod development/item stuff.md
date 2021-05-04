### 本次我们来介绍一下如何创建一个基础物品：
## 演示包名：com.Joy187.newmod (之后都简称为包名)
### 1. 新建 -> 创建一个 包名.init 包
![cr.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_98ed5724ac-cr.png) 
### 2.在刚刚创建的init包中新建一个类 ModItems
![cr1.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_fee7d666ac-cr1.png) 
### 3.在util包中新建 -> 接口 -> 名称为 IHasModel -> 完成
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_6d815053ac-cr2.png) 
#### 在IHasModel.java 中编辑如下代码：
```
package com.Joy187.newmod.util; //这个是你的包名,和我的不一样

public interface IHasModel {
	
	public void registerModels();
	
}
```
### 4.新建 -> 创建一个 包名.items包
![cr3.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_111c46b6ac-cr3.png) 
### 5.在items包中新建 ItemBase 类
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_4631aee2ac-cr4.png)
#### 在ItemBase.java中进行编辑：
```
package com.Joy187.newmod.items;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.item.Item;

public class ItemBase extends Item implements IHasModel{
	
	public ItemBase(String name) {
		setUnlocalizedName(name);
		setRegistryName(name);
		setCreativeTab(CreativeTabs.COMBAT); //这个决定你的物品会放在哪里,我这里默认放在攻击武器(锐利的剑)一栏
		
		ModItems.ITEMS.add(this);
	}
	
	@Override
	public void registerModels() {
		Main.proxy.registerItemRenderer(this, 0, "inventory");
	}
}
```
### 6.对包名.CommonProxy.java 进行编辑
```
package com.Joy187.newmod.proxy;

import net.minecraft.item.Item;

public class CommonProxy {
	public void registerItemRenderer(Item item, int meta,String id) {}
}
```
### 7.对包名.CommonProxy.java 进行编辑
```
package com.Joy187.newmod.proxy;

import net.minecraft.client.renderer.block.model.ModelResourceLocation;
import net.minecraft.item.Item;
import net.minecraftforge.client.model.ModelLoader;

public class ClientProxy extends CommonProxy{
	public void registerItemRenderer(Item item, int meta,String id) {
	    //对你自定义的物品进行定位
		ModelLoader.setCustomModelResourceLocation(item, meta, new ModelResourceLocation(item.getRegistryName(), id));
	
	}
}
```
#### 代码示例:
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_2ab8d850ac-cr5.png) 
### 8.在util包中新建一个包 -> 命名为 包名.util.handlers
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_9f7dcfb6ac-cr6.png) 
### 9.在刚刚创建的handlers包中新建一个类 -> 命名为RegistryHandler
![cr7.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_fa502647ac-cr7.png) 
#### 在 RegistryHandler.java 中进行编辑,之后保存：
```
package com.Joy187.newmod.util.handlers;

import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.item.Item;
import net.minecraftforge.client.event.ModelRegistryEvent;
import net.minecraftforge.event.RegistryEvent;
import net.minecraftforge.fml.common.Mod.EventBusSubscriber;
import net.minecraftforge.fml.common.eventhandler.SubscribeEvent;

@EventBusSubscriber
public class RegistryHandler {
	@SubscribeEvent
	public static void onItemRegister(RegistryEvent.Register<Item> event) {
		event.getRegistry().registerAll(ModItems.ITEMS.toArray(new Item[0]));
	}

	@SubscribeEvent
	public static void onModelRegister(ModelRegistryEvent event) {
		for(Item item: ModItems.ITEMS){
			if(item instanceof IHasModel) {
				((IHasModel)item).registerModels();
			}
		}

	}
}
```
### 10.对ModItems.java 编写代码：
#### 这里我创建了一个铲子作为我的一个物品,可以根据个人创意进行修改
```
package com.Joy187.newmod.init;

import java.util.ArrayList;
import java.util.List;

import com.Joy187.newmod.items.ItemBase;

import net.minecraft.item.Item;

public class ModItems {

	public static final List<Item> ITEMS = new ArrayList<Item>();
	
	public static final Item LABOR_SHOVEL = new ItemBase("labor_shovel");
	                         //要全部大写,可以加下划线    //你的物品名称               
}
```
### 11.在src/main/resources 包中新建三个包，分别命名为lang，models，textures
![cr8.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_e8dec9c3ac-cr8.png) 
## 你的mod名称实际上是你的modid
![cr9.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_26bab5c9ac-cr9.png)
### 12.在models包下新建 item (单数)包，在textures包下新建 items (复数)包
![c1.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_bec08741ac-c1.png) 
### 13.新建一无标题文本文件 (对语言文件进行编辑)
![c2.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_e2e09384ac-c2.png) 
#### 输入代码
```
//item
item.labor_shovel.name=Labor Shovel 
     //这个应于你的ModItems中的物品名称保持一致 ，等号后面的是你在游戏中的真实方块名称
```
#### 将其命名为en_us.lang -> 保存在lang包下面就可以了
![c3.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_d28abfafac-c3.png)  
### 14.新建一无标题文本文件 (对物品模型文件进行编辑)
#### 输入代码
```
{
	"parent": "item/generated",
	"textures": {
		"layer0": "joymod:items/labor_shovel"
		           //你的modid:items/你的物品名称(和ModItems中保持一致)
	}
}
```
#### 将其命名为 物品名称.json  -> 保存在models/item包下面就可以了
![c4.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_a546255cac-c4.png) 
### 15.对物品材质文件进行操作
#### 将你的材质(.png文件)放入textures/items文件夹下
![c5.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_27ceec28ac-c5.png) 
#### 演示材质：
![labor_shovel.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_449e5e7fac-labor_shovel.png) 
### 16. 保存所有文件，对项目进行刷新，之后进入游戏
![c6.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_76bd2c0aac-c6.png) 
## 17. 游戏中成功出现我们的物品，起飞！
![c7.png](https://cdn.acwing.com/media/article/image/2021/05/04/39383_d2869744ac-c7.png)
