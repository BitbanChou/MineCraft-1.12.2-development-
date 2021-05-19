## 本次我们准备为一个防具加上buff
### [盔甲套装教程](https://www.acwing.com/blog/content/7220/)
### 1.对 ArmorBase.java (第8讲中创建)添加buff函数effectPlayer 和 防具点击事件onArmorTick
```
	@Override
	public void onArmorTick(World world, EntityPlayer player, ItemStack itemStack){
		//itemStack.getItem() == ModItems.EIGHT_GLASSES && 
		if(player.inventory.armorItemInSlot(3).getItem() == ModItems.EIGHT_GLASSES &&
		   player.inventory.armorItemInSlot(3)!=null) {
			effectPlayer(player, MobEffects.SPEED, 3);      //增加速度效果,级别为4
			effectPlayer(player, MobEffects.NIGHT_VISION, 1);   //增加夜视效果，级别为2
		}
		super.onArmorTick(world, player, itemStack);
		
	}
	
	private void effectPlayer(EntityPlayer player, Potion effect, int amplifier) {
		if(player.getActivePotionEffect(effect)==null || player.getActivePotionEffect(effect).getDuration() <=1) {
			player.addPotionEffect(new PotionEffect(effect, 200*20,  amplifier, false, true));
			                                                //时间为20*(你要持续的时间),比如20*60就是持续60秒(1分钟)
		}
	}
```
![cr3.jpg](https://cdn.acwing.com/media/article/image/2021/05/17/39383_f047517fb7-cr3.jpg) 
### 注意:我们需要判定所穿戴的护具的位置来决定增加相应的效果,从下到上0~3分别对应不同的部位
```
armorItemInSlot(3):helmet 头盔
armorItemInSlot(2):chestplate, 护胸 
armorItemInSlot(1):leggings, 裤子
armorItemInSlot(0):boots 鞋子

```
### 2.保存文件 -> 运行游戏
#### 无buff未穿戴任何护具
![cr.jpg](https://cdn.acwing.com/media/article/image/2021/05/17/39383_e01ab59bb7-cr.jpg)

### 穿戴好眼镜后，我们增加了夜视和急速的效果
![cr1.jpg](https://cdn.acwing.com/media/article/image/2021/05/17/39383_e5efdb67b7-cr1.jpg)
