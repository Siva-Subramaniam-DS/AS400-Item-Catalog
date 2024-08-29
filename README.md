# `File Declarations and Main Logic` 💻

## Table of Contents 📍
- [File Declarations](#file-declarations)
- [Main Logic](#main-logic)
- [Subroutine SBPRC](#subroutine-sbprc)
- [Logical Inference](#logical-inference)
- [DDS (Data Description Specifications) for FPRCLF](#dds-data-description-specifications-for-fprclf)

## `File Declarations`
- **FVPCMST**: Declares a workstation file.
- **FFPRCLF**: Declares a database file with indexed (keyed) access.

## `Main Logic`
- **MOVE 'VPCMST' VSPROG 10**: Moves the string 'VPCMST' to the variable VSPROG with a length of 10.
- **EXSR SBPRC**: Calls the subroutine SBPRC.
- **SETON LR**: Sets the Last Record (LR) indicator on, signaling the end of the program.

## `Subroutine SBPRC`
- **BEGSR**: Begins the subroutine SBPRC.
- **\*IN03 DOWEQ '0'**: Enters a loop while the indicator \*IN03 is equal to 0.
- **EXFMT VPCREC**: Displays the format VPCREC on the screen and waits for input.
- **CLEAR MSG**: Clears the message variable MSG.
- **PRODID CHAIN FPRCLF 90**: Chains to the FPRCLF file using PRODID as the key. If the record is found, the corresponding data is read into the program variables. If not found, indicator \*IN90 is set.
- **\*IN90 IFEQ '1'**: Checks if the record was not found (\*IN90 is 1).
- **MOVEL 'NO REC' MSG 15**: Moves the string 'NO REC' to the message variable MSG.
- **WRITE VPCREC**: Writes the format VPCREC to the screen.
- **ENDIF**: Ends the if block.
- **ENDDO**: Ends the dow loop.
- **ENDSR**: Ends the subroutine SBPRC.

## `Logical Inference`
The program starts by setting up the screen format and moving control to the SBPRC subroutine. In the subroutine, it enters a loop where it:

- Displays the screen format VPCREC and waits for user input.
- Clears any previous messages.
- Attempts to read a record from the FPRCLF file using the PRODID key.
- If the record is not found, it sets an error message (`NO REC`) and writes this message to the screen.
- The loop continues until the user sets the \*IN03 indicator to 1, likely by some user action.
- Once the loop exits, the program sets the LR indicator and ends.

## `DDS (Data Description Specifications) for FPRCLF`
This is the layout of the FPRCLF file, defining the structure of the data it holds:

- **PRODID**: Product ID, 10 characters alphanumeric.
- **PRONAM**: Product Name, 15 characters alphanumeric.
- **PRICE**: Price, 7 digits with 2 decimal places.
- **CURREN**: Currency, 3 characters alphanumeric.
- **DISCOU**: Discount, 5 digits with 2 decimal places.
- **EFFDAT**: Effective Date, 8 characters alphanumeric.
- **EXPDAT**: Expiration Date, 8 characters alphanumeric.
- **TAXRAT**: Tax Rate, 4 digits with 2 decimal places.
- **PRICAT**: Price Category, 20 characters alphanumeric.
- **LAUPDT**: Last Update Date, 8 characters alphanumeric.

## `Visual Representation`
![no rec](https://github.com/user-attachments/assets/7de15ac1-fdc6-4d59-8890-706763457adc)

![with rec](https://github.com/user-attachments/assets/028b4343-9ece-44ed-9667-4eb393b4edfe)

![with err rec](https://github.com/user-attachments/assets/a1437e93-8d0e-48fa-a578-cc32cdd86cb8)
