# Run the GOMC simulation in NPT for 1 million steps from equilibrated system.
# Assuming that GOMC base directory was cloned in your Desktop:

~/Desktop/GOMC/bin/GOMC_CPU_NPT +p4 water_SPCE.conf > output_water.log &

# Or if you have CUDA installed in your machine use the following command:

~/Desktop/GOMC/bin/GOMC_GPU_NPT water_SPCE.conf > output_water.log &

# You can monitor the simulation by running the following command: 

tail -f output_water.log

# Wait until simulation finished, then exit command by typing "ctrl C"
# To generate the RDF, we use vmd to calculate the RDF. Load the GOMC output 
# PDB and PSF file into vmd.

vmd SPCE_300_00_K_RDF_merged.psf  SPCE_300_00_K_RDF_BOX_0.pdb &

# Under "Extensions" tab, select "Analysis", the click on 
# "Radial Pair Distribution Function g(r)". Follow the steps on opened window
# 1- To select the file, click on "(none)" and select 
#    "0 SPCE_300_00_K_RDF_merged.psf".
# 2- Select the residue name that you want to calculate RDF. Type "type OT" 
#    in Selection 1 and Selection 2.
# 3- Check mark on "Save to File".
# 4- Click the "Compute g(r)" button to plot and save the g(r).
# 5- Click the "Save" button on the open window.
# 6- Close the vmd application from VMD main window.

# To extract the total energy and steps number use the following command:

cat Blk_SPCE_300_00_K_RDF_BOX_0.dat | awk '{print $1 " " $2}' > energy.dat

# To extract the density and steps number use the following command:

cat Blk_SPCE_300_00_K_RDF_BOX_0.dat | awk '{print $1 " " $11}' > density.dat

