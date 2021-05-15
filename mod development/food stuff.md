### 我们本次来制作一款食物(food)

### 1.在items包下 新建 food 包
![cr1.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_5a2fd468b4-cr1.png)  
### 在food 包中新建 FoodBase 类：
![cr2.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_5de40532b4-cr2.png) 
```
public FoodBase(String name(食物名称), int amount(恢复量), float saturation(饱和度), boolean iswolfFood(狼是否可以吃),CreativeTabs tab(放在物品栏的位置))
```
#### 在 FoodBase.java 中进行编写:
```
package com.Joy187.newmod.items.food;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.init.ModItems;
import com.Joy187.newmod.util.IHasModel;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.item.ItemFood;

public class FoodBase extends ItemFood implements IHasModel{
	public FoodBase(String name, int amount, float saturation, boolean iswolfFood,CreativeTabs tab) {
		super( amount, saturation, iswolfFood );
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
### 2.在 models.item 下新建.json文件 -> 编写物品的信息
```
{
	"parent": "item/generated",
	"textures": {
		"layer0": "joymod:items/secret_tiny_burger"
	}
}
```
### 3.将食物材质拖入 textures.items 包中:
![cr3.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_f27eeda8b4-cr3.png) 

### 4.在en_us.lang 文件中添加食物游戏中的名称
![cr4.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_6b7d3875b4-cr4.png) 

### 5.保存所有文件 -> 运行游戏
#### 游戏中成功出现食物
![cr5.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_d71f6bb7b4-cr5.png) 
#### 食物吃下去后恢复5点饱食度，与最初设定完美符合！
![cr6.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_f69e02a3b4-cr6.png)


### 如果要制作具有效果的食物，我们可以在food包中新建一个 EffectFoodBase 类
#### 在EffectFoodBase.java 中编写:
```
package com.Joy187.newmod.items.food;

import com.Joy187.newmod.util.IHasModel;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.entity.player.EntityPlayer;
import net.minecraft.item.ItemStack;
import net.minecraft.potion.PotionEffect;
import net.minecraft.world.World;
import net.minecraftforge.fml.relauncher.Side;
import net.minecraftforge.fml.relauncher.SideOnly;

public class EffectFoodBase extends FoodBase implements IHasModel{
	
	PotionEffect effect;
	public EffectFoodBase(String name, int amount, float saturation, boolean iswolfFood,CreativeTabs tab, PotionEffect effect) {
		super(name, amount, saturation, iswolfFood, tab);
		//setAlwaysEdible();
		this.effect=effect;
	}
	
	@Override
	protected void onFoodEaten(ItemStack stack,World worldIn, EntityPlayer player) {
		if (!worldIn.isRemote)
		{
			player.addPotionEffect(new PotionEffect(effect.getPotion(), effect.getDuration(), effect.getAmplifier(), effect.getIsAmbient(), effect.doesShowParticles()));
		}
	}
	
	@SideOnly(Side.CLIENT)
	public boolean hasEffect( ItemStack stack)
	{
		return true;
	}
}
```
#### 之后在ModItem中添加食物，重复之前的步骤即可。
![cr8.png](https://cdn.acwing.com/media/article/image/2021/05/14/39383_5a380c25b4-cr8.png)
