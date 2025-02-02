
|       | Byte   | Byte   |                     |
| ----- | ------ | ------ | ------------------- |
| AX    | **AL** | **AH** | Accumulator         |
| BX    | **BL** | **BH** | Base                |
| CX    | **CL** | **CH** | Count               |
| DX    | **DL** | **DH** | Data                |
| SP    |        |        | Stack Pointer       |
| BP    |        |        | Base Pointer        |
| IP    |        |        | Instruction Pointer |
| FLAGS |        |        | Status Flags        |


| 16-Bit (W = 1) |       |     | 8-Bit (W = 0) |     |
| -------------- | ----- | --- | ------------- | --- |
| 000            | AX    |     | 0             | AL  |
| 001            | BX    |     | 1             | BL  |
| 010            | CX    |     | 10            | CL  |
| 011            | DX    |     | 11            | DL  |
| 100            | SP    |     | 100           | AH  |
| 101            | BP    |     | 101           | BH  |
| 110            | IP    |     | 110           | CH  |
| 111            | FLAGS |     | 111           | DH  |

