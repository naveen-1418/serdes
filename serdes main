// NOTE:This is the code for only simulation purpose not on the on board implementation



`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date:    21:20:01 05/27/2025 
// Design Name: 
// Module Name:    serdes_1
// Project Name: 
// Target Devices: 
// Tool versions: 
// Description: 
//
// Dependencies: 
//
// Revision: 
// Revision 0.01 - File Created
// Additional Comments: 
//
//////////////////////////////////////////////////////////////////////////////////
module ser(
input clk,
input [7:0]data_in,
output reg [3:0]bit_index=0,
output reg serial_out=0
);
reg [9:0]en_code;
reg [7:0]data;
always@(*) begin
case(data_in)
    8'h01:en_code=10'b0111100000;
    8'h02:en_code=10'b0111000001;
    8'h03:en_code=10'b0110000011;
    default:en_code=10'b0000000000;
 endcase
end
always@(posedge clk) begin
serial_out<=en_code[bit_index];
if(bit_index==9)
    bit_index<=0;
else
    bit_index<=bit_index+1;
end
endmodule
module deser(
input clk,
input serial_in,
output reg [3:0]bit_index=0,
output reg [7:0]data_out=0,
output reg [9:0]parallel_data=0
);
reg en=0;
reg [9:0]p_data=0;
always@(posedge clk) begin
if(bit_index==10) begin
    bit_index<=1;
    p_data<=0;
end
else begin
    bit_index<=bit_index+1;
end
p_data<={serial_in,p_data[8:1]};
end

always @(posedge clk) begin
  if(bit_index == 10)
  parallel_data <= p_data;
  end

always@(*) begin
case(parallel_data)
    10'b0111100000:data_out=8'b00000001;
    10'b0111000001:data_out=8'b00000010;
    10'b0110000011:data_out=8'b00000011;
    default:data_out=8'b00000000;
endcase
end
endmodule
module serdes_1(
input clk,
input [7:0]tx_in,
output [7:0]rx_out,
output [3:0]bit_in_se,
output s_out,
output s_in,
output [3:0]bit_in_de,
output [9:0]par_data
    );
ser serilizer(.clk(clk),.data_in(tx_in),.bit_index(bit_in_se),.serial_out(s_out));
deser deserilizer(.clk(clk),.serial_in(s_in),.bit_index(bit_in_de),.data_out(rx_out),.parallel_data(par_data));
assign s_in=s_out;
endmodule
