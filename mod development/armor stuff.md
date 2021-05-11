### 本次我们尝试在Minecraft中创造一套盔甲套装
### 1.在items包下新建armor包:
![cr3.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_adcdf27fb2-cr3.png) 
### 在armor包中新建 ArmorBase 类:
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_aa4269d3b2-cr4.png) 
#### 在 ArmorBase.java中编写代码：
```
package com.Joy187.newmod.items.armor;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.inventory.EntityEquipmentSlot;
import net.minecraft.item.ItemArmor;

public class ArmorBase extends ItemArmor implements IHasModel{

	public ArmorBase(String name,ArmorMaterial materialIn, int renderIndexIn, EntityEquipmentSlot equipmentSlotIn,CreativeTabs tab) {
		super(materialIn, renderIndexIn, equipmentSlotIn);
		// TODO 自动生成的构造函数存根
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
### 2.在init下的 ModItem.java 中添加盔甲信息：
```
//material 根据情况更改 
public static final ArmorMaterial ARMOR_MATERIAL_ZS = EnumHelper.addArmorMaterial(name(盔甲名称), textureName(合成材料名称), durability(耐久值), reductionAmounts(盔甲值，包含靴子、护腿、护甲、头盔), enchantability(附魔能力), soundOnEquip(穿上盔甲的声音), toughness(盔甲硬度),钻石是2.0F);

//armor
public static final Item ZS_HELMET = new ArmorBase("zs_helmet",ARMOR_MATERIAL_ZS,1,EntityEquipmentSlot.HEAD,CreativeTabs.COMBAT);
public static final Item ZS_CHESTPLATE = new ArmorBase("zs_chest",ARMOR_MATERIAL_ZS,1,EntityEquipmentSlot.CHEST,CreativeTabs.COMBAT);
public static final Item ZS_LEGGINGS = new ArmorBase("zs_leggings",ARMOR_MATERIAL_ZS,2,EntityEquipmentSlot.LEGS,CreativeTabs.COMBAT);
public static final Item ZS_BOOTS = new ArmorBase("zs_boots",ARMOR_MATERIAL_ZS,1,EntityEquipmentSlot.FEET,CreativeTabs.COMBAT);
```
### 代码示例：
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_30202653b2-cr5.png) 
### 我的世界伤害计算公式
![cr1.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_88a5d346b2-cr1.png) 
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_8cede06bb2-cr2.png) 

### 3.注册物品信息 在model.item包下 将所有套装的信息进行注册
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_b38bee1ab2-cr6.png) 
### 4.在语言包中添加四中防具的游戏内名称
![cr7.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_df6f343ab2-cr7.png)
### 5.防具材质设置
### 在textures包下新建models包，之后在models包下新建armor包
![cr8.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_792dd2dcb2-cr8.png) 
![cr9.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_7cffabb3b2-cr9.png) 
### 将我们准备好的四种护具材质放入items包中(物品栏中显示用)
![d1.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_d419c0b0b2-d1.png) 
### 将两种全身材质放入armor包中:
![d3.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_4758e8bab2-d3.png) 
### 6.保存文件 -> 运行游戏
![d2.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_56f3af4ab2-d2.png)
### 切换生存模式，全身效果属性全部正常显示！
![d4.png](https://cdn.acwing.com/media/article/image/2021/05/11/39383_ab196f4cb2-d4.png) 
### 游戏内成功显示护具！
