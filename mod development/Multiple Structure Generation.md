#### Make sure you have watched Hary's tutorial video:[Structures - Minecraft Modding Tutorial 1.12.2 - Episode 15](https://www.youtube.com/watch?v=cq1wNwuGxu4)
### Just use a "next" number to make sure what building to be built
```
package com.Joy187.newmod.world;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Random;
import com.Joy187.newmod.blocks.MutamyceteBlock;
import com.Joy187.newmod.init.ModBlocks;
import net.minecraft.block.Block;
import net.minecraft.init.Blocks;
import net.minecraft.util.math.BlockPos;
import net.minecraft.world.World;
import net.minecraft.world.WorldType;
import net.minecraft.world.biome.Biome;
import net.minecraft.world.biome.BiomePlains;
import net.minecraft.world.biome.BiomeSavanna;
import net.minecraft.world.biome.BiomeStoneBeach;
import net.minecraft.world.chunk.IChunkProvider;
import net.minecraft.world.gen.IChunkGenerator;
import net.minecraft.world.gen.feature.WorldGenerator;
import net.minecraftforge.fml.common.IWorldGenerator;

public class ModWorldGenCustomStructure implements IWorldGenerator {
	private int next = 1;  //this deside to spawn the buiding


	@Override
	public void generate(Random random, int chunkX, int chunkZ, World world, IChunkGenerator chunkGenerator,
			IChunkProvider chunkePrvider) {
		if (world.provider.getDimension() == 0) {
			if(next==1) //if next is 1,generate building 1
				this.generateStructureXC(new ModWorldGenStructure("xchamberx"), world, random, chunkX, chunkZ, 35, Blocks.GRASS, BiomePlains.class);
			else      //generate building 2
				this.generateStructureDCH(new ModWorldGenStructure("dchurc"), world, random, chunkX, chunkZ, 35, Blocks.GRASS, BiomePlains.class);
      //you can continue to do this on building 3、4、5……
		}
	}

	private void generateStructureXC(WorldGenerator generator, World world, Random random, int chunkX, int chunkZ,
			int chance, Block topBlock, Class<?>... classes) {
		ArrayList<Class<?>> classesList = new ArrayList<Class<?>>(Arrays.asList(classes));
		int x = (chunkX * 32) + random.nextInt(15) +8;
		int z = (chunkZ * 32) + random.nextInt(15) +8;
		int y = calculateGenerationHeight(world, x, z, topBlock);
		BlockPos pos = new BlockPos(x, y, z);

		Class<?> biome = world.provider.getBiomeForCoords(pos).getClass();
		if (world.getWorldType() != WorldType.FLAT) {
			if (classesList.contains(biome)) {
				if (random.nextInt(chance) == 0) {
					generator.generate(world, random, pos);
					next=0; //once your building has built,change the value of next 
				}
			}
		}
	}
	
	private void generateStructureDCH(WorldGenerator generator, World world, Random random, int chunkX, int chunkZ,
			int chance, Block topBlock, Class<?>... classes) {
		ArrayList<Class<?>> classesList = new ArrayList<Class<?>>(Arrays.asList(classes));
		int x = (chunkX * 32) + random.nextInt(15) +8;
		int z = (chunkZ * 32) + random.nextInt(15) +8;
		int y = calculateGenerationHeight(world, x, z, topBlock);
		BlockPos pos = new BlockPos(x, y, z);

		Class<?> biome = world.provider.getBiomeForCoords(pos).getClass();
		if (world.getWorldType() != WorldType.FLAT) {
			if (classesList.contains(biome)) {
				if (random.nextInt(chance) == 0) {
					generator.generate(world, random, pos);
					next=1;    //once your building has built,change the value of next 
				}
			}
		}
	}
	
	private static int calculateGenerationHeight(World world, int x, int z, Block topBlock) {
		int y = world.getHeight();
		boolean foundGround = false;

		while (!foundGround && y-- >= 0) {
			Block block = world.getBlockState(new BlockPos(x, y, z)).getBlock();
			foundGround = block == topBlock;
		}
		return y;
	}

}

```
