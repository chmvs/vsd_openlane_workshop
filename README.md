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

           










