Traffic Light Controller (Verilog + Testbench)

This project implements a basic Traffic Light Controller in Verilog using a three-state Finite State Machine (FSM). The traffic signal transitions through Green → Yellow → Red using a clock-driven counter, and each light stays ON for a fixed number of cycles.

## Features

* Three states: Green, Yellow, Red
* Green active for 3 cycles
* Yellow active for 2 cycles
* Red active for 1 cycle
* Automatically repeats the sequence
* Includes a complete testbench with waveform dumping (VCD)

## How It Works

The design uses a synchronous FSM with an internal counter:

* The system starts in the Green state after reset.
* A cycle counter increments on every clock edge.
* State transitions happen when the counter reaches:

  * 3 → switch from Green to Yellow
  * 5 → switch from Yellow to Red
  * 6 → switch from Red to Green (and counter resets)

Only one output (red, yellow, green) is high at a time.

## File Structure

```
traffic_light.v   – RTL design  
tb_traffic_light.v – Testbench  
dump.vcd          – Waveform output after simulation  
```

## How To Run

1. Install any Verilog simulator (Icarus Verilog preferred):

   ```
   sudo apt install iverilog
   ```
2. Compile:

   ```
   iverilog -o traffic_light tb_traffic_light.v traffic_light.v
   ```
3. Run:

   ```
   vvp traffic_light
   ```
4. View waveform using GTKWave:

   ```
   gtkwave dump.vcd
   ```

## What You Learn From This Project

* Designing a simple FSM in Verilog
* Writing combinational and sequential logic
* Creating a testbench
* Generating clock and reset signals
* Viewing waveforms using VCD files


