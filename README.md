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

Different methods are done to get the proper embedding on protein in membrane: CHARMM36m_POPCbilayer.pdb is a pre equilibrated lipid bilayer which I got it from Saskia (works at Juelich)
Note: the rP2X1 has a huge extracellular domain and when inserted into membrane some part of it is not covereed with teh solvent of the pre equilibrated membrane.
Method1: 
