## Program: add1.asm

### 1. Operation Details
- **Operands:** `num1 = 120` (`0x78` or `01111000b`), `num2 = 10` (`0x0A` or `00001010b`)
- **Instruction:** `add al, [num2]`
- **Result:** `al = 130` (`0x82` or `10000010b`)

### 2. Flag Status and Explanations

| Flag | Status | Value | Reason / Arithmetic Explanation |
| :--- | :---: | :---: | :--- |
| **CF** (Carry) | Cleared | 0 | The unsigned addition $120 + 10 = 130$ does not exceed 255. No carry occurred out of the 8th bit (bit 7). |
| **OF** (Overflow) | **Set** | 1 | Signed overflow occurred. Two positive numbers ($+120$ and $+10$) were added, but resulted in a negative two's complement value ($-126$, because bit 7 became 1). $130$ exceeds the maximum 8-bit signed limit ($+127$). |
| **SF** (Sign) | **Set** | 1 | The most significant bit (MSB, bit 7) of the 8-bit result `10000010b` is `1`, indicating a negative signed value. |
| **ZF** (Zero) | Cleared | 0 | The result is `0x82` (130), which is non-zero. |
| **PF** (Parity) | **Set** | 1 | The lowest byte `10000010b` contains exactly two `1` bits. Because 2 is an even number, the parity is even (PF = 1 in x86). |
| **AF** (Auxiliary) | **Set** | 1 | A carry occurred from bit 3 into bit 4 during the lower-nibble addition (`0x8 + 0xA = 0x12`). |

## Program 2: add2.asm

### 1. Operation Details
- **Source File:** `add2.asm`
- **Instruction Executed:** `add ax, [num2]`
- **Destination Register:** `AX`
- **Observed EFLAGS:** `0x202 [ IF ]`

### 2. Flag Status and Explanations

| Flag | Status | Value | Reason / Arithmetic Explanation |
| :--- | :---: | :---: | :--- |
| **CF (Carry)** | Cleared | 0 | The unsigned sum does not exceed the 16-bit maximum limit ($65,535$). There is no carry-out from bit 15. |
| **OF (Overflow)** | Cleared | 0 | Adding two positive signed numbers produced a positive signed number that fits comfortably within the 16-bit signed limit ($-32,768$ to $+32,767$). No signed overflow occurred. |
| **SF (Sign)** | Cleared | 0 | The most significant bit (MSB, bit 15) of the result is `0`, indicating a positive result. |
| **ZF (Zero)** | Cleared | 0 | The result of the addition is non-zero. |
| **PF (Parity)** | Cleared | 0 | The lowest byte of the result contains an odd count of set bits (`1`s), which clears the parity flag. |
| **AF (Auxiliary)** | Cleared | 0 | No carry occurred out of bit 3 into bit 4 in the low nibble during addition. |
| **IF (Interrupt)** | Set | 1 | Hardware interrupt flag enabled by the operating system (system control flag, not an arithmetic status flag). |