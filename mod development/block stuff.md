### 本次创建方块block的流程和上一次创建物品item的流程比较相似
## 演示包名：com.Joy187.newmod (之后都简称为包名)
### 1. 新建 -> 创建一个 包名.blocks 包
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504232625829.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 2.在刚刚创建的blocks包中新建一个类 BlockBase
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504232953739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 3.在 包名.init 包中新建一个 ModBlocks 类
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504233223282.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 4.对BlockBase.java 进行编写：

```java
package com.Joy187.newmod.blocks;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.init.ModBlocks;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.block.Block;
import net.minecraft.block.material.Material;
import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.item.Item;
import net.minecraft.item.ItemBlock;

public class BlockBase extends Block implements IHasModel{
	
	public BlockBase(String name, Material material) {
		super(material);
		setUnlocalizedName(name);
		setRegistryName(name);
		setCreativeTab(CreativeTabs.BUILDING_BLOCKS);//将你的方块放在哪个物品栏，这里我们选择的是草方块(建筑方块)那一类
		
		ModBlocks.BLOCKS.add(this);
		ModItems.ITEMS.add(new ItemBlock(this).setRegistryName(this.getRegistryName()));
	}
	
	@Override
	public void registerModels() {
		Main.proxy.registerItemRenderer(Item.getItemFromBlock(this), 0, "inventory");
	}
	
}
```
### 4.对RegistryHandler.java 进行编写(加入关于方块的信息，和上一节的物品item方法类似)：

```java
package com.Joy187.newmod.util.handlers;

import com.Joy187.newmod.init.ModBlocks;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.block.Block;
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
	
	//新加入对物品的注册事件
	@SubscribeEvent
	public static void onBlockRegister(RegistryEvent.Register<Block> event) {
		event.getRegistry().registerAll(ModBlocks.BLOCKS.toArray(new Block[0]));
	}

	@SubscribeEvent
	public static void onModelRegister(ModelRegistryEvent event) {
		//对于item的信息注册
		for(Item item: ModItems.ITEMS){
			if(item instanceof IHasModel) {
				((IHasModel)item).registerModels();
			}
		}
		
		//新加入对于block的信息注册
		for (Block block: ModBlocks.BLOCKS) {
			if (block instanceof IHasModel) {
				((IHasModel)block).registerModels();
			}
		}
		
	}
}
```
### 5.对ModBlocks.java 进行编写(创造方块)：
```java
package com.Joy187.newmod.init;

import java.util.ArrayList;
import java.util.List;

import com.Joy187.newmod.blocks.BlockBase;
import net.minecraft.block.Block;
import net.minecraft.block.material.Material;

public class ModBlocks {
	
	public static final List<Block> BLOCKS = new ArrayList<Block>();
	
	public static final Block ZS_BLOCK = new BlockBase("zs_block", Material.IRON);
	                         //此处只能大写+下划线        该方块名称(小写+下划线)  方块的材料属性为铁方块(击打的音效，挖掘等级与铁块一致，可随意修改)
}
```
### 6. 在 src/main/resources 中新建一个 包->命名为 assets.你的modid.blockstates
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504235722437.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 7. 新建一个 无标题文本文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504235932891.png#pic_center)
#### 在文件中进行编辑：
```
{
    "variants": {
        "normal": { "model": "joymod:zs_block" }
        					//你的modid(和mcmod.info文件一致)    :   你的方块名称(与ModBlocks的名称保持一致)
    }
}
```
#### 将文件保存至blockstates文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505000512504.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 8. 在models文件夹下 -> 新建 assets.你的modid.models.block->完成(用于存储方块模型信息)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505001205425.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 9. 新建一个 无标题文本文件(编写方块models)
#### 编辑如下代码
```
{
   "parent": "block/cube_all",
   "textures": {
       "all": "joymod:blocks/zs_block"
       		 //modid         你的方块名称
   }
}
```
#### 文件命名为方块名.json -> 保存到 models.block文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505001659942.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 10. 新建一个 无标题文本文件(编写方块物品栏models)
#### 编辑如下代码
```
{
	"parent": "joymod:block/zs_block"
			//modid         你的方块名称
}
```
#### 文件命名为方块名.json -> 保存到 models.item 文件夹
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505002310564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 11. 对方块lang文件进行编辑
```
//item
item.labor_shovel.name=Labor Shovel

//blocks
tile.zs_block.name=ZS Block
//与ModBlocks保持一致   等号后是游戏中的实际名称
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505002748176.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 12. 在textures文件夹下 -> 新建 assets.你的modid.textures.blocks->完成(用于存储方块材质信息)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505003107595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 13. 将两种材质分别放入textures.blocks和textures.items中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505003418657.png#pic_center)
### 测试zs_block.png图片
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505003501624.png#pic_center)
## 解释：textures.blocks(方块材质) 和 textures.items (方块物品栏材质) 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210505003629271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 14. 保存所有文件，刷新项目 (F5) -> 运行程序
![在这里插入图片描述](https://img-blog.csdnimg.cn/202105050038329.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
### 15. 游戏中成功出现我们的方块，创建成功!
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021050500422512.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0pheV9mZWFybGVzcw==,size_16,color_FFFFFF,t_70#pic_center)
