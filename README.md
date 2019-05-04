# Assembly-Red-Green

--changes the color of LED on MSP430 depending on the number being Odd or Even--

 bis.b #01000001b,P1DIR
 mov.w #0200h,R5 ; id
 mov.w #0000h,R7 ; odd counter
 mov.w #0000h,R6 ; even counter
 mov.w #0200h,R8 ; pointpoint
 call #redlightdistrict

redlightdistrict:
Control:
 mov #0000h,0(R5) 
 mov #0002h,2(R5)
 mov #0004h,4(R5)
 mov #0006h,6(R5)
 mov #0008h,8(R5)
 mov #0009h,10(R5)
 mov #0006h,12(R5)
 mov #0005h,14(R5)
 mov #0001h,16(R5)
 mov #0000h,18(R5)
 mov #0000h,20(R5)
 rrc @R8
 jc Odd
 jge Even
 jlo Even
Even:
 inc R6
 cmp #0214h,R8
 jz End
 incd R8
 jmp Control
Odd:
 inc R7
 cmp #0214h,R8
 jz End
 incd R8
 jmp Control
End:
 cmp R7,R6
 jge red
 jl green
red:
 bic.b #01000000b,P1OUT
 bis.b #00000001b,P1OUT
 jmp red
green:
 bic.b #00000001b,P1OUT
 bis.b #01000000b,P1OUT
 jmp green
