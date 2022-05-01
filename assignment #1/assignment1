.data
	menu: 			.asciiz "\nMain Menu:\n1. Base Converter\n2. Add Rational Number\n3. Text Parser\n4. Mystery Matrix Operation\n5. Exit\nPlease select an option: "
	progEnd:		.asciiz "Program ends. Bye :)"
	inputMessage: 		.asciiz "input: "
	typeMessage:		.asciiz "type: "
	firstNumerator:		.asciiz "Enter the first numerator: "
	firstDenominator:	.asciiz "Enter the first denominator: "
	secondNumerator:	.asciiz "Enter the second numerator: "
	secondDenominator:	.asciiz "Enter the second denominator: "
	inputTextMessage: 	.asciiz "Input text : "
	parserCharMessage:	.asciiz "Parser characters: "
	table: 			.word	L1,L2,L3,L4,L5
	input:			.space 256
	userInput:		.space 2048
	int_array: 		.space 8192
	type: 			.space 256
	inputText:		.space 1024
	parserChar:		.space 1024
.text
	.globl main
main:
	li 	$v0, 4
	la 	$a0, menu
	syscall
		
	li 	$v0,5		
	syscall			
	move 	$t7, $v0
	
	la 	$t1, table		# &table
	blt 	$t7, $zero, L5		# if k < 0, goto exit
	li 	$t6, 5
	bgt 	$t7, $t6, L5		# if k > 5 goto exit	
	
	sll	 $t0, $t7, 2		# $t0 = k*4
	add 	$t0, $t0, $t1		# $t0 = &table + k*4
	addi 	$t0, $t0, -4		# if k == 1 go to L1
	
	lw 	$t1, 0($t0)
	jr 	$t1
	
L1: # Base Converter

	li 	$v0, 4
	la 	$a0, inputMessage
	syscall				# input message

	li 	$v0, 8
	la 	$a0 input
	li 	$a1, 256
	syscall				# get input from user

	li 	$v0, 4
	la 	$a0, typeMessage
	syscall				# type message

	li 	$v0, 5
	syscall				# get type from user (integer)
	
	
	la 	$a0, input
	jal 	baseConverter		# go to baseConverter()
	
	

	li 	$v0, 1
	move 	$a0, $v1	
	syscall				# output
	
	
	j main			
L2: # .Add Rational Number

	li 	$v0, 4
	la 	$a0, firstNumerator
	syscall			
	
	
	li 	$v0, 5
	syscall			# get firstNumerator from user
	move 	$t0, $v0	

	
	li 	$v0, 4
	la 	$a0, firstDenominator	# print "firstDenominator"
	syscall
	

	li 	$v0, 5
	syscall			# get firstDenominator from user
	move 	$t1, $v0	

	
	li 	$v0, 4
	la 	$a0, secondNumerator	# print "secondNumerator"
	syscall
	
	
	li 	$v0, 5
	syscall			# get secondNumerator from user
	move 	$t2, $v0	


	li 	$v0, 4
	la 	$a0, secondNumerator	# print "secondDenominator"
	syscall
	

	li 	$v0, 5
	syscall			# get secondDenominator from user
	
	move 	$t3, $v0	
	move 	$a0, $t0	# $a0 = $t0
	move 	$a1, $t1	# $a1 = $t1
	move 	$a2, $t2	# $a2 = $t2
	move 	$a3, $t3	# $a3 = $t4
	
	jal 	addRationalNumbers	
	
	# simplified form
	move 	$t0, $v0
	move 	$t1, $v1
	
	
	li 	$v0, 1
	move 	$a0, $a0
	syscall			# first numerator
	
	li 	$v0, 11
	li 	$a0, '/'
	syscall			# print '/'

	li 	$v0, 1
	move 	$a0, $a1
	syscall			# first denominator
	
	
	li 	$v0, 11
	li 	$a0, '+'
	syscall			# print '+'
	

	li 	$v0, 1
	move 	$a0, $a2
	syscall			# second numerator
	

	li 	$v0, 11
	li 	$a0, '/'
	syscall			# print '/'

	li 	$v0, 1
	move 	$a0, $a3
	syscall			# second denominator
	

	li 	$v0, 11
	li 	$a0, '='
	syscall			# print '='
	
	li 	$v0, 1
	move 	$a0, $t0
	syscall
	
	
	li 	$v0, 11
	li 	$a0, '/'
	syscall			# print '/'
	
	li 	$v0, 1
	move 	$a0, $t1
	syscall
	
	j main
L3: # Text Parser
	li $v0, 4
	la $a0, inputTextMessage
	syscall
	
	li $v0, 8
	la $a0, inputText
	li $a1, 1024
	syscall
	
	li $v0, 4
	la $a0, parserCharMessage
	syscall
	
	li $v0, 8
	la $a0, parserChar
	li $a1, 1024
	syscall
	
	la $a0, inputText		# base_addr of input text
	la $a1, parserChar		# base_addr of parser characters
	
	jal text_parser
	
	j main

L4: # Mystery Matrix Operation

	li 	$v0, 4
	la 	$a0, inputMessage
	syscall 
	
	li 	$v0, 8
	la 	$a0, userInput
	li 	$a1, 2048
	syscall		

				
	#args
	la 	$a0, userInput		# string_input base_addr
	la 	$a1, int_array		# int_array base_addr
	jal parse_string		# $v0 = array_length
	
	move 	$a0, $v0		# $a0 = array_length
	jal   	isqrt 			# $v0 = √$a0 
	
	move 	$a0, $v0		# $a0 = √$a0
	jal	 matrix			# void
	
	j main
L5: # exit

	la 	$a0, progEnd
	li	$v0, 4
	syscall
	
	li $v0, 10
	syscall
baseConverter:	
	addi 	$sp,$sp,-20		# Adjust stack pointer
	sw 	$ra,16($sp)		# Save $ra
	sw 	$a0, 12($sp)		# save $a0
	sw 	$s0, 8($sp)		# save $s0
	sw 	$s1, 4($sp)		# save $s1
	sw 	$s2, 0($sp)		# save $s2
	
	jal strlen
	
	#variables
	li 	$s0, 0			# type1_result = 0 initially
	li 	$s1, 0			# type2_result = 0 initially
	move 	$s2, $v1		# $s2 = strlen()
	li 	$t7, 0			# i = 0
	li 	$t6, 48			# ascii 48 = '0'
	
	# most significant bit part
	lb 	$t0, 0($a0)
	beq 	$t0,$t6, baseConverter_loop		# if msb == 0, go to baseConverter_loop
	addi 	$t1, $s2, -1		# strlen() -1 -	index, first index = 0 no need index - 1
	li, 	$t2, -1			# $t5 = -1 (inittially)
	sllv 	$t2, $t2, $t1		# $t5 = - 2 to the power of t6
	add 	$s0, $s0, $t2		# add $t5 to type1_result
	
	addi 	$a0, $a0, 1		# input[c++]
	addi 	$t7, $t7, 1		# i++
	
	
baseConverter_loop:
	# clear registers
	li 	$t2, 1			# $t2 = 1
	li 	$t1, 0			# $t1 = 0
	
	lb 	$t0, 0($a0)
	slt 	$at, $t7, $s2		# $at = 1 if i < strlen()	
	beqz	$at, baseConverter_end
	beq 	$t0, $t6 if_char_zero
	addi 	$t1, $s2, -1		# strlen -1
	sub 	$t1, $t1, $t7 		# $t1 = (strlen -1) - index
	sllv 	$t2, $t2, $t1		# $t2 = 2^($t6)
	add 	$s0, $s0, $t2		# add $t2 to type1_result
	addi 	$a0, $a0, 1		# input[c++]
	addi 	$t7, $t7, 1		# i++
	
	j baseConverter_loop
if_char_zero:
# if char == '0', increment index and address of $a0

	addi 	$a0, $a0, 1		# input[c++]
	addi 	$t7, $t7, 1		# i++
	j 	baseConverter_loop
	
baseConverter_end:
# return type1_result

	move 	$v1, $s0		# put type1_result into return regiser
	
	lw 	$s2, 0($sp)		# restore $s2
	lw 	$s1, 4($sp)		# restore $s1
	lw 	$s0, 8($sp)		# restore $s0
	lw 	$a0, 12($sp)		# restore $a0
	lw 	$ra,16($sp)		# restore $ra
	addi 	$sp, $sp, 16
	
	jr $ra
		

strlen:
## strlen($a0: char[])-> integer 

	addi 	$sp,$sp,-4		# Adjust stack pointer
	sw 	$a0,0($sp)		# Save $a0
	li 	$t0, 0			# string_length = 0 inittially
strlen_loop:
	lb 	$t1, 0($a0)
	beq 	$t1, $zero, strlen_end
	addi 	$a0, $a0, 1
	addi 	$t0, $t0, 1
	j 	strlen_loop
strlen_end:
	addi 	$t0, $t0, -1		# string_length -1 remove '\0' count from length
	move 	$v1, $t0
	lw 	$a0,0($sp)		# Restore $a0
	addi 	$sp, $sp, 4
	jr 	$ra
	
	
# $a0= firstNumerator, $a1= firstDenominaotor
# $a2= secondNumerator, $a3= secondDenominator
addRationalNumbers:
	
	addi 	$sp, $sp, -24		# Adjust stack pointer
	sw 	$a0, 20($sp)		# save $a0
	sw 	$a1, 16($sp)		# save $a1
	sw 	$a2, 12($sp)		# save $a2
	sw 	$a3, 8($sp)		# save $a3
	sw 	$s0, 4($sp)		# save $s0
	sw 	$s1, 0($sp)		# save $s1
	
	mul 	$t0, $a0, $a3		# $t0 = fNumerator * sDenominator
	mul	 $t1, $a1, $a2 		# $t1 = sNumerator 0 fDenominator
	add 	$t0, $t0, $t1		# $t0 = (fN * sD) + (sN * fD) -> numerator
	mul 	$t1, $a1, $a3		# $t1 = fD * sD -> denominator
	# save numerator and denominator at $t6 and $t7 respectively
	move	 $s0, $t0		
	move	 $s1, $t1
	
	
	
	
	############ Greatest common divisor
	
	# find max($t0, $t1)
	bge 	$t0, $t1, aRN_while	# if $t0 > $t1 go to aRN_gcd
	move 	$t2, $t1		# temp = $t1	
	move 	$t1, $t0,		# $t1 = $t0
	move 	$t0, $t2		# $t0 = temp
	
	# $t0 should be greater than $t1
aRN_while:
	blez 	$t1, aRN_end
	div 	$t0, $t1		# numerator / denominator || denominator / numerator 
	mfhi 	$t2			# $t2 = remainder
	move	$t0, $t1		# $t0 = $t1
	move 	$t1, $t2		# $t1 = remainder
	
	j 	aRN_while

	
aRN_end:
	div 	$s0, $t0		# numerator / $t0
	mflo 	$v0			
	div 	$s1, $t0		# denominator / $t1
	mflo 	$v1			
	
	lw 	$s1, 0($sp)		# restore $s1
	lw 	$s0, 4($sp)		# restore $s0
	lw 	$a3, 8($sp)		# restore $a3
	lw 	$a2, 12($sp)		# restore $a2
	lw 	$a1, 16($sp)		# restore $a1
	lw 	$a0, 20($sp)		# restore $a0
	addi 	$sp, $sp, 16 		# restore $sp
	
	
	jr $ra
	
	

	
# $a0 = base_addr of input string
# $a1 = base_addr of int_array
parse_string:
	addi 	$sp, $sp, -24		# adjust stack pointer
	sw	$ra, 20($sp)		# save $ra
	sw 	$a0, 16($sp)		# save $a0
	sw 	$a1, 12($sp)		# save $a1
	sw 	$s0, 8($sp)		# save $s0
	sw 	$s1, 4($sp)		# save $s1
	sw	$s2, 0($sp)		# save $s2
	
#initial values		
	move 	$t0, $a0 		# base_addr of temp string
	li 	$s0, 0			# parsed_string lenght
	li 	$s2, 0			# array lenght 			
parse_loop:
	lb  	$t1, 0($a0)        	# Load the first byte of $a0  into $t1
	beq	$t1, 10, str_to_int	# end of the string	if $t1 10('\n')
	beq 	$t1, 32, str_to_int	# if $t1 == ' ', goto str_to_int
	addi 	$a0, $a0, 1		# increment & of input string
	addi 	$s0, $s0, 1		# increment parsed_string lenght
	j parse_loop		
str_to_int:
	li	$t2, 0			# int i = 0;
	li 	$t3,0			# parsed_integer
str_to_int_loop:
	lb	$t1, 0($t0)
	bge	$t2, $s0, str_to_int_end	# if current index >= temp_str_len, goto str_to_int_end
	
	addi	$sp, $sp, -8		# adjust stack pointer
	sw	$a0, 4($sp)		# store $a0
	sw	$a1, 0($sp)		# store $a1
	li 	$a0, 10			# $a0 = 10
	sub	$a1, $s0, $t2 		# $a1=  str_len - index
	addi	$a1, $a1, -1 		# $a1 = (str_len - index) -1

	jal 	power

	lw	$a1, 0($sp)		# restore $a1
	lw	$a0, 4($sp)		# restore $a0
	addi	$sp, $sp, 8	 	# restore $sp
	
	andi  	$t4 $t1, 0x0F		# Mask the first four bits
	mul 	$v0, $v0, $t4		# 10^n * $t4
	add 	$t3, $t3, $v0	
	addi	$t0, $t0, 1		# increment pointer 
	addi 	$t2, $t2, 1		# i++ increment index
	j 	str_to_int_loop

power: 
	bne 	$a1, $zero, recursion
	li 	$v0, 1
	jr 	$ra
recursion:
	addi	$sp, $sp, -4
	sw 	$ra, 0($sp)
	addi 	$a1, $a1, -1
	jal 	power
	mul 	$v0, $a0, $v0
	lw 	$ra, 0($sp)
	addi 	$sp, $sp, 4
	jr	$ra	
	
	
str_to_int_end:

	sw 	$t3, 0($a1)		# store integer into 'int_array'
	addi 	$a1, $a1, 4		# base_address + 4 for next pointer
	addi 	$s2, $s2, 1		# increment array_length
	beq	$t1, 10, proc_end	# end of the string	if $t1 10('\n')
	
	
	# reset variables
	li 	$s0, 0			# reset parsed_string lenght
	addi 	$a0, $a0, 1		# address of the first character of the next string
	move 	$t0, $a0		# temp_ address of the first character of the next string 
	j 	parse_loop
proc_end:
	
	move $v0, $s2			# store array_length into return register ($v0) 
	lw	$s2, 0($sp)		# restore $s2
	lw 	$s1, 4($sp)		# restore $s1
	lw 	$s0, 8($sp)		# restore $s0
	lw 	$a1, 12($sp)		# restore $a1
	lw 	$a0, 16($sp)		# restore $a0
	lw	$ra, 20($sp)		# restore $ra
	addi 	$sp, $sp, 24		# restore $sp
	jr 	$ra
	
############### MATRIX CALCULATION
matrix:
	addi 	$sp, $sp -8
	sw	$s0, 4($sp)
	sw 	$s2, 0($sp)
	
	li 	$s5, 2			# CONSTANT = 2
	la 	$s0, int_array		# load int_array base addr into $t0
	move	$t1, $a0		# store N into $t1
    	li 	$t3, 0               	# initialize outer-loop counter to 0 (i)

horizontal_matrix_loop_outer:
    	bge 	$t3, $t1, horizontal_matrix_loop_outer_end
	li 	$t2, 1		    	# temp_result 
    	li 	$t4, 0               	# initialize inner-loop counter to 0 (y)

horizontal_matrix_loop_inner:
    	bge 	$t4, $t1, horizontal_matrix_loop_inner_end
	div   	$t4, $s5	    	# $t4 / 2		
	mfhi	$t7			# remainder
	bnez	$t7, remainder_one		
    	mul 	$t5, $t3, $t1       	# $t5 = width * i
    	add 	$t5, $t5, $t4       	# $t5 = width * i + y
    	sll 	$t5, $t5, 2         	# $t5 = DATA_SIZE * (width * i + y)
    	add 	$t5, $s0, $t5       	# $t5 =  base address + (2^2 * (width * i + y))
	lw 	$t6, 0($t5)          	# load $t5 address into $t6
	mul 	$t2, $t2, $t6		# temp_result *= array[i][j]
    	addiu 	$t4, $t4, 1         	# increment y++ (inner-loop)
    	j 	horizontal_matrix_loop_inner    

remainder_one:
	addi	$sp, $sp, -4		# adjust stack pointer
	sw	$t3, 0($sp)		# store $t3
	
	addi 	$t3, $t3, 1		# i += 1
	mul 	$t5, $t3, $t1       	# $t5 <-- width * i
    	add 	$t5, $t5, $t4       	# $t5 <-- width * i + y
    	sll 	$t5, $t5, 2         	# $t5 <-- 2^2 * (width * i + y)
    	add 	$t5, $s0, $t5       	# $t5 <-- base address + (2^2 * (width * i + y))
	lw $t6, 0($t5)          	# store input number into array
	mul 	$t2, $t2, $t6		# temp_result *= array[updated_i][j]	
	addiu 	$t4, $t4, 1         	# increment y++ (inner-loop)
	
	lw	$t3, 0($sp)		# restore $t3
	addi 	$sp, $sp, 4		# restore $sp
	
    	j	horizontal_matrix_loop_inner

horizontal_matrix_loop_inner_end:
    	addi 	$t3, $t3, 2          	# increment i++ (outer-loop)
    	
    	li 	$v0, 1
    	move 	$a0, $t2
    	syscall
    	
    	la 	$a0, '\t'
    	li 	$v0, 11
    	syscall
    	j 	horizontal_matrix_loop_outer 

############### VERTICAL MATRIX INITIALIZATION
horizontal_matrix_loop_outer_end:
	
	la 	$a0, '\n'
    	li 	$v0, 11
    	syscall				# print '\n'
	la 	$s0, int_array
    	li 	$t3, 1               	# initialize outer-loop counter to 0 (i)
vertical_matrix_loop_outer:
    	bge 	$t3, $t1, vertical_matrix_loop_outer_end
	li 	$t2, 1		    	# temp_result 
    	li 	$t4, 0               	# initialize inner-loop counter to 0 (y)
vertical_matrix_loop_inner:
    	bge 	$t4, $t1, vertical_matrix_loop_inner_end
	div   	$t4, $s5	    	# $t4 / 2	
	mfhi	$t7			# remainder
	bnez	$t7, v_remainder_one	# if remainder == 1, goto v_remainder_one	
    	mul 	$t5, $t4, $t1       	# $t5 = width * y
    	add 	$t5, $t5, $t3       	# $t5 = width * y + i
    	sll 	$t5, $t5, 2         	# $t5 = DATA_SIZE * (width * y + i)
    	add 	$t5, $s0, $t5       	# $t5 = base address + (DATA_SIZE * (width * y + i))
	lw 	$t6, 0($t5)          	# load $t5 address into $t6
	mul 	$t2, $t2, $t6		# temp_result *= array[i][y]
    	addiu 	$t4, $t4, 1         	# increment y++ (inner-loop)
    	j 	vertical_matrix_loop_inner    

v_remainder_one:
	addi	$sp, $sp, -4		# adjust stack pointer
	sw	$t3, 0($sp)		# store $t3 
	
	addi 	$t3, $t3, -1		# i -= 1
	mul 	$t5, $t4, $t1       	# $t5 = width * y
    	add 	$t5, $t5, $t3       	# $t5 = width * y + i
    	sll 	$t5, $t5, 2         	# $t5 = 2^2 * (width * y + i)
    	add 	$t5, $s0, $t5       	# $t5 = base address + (DATA_SIZE * (width * y + i))
	lw 	$t6, 0($t5)          	# load $t5 address into $t6
	mul 	$t2, $t2, $t6		# temp_result *= array[i][updated_y]	
	addiu 	$t4, $t4, 1         	# increment y++ (inner loop)
	
	lw	$t3, 0($sp)		# restore $t3
	addi 	$sp, $sp, 4		# restore $sp
	
    	j	vertical_matrix_loop_inner    

vertical_matrix_loop_inner_end:
    	addi 	$t3, $t3, 2          	# increment i++ (outer-loop)
    	li 	$v0, 1
    	move 	$a0, $t2		# put temp_result to $a0
    	syscall				# print temp_result
  
    	la 	$a0, '\t'
    	li 	$v0, 11
    	syscall				# print '\t'
    	j 	vertical_matrix_loop_outer    

############### END OF THE MATRIX PROCEDURE
vertical_matrix_loop_outer_end:
	lw	$s2, 0($sp)		# restore $s2
	lw	$s0, 4($sp)		# restore $s0
	addi 	$sp, $sp 8		# restore $sp
	
	jr 	$ra
    
    	
    
# find square root for N
 isqrt:
	move  	$v0, $zero        	# initalize return
  	move  	$t1, $a0          	# move a0 to t1

  	addi  	$t0, $zero, 1
  	sll   	$t0, $t0, 30      	# shift to second-to-top bit

isqrt_bit:
  	slt   	$t2, $t1, $t0     	# num < bit
  	beq   	$t2, $zero, isqrt_loop

  	srl   	$t0, $t0, 2       	# bit >> 2
  	j     	isqrt_bit

isqrt_loop:
  	beq   	$t0, $zero, isqrt_return

  	add   	$t3, $v0, $t0     	# t3 = return + bit
  	slt   	$t2, $t1, $t3
  	beq   	$t2, $zero, isqrt_else

  	srl   	$v0, $v0, 1       	# return >> 1
  	j     	isqrt_loop_end

isqrt_else:
  	sub   	$t1, $t1, $t3     	# num -= return + bit
  	srl   	$v0, $v0, 1       	# return >> 1
  	add   	$v0, $v0, $t0     	# return + bit

isqrt_loop_end:
  	srl   	$t0, $t0, 2       	# bit >> 2
  	j     	isqrt_loop

isqrt_return:
  	jr 	$ra
    
    
    
    
    
    
text_parser:
	#initialization
	addi 	$sp, $sp, -16
	sw	$a0, 12($sp)		# store $a0
	sw	$a1, 8($sp)		# store $a1
	sw	$s0, 4($sp)		# store #s0
	sw	$s1, 0($sp)		# store $s1

	li	$t0, 0			# outer loop counter = 0
	li 	$t1, 0			# inner loop counter = 0,
	li	$t2, 0			# start address of next word
	li	$t3, 0			# register where each iterated character is stored (Input)
	li 	$t4, 0			# register where each iterated character is stored (Parser)

	move 	$s0, $a0		# base_addr of input text	
text_parser_outer_loop:
	move	$s1, $a1		# base_addr of parser characters
	lb	$t3, 0($s0)
	beq	$t3, $zero, text_parser_outer_loop_end
	beq	$t3, 32, new_line
text_parser_inner_loop:

	lb	$t4, 0($s1)	
	beq 	$t4, $t3, new_line
	beq	$t4, $zero, print_char	
	
	addi	$s1, $s1, 1		# increment y++ (inner-loop)
	j 	text_parser_inner_loop
	
new_line:
	li $v0, 11
	la $a0, '\n'
	syscall 
text_parser_inner_loop_end:
	addi 	$s0, $s0, 1          	# increment i++ (outer-loop)
    	
    	j 	text_parser_outer_loop

text_parser_outer_loop_end:

	
	lw	$s1, 0($sp)		# store $s1
	lw	$s0, 4($sp)		# store #s0
	lw	$a1, 8($sp)		# store $a1
	lw	$a0, 12($sp)		# store $a0
	addi 	$sp, $sp, 16		# store $sp
	
	jr 	$ra
	

print_char:
	li $v0, 11
	move $a0, $t3
	syscall 
	
	j text_parser_inner_loop_end