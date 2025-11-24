// Code your testbench here
// or browse Examples
`timescale 1ns/1ps

module traffic_light (
    input  wire clk,         // clock
    input  wire reset,       // async reset
    output reg  red,
    output reg  yellow,
    output reg  green
);

    // states
    typedef enum reg [1:0] {
        S_GREEN  = 2'b00,
        S_YELLOW = 2'b01,
        S_RED    = 2'b10
    } state_t;

    state_t state, next_state;

    // Counter for timing
    integer count;

    // State transition
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            state <= S_GREEN;
            count <= 0;
        end
        else begin
            state <= next_state;
            
            // Counter increments every cycle
            count <= count + 1;
        end
    end

    // Next state logic
    always @(*) begin
        next_state = state;
        case (state)
            // Green for 3 cycles
            S_GREEN: begin
                if (count >= 3) next_state = S_YELLOW;
            end
            
            // Yellow for 2 cycles
            S_YELLOW: begin
                if (count >= 5) next_state = S_RED;
            end
            
            // Red for 1 cycle
            S_RED: begin
                if (count >= 6) next_state = S_GREEN;
            end
        endcase
    end

    // Output logic
    always @(*) begin
        red    = 0;
        yellow = 0;
        green  = 0;

        case (state)
            S_GREEN:  green  = 1;
            S_YELLOW: yellow = 1;
            S_RED:    red    = 1;
        endcase
    end

endmodule
