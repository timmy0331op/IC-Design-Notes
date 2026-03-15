# Coding Style

* 組合邏輯用 = (blocking)，循序邏輯用 <= (blocking)
* sensitivity list 用 always(*)
* 在設計電路時要盡量避免 Latch 的產生
* 組合邏輯中 if/case 條件要寫滿，否則 Design Complier 在合成的時候在非條件狀態下加上 Latch 以確保其值不會改變
* 如果有 Feedback 就需要加上 Flip-Flop (FF)
* Latch 只會在 Combinational 中出現
* 不要使用 conditional reset
* 不要直接拿 Input data 做運算，先用 FF 存起來，若輸入序列一筆一筆進入，用 Shift Register (FIFO or SIPO)
* Output 也先用 FF 儲存後再送出
* 使用 FSM 控制電路
* 無號數運算成有號數:  
```verilog
wire [2:0] a,b;  
wire signed [3:0] result;  
assign result = $signed({1'b0, a}) - $signed({1'b0, b});  
```
* 運算化簡  
1. 乘以常數可以用 2 的冪次組合:  
```verilog
assign b = a * 5;  
assign b = (a << 2) + a;  
```
2. 除以 2 的冪次要注意精度，可以將整個式子乘以 2 的冪次 (將最低冪次令為常數):  
```verilog
assign b = (a >>> 1) + a;  
assign bx2 = a + (a << 1); 
``` 
3. 取 2 的冪次餘數:  
```verilog
assign b = a % 16;  
assign b = a[3:0];
```  
4. 判斷奇偶:  
```verilog
assign b = a[0]; // b 為 1 的話 a 是奇數 為 0 則 a 是偶數
```
* 左位移用 << 邏輯左移，右位移用 >>> 算術位移    

| 算術左移 | 算術右移 | 邏輯左移 | 邏輯右移 |
| :---: | :---: | :---: | :---: |
| <div style="background-color:white; padding:10px; display:inline-block;"><img src="src/p1.png" width="200" style="mix-blend-mode: multiply;"></div> | <div style="background-color:white; padding:10px; display:inline-block;"><img src="src/p2.png" width="160" style="mix-blend-mode: multiply;"></div> | <div style="background-color:white; padding:10px; display:inline-block;"><img src="src/p3.png" width="200" style="mix-blend-mode: multiply;"></div> | <div style="background-color:white; padding:10px; display:inline-block;"><img src="src/p4.png" width="200" style="mix-blend-mode: multiply;"></div> |

