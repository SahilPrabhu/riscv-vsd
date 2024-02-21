# Riscv-VSD

## This repositiry is intended to document the learning outcomes and experience of a 4-week workshop on RISC-V using Open source tools like yosys and Skywater 130nm PDK.

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
```add r6,r2,r1``` <br>
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

![rv-32bit](https://github.com/SahilPrabhu/riscv-vsd/assets/92974277/2f492828-7592-4467-9083-f02a935318d5)
