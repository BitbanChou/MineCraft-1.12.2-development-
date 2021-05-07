### 本次我们尝试在Minecraft中创造一个人物实体(Zombie类型)
### 1.mod包中新建一个 entity 包
![1](https://cdn.acwing.com/media/article/image/2021/05/07/39383_a87f446eaf-cr1.png)
### entity包中新建一个 EntityInit 类
![2](https://cdn.acwing.com/media/article/image/2021/05/07/39383_cb0f09bbaf-cr2.png)
#### 在 EntityInit.java 中编写代码：
```
package com.Joy187.newmod.entity;

import com.Joy187.newmod.Main;
import com.Joy187.newmod.util.Reference;

import net.minecraft.entity.Entity;
import net.minecraft.util.ResourceLocation;
import net.minecraftforge.fml.common.registry.EntityRegistry;

public class EntityInit {
	
	//对生物信息进行注册
	public static void registerEntities(){
					//生物名称，所编写的生物类，在Reference中的名称，追踪范围，生物蛋颜色1，颜色2  
		registerEntity("ra3", EntityRA3.class, Reference.RA3, 20, 14833957, 0);
	}	
	

	public static void registerEntity(String name, Class<? extends Entity> entity, int id, int range,int color1,int color2) {
		
		EntityRegistry.registerModEntity(new ResourceLocation(Reference.Mod_ID + ":" + name), entity, name, id, Main.instance, range, 1, true, color1, color2);
		
	}

}
```
### 2.在entity中新建我们的生物类 -> 名称与EntityInit中的生物名称保持一致 (以EntityRA3为例子)
![3](https://cdn.acwing.com/media/article/image/2021/05/07/39383_0de990d2af-cr3.png)
#### 在 EntityRA3.java 中编写
```
package com.Joy187.newmod.entity;

import net.minecraft.entity.monster.EntityZombie;
import net.minecraft.world.World;

							 //我们这里设定的生物是僵尸类型，也可以设置成其他类型(小白，小黑等)
public class EntityRA3 extends EntityZombie{

	public EntityRA3(World worldIn) {
		super(worldIn);
		// TODO 自动生成的构造函数存根
	}

}

```

### 3.在 util.handles 中 的 RegistryHandler.java 中 添加语句(生物信息)
```
	public static void preInitRegistries(){
		
		EntityInit.registerEntities();
		RenderHandler.registerEntityRenders();
	}
	
	public static void postInitRegistries() {
		
	}
```

### 示例：
![4](https://cdn.acwing.com/media/article/image/2021/05/07/39383_e0b91fd4af-cr4.png)


### 4.在entity包中新建render包 (渲染生物)
![5](https://cdn.acwing.com/media/article/image/2021/05/07/39383_6c8ed546af-cr5.png)

#### 在render包中 新建 RenderRA3(针对RA3的渲染) 类
![6](https://cdn.acwing.com/media/article/image/2021/05/07/39383_eaabc23daf-cr6.png)
#### 在 RenderRA3.java 中编写代码：
```
package com.Joy187.newmod.entity.render;

import com.Joy187.newmod.entity.EntityRA3;
import com.Joy187.newmod.util.Reference;

import net.minecraft.client.model.ModelBase;
import net.minecraft.client.renderer.entity.RenderLiving;
import net.minecraft.client.renderer.entity.RenderManager;
import net.minecraft.util.ResourceLocation;

public class RenderRA3 extends RenderLiving<EntityRA3>{

	public static final ResourceLocation TEXTURES = new ResourceLocation(Reference.Mod_ID + ":textures/entity/ra3.png");

	
	public RenderRA3(RenderManager rendermanagerIn) {
		super(rendermanagerIn,new ModelRA3(), 0.5f);
				//渲染管理，生成RA3的模型，该生物的阴影占身体的比重()
		// TODO 自动生成的构造函数存根
	}

	protected ResourceLocation getEntityTexture(EntityRA3 entity){
		
		return TEXTURES;
	}
	
}
```
### 5.在 util.handlers 包中新建 RenderHandler 类
![7](https://cdn.acwing.com/media/article/image/2021/05/07/39383_9994eb62af-cr7.png)
#### 在RenderHandler.java中编写Java代码：
```
package com.Joy187.newmod.util.handlers;

import com.Joy187.newmod.entity.EntityRA3;

import com.Joy187.newmod.entity.render.RenderRA3;

import net.minecraft.client.renderer.entity.Render;
import net.minecraft.client.renderer.entity.RenderManager;
import net.minecraftforge.fml.client.registry.IRenderFactory;
import net.minecraftforge.fml.client.registry.RenderingRegistry;

public class RenderHandler {
	
	public static void registerEntityRenders(){
		  
		RenderingRegistry.registerEntityRenderingHandler(EntityRA3.class, new IRenderFactory<EntityRA3>()
		{
			@Override
			public Render<? super EntityRA3> createRenderFor(RenderManager manager)
			{
				return new RenderRA3(manager) ;
			}
		});
	}
}
```

#### 

### 6.之后我们需要对该生物的模型进行制作
#### 我们需要下载iChunUtil和Tabula两个模组放入1.12.2中，之后启动游戏
[相关模组下载地址](https://github.com/brianShan97/hello-world/tree/model)
![cr8.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_805b882aaf-cr8.png) 
#### 由于我们本次是制作僵尸的同类，所以我们找到僵尸的模型导入


1. 点击"从Minecraft导入"
![cr9.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_2d8b159aaf-cr9.png) 
2. 找到Zombie的模型，双击导入。
![c1.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_36d4e309af-c1.png)
3. 对模型进行修改后，点击保存
![c2.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_7f780a19af-c2.png) 
4. 保存后点击导出项目 -> 导出为Java项目
![c3.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_4aaa659daf-c3.png) 
5. 我们保存的名称为 包名.model ，命名为ModelRA3() (与第4步中RenderRA3中的名称对应)
![c5.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_dc0fd780af-c5.png) 
![c4.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_98ffb0c7af-c4.png) 
6. 点击导出项目 -> 保存实体的 texture map(材质映射)
![c6.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_231206baaf-c6.png) 
7. 完成操作后可以关闭游戏

### 7.在MC中找到mods文件夹 -> 找到tabula -> 找到export -> 找到.Java和.png文件(物体的模型和皮肤)
![c7.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_93a704f2af-c7.png) 
### 8.在entity包中新建 model 包
![c8.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_aded6bb6af-c8.png) 
### 9.将export中的.java文件放入entity.model文件(放置模型文件)
![c9.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_b546a152af-c9.png) 
### 10.对Main.java中PreInit函数的进行修改
```
	public static void PreInit(FMLPreInitializationEvent event)
	{
		RegistryHandler.preInitRegistries( );
	}

```
### 11.在resources文件夹下的 textures 包中新建 entity 包
![d1.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_70b0f296af-d1.png) 
#### 将 export 中的.png文件加入到entity包中,名称和RenderRA3.java中保持一致
![d2.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_5c88cb92af-d2.png) 

### 12.在assets中的 lang文件中加入我们实体刷怪蛋的名称
```
//entities
entity.ra3.name=RA3
```
### 13保存文件 -> 启动游戏 -> 找到刷怪蛋
![d3.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_34084fe8af-d3.png) 
![entit.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_40f923e7af-entit.png) 
我们的Zombie出现，芜湖！

### 演示材质
![ra3.png](https://cdn.acwing.com/media/article/image/2021/05/07/39383_6459df54af-ra3.png) 
### 关于材质绘制：我们可以使用PS，画图软件(Windows自带)进行材质的制作
