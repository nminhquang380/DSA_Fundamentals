# Bit Manipulation
## Introduction
Computers do not understand natural languages as humans do. Instead, a computer is encoded at the lowest level to a series of ones and zeroes, called **binary code**. This code is read by the computer as instructions, telling it what to do next.

A single digit of a binary sequence is called a bit (or, binary digit), and can be either a one or a zero. Bits are the smallest unit of data used by computers to write instructions.

A binary sequence (a sequence of bits) is read from right to left. In this case, we call the rightmost bit, the Least Significant Bit (LSB), and the leftmost bit, the Most Significant Bit (MSB).

A binary sequence of 8 bits (byte) can store any number from 0 to 255. However, historically, a byte represents different lengths of binary sequences in different computer architectures. For example, early IBM PCs used a byte to store 8 bits, while later models used a byte to store 6 or 7 bits. Similarly, a binary sequence consisting of multiple bytes (sometimes referred to as a “word”) can represent different lengths as well.

## Basics of bit manipulation: Operators
1. AND (&)
The AND operator (&) takes in two binary values and produces a third value whose bits are set to 1 if both of the bits compared are 
equal to 1. Otherwise, it returns a 0.

We can use the AND (&) operator on two binary sequences of an equal length. To that end, you can compare each pair of bits at the same corresponding position and accumulate their result.

    For Example:
    X = 1001
    Y = 1010
    X&Y = 1000

2. OR (|)
The | operator compares two bits and returns 1 if at least one of the bits compared is equal to 1. Otherwise, it produces a 0.

We can use the OR operator on two binary sequences of an equal length. To that end, you compare each pair of bits at the same corresponding position and accumulate their result.

    For Example:
    X = 1001
    Y = 1010
    X|Y = 1011

3. XOR (^)
The XOR operator (^) stands for Exclusive OR. The XOR operator compares two bits and returns 1 if those bits are **different**. If both bits are the **same**, then XOR returns a 0.

| X | Y | X^Y |
|---|---|-----|
| 0 | 0 |  0  |
| 0 | 1 |  1  |
| 1 | 0 |  1  |
| 1 | 1 |  0  |

For example:
    X XOR Y = (1010) XOR (1001) = (0011)

4. NOT (~)
The operations described above are two bits operators and take two bits as input while producing a single bit as output. In contrast, the NOT operator is a single-bit operator as it takes a single bit as its input. The ~ operator flips the input bit. That is, it converts (flips) an input bit of 1 to 0 and 0 to 1.

We can apply the NOT operator to a binary sequence of any length. In that case, it will flip each bit of that sequence from 0 to 1 and from 1 to 0.

## Bit Facts and Tricks

X ^ 0 = X 
X ^ 1 = ~X 
X ^ X = 0 
X & 0 = 0 
X & 1 = X 
X & X = X 
x | 0 = x 
x | 1 = 1  
X | X = X

## Two's Complement and Negative Numbers
Computers typically store integers in two's complement representation. A positive number is represented 
as itself while a negative number is represented as the two's complement of its absolute value (with a 1 in its 
sign bit to indicatethat a negative value). The two's complement of an N-bit number (where N is the number 
of bits used for the number, excluding the sign bit) is the complement of the number with respect to $2^N$.

In other words, the binary representation of -K (negative K) as a N-bit number is cone at ( 1, $2^N-1 - K$ ).

## Arithmetic vs Logical Right Shift
There are two types of right shift operators. The arithmetic right shift essentially divides by two. The logical 
right shift does what we would visually see as shifting the bits. This is best seen on a negative number.

In a logical right shift, we shift the bits and put a 0 in the most significant bit. It is indicated with a >>> 
operator. 

In an arithmetic right shift, we shift values to the right but fill in the new bits with the value of the sign bit. 
This has the effect of (roughly) dividing by two. It is indicated by a >> operator.

## Common Bit Tasks
The following operations are very important to know, but do not simply memorize them. Memorizing leads 
to mistakes that are impossible to recover from. Rather, understand how to implement these methods, so 
that you can implement these, and other, bit problems. 
### Get Bit
This method shifts 1 over by i bits, creating a value that looks like 00010000. By performing an AND with 
num, we clear all bits other than the bit at bit i. Finally, we compare that to 0. Jf that new value is not zero, 
then bit i must have a 1. Otherwise, bit i is a 0.
```
boolean getBit(int num, int i) {
    return ((num & (1 << i)) != 0);
}
```
### Set Bit
SetBit shifts 1 over by i bits, creating a value like 00010000. By performing an OR with num, only the 
value at bit i will change. All other bits of the mask are zero and will not affect num. 
```
int setBit(int num, int i){
    return num | (1 << i);
}
```
### Clear Bit
This method operates in almost the reverse of setBit. First, we create a numberlike 11101111 by creating 
the reverse of it (00010000) and negating it. Then, we perform an AND with num. This will clear the ith bit 
and leave the remainder unchanged. 
```
int clearBit(int nun, inti) { 
int mask= N(l << i); 
return nun & mask; 
} 
```

To clear all bits from the most significant bit through i (inclusive), we create a mask with a 1 at the ith bit (1 
< < i). Then, we subtract 1 from it, giving us a sequence of 0s followed by i ls. We then AND our number 
with this mask to leave just the last i bits. 
```
int clearBitsMSBthroughI(int nun, inti) { 
int mask= (1 << i) - 1; 
return nun & mask; 
} 
```

lo clear all bits from i through 0 (inclusive), we take a sequence of all ls (which is -1) and shift it left by i + 1 bits. This gives us a sequence of 1 s (in the most significant bits) followed by i 0 bits. 
```
int clearBitsithrough0(int num, inti) { 
int mask= (-1 << (i + 1)); 
return num & mask; 
} 
```

### Update Bit
To set the ith bit to a value v, we first clear the bit at position i by using a mask that looks like 11101111. 
Then, we shift the intended value, v, left by i bits. This will create a number with bit i equal to v and all 
other bits equal to 0. Finally, we OR these two numbers, updating the ith bit if vis 1 and leaving it as 0 
otherwise. 
```
int updateBit(int num, inti, boolean bitlsl) { 
int value= bitlsl? 1: 0; 
int mask= N(l << i); 
return (num & mask) I (value<< i); 
} 
```