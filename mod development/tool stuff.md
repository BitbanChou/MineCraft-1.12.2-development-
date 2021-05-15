### 我们本次制作一套属于自己的新工具
### 1.在 ModItem.java 中进行编辑:
### 添加工具材质信息
```
	static final ToolMaterial MATERIAL_OBSIDIAN =EnumHelper.addToolMaterial(name(材质名称), harvestLevel(挖掘等级), maxUses(工具耐久), efficiency(挖掘效率), damage(工具造成的伤害), enchantability(工具附魔能力,越高附的魔越好))

```
示例：
```
	static final ToolMaterial MATERIAL_OBSIDIAN =EnumHelper.addToolMaterial("material_zstool", 4, 2670, 15.0F, 3.0F, 40)

```
### 2.在items包下 新建 tools 包
![cr1.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_147d0b05b3-cr1.png) 
### 在tools 包中新建 ToolSword 类：
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_2d3e329bb3-cr2.png) 
#### 在ToolSword.java中编写代码：
```
package com.Joy187.newmod.items.tools;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.item.ItemSword;

public class ToolSword extends ItemSword implements IHasModel{
	public ToolSword(String name,CreativeTabs tab,ToolMaterial material) {
		
		super(material);
		setUnlocalizedName(name);
		setRegistryName(name);
		setCreativeTab(tab);
		
		ModItems.ITEMS.add(this);
	}
	
	@Override
	public void registerModels() {
		Main.proxy.registerItemRenderer(this, 0, "inventory");
	}
}
```
### 3.回到 ModItem.java ，继续编写物品信息：
```
	public static final ItemSword ZS_SWORD = new ToolSword("zs_sword", Main.ITEM_TAB, MATERIAL_ZS);
	                                                       //物品名   物品属于哪一个工具栏 物品的材质
```
### 4.在物品栏添加物品信息
#### 新建一个 无标题的文本文件
```
{
                    //注意更改类型
	"parent": "item/handheld",
	"textures": {
		"layer0": "joymod:items/zs_sword" 
		                        //改成你的名字
	}
}
```
#### 将物品保存到models.item 中
![cr3.jpg](https://cdn.acwing.com/media/article/image/2021/05/13/39383_1b7fbeedb3-cr3.jpg) 
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_1fa64da8b3-cr4.png) 

### 5.在en_us.lang 文件中将物品在游戏中的名称进行设置：
```
item.zs_sword.name=ZS Sword
```
### 同时将物品的材质放入textures.items包中
![cr10.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_e4776138b3-cr10.png) 
### 6.重复3、4、5步将axe(斧子)、pickaxe(稿子)、hoe(锄子)等工具都加入到游戏中(将名字中的Sword替换成其他工具)
### 注意：添加斧子时请在斧子的 ItemAxe.java中 写成如下样式：(斧子需要单独传递伤害和攻速)
```
package com.Joy187.newmod.items.tools;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.item.ItemAxe;
import net.minecraft.item.Item.ToolMaterial;

public class ToolAxe extends ItemAxe implements IHasModel{
	public ToolAxe(String name,CreativeTabs tab,ToolMaterial material) {
		
		super(material,12.0F,-1.5F);
		setUnlocalizedName(name);
		setRegistryName(name);
		setCreativeTab(tab);
		
		ModItems.ITEMS.add(this);
	}
	
	@Override
	public void registerModels() {
		Main.proxy.registerItemRenderer(this, 0, "inventory");
	}
}
```
#### 五种工具都操作完后可进行下一步骤
### ModItem.java 中的信息:
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_78309ba7b3-cr5.png) 
### items.tools 中的五种工具类
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_a0ca2f46b3-cr6.png) 
### en_us.lang 文件：
![cr7.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_c822b8d9b3-cr7.png) 
### 所有工具材质:
![cr8.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_e3912aa3b3-cr8.png) 

### 7保存所有文件 -> 运行游戏
![cr9.png](https://cdn.acwing.com/media/article/image/2021/05/13/39383_80683813b3-cr9.png) 
### 游戏中出现所有我们制作的工具，圆满完成！
