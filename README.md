# EXP1: 4 Bit Adder functionality verification

## Aim:
To write a verilog code for 4bit adder and verify the functionality using Test bench.

 Write Verilog Code

 Verify the Functionality using Test-bench.

## Tool Required: 
Functional Simulation: nclaunch Simulator (nclaunch) 

## 4-bit Adder Design:
To construct a 4-bit adder, need to chain together four 1-bit full adders. Each full adder computes the sum and carry for one bit of the two numbers. The carry-out from one adder feeds into the carry-in of the next adder in the sequence. This process adds the two 4-bit numbers bit by bit, with the carry propagating through each stage, resulting in a final sum and carry-out at the end.

To design a 1-bit full adder, the first step is to create a truth table that represents all possible combinations of the inputs (A, B, and CIN) and the corresponding outputs (Sum(S) and COUT).

![image](https://github.com/user-attachments/assets/716a26b6-a449-42e0-9e2d-cdbaa4b291b9)

Here’s the truth table for a 1-bit full adder:

![tt](https://github.com/user-attachments/assets/0b3ab24f-1d7e-4a01-80ce-5e7406f4082b)

### Fig 1 : Diagram and truth table of full adder

### Logic Expressions:

1.	Sum (S):
   
S=A⊕B⊕CIN

Where ⊕ represents XOR.

3.	Carry out (COUT):
   
COUT=(A&B) | (CIN&(A^B))

![image](https://github.com/user-attachments/assets/7d6fa554-2614-4f19-aa68-65c9e6153caa)

### Fig 2:Diagram of 4 Bit Adder
ADDER
```
module full_adder(A,B,CIN,S,COUT);
input A,B,CIN;
output S,COUT;
 assign S=A^B^CIN;
assign COUT=(A&B) | (CIN&(A^B));
endmodule
```
4-BIT ADDER
```
module fulladd_4bit(A,B,C0,S,C4);
input [3:0] A,B;
input C0;
output [3:0] S;
output C4;
wire C1,C2,C3;
full_adder fa0 (A[0],B[0],C0,S[0],C1);
full_adder fa1 (A[1],B[1],C1,S[1],C2);
full_adder fa2 (A[2],B[2],C2,S[2],C3);
full_adder fa3 (A[3],B[3],C3,S[3],C4);
endmodule
```
TEST
```
module test_4bit; 
reg [3:0] A;
reg [3:0] B; reg C0; wire [3:0] S; wire C4;
fulladd_4bit dut (A,B,C0,S,C4); initial
begin A=4'b0011;B=4'b0011;C0=1'b0;
#10; A=4'b1011;B=4'b0111;C0=1'b1;
#10; A=4'b1111;B=4'b1111;C0=1'b1;
#10;
end initial
#50
$finish;
endmodule
```

	In the Terminal, type gedit <filename>.v (ex: gedit 4bitadder.v). 

	A Blank Document opens up into which the following source code can be typed down. 

Note : File name should be with HDL Extension

### a) Verify the Functionality 

	Three Codes shall be written for implementation of 4-bit Adder as follows, 

•	fa.v → Single Bit 3-Input Full Adder [Sub-Module / Function] 

•	fa_4bit.v → Top Module for Adding 4-bit Inputs. 

•	fa_4bit_test.v → Test bench 

*/Program to design 4 bit adder by instantiating 1 bit Full adder.also add test bench program */
Developed by: Register Number*/

## Functional Simulation: 

	Invoke the cadence environment by type the below commands 

	tcsh (Invokes C-Shell) 

	source /cadence/install/cshrc (mention the path of the tools) 

      (The path of cshrc could vary depending on the installation destination)
      
	After this you can see the window like below 

### Fig 3:Invoke the Cadence Environment


	To Launch Simulation tool 
![Screenshot 2025-04-23 155534](https://github.com/user-attachments/assets/779a6877-24f6-4bb7-bd9f-639bfe2c3739)

•	linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design 

or

•	linux:/> nclaunch& // On subsequent calls to NCVERILOG 

	It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple Step .


### Fig 4:Setting Multi-step simulation
![Screenshot 2025-04-23 155603](https://github.com/user-attachments/assets/407f2ce8-4a82-4ca9-a3a5-4fd71c6d63fc)


	Select Multiple Step and then select “Create cds.lib File” .

	Click the cds.lib file and save the file by clicking on Save option 

### Fig 5:cds.lib file Creation

![Screenshot 2025-04-23 155609](https://github.com/user-attachments/assets/51e801ee-a4e6-4aa9-8dc8-c5ef4453b651)

	Save cds.lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used. 

	Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure .

•	We are simulating verilog design without using any libraries 

•	A Click “OK” in the “nclaunch: Open Design Directory” window as shown in below figure 

![image](https://github.com/user-attachments/assets/781b297a-11e9-4140-89c5-ee3b0d15bbd4)

### Fig 6: Selection of Don’t include any libraries
![Screenshot 2025-04-23 155932](https://github.com/user-attachments/assets/6bbc4824-f52f-4e82-9193-8efb54af1bf4)


	A ‘NCLaunch window’ appears as shown in figure below 

	Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. 

	Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .

	To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. 

### Fig 7: Nclaunch Window
![Screenshot 2025-04-23 155959](https://github.com/user-attachments/assets/8fa22827-3edb-4031-a12c-6245876761d9)


## Step 1: Compilation:– Process to check the correct Verilog language syntax and usage 

	Inputs: Supplied are Verilog design and test bench codes 

	Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file 

	Steps for compilation: 

1. Create work/library directory (most of the latest simulation tools creates automatically) 
2. Map the work to library created (most of the latest simulation tools creates automatically) 
3. Run the compile command with compile options 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v

Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

### Fig 8: Compiled database in worklib
![Screenshot 2025-04-23 161432](https://github.com/user-attachments/assets/cd7034a6-dd52-414d-aae3-d8ae5a371fb8)


	After compilation it will come under worklib you can see in right side window

	Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. 

	The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

## Step 2: Elaboration:– To check the port connections in hierarchical design 
	Inputs: Top level design / test bench Verilog codes 

	Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file 

	Steps for elaboration – Run the elaboration command with elaborate options 

1.	It builds the module hierarchy 
2.	Binds modules to module instances 
3.	Computes parameter values 
4.	Checks for hierarchical names conflicts 
5.	It also establishes net connectivity and prepares all of this for simulation
   
	After elaboration the file will come under snapshot. Select the test bench and elaborate it.

### Fig 9: Elaboration Launch Option
![Screenshot 2025-04-23 161517](https://github.com/user-attachments/assets/b0fa1098-f4ad-40bc-a599-52c65b8087e3)


## Step 3: Simulation: – Simulate with the given test vectors over a period of time to observe the output behaviour. 

	Inputs: Compiled and Elaborated top level module name 

	Outputs: Simulation log file, waveforms for debugging 

	Simulation allow to dump design and test bench signals into a waveform 

	Steps for simulation – Run the simulation command with simulator options

### Fig 10: Design Browser window for simulation
![Screenshot 2025-04-23 161605](https://github.com/user-attachments/assets/ac2fa0fc-73b9-4b35-8b38-006c39578c17)

### Fig 11: Launching Simulation Waveform WindowSimulation Waveform Window
![Screenshot 2025-04-23 161637](https://github.com/user-attachments/assets/4d31e04f-b1ca-485d-86f1-f7ca819a9957)

### Fig 12: Simulation Waveform Window
![Screenshot 2025-04-23 161710](https://github.com/user-attachments/assets/88279adf-8a33-40ff-8d1d-b1864cbe7d0e)

### Result:

The functionality of a 4-bit adder was successfully verified using a test bench and simulated with the nclaunch tool.















