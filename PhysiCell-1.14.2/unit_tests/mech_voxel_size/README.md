## Explanation of why different mechanics voxel sizes can lead to different results


Let's begin with an agreed upon premise: running a simulation on the same machine (same OS release, same compiler, etc), with 
* the same model parameters,
* same initial conditions (ICs),
* no cell rules,
* using a single thread (1 core), and
* using the same seed for the PRNG (pseudo-random number generator),

we should get the very same, exact, bitwise reproducible results.

Now, what happens if we change just one model parameter - the mechanics voxel size? Will that affect reproducibility and, if so, by how much? In this unit test, we do just that: we compare a simulation using mechanics voxel size =20 to another using 25; all other parameters are the same.

The model is quite simple: it has a single cell type, default, and the ICs has a single cell starting at the origin (0,0). At the end of our simulations, we see these results - the left using mechanics voxel size=20, the right =25. One thing to point out are that the cell pressures are quite different - notice the colorbars. The left has a max of ~0.45; the right a max of ~0.7. Why? Because a cell's pressure is a function of its neighbor cells and when we have different mechanics voxel sizes, it is quite possible for a cell to have a different number of neighbors (as is the case here).

<img src="final_time_compare.png" width="600" />


<img src="mech_sizes_20_25_v2.png" width="600" />

Note the x-positions differ for cell ID 8 (lower center). Why?

```
(base) M1P~/git/mech_grid_xml$ python beta/plot_cell_ids.py output_mech_voxel_20 1240 20
-->
nbrs= {0: {5, 7, 8, 9, 10}, 2: {9}, 3: {9}, 4: {8, 10, 6}, 5: {0, 10, 7}, 6: {8, 4}, 7: {0, 5},
8: {0, 9, 10, 6},
9: {8, 0, 2, 3}, 10: {0, 8, 4, 5}}

(base) M1P~/git/mech_grid_xml$ python beta/plot_cell_ids.py output_mech_voxel_25 1240 25
-->
nbrs= {0: {5, 7, 8, 9, 10}, 2: {9}, 3: {9}, 4: {8, 10, 6}, 5: {0, 10, 7}, 6: {8, 4}, 7: {0, 5},
8: {0, 4, 6, 9, 10},
9: {8, 0, 2, 3}, 10: {0, 8, 4, 5}}
``
