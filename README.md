# g_surf
Analyze membrane thickness and curvature profiles. Note that currently it only supports the Martini model. 


Note: We are working on writing some tutorials on how to use g_surf and also integrate it as part of `prolintpy`. In the meantime, please have a look at the following link to see how g_surf is used within the ProLint framework: https://github.com/ProLint/ProLint/blob/main/prolint/calcul/tasks.py#L373

This repository contains the binary for `g_surf`, a program to calcualte membrane physical properites. The source code is available here: https://github.com/IBIxsoftware/g_surf

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

## Python Wrapper
We will soon release a python wrapper script that you can use to interface with `g_surf`. For now, you can have a look at how ProLint uses it in its workflow here: https://github.com/ProLint/ProLint/blob/main/prolint/calcul/tasks.py#L323 which accomplishes largely the same thing. 

## Citation
ProLint and its associated tools are research software. If you make use of them in work which you publish, please cite them. The BibTeX reference is

```
@article{10.1093/nar/gkab409,
    author = {Sejdiu, Besian I and Tieleman, D Peter},
    title = "{ProLint: a web-based framework for the automated data analysis and visualization of lipid–protein interactions}",
    journal = {Nucleic Acids Research},
    year = {2021},
    month = {05},
    issn = {0305-1048},
    doi = {10.1093/nar/gkab409},
    url = {https://doi.org/10.1093/nar/gkab409},
    note = {gkab409},
    eprint = {https://academic.oup.com/nar/advance-article-pdf/doi/10.1093/nar/gkab409/38270894/gkab409.pdf},
}
```
  
