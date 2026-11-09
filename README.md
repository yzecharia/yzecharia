# Hi, I'm Yuval Zecharia

<p>
  <a href="https://linkedin.com/in/yuval-zecharia"><img src="https://img.shields.io/badge/LinkedIn-yuval--zecharia-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="mailto:zechariayuval@gmail.com"><img src="https://img.shields.io/badge/Email-zechariayuval%40gmail.com-555?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
  <img src="https://img.shields.io/badge/Hod_HaSharon,_Israel-777?style=flat-square" alt="Hod HaSharon, Israel">
</p>

Electrical Engineering graduate (B.Sc., Ariel University, computers and communications track), currently in the **Google & Reichman Tech School Chip Design & Verification program** (Verilog and verification track). I'm looking for an entry-level **RTL design or FPGA** role in Israel, and open to **design verification**.

## Experience

- **Habana Labs (Intel)** – System Validation Engineer, intern, 3.5 years. Wrote validation tests for the **Gaudi3** AI accelerator and worked with the hardware and software teams on debug and integration.

## Featured project

<!-- FEATURED BLOCK, from here to "## Also". After each lab push, follow section 9 of GITHUB_PUSH_RULES.md: lab counts, the two lab bullets, the "What went wrong" bullets and the photo. Nothing else on the page depends on this block. -->

[**chip-design-verification-labs**](https://github.com/yzecharia/chip-design-verification-labs) – the Reichman program labs so far (six), in Verilog and SystemVerilog, each taken through lint, synthesis, place and route and bitstream in Vivado; five of them run and photographed on a **Nexys A7-100T**. The latest two are complete small systems:

- [**Lab 5**](https://github.com/yzecharia/chip-design-verification-labs/tree/main/lab5_trx_controller) – UART transceiver at 57600 bps with a packet parser: a `{R<ddd>,C<ddd>,V<ddd>}` message from the PC is checked byte by byte and shown on the display. RX PHY with 16× oversampling, FSMs with state diagrams and transition tables.
- [**Lab 6**](https://github.com/yzecharia/chip-design-verification-labs/tree/main/lab6_pwm_rgb_led_controller) – an sRGB pixel from the PC drives an RGB LED through a gamma table in Block RAM, CIE scaling and three PWM channels, and the PWM values go back over UART. 17 modules on one 100 MHz clock, synchronous reset, synchronizers on the asynchronous inputs, `create_clock` and `set_false_path` constraints. Timing met with 2.84 ns of slack; 424 LUTs, 535 flip-flops, one BRAM tile, and a bitstream with zero warnings.

**What went wrong, and what I did about it**

- **Verification:** a directed, self-checking testbench per module, 91 immediate assertions and 10 SVA properties in xsim ([summary](https://github.com/yzecharia/chip-design-verification-labs/blob/main/lab6_pwm_rgb_led_controller/results/1_simulation/simulation_summary.txt)), then the board. Five bugs were found in simulation. One got through: my first CIE scaling multiplied by the weights instead of dividing, the testbench compared the RTL against my own model, so white looked green on the board and only the photo caught it.
- **Timing:** a combinational binary-to-BCD with `/` and `%` failed at 100 MHz (WNS −0.81 ns). It became a sequential double-dabble that finishes long before its digits go out.
- **DRC:** an asynchronous reset left over from Lab 5 put the Block RAM enable under asynchronous control (REQP-1840). Changed to a synchronous reset like the rest of the design.
- Flip-flops are counted from the RTL per module and reconciled against the synthesis report.
- 13 of the 17 testbenches are mine. Four were generated with AI under the course deadline, and the lab README says which.

<p align="center">
  <a href="https://github.com/yzecharia/chip-design-verification-labs/tree/main/lab6_pwm_rgb_led_controller/board_test">
    <img src="https://raw.githubusercontent.com/yzecharia/chip-design-verification-labs/main/lab6_pwm_rgb_led_controller/board_test/board_2_white.jpg" alt="Nexys A7 running Lab 6: the display shows the pixel and LED, LED16 is lit white, and the terminal shows the PWM values the FPGA sent back" width="640">
  </a>
  <br>
  <sub>Lab 6 on the board: the PC sent white, the display shows the pixel and the LED number, and the terminal shows the three PWM values the FPGA sent back.</sub>
</p>

## Also

- [**hdl-bits-solutions**](https://github.com/yzecharia/hdl-bits-solutions) – most of HDLBits from the flip-flops chapter onward, one module per problem with a schematic next to it.

## Tools & skills

- **HDL:** Verilog, SystemVerilog (packages, structs, enums, `generate`, parameterised modules)
- **Verification:** directed self-checking testbenches, immediate assertions, SVA properties, waveform review in xsim
- **FPGA flow:** Vivado (xsim, lint, synthesis, implementation, XDC constraints, timing and utilization reports)
- **Boards:** Digilent Nexys A7-100T, Basys3
- **Also:** UART bring-up with tio and CoolTerm, block and state diagrams, Git
