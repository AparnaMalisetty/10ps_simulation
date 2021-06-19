# 10ps_simulation
A 10ps of equilibration with varying constarints and production is done to verify the code and to verify the input and output files to use it later in cluster.

simulation is done using GROMACS 2018. the protein used here is rP2X1 homology model built using template hP2X3 (5svj)

STEPS: 
1) Protein alignment with membrane using opm server: different methods are tried to align the protein properly to the membrane.
2) embedding the protein in membrane using g_membed
3) energy minimisation
4) equilibration with constarints on protein
5) equilibration with constraints on heavy atoms
6) equilibration with constraints on c-alpha atoms
7) production

