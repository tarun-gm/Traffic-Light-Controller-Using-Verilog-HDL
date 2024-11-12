# Traffic-Light-Controller-Using-Verilog-HDL
Aim
To design and simulate a traffic light controller using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 simulation environment. The objective is to control the traffic lights for a junction with a specific time-based sequence for Red, Yellow, and Green lights.

Apparatus Required
Vivado 2023.1 or equivalent Verilog simulation tool.
Computer system with a suitable operating system.
FPGA board (optional for hardware verification).
Procedure
Launch Vivado 2023.1:

Open Vivado and create a new project.
Design the Traffic Light Controller Verilog Code:

Write the Verilog code for the traffic light controller, using an FSM (Finite State Machine) to transition between Green, Yellow, and Red lights based on timing intervals.
Create the Testbench:

Write a testbench to simulate the traffic light controller. The testbench will check the sequence of light transitions based on time.
Add the Verilog Files:

Add the traffic light controller Verilog code and the testbench file to the project.
Run Simulation:

Run the behavioral simulation in Vivado to verify the correct sequence of the traffic lights.
Observe the Waveforms:

Examine the waveform output to verify that the traffic light transitions through the Green, Yellow, and Red lights in the correct sequence.
Save and Document Results:

Capture screenshots of the waveform and save the simulation logs to include in your report.

Verilog Code for Traffic Light Controller
CODE:
module Traffic_light_controller_TB;
reg clk,rst;
wire[2:0]light_M1;
wire[2:0]light_S;
wire[2:0]light_MT;
wire[2:0]light_M2;

initial
begin
     clk=1'b0;
     forever # (1000000000/2) clk=~clk;
end
initial
begin
     rst=0;
     #1000000000;
     rst=1;
     #1000000000;
     rst=0;
     #(1000000000*200);
     $finish;
     end
     endmodule
OUTPUT:![TRAFFIC-OUTPUT](https://github.com/user-attachments/assets/289ce4a6-bc70-403b-80e0-5313c1210a01)


Testbench for Traffic Light Controller
CODE:
module Traffic_light_controller_TB;
  reg clk, rst;
  wire [2:0] light_M1;  // Outputs for traffic light in direction M1
  wire [2:0] light_S;   // Outputs for traffic light in direction S
  wire [2:0] light_MT;  // Outputs for traffic light in direction MT
  wire [2:0] light_M2;  // Outputs for traffic light in direction M2

  // Instantiate the DUT (Device Under Test), i.e., Traffic_light_controller module
  Traffic_light_controller DUT (
    .clk(clk),
    .rst(rst),
    .light_M1(light_M1),
    .light_S(light_S),
    .light_MT(light_MT),
    .light_M2(light_M2)
  );

  // Clock generation: Clock toggles every 0.5 seconds (1 GHz clock frequency)
  initial begin
    clk = 1'b0;
    forever #(1000000000 / 2) clk = ~clk;  // Toggle clock every 0.5 seconds
  end

  // Reset sequence
  initial begin
    rst = 0;             // Start with reset low
    #1000000000;         // Wait for 1 second
    rst = 1;             // Assert reset
    #1000000000;         // Wait for 1 second
    rst = 0;             // De-assert reset
    #(1000000000 * 200); // Run the simulation for 200 more clock cycles
    $finish;             // End simulation
  end
endmodule
OUTPUT:
![TESTBENCH-OUTPUT-TRAFFIC](https://github.com/user-attachments/assets/b16c7f07-99f1-4e3a-a9d9-2c6627907414)

Conclusion
In this experiment, a traffic light controller was successfully designed and simulated using Verilog HDL. The design controlled the traffic lights to switch between Green, Yellow, and Red in a cyclic manner based on timing intervals. The testbench verified that the traffic lights followed the correct sequence and timing. The simulation results confirm the correct functionality of the traffic light controller, demonstrating the effectiveness of Verilog HDL in designing FSM-based controllers for real-world applications.
