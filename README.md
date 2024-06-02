# vsd_openlane_workshop
This workshop is based on how to RTL netlist into a tape-out. This workshop is organized by VLSI system design in collaboration with NASSCOM.

# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 

`Move to the directory where Openlane is Installed

cd Desktop/work/tools/openlane_working_dir/openlane

Start the Docker container and enter the OpenLANE shell:

docker

./flow.tcl -interactive`

![Screenshot 2024-05-29 110933](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/252b9f00-5ab7-4bc4-8337-93a2a838a2da)

**Initilize the environment**

package require openlane 0.9

**The picorv32a Directory**

prep -design picorv32a

![Screenshot 2024-05-29 111058](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/6e7b5dbd-a2f9-49d6-bf05-15ad0c06a2e3)
![Screenshot 2024-05-29 111211](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/2d06997c-160b-42ae-a3b9-3df4cc474fa4)

Now we can see that there is a directory created(check timestamp) under which we could navigate to the runs directory where we can find the `merged.lef`
![Screenshot 2024-05-29 111306](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/c11615a8-f288-4079-a310-71fd2bbd4aed)
![Screenshot 2024-05-29 111334](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/7df6a0b8-c614-43b9-9e66-cf5b55c71dfc)

We can see the specs about the vias metal layer cuts and the dimension

**Synthesis**

`run_synthesis`

![Screenshot 2024-05-29 111509](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/969aeaba-202a-4186-bdbe-4d9c7860ff26)

After Running the synthesis command we can see the update inside the design directory of openlane where we have the picorv32a (check the modified date) `/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_11/results/synthesis`

![Screenshot 2024-05-29 111628](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/ec64db54-4a96-4754-b37e-4bc28389766d)

![Screenshot 2024-05-29 111734](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/079a54c6-989a-4d77-bdfa-fdd75db46b6a)

![Screenshot 2024-05-29 111823](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/806ba9ce-1467-4641-8d3c-1e72a751f36e)

![Screenshot 2024-05-29 111844](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/830d8bb5-d8f1-4c17-a2f9-091aa8187e4d)

![Screenshot 2024-05-29 111509](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/e5eaf253-4f59-43a3-b3d1-ab4941d73fad)

**Synthesis results**

Flop ratio = (Number of D flip flops)/(Total number of cells)

           = 1613/14876
           
           = 0.1084

DFF's percent = Flop ratio * 100 = 10.84% 

# Section 2 - Goodfloorplan vs bad floorplan and introduction to library cells

**What's inside the README.md of Config files?**

![Screenshot 2024-05-29 112043](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/94c54cea-4164-476f-8bb0-66a9bce56af2)

This gives a documentation the various settings are user can use by help of the switches we we can set in the `~/Desktop/work/tools/openlane_working_dir/openlane/configuration/floorplan.tcl`

**Inside the floorplan.tcl**

![Screenshot 2024-05-29 112122](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/3cddd917-e8d3-4157-9c7c-bbfb7a3a5eb8)

In the openlane interactive mode

`run_floorplan`

![Screenshot 2024-05-29 180857](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/65be8579-2bfd-42a5-8ee0-a9e91c62a8f1)

**floorplan.def was updated as shown in the below image**

![Screenshot 2024-05-29 180857](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/65be8579-2bfd-42a5-8ee0-a9e91c62a8f1)

**Reviewing the floorplan reports**

`~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-05_05-22/results/floorplan
`
![Screenshot 2024-05-29 181123](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/9e33bb6f-8009-4fd1-91a1-60578aa61d3e)

**picorv32a.floorplan.def.png**

![Screenshot 2024-05-29 181344](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/ed9f6833-30b4-4144-b27f-5bcac83c614b)

**Inside the picorv32a.floorplan.def**

![Screenshot 2024-05-29 181434](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/a480f788-f288-41e2-a08b-a806f79cb511)

**OBSERVATIONS FROM THE FLOORPLAN RESULTS**

Given 1000 unit distance = 1 Micron

Die width = 660685 in unit distance = 660.685 microns

Die height = 671405 in unit distance = 671.405 microns

Area of the die = 660.685*671.405 = 443587.212425 sq microns.

# Layout in Magic Tool

**Inside the config.tcl**

`~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/config.tcl`
![Screenshot 2024-05-29 181542](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/1761a963-b5c8-45e0-8779-015e31f929f5)

We need a lef and def file along with pdk's techfile into order to map accordingly and view the floorplan in the Magic

`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
`
![Screenshot 2024-05-29 183709](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/56008f26-6548-41c0-8648-6ca2cf986d05)

**Decap cells**

![Screenshot 2024-05-29 183809](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/334fb1f7-0a5c-48f7-b321-c6957c007122)

**An overview of decap tap cells**

![Screenshot 2024-05-29 183936](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/43f8a407-f4e5-41c8-8775-147250a18c7d)

`Click on any cell and select it, Then press "S" which will open a tkcon window and type "what" to get a brief note on the selected cell" 
`
![Screenshot 2024-05-29 184023](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/c16ce89e-e4e6-4c94-b66c-6f3cfb085de9)

**Standard cells placed at the bottom of the layout**

![Screenshot 2024-05-29 184238](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/84c99cab-f098-4305-949c-7eb71f2705f4)

**Complete layout**

![Screenshot 2024-05-29 182914](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/0eb99317-ab9d-44d1-a91b-4f149cbd8d8b)
Right click on z to zoom 

**PLACEMENT**

`run_placement`

![Screenshot 2024-05-31 064147](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/a6167592-722b-4917-86d9-079d21a09405)
![Screenshot 2024-05-31 064217](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/cb84b6d0-04da-441c-9ba7-8457ddfe9f1d)
![Screenshot 2024-05-31 064039](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/8239d7e2-53bc-499f-aa33-a3698d3ad7d9)

**PLACEMENT RESULTS**

![331088445-fa1278d2-0e85-4e23-a439-75d48a48f8e7](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/04110370-f9fc-4689-88ba-a7050bdee278)

# Change directory to path containing generated placement def

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Screenshot of floorplan def in magic

![Screenshot 2024-05-31 065220](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/db18eddc-2aab-4bbd-8553-f9d1806bf4d1)

![Screenshot 2024-05-31 065427](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/8691d696-96e0-4958-9a89-69d92b121f7e)

![Screenshot 2024-05-31 065311](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/6450e628-5f85-4b63-83e2-cb8a5cd03ae2)

![Screenshot 2024-05-31 065345](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/52b70240-3eee-4513-b801-6fb8b3fcbc34)

**TRYING DIFFERENT SWITCHES**

With the default configuration

![Screenshot 2024-05-31 073649](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/e0f5cc33-6657-4358-aa0d-de327642da5c)

In the openlane interavtive window

`set ::env(FP_IO_MODE) 2`

`inside the ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-05_05-22/results/floorplan
`

`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
`
![Screenshot 2024-05-31 073726](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/ec6e57ca-8182-4fc4-bcef-e07484a6b943)

# Section 3 - Design library cell using Magic Layout and ngspice characterization

`git clone https://github.com/nickson-jose/vsdstdcelldesign.git
`

We need to clone the working directory in the above github repo

To view th CMOS inverter layout use 

`magic -T sky130A.tech sky130_inv.mag &
`

![Screenshot 2024-05-31 120331](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/b59e84c6-62ea-4116-a21f-2f79ef790efe)

**DEFINING THE LAYERS**

![Screenshot 2024-05-31 142344](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/f74d8775-7446-4078-8604-55b08a735859)

![Screenshot 2024-05-31 142425](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/972937a0-8920-4a0d-8542-1d7c076f3f64)

![Screenshot 2024-05-31 142448](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/a0046d6f-7dbb-4b44-8528-d1c3388c860b)

**Extracting the SPICE netlist**

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

`# Check current directory
pwd

**Extraction command to extract to .ext format**
extract all

**Before converting ext to spice this command enable the parasitic extraction also**
ext2spice cthresh 0 rthresh 0

**Converting to ext to spice**
ext2spice


Inside the `sky130_inv.ext` We can witness the extracted netlist information

![Screenshot 2024-05-31 151222](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/b9993740-dc80-4383-9191-d26524e79832)

Actual extracted spice netlist

![Screenshot 2024-05-31 151119](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/934366a9-d9cf-4af0-92f4-2dc48d2712b0)

Modified extracted spice netlist

`.option scale=0.01u

.include ./libs/pshort.lib

.include ./libs/nshort.lib

//.subckt sky130_inv A Y VPWR VGND

M1001 Y A VGND VGND nshort_model.0 ad=1.44n pd=0.152m as=1.37n ps=0.148m w=35 l=23

M1000 Y A VPWR VPWR pshort_model.0 ad=1.44n pd=0.152m as=1.52n ps=0.156m w=37 l=23

VDD VPWR 0 3.3V

VSS VGND 0 0V

C6 Y 0 2fF

Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)

C0 A VPWR 0.0774fF

C1 Y VPWR 0.117fF

C2 A Y 0.07f4fF

C3 Y VGND 0.279fF

C4 A VGND 0.45f

C5 VPWR VGND 0.781f

//.ends


.tran 1n 20n

.control

run

.endc

.end`

**SPICE SIMULATION RESULTS**

![Screenshot 2024-06-02 020215](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/e4b09a08-8cf6-4fb2-b8ba-5bf46de3ec72)

**RISE TIME**

x0 = 2.16151e-09, y0 = 0.659639  x0 = 2.20386e-09, y0 = 2.63012

Rise time transition 20% to 80% - time value = 43ps

FALL TIME

x0 = 4.04043e-09, y0 = 0.264059  x0 = 4.06827e-09, y0 = 0.662766

Fall time transition 20% to 80% - time value = 28ps

CELL RISE DELAY Calculated at 50% of VDD = 35ps

        x0 = 2.15e-09, y0 = 1.65189  x0 = 2.185e-09, y0 = 1.65094
        
CELL FALL DELAY Calculated at 50% of VDD = 20ps

        x0 = 4.06051e-09, y0 = 1.65147  x0 = 4.05492e-09, y0 = 1.65

**DRC ERRORS AND TECH FILE - AN OVERVIEW**

Link to Sky130 Periphery rules: https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

**Change to home directory**
cd

**Command to download the lab files**
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

**Since lab file is compressed command to extract it**
tar xfz drc_tests.tgz

**Change directory into the lab folder**
cd drc_tests

**List all files and directories present in the current directory**
ls -al

**Command to view .magicrc file**
gvim .magicrc

**Command to open magic tool in better graphics**
magic -d XR &

Scrrenshots of commands run

![Screenshot 2024-06-01 114549](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/d23db3fd-c5a9-4c6b-a561-425b7a711557)

Screenshot of .magicrc file

![Screenshot 2024-06-01 114638](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/44251670-7790-4eb8-8dd8-493a48b4256b)

open `met3.mag` in magic 

![Screenshot 2024-06-01 201655](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/7a36b945-b992-4369-a3d5-cd626fe2c3c9)
![Screenshot 2024-06-01 202926](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/964563c1-5771-481f-8ba4-6fbf957995d9)
![Screenshot 2024-06-01 203023](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/ecd35983-7592-44c8-bc02-d8327f99370f)
![Screenshot 2024-06-01 203228](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/98a0cdcd-b434-4628-8449-e40dd7fa37d2)

**Fixing poly.9 error in Sky 130 tech-file**

open the plu.mag file

`gvim sky130A.tech
`

![2222](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/b404fc32-0bc2-4da0-8bf9-887e5e172027)

`change to allpolynonres`

![Screenshot 2024-06-02 000729](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/2f6455ae-8049-41e9-a987-9b2f1f31bdb4)

![Screenshot 2024-06-02 004438](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/aec02618-74cf-481d-8a57-a075a35c78b3)

implement poly resistor spacing to diffusion and tap

add this line---------------------
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching illegal \
    "xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"

![Screenshot 2024-06-02 000827](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/15c8a59f-d61e-4298-8b20-815afdff2aa3)

![Screenshot 2024-06-02 003108](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/1ddd77a5-14fb-433e-ac58-435901d72dd4)

**Describing DRC error as Geometrical Construct**

First we need to open `nwell.mag`

New commands inserted in sky130A.tech file to update drc
![Screenshot 2024-06-02 014141](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/1909b8bc-aa41-4628-9987-8b4a5c00a696)

**Commands to run in tkcon window**

**Loading updated tech file**
tech load sky130A.tech

**Change drc style to drc full**
drc style drc(full)

**Must re-run drc check to see updated drc errors**
drc check

**Selecting region displaying the new errors and getting the error messages** 
drc why

After implementing the rules mentioned above
![Screenshot 2024-06-02 014238](https://github.com/chmvs/vsd_openlane_workshop/assets/129481779/2062fa05-8e3c-4414-8618-a0c2dac9f0b9)

# Section 4 - Pre-layout timing analysis and importance of good clock tree





















           










