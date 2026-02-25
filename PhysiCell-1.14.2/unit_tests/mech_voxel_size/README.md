## Visual explanation of why different mechanics voxel sizes lead to different results

<img src="mech_sizes_20_25_v2.png" width="700" />

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
