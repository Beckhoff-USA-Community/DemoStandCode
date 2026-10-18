# Demo Rack Switches

Function of switches S10–S17 and S20–S27, taken from the PLC1 code in `Tc3_Sample_Demo_Rack`. Each switch is read into the PLC as an input called `bSwitchSxx`.

## Row 1: S10–S17 (CX inputs, `GVL00_IO_CX`)

| Switch | Function | What it does in the code |
|---|---|---|
| **S10** | Blinker 1 on/off | Turns on `fbBlinker1`, which flashes LED **H10**. Potentiometer **R10** sets the blink rate. (`Blinker`) |
| **S11** | Blinker 2 on/off | Turns on `fbBlinker2`, which flashes LED **H11** at a fixed 0.5 s. (`Blinker`) |
| **S12** | Enable Axis 1 (EL7037 stepper) | Turns on power to Axis 1. LED **H12** shows that Axis 1 has power. Potentiometer R10 also sets the speed override. (`Axis1`) |
| **S13** | Enable Axis 2 (EL7201) | Turns on power to Axis 2. (`Axis2`) |
| **S14** | Enable Axis 3 (AX5203, channel 1) | Turns on power to Axis 3. (`Axis3`) |
| **S15** | Enable Axis 4 (AX5203, channel 2) | Turns on power to Axis 4. (`Axis4`) |
| **S16** | Start absolute move, axes 1–4 | Starts an absolute move on each axis that isn't coupled to the handwheel. LED **H16** blinks while a move is running and stays on once all four are done. |
| **S17** | Uncouple axes 1–4 / zero target | Uncouples each axis from the handwheel (Axis 5) and sets the target position back to 0. LED **H17** stays on while S17 is on and blinks while any axis is coupled. |

## Row 2: S20–S27

| Switch | Function | What it does in the code |
|---|---|---|
| **S20** | Start reversing sequence, axes 1–4 | Starts the back-and-forth sequence on each axis that has power. On Axis 1 that means 720° at 500, then back to 0 at 3000, with a 500 ms pause. LED **H20** blinks while it runs. |
| **S21** | Reset axes 1–4 | Clears axis errors. LED **H21** blinks when any axis has an error. |
| **S22** | Not in use | It's declared as "not in use" and nothing reads it. |
| **S23** | Home Axis 1 (stepper) | Homes Axis 1 against its reference cam, only when Axis 1 has power. LED **H23** blinks slowly when the axis isn't homed, blinks fast while homing, and stays on when homing is done. (`Axis1`) |
| **S24** | Touch probe, Axis 1 | Captures one position on a rising edge of touch probe 1. LED **H24** blinks while waiting and stays on once a position is captured. (`Axis1`) |
| **S25** | LED H25 on/off | Turns LED **H25** on and off directly (`GeneralPlc`). The variable's comment says "Modulo touch probe on", but no touch-probe logic is hooked to it. |
| **S26** | Not used | Wired to AX5203 digital input bit 2. The PLC reads it but doesn't do anything with it. (`AxisGeneral`) |
| **S27** | Not used | Wired to AX5203 digital input bit 3, with the same no-effect read. (`AxisGeneral`) |

## Notes

- S20, S21, S22 and S25 are declared in `GVL01_IO_EK1100` (EtherCAT/EK1100 terminals). S23 and S24 are declared in `GVL00_IO_CX`. S26 and S27 are digital inputs on the AX5203 drive.
- S16 and S20 only move axes that have been enabled with S12–S15.
- The handwheel coupling is done by a separate switch, **S28**. S17 is the switch that undoes it.
