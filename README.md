# Riscv-VSD

## This repository is intended to document the learning outcomes and experience of a 4-week workshop on RISC-V using Open source tools like yosys and Skywater 130nm PDK.

### Day 0

<details>
 <summary> Summary </summary>
	
Installed all required tools.
</details>	
	<details>
    <summary> Riscv GNU Toolchain</summary>

  ```bash 
    git clone https://github.com/riscv/riscv-gnu-toolchain
    sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool   
    patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev
    ./configure --prefix=/opt/riscv
    make
  ```
    
  ![gnutool](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/837c8d1f-48fb-4c40-9465-0d56a78147fa)
  ![gnutool2](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/22b75d96-368b-4af9-ab8d-3d12be9addd2)

  </details>
 <details>
 <summary> Yosys </summary>
   
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```
</details>
<details>
<summary> Iverilog </summary>
  
  ```bash
sudo apt-get install iverilog
 ```
![iverilog](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/cfaff753-c5cd-4c0f-ae22-ecca83fd724d)
</details>
<details>
 <summary> gtkwave </summary>
  
  ```bash
sudo apt-get install gtkwave
 ```
![gtkwave](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/8405619b-76be-4f70-bcbb-063253a1c740)
</details>
<details>
 <summary> OpenSTA </summary>

 ```bash
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
![opensta](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/4a8b624d-3615-4e2f-bae4-67b821ac4271)
</details>
<details>
  <summary> Ngspice </summary>

 ```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```
![ngspice1](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/797366ca-cfe9-40d5-b8dd-b1ae07bca036)
</details>
<details>
<summary> Magic </summary>
  
  ```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
 ```
![magic1](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/efadb056-1548-4298-865b-a29e4beba0f5)
![magic2](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/530caf36-3315-41a3-a979-ef287589e9a3)
![magic3](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/ca33ac28-baf6-42e8-b6cc-8a10bab02a1a)
![magicmain](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/bef109c7-7bc7-46b9-9e01-f9ba476eef6b)
</details>
<details>
<summary> OpenLane </summary>
  
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot
```
![openlane1](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/9f616a42-5d3f-4f03-a859-6896ff12da5f)
![openlane2](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/2683c2ce-5b9e-43b3-bbc8-504f57317103)
![openlanemain](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/88070cfb-9af7-4520-a203-0f5687bfd2ff)
</details>
<details>
  <summary> PDKs </summary>

```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```
![openlanemain2](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/a2dfe03b-cb5b-4ebb-a7a1-6c9b40947f78)

</details>

### Day 1
<details>
<summary>Identifying Instruction Type</summary>
<br><br>
<strong>In RISC-V, the base instruction format is a 32-bit instruction word divided into several fields. The basic format consists of opcode, rd (destination register), funct3 (function 3), rs1 (source register 1), imm (immediate value), and funct7 (function 7). This design allows for a wide range of instructions while maintaining simplicity and flexibility, which are key principles of the RISC-V architecture.</strong>
	
<br><br>
 
```add r6,r2,r1``` 
<br><br>
This is an R type instruction - instructions using 3 register inputs
– add, xor, mul —arithmetic/logical operations.

32-bit instruction format of R-format:
<ul>
<li>opcode: Partially identifies the operation type (add in this case) (Bit 0 to Bit 6)</li>
<li>rd: Specifies the destination register where the result will be stored (r6) (Bit 7 to Bit 11)</li>
<li>funct3: Further encodes the operation (000 for addition) (Bit 12 to Bit 14)</li>
<li>rs1: Specifies the first source register to be added (r2) (Bit 15 to Bit 19)</li>
<li>rs2: Specifies the second source register to be add (r1) (Bit 20 to Bit 24)</li>
<li>funct7: Specifies the exact operation to be executed (Bit 25 to Bit 31)</li>
</ul>


```add x1, x2, x3  R-type``` <br>
0000000 00011 00010  &emsp; 000  &emsp; &nbsp;&ensp; 00001 &emsp; 0110011 <br>
funct7 &emsp; &nbsp; x3 &emsp;  &ensp; x2  &emsp;  &ensp;funct3 &emsp; &emsp;x1  &emsp;  &ensp;opcode

![rv-32bit](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/2f492828-7592-4467-9083-f02a935318d5)
</details>

## Day 2
<details>
<summary>Compiling C code using Risc-V GNU Toolchain</summary>
<br>
 
```bash
#include<stdio.h>
int main() {
  int sum=0, i=1, n=100;
  for(i = 1; i <= n; ++i){
    sum += 1;
  }
  printf("Sum of numbers from 1 to %d is %d \n",n,sum);
  return 0;
}
```
<details>
<summary>optimization -O1</summary>

```riscv64-unknown-elf-gcc -O1 -mabi=lp64  -o sum.o sum.c```
 
![optimization_1](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/a4c92f40-a159-4448-8662-8e483592cc64)
</details>
<details>
<summary>optimization -Ofast</summary>

```riscv64-unknown-elf-gcc -Ofast -mabi=lp64  -o sum1ton.o sum1ton.c```
 
![optimization_fast](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/69fa4d0d-cbd5-4dc9-a884-4a722516f741)
</details>
</details>

## Day 3
<details>
<summary>Checking if output of GCC and RISC-V GCC is same </summary>
<br>
The C code should give the same output when compiled using GCC X86 Compiler (F1) and riscv compiler (F2) (SPIKE Simulation)

<br> <br>

	
![Screenshot from 2024-03-03 15-37-56](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/6a2b1dba-737a-4ffe-aaf9-7f435e967ad3)

![Screenshot from 2024-03-03 15-41-06](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/e94d3438-c6f4-4c08-ba6a-bfbb9fe714ea)

</details>

## Day 4
<details>
<summary>Running Verilog code and Testbench using IVerilog and simulating waveforms</summary>
<br>
	
![riscv_block](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/d53109b1-78a7-444d-ae39-54f62622ac9c)	
<br>
 
Instruction to be run -

 ```Instruction 1:add r6,r2,r1```
<br>
<strong>Verilog Design Code</strong>

```iiitb_rv32i.v```
<br>
<strong>Verilog Testbench</strong>

```iiitb_rv32i_tb.v```
<br>

![Screenshot from 2024-03-03 17-42-41](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/1411c325-b5fb-4a11-89b3-3911185fb554)

```GTK Waveform Simulations```

![Screenshot from 2024-03-15 15-21-10](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/9a03f228-f43d-4d1d-9489-aaceab80863a)

<br>

![Screenshot from 2024-03-14 21-57-08](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/d1779245-3ab6-491e-88f7-0ddf5b7e5285)

<br>

![Screenshot from 2024-03-14 22-00-05](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/eb5e1b2b-a6a7-40aa-b81a-4c438fbc964c)

<br>
<strong>Where ID_EX_A and ID_EX_B are the Oprands,ADD=0 is operation, EX_MEM_ALUOUT is the output and EX_MEM_IR is the ADD OPCode/Instruction Code</strong>
</details>

## Day 5
<details>
<summary>Gate Level Simulation</summary>
<br>
GLS is generating the simulation output by running test bench with netlist file generated from synthesis as design under test. Netlist is logically same as RTL code, therefore, same test bench can be used for it.We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met. Folllowing are the commands to run the GLS simulation: <br>
<br>
	
![Screenshot from 2024-03-11 20-26-39](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/d25ab142-02a2-425e-b834-b10f2248ad4b)

The output waveform of the synthesized netlist given below:
<br>

![Screenshot from 2024-03-14 18-42-17](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/1e8e98a3-e84f-410c-90c7-eaee13e78b23)

<strong> As we can see GLS is matching RTL Waveforms. </strong>
</details>
