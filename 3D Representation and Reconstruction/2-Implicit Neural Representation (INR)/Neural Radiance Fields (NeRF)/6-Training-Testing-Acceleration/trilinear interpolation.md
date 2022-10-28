采用一种新的视角**来统一地看待** LoD, hash, tensoRF, eg3d 等工作的表征方式：

- 空间的显式划分仍然是  single_tree + batch_trees + forest_trees  三选一 + LoDTree；具体实现方式仍可使用 CUDA kernel 来显著提速；
- 区别在于，具体一个 LoDTree中的参数的数学调用、梯度回传公式，是直接 dense，还是有一定的重复使用或者科学的分解规则，是可以配置的（配置在 kernell 中的 grid_val 函数 和 add_grid_gradient 函数中）





![image-20220329114118887](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/image-20220329114118887.png)



Trilinear interpolation









replace MLP modules by caching the whole scene in voxels



tree-based 
