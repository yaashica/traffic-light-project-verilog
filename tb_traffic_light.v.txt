// Code your design here
`timescale 1ns/1ps

module tb_traffic_light;

    reg clk;
    reg reset;
    wire red, yellow, green;

    // DUT
    traffic_light dut (
        .clk(clk),
        .reset(reset),
        .red(red),
        .yellow(yellow),
        .green(green)
    );

    // Clock generation (10ns period)
    always #5 clk = ~clk;

    initial begin
        $dumpfile("dump.vcd"); 
        $dumpvars(0, tb_traffic_light.dut);
        clk = 0;
        reset = 1;
        #10 reset = 0;   // release reset

        #200;            // run simulation
        $finish;
    end

endmodule
