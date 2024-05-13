# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

# APPARATUS REQUIRED:

Xilinx 14.7 
Spartan6 FPGA

**LOGIC DIAGRAM**

# SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


# JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)


# T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)



# D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


# COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)



# PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

# D-FLIP FLOP
VERILOG CODE
~~~
module Dflipflop(D,clk,reset,Q);
input D;
input clk;
input reset;
output reg Q;
always @(posedge clk)
begin
 if(reset==1'b1)
  Q <= 1'b0;
 else
  Q <= D;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329866143-f57d74d6-3e76-41dc-84be-860904351e48" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/03e5b43e-8fd1-42db-bec9-d8e1cd6342b0">
<img width="962" alt="329866258-a234cf46-c2ab-49a3-9d76-c4ba2f106838" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/3b92b980-ac92-4606-a838-c6d9648e3a01">



# JK FLIP FLOP

VERILOG CODE:
~~~
module JK_flipflop (q, q_bar, j,k, clk,reset);
input j,k,clk, reset;
output reg q;
output q_bar;
always@(posedge clk)
begin
  if(!reset)        
    q <= 0;
  else 
  begin
      case({j,k})
        2'b00: q <= q;    // No change
        2'b01: q <= 1'b0; // reset
        2'b10: q <= 1'b1; // set
        2'b11: q <= ~q; // Toggle
      endcase
  end
end
assign q_bar = ~q;
endmodule
~~~

# OUTPUT:
<img width="962" alt="329866454-1d531d02-4af8-4f5a-89f2-3fd7156cbcb7" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/4a094ca4-dfb9-47e5-8a78-b95b280128cf">
<img width="962" alt="329866915-c080f42f-e595-43c3-809f-002896ad0846" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/8e770e54-6496-4f60-85cb-b508304bc995">


# MOD-10 COUNTER

VERILOG CODE:
~~~
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329866929-c3de4345-cc63-4ad7-84be-a34824a50b9c" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/35aedae2-4db5-4e7d-8adf-6c4fd4293013">
<img width="962" alt="329866934-6b7cde7f-a59a-4af1-8687-4fb414d9bf3f" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/01a592b8-068c-4dca-be79-f060cf02930f">



# RIPPLE CARRY COUNTER

VERILOG CODE:
~~~
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule
module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule
module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf0(q[0],clk,rst);
tff tf1(q[1],q[0],rst);
tff tf2(q[2],q[1],rst);
tff tf3(q[3],q[2],rst);
endmodule
~~~

# OUTPUT:
<img width="962" alt="329866946-bacae57e-902c-4441-9885-d0712388dfa0" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/b3729306-b93d-4b9b-8f30-31e23103d84e">
<img width="962" alt="329866952-3d4038ce-6610-40e2-a084-efa65d08e43e" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/af913a78-3179-4fbb-b0e6-ee33c1efb1cf">


# SR FLIP FLOP

VERILOG CODE:
~~~
module sr_flipflop(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329866961-e27f7186-3a2a-41ae-a34d-ffeceba454a0" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/bdee999f-58b1-4a98-95a8-11411516bdc3">
<img width="962" alt="329866965-d9ac4afa-6a0b-4fdb-8480-b38117172d39" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/26a92567-0cf6-41da-ac9d-d5afc43d865d">



# T FLIP FLOP

VERILOG CODE:
~~~
module T_flipflop(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329866968-8ff417da-2a48-43d1-b365-47d4b9c6e6b2" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/64d9a351-3be8-4bb5-9b09-40ec166f94be">
<img width="962" alt="329866975-47885c7a-6132-4438-8f20-3113b429a26d" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/6540708a-a079-4138-a05d-a326b34277fa">


# UP-DOWN COUNTER

VERILOG CODE:
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

# OUTPUT:
<img width="617" alt="329866984-930238e6-ac1f-4f0d-a872-7df3ab5ecbe2" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/530d78ab-9c07-4497-b308-fea125c000c3">
<img width="962" alt="329866989-ac0de8ec-c9a9-4c95-bdd9-e5960ed4c0d7" src="https://github.com/rajeshkumarm1/VLSI-LAB-EXP-4/assets/160701441/9b5a2a72-aaf6-451b-ac4d-d2774f326aaf">



RESULT:
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.


