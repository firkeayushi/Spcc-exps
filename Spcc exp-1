#include<stdio.h>      // For input-output functions
#include<conio.h>      // For clrscr() and getch()
#include<string.h>     // For string operations like strcmp()
#include<stdlib.h>     // For atoi()

void main()
{
FILE *f1, *f2, *f3;   // File pointers
int lc, sa, l, op1, o, len;   // lc = location counter, sa = starting address
char m1[20], la[20], op[20], otp[20]; // m1=mnemonic, la=label, op=operand

clrscr();  // Clear screen

// Open input file and symbol table file
f1 = fopen("input.txt", "r");
f3 = fopen("symtab.txt", "w");

// Read first line (START statement)
fscanf(f1, "%s %s %d", la, m1, &op1);

// Check if program starts with START directive
if(strcmp(m1, "START") == 0)
{
    sa = op1;       // Set starting address
    lc = sa;        // Initialize location counter
    printf("\t%s\t%s\t%d\n", la, m1, op1);
}
else
{
    lc = 0;         // Default LC if no START
}

// Read next instruction
fscanf(f1, "%s %s", la, m1);

// Loop till end of file
while(!feof(f1))
{
    fscanf(f1, "%s", op);   // Read operand

    // Print current instruction with LC
    printf("\n%d\t%s\t%s\t%s\n", lc, la, m1, op);

    // If label is present, store it in symbol table
    if(strcmp(la, "-") != 0)
    {
        fprintf(f3, "\n%d\t%s", lc, la);
    }

    // Open OPTAB (Machine Operation Table)
    f2 = fopen("optab.txt", "r");

    fscanf(f2, "%s %d", otp, &o);

    // Search mnemonic in OPTAB
    while(!feof(f2))
    {
        if(strcmp(m1, otp) == 0)
        {
            lc = lc + 3;   // Instruction length = 3 bytes
            break;
        }
        fscanf(f2, "%s %d", otp, &o);
    }

    fclose(f2); // Close OPTAB

    // Handle pseudo-operations
    if(strcmp(m1, "WORD") == 0)
    {
        lc = lc + 3;   // WORD takes 3 bytes
    }
    else if(strcmp(m1, "RESW") == 0)
    {
        op1 = atoi(op);          // Convert operand to integer (atoi – ASCII to Integer)
        lc = lc + (3 * op1);     // Reserve words
    }
    else if(strcmp(m1, "BYTE") == 0)
    {
        if(op[0] == 'X')         // Hex constant
            lc = lc + 1;
        else
        {
            len = strlen(op) - 2; // Character constant length
            lc = lc + len;
        }
    }
    else if(strcmp(m1, "RESB") == 0)
    {
        op1 = atoi(op);
        lc = lc + op1;           // Reserve bytes
    }

    // Read next instruction
    fscanf(f1, "%s %s", la, m1);
}

// Check END directive and print program length
if(strcmp(m1, "END") == 0)
{
    printf("\nProgram length = %d", lc - sa);
}

// Close files
fclose(f1);
fclose(f3);

getch();  // Wait for key press
}





B.2	Input and Output: (Create input.txt and optab.txt with notepad and save all these three files in BIN)
input.txt file: 
- START 100
- LDA ALPHA
- ADD ONE
- STA BETA
ALPHA WORD 1
ONE WORD 1
BETA RESW 1
- END -

optab.txt file:
LDA 00
ADD 01
STA 02

Output - Symbol table: (Will automatically create a symtab.txt inside BIN and inside output will be there and also 
•	Compile: Alt + F9
•	Run: Ctrl + F9
•	See output: Alt + F5)
