# UMRT CAN to PPM Gateway
This is an adapter board used by the University of Manitoba Robotics Team for controlling standard hobby servos over a CAN bus.

The PCB is designed in KiCad.
The module uses a PIC18F25K83 microcontroller, which can be programmed through MPLAB X IDE using an MPLAB Snap debugger.

## Hardware Description


## Control Commands

The module follows a J1939-style message structure.
Bits labeled "X" are allowed to be anything; "A" and "B" refer to the address bits chosen with jumpers.
For commanding a servo position, the frame identifier (29-bit CAN ID) follows the format:
<table><thead>
  <tr>
    <th colspan="3" rowspan="2">Priority [3]</th>
    <th colspan="18">J1939 Parameter Group Number (PGN) [18]</th>
    <th colspan="8" rowspan="2">Source Address [8]</th>
  </tr>
  <tr>
    <th>R</th>
    <th>DP</th>
    <th colspan="8">PF</th>
    <th colspan="8">PS (Destination Address) [8]</th>
  </tr></thead>
<tbody>
  <tr>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>A</td>
    <td>B</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

The message payload for controlling a servo consists of 8 bytes:

<table><thead>
  <tr>
    <th>&nbsp;&nbsp;&nbsp;<br>Byte Index&nbsp;&nbsp;&nbsp;</th>
    <th>&nbsp;&nbsp;&nbsp;<br>Signal Label&nbsp;&nbsp;&nbsp;</th>
    <th>&nbsp;&nbsp;&nbsp;<br>Scaling&nbsp;&nbsp;&nbsp;</th>
    <th>&nbsp;&nbsp;&nbsp;<br>Limit&nbsp;&nbsp;&nbsp;</th>
    <th>&nbsp;&nbsp;&nbsp;<br>Offset&nbsp;&nbsp;&nbsp;</th>
    <th>&nbsp;&nbsp;&nbsp;<br>Transfer&nbsp;&nbsp;&nbsp;</th>
    <th>&nbsp;&nbsp;&nbsp;<br>J1939 SLOT ID&nbsp;&nbsp;&nbsp;</th>
  </tr></thead>
<tbody>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>0&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>Servo Index&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>1 count per bit&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>0 to 250&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>0&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>Numeric&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>129&nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>1&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="2">&nbsp;&nbsp;&nbsp;<br>Servo Percent&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="2">&nbsp;&nbsp;&nbsp;<br>0.0015625 % per bit&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="2">&nbsp;&nbsp;&nbsp;<br>0 to 100.3984375 %&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="2">&nbsp;&nbsp;&nbsp;<br>0 %&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="2">&nbsp;&nbsp;&nbsp;<br>Numeric&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="2">&nbsp;&nbsp;&nbsp;<br>345&nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>2&nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>3&nbsp;&nbsp;&nbsp;</td>
    <td rowspan="3">&nbsp;&nbsp;&nbsp;<br>Don’t Care&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>4&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>5&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br> &nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>6&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>Message Counter&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>1 count per bit&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>0 to 250&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>0&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>Numeric&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>129&nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>7&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>CRC&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>N/A&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>0 to 255&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>0&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>Statevalue&nbsp;&nbsp;&nbsp;</td>
    <td>&nbsp;&nbsp;&nbsp;<br>93&nbsp;&nbsp;&nbsp;</td>
  </tr>
</tbody></table>

A more detailed description of each of these signals is:
<table><thead>
  <tr>
    <th>Signal</th>
    <th>Description</th>
  </tr></thead>
<tbody>
  <tr>
    <td>   <br>Servo Index   </td>
    <td>- Differentiates which servo to control<br>- We don’t want to set all servos in one message, because then someone wanting to send a new message to adjust a servo needs to know what the correct position for every servo is<br>- For J1939, 0xFF indicates no data available and 0xFE indicates error, so we don’t allow either of those- We don’t actually need 8 bits for this, but having fields stick to nice byte boundaries makes hand-decoding for verification easier, and we’ve got space in the packet<br></td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>Servo Percent&nbsp;&nbsp;&nbsp;</td>
    <td>- Pretty straightforward, describes the percentage of the servo range it should be commanded to<br>- At a hardware level, will correspond to the percentage of time in the PPM window before a pulse is generated</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>Don’t Care&nbsp;&nbsp;&nbsp;</td>
    <td>- Things are simpler if we always send 8 byte messages<br>- Just here to fill out the packet<br>- Gives room for expansion later without breaking the interface</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>Message Counter&nbsp;&nbsp;&nbsp;</td>
    <td>- Allows us to detect if messages are being lost (for functional safety)</td>
  </tr>
  <tr>
    <td>&nbsp;&nbsp;&nbsp;<br>CRC&nbsp;&nbsp;&nbsp;</td>
    <td>- CRC8 J1850 checksum of the message, less this field</td>
  </tr>
</tbody></table>

### Implementation Specific Limits 
- Commands above 100% are treated as commands to 100%
- Only 2 servo outputs are supported, indices 0 and 1
