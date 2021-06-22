# 10ps_simulation
A 10ps of equilibration with varying constraints and production is done to verify the code and to verify the input and output files to use it later in cluster.

simulation is done using GROMACS 2018. the protein used here is rP2X1 homology model built using template hP2X3 (5svj)

steps:
1) orientation of the protein using opm server
2) Protein embedding with membrane using  using g_membed: different methods are tried to align the protein properly to the membrane.
4) energy minimisation
5) NVT equilibration with position restraints on the protein of force constant 1000 kj/mol/nm2 and run for 10ps
6) NPT equilibration with position restraints on the protein of force constant 1000 kj/mol/nm2 and run for 10ps
7) NPT equilibration with restraints on backbone of force constant 1000 kj/mol/nm2 and run for 10ps
8) NPT equilibration with restraints on c-alpha atoms of force constant 1000 kj/mol/nm2 and run for 10ps
9) production with no restraints for 10ps

STEP1: Orientation of the protein using Opm server
1) rP2X1 homology model is built usinmg the software Modeller 10.0. The sidechains are modelled using scwrl4 program : rP2X1_sc.pdb
2) opm server (https://opm.phar.umich.edu/ppm_server) is used for the proper orientation of the protein in membrane and the output from the server is saved as rP2X1_opmout.pdb
3) rP2X1_sc.pdb is aligned to rP2X1_opmout.pdb in pymol and molecule is saved as rP2X1_opm.pdb
4) this is used to generate topology file in GROMACS 2018.
 
STEP2: Protein embedding in pre-equilibrated lipid bilayer
Different methods are done to get the proper embedding on protein in membrane: CHARMM36m_POPCbilayer.pdb is a pre equilibrated lipid bilayer which I got it from Saskia (works at Juelich)
Note: the rP2X1 has a huge extracellular domain and when inserted into membrane some part of it is not covereed with teh solvent of the pre equilibrated membrane.
1) Method1_Unsuccesful: the water and ions that are present in the membrane are removed completely and the box size is increased. Then the water is added again and embedding is done after removing the water in lipid bilayers. Result: stopped at step0: stating bad contacts and bad rotations and cannot make triclinic boxes. I even decraesed the time step to 1fs this time I got the error stating only about the bad contacts and bad angles.
2) Method2_succesful: I ran the simulation without any solvent and with only lipids, protein. REsult: protein was embedded in the membrane.
3) Method3_ Succesful: using gms genconf tool: a grid of molecules with specifies dimensions can be obtained.so I used this to make two lipid layers in z direction and teh protein is aligned in teh second lipid layer. by this it can be covered with solvent present from the above lipis layer and also below lipid layer and after embediing the above lipid layer and the complete solvent, ions are removed. REsult: took more time due to increase in system size but teh protein is properly embedded. the only probelm is I didnot number the protein chains so all the three chains are combined in input file and is shown as monomer when you click show as cartoon. When you run energy minimisation later the error occurs showing mismatched atoms because of this.
4) Method4_ succesful: even though the protein is not covered with solvent. tHe box size is increased and did the simulation. Result: it worked and the solvent molecules moved and covered theprotein.

STEP3: energy minimisation
For thi step Method4 output is selected again tries two methods: Method4.1 and Method 4.2
1) Method4.1: the output of protein embedded in membrane : rP2X1_POPCmembrane.pdb is directly energy minimised without adding any further solvent. 5000 steps of steepest descent is done.
2) Method 4.2: the output rP2X1_POPCmembed.pdb is olvated to cover the remaining part of the protein. The water present in between the lipid bilayer is then removed using the waterdeletor.pl script present in the gromacs tutorial. then energy minimised until the force converges to  <1000
