# g_surf
Analyze membrane thickness and curvature profiles

This repository contains the binary for `g_surf`, a program to calcualte membrane physical properites. 
`g_surf` can calculate membrane densities, thickness, and gaussian as well as mean curvature profiles. 

To use `g_surf` you need the following: 
- you need to generate an `.mdp` file and provide it as input to the program. An example `.mdp` file is provided with this repository. 
- The software requires a lipid definition (think of it as its own topology). The file `LIPIDS.lib` contains the currently supported lipid definitions. 
- Define the lipids to include in the analysis (using `l-grp1.dat`) and exclude (using `l-grp2.dat`). 
- Finally, `g_surf` has gromacs as a dependency, so you will need to install and source it first. 
 
All of those requirements may sound like a lot, but in practice to get `g_surf` running you need only run: 

```sh
export GMX_MAXBACKUP=-1
g_surf -f protein.mdp -tr trajectory.xtc -c coordinates.gro -po out.mdp 
```

You can tweak many of the options used by `g_surf` by modifying the input `mdp` file. For example, if you want to calculate the density of cholesterol in the system, you make sure to uncomment the adequate line in the input mdp file, put CHOL in the l-grp1.dat file and put all the other lipids in the l-grp2.dat file (separated by newline). 
