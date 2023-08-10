## Steps

1. Install Vivado and Vitis

2. Add Vivado and Vitis bin folders to path

3. Clone analogdevicesinc/hdl repository

4. Open Vivado tcl console
   1. go to hdl/scripts
   2. make sure Vivado version from adi_env.tcl is the same as the installed version
   3. $ source ./adi_env.tcl

   or

    to build library manually
    (optional)
    Tcl Console:
        go to hdl/library
        go to library folder
        ./source <name>_ip.tcl

5. Build project
   1. go to hdl/projects
   2. go to project folder
   3. go to board subfolder
   4. $ make
	outputs <project_name>.sdk/system_top.xsa

6. Obtain u-boot.elf
    a. build it
    b. take it from the formated SD card -> project folder -> bootgen_sysfiles.tgz

7. Build Zynq boot image BOOT.BIN (Linux)
   1. need system_top.xsa and u-boot.elf
   2. get script from
        https://raw.githubusercontent.com/analogdevicesinc/wiki-scripts/master/zynq_boot_bin/build_boot_bin.sh
   3. chmod +x build_boot_bin.sh
   4. $ build_boot_bin.sh system_top.xsa u-boot.elf [output-archive]


Cora Z7s constraints file

constraints template
    https://github.com/Digilent/digilent-xdc/blob/master/Cora-Z7-07S-Master.xdc

schematic
    https://s3-us-west-2.amazonaws.com/digilent/resources/programmable-logic/cora-z7/Cora+Z7_sch-public.pdf

ad7195 asdz board
    P5 - DIGI1
        10 -> cs
        11 -> din
        12 -> dout
        13 -> sclk


adc_spi_sclk =			ja_n[2] = JA[4]
adc_spi_miso_rdyn =		ja_p[2] = JA[3]
adc_spi_mosi =			ja_n[1] = JA[2]
adc_spi_csn = 			ja_p[1] = JA[1]
