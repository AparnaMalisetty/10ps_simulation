# 10ps_simulation
A 10ps of equilibration with varying constraints and production is done to verify the code and to verify the input and output files to use it later in cluster.

simulation is done using GROMACS 2018. the protein used here is rP2X1 homology model built using template hP2X3 (5svj)

steps:
1) orientation of the protein using opm server
2) Protein embedding with membrane using  using g_membed: different methods are tried to align the protein properly to the membrane.
4) energy minimisation
5) equilibration with constraints on protein
6) equilibration with constraints on heavy atoms
7) equilibration with constraints on c-alpha atoms
8) production

STEP1: Orientation of the protein using Opm server
1) rP2X1 homology model is built usinmg the software Modeller 10.0. The sidechains are modelled using 
Different methods are done to get the proper embedding on protein in membrane: CHARMM36m_POPCbilayer.pdb is a pre equilibrated lipid bilayer which I got it from Saskia (works at Juelich)
Note: the rP2X1 has a huge extracellular domain and when inserted into membrane some part of it is not covereed with teh solvent of the pre equilibrated membrane.
1) Method1_Unsuccesful: the water and ions that are present in the membrane are removed completely and the box size is increased. Then the water is added again and embedding is done after removing the water in lipid bilayers. Result: stopped at step0: stating bad contacts and bad rotations and cannot make triclinic boxes. I even decraesed the time step to 1fs this time I got the error stating only about the bad contacts and bad angles.
2) Method2_succesful: I ran the simulation without any solvent and with only lipids, protein. REsult: protein was embedded in the membrane.
3) Method3_ Succesful: using gms genconf tool: a grid of molecules with specifies dimensions can be obtained.so I used this to make two lipid layers in z direction and teh protein is aligned in teh second lipid layer. by this it can be covered with solvent present from the above lipis layer and also below lipid layer and after embediing the above lipid layer and the complete solvent, ions are removed. REsult: took more time due to increase in system size but teh protein is properly embedded. the only probelm is I didnot number the protein chains so all the three chains are combined in input file and is shown as monomer when you click show as cartoon. When you run energy minimisation later the error occurs showing mismatched atoms because of this.
4) Method4_ succesful: even though the protein is not covered with solvent. tHe box size is incraesed and did the simulation. Result: it worked and the solvent molecules moved and covered theprotein.
