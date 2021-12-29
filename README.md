![image](https://github.com/automatanism/UNITY_3D_INDIVIDUAL_BRICK_BLOCK_DESTRUCTION/blob/main/thumb_jpg.jpg)

# UNITY_3D_INDIVIDUAL_BRICK_BLOCK_DESTRUCTION
Quick instructions on how to accomplish brick/brick destruction. (contact me here if my game code for unity 2019.4.14f1 is desired for educational purposes etc. Hefty, 20 gigabytes uncompressed, 10gb download google drive)


Author: God Bennett, [Extortionist gameplay](https://youtu.be/B4mDnA1M0nE)

Game (around 20gb, has around 6800+ buildings based on real world GIS location
data/Jamaica/Montego Bay, although the only 1 destructive instance seen in video, along with
vegetation biome, dynamic grass, aura lighting etc)!

For destruction, with a little trick of mine on top, I used [DinoFracture plugin](https://assetstore.unity.com/packages/tools/physics/dinofracture-a-dynamic-fracture-library-26599). (See [a youtube video on basic setup](https://www.youtube.com/watch?v=Ob915rNk3-k))

In short [without the trick, one typically gets large cracks of entire walls](https://www.youtube.com/watch?v=Kn8YgywItXQ&feature=youtu.be), where instead I sought
to get the brick by brick destruction seen in my video.

1. I started with an individual concrete block/brick, preferably low poly. (Use unity mesh
simplify or blender etc, around 800 faces doesn't pressure my gtx 1060/i76700 too much)

2. I then auto-computed pre-fracture data using [DinoFracture plugin](https://assetstore.unity.com/packages/tools/physics/dinofracture-a-dynamic-fracture-library-26599), using a total of about 94 chunks for an individual concrete block/brick (in the Dino Unity ui/pre-fractured
option, you get 94 resulting from input of 10, 2 iterations, and 1 generation), in my case.
More than this combo can lead to unity halts depending on the complexity of input
model.

3. The process above creates a new folder sharing the name of your single brick/block, and
also the original brick item with the guiding pre-fracture script etc.

4. Next, I organized the brick into a collection, a front wall GameObject group, rear, left
and right. Each brick/block to my knowledge, will require a unique prefab collection, so
simply duplicate each brick with and collection, which automatically assigns pairings of
guiding brick and prefrac collection.

5. Why group the bricks into collections above? If not I would end up with hundreds of
bricks in my project hierarchy, and working on the project would become a huge mess.

6. However, grouping came with an issue. Instead of the nice individual chunks one gets
with the single brick collision, one instead gets large chunks erupting upon collision
when the bricks are grouped, i.e. even if the guiding original bricks are in the same level
with the prefac folders. Solution was one line of code attached to each brick collection,
which simply unlinked the brick/prefac folder from parent group name at runtime, and
precise/chunk eruption returned:

![image](https://github.com/automatanism/UNITY_3D_INDIVIDUAL_BRICK_BLOCK_DESTRUCTION/blob/main/frac_correction_on_grouping.png)

Future work: Some type of dynamic collision system, [like seen in this one other similar unity 3d video of brick destruction on a smaller scale, although the system in the video seems to freeze everytime a brick is destroyed](https://youtu.be/_-WdU4VQjZI), unlike my system or [this unreal engine sleeping function that kills simulation of already grounded/fractured pieces](https://youtu.be/VWzCMGcC6eA?t=610). Apart from the 6 DinoFracture steps above, another reasonably fast unity destruction that seems to do individual bricks is seen [in CaronteFx](https://youtu.be/JqctvCmlky0).
