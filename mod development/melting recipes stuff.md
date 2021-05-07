### 本次我们对冶炼配方进行制作
### 1.在init包中 -> 新建 ModRecipes 类
![1](https://img-blog.csdnimg.cn/img_convert/e1b389b5880908456d73455df2f20cce.png)
#### 在ModRecipes.java中编写代码:
```
package com.Joy187.newmod.init;

import net.minecraft.init.Blocks;
import net.minecraft.init.Items;
import net.minecraft.item.ItemStack;
import net.minecraftforge.fml.common.registry.GameRegistry;

public class ModRecipes {

	public static void init(){
		GameRegistry.addSmelting(Blocks.BLOCK,new ItemStack(ModBlocks.BLOCK,1),0.7f);
								//原料,产出(物品名称,个数),获取经验的概率
	}
}
```
```
对于原版，我们的物品名称可以为
Items.物品名称
Blocks.物品名称
对于模组，我们的名称则要变为
ModItems.物品名称
ModBlocks.物品名称
```
#### 这些名称与我们的ModBlocks，ModItems类相对应
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/06/39383_491e805aae-cr2.png) 

### 我们打算用原版的黑曜石烧制1个模组中的哭泣的黑曜石，同时用模组中的zs_block烧制出3个钻石，一个红石烧制出9个红色染料，则进行如下编辑：
```
package com.Joy187.newmod.init;

import net.minecraft.init.Blocks;
import net.minecraft.init.Items;
import net.minecraft.item.ItemStack;
import net.minecraftforge.fml.common.registry.GameRegistry;

public class ModRecipes {

	public static void init(){
		GameRegistry.addSmelting(Blocks.OBSIDIAN,new ItemStack(ModBlocks.CRYING_OBSIDIAN_BLOCK,1),0.7f);
		GameRegistry.addSmelting(ModBlocks.ZS_BLOCK,new ItemStack(Items.DIAMOND,3),1.8f);
	}
	
}
```
###注意：当我们要烧制出玫瑰红、紫罗兰等染料时，因为其都属于染料Item，无法直接找出，所以我们应该特地将其在配方文件中进行命名：
```
public class ModRecipes {
    
    //特地将玫瑰红拿出来                                 //染料,产出数量,几号染料(玫瑰红是1号染料)
	public static final ItemStack ROSE_RED=new ItemStack(Items.DYE,9,1);
	public static final ItemStack Cactus_Green=new ItemStack(Items.DYE,1,2); (仙人掌绿是2号染料)
	
	
	public static void init(){
		GameRegistry.addSmelting(Blocks.OBSIDIAN,new ItemStack(ModBlocks.CRYING_OBSIDIAN_BLOCK,1),0.7f);
		GameRegistry.addSmelting(ModBlocks.ZS_BLOCK,new ItemStack(Items.DIAMOND,3),1.8f);
		GameRegistry.addSmelting(Blocks.REDSTONE_BLOCK,ROSE_RED,1.0f);
		                        //我们让一个红石烧制出9个红色染料
	}
	
}
```
### Tips:对于查看物品染料是多少号，我们可以通过游戏中按下'F3'+'H'键进行查看：
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/06/39383_4e704951ae-cr5.png) 
### 2.对 Main.java 进行修改(初始化模组中的合成配方) 
#### 找到 Init(FMLInitializationEvent event) 进行修改
```
	@EventHandler
	public static void Init(FMLInitializationEvent event)
	{
		ModRecipes.init();
	}
```
### 3. 保存文件 -> 进入游戏进行测试
![cr3.png](https://cdn.acwing.com/media/article/image/2021/05/06/39383_0b821629ae-cr3.png) 
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/06/39383_0e634595ae-cr4.png) 
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/06/39383_5531674dae-cr6.png) 
### 所冶炼的配方全部成功实现！
