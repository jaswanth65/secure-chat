Explanation of AES - 128 bit

It is easy to understand, think of it less like a math problem and more like a very sophisticated, automated shuffling machine.

I will break this down into 3 Parts: The Setup, the 4 Shuffling Moves, and The Repetition.

Part 1: The Setup (The Block and The Grid) 
Before the encryption starts, AES prepares your data. AES is a Block Cipher, which means it doesn't encrypt your file byte-byte in a stream. Instead, it chops your data into fixed chunks called "blocks."
1. The Block: Imagine you have a long message. AES takes the first 128 bits (which is 16 bytes/characters) and puts the rest aside later. It focuses entirely on this one block.
2. The Grid (The State): It doesn't process these 16 bytes in a straight line. It arranges them into a 4X 4 grid called the "State Array."
The Key: You also have a secret password (the Key) that is 128 bits long. This key is also arranged into a grid.
•	State Array
			
			
			
			
•	Key Grid
			
			
			
			

This is a great topic. To make AES-128 (Advanced Encryption Standard) easy to understand, think of it less like a math problem and more like a very sophisticated, automated shuffling machine.
I will break this down into 3 Parts: The Setup, The 4 Shuffling Moves, and The Repetition.
________________________________________
Part 1: The Setup (The Block and The Grid)
Before the encryption starts, AES prepares your data. AES is a Block Cipher, which means it doesn't encrypt your file byte-by-byte in a stream. Instead, it chops your data into fixed chunks called "blocks."
1. The Block:
Imagine you have a long message. AES takes the first 128 bits (which is 16 bytes/characters) and puts the rest aside for later. It focuses entirely on this one block.
2. The Grid (The State):
It doesn't process these 16 bytes in a straight line. It arranges them into a $4 \times 4$ grid called the "State Array."
•	The Key: You also have a secret password (the Key) that is 128 bits long. This key is also arranged into a grid.
The Goal: We want to scramble the "Data Grid" using the "Key Grid" so thoroughly that no one can reverse it without the key.
________________________________________
Part 2: The 4 Shuffling Moves (The Round)
This is where the magic happens. To scramble the data, AES performs a specific sequence of four operations. This sequence is called a Round.
Think of a Round as one full spin of a Rubik's Cube.
Move 1: SubBytes (The Disguise)
•	What happens: AES looks at every single byte in the grid and replaces it with a different byte based on a fixed lookup table (called an S-Box).
•	Analogy: It’s like a decoder ring. If the box says "A," change it to "Z." If it says "B," change it to "Q." This breaks the relationship between the original text and the cipher.
Move 2: ShiftRows (The Shuffle)
•	What happens: AES takes the rows of the grid and shifts them to the left.
o	Row 1: Stays put.
o	Row 2: Shifts left by 1.
o	Row 3: Shifts left by 2.
o	Row 4: Shifts left by 3.
•	Analogy: This is like shuffling a deck of cards. Data that was in one column is now spread across different columns.
Move 3: MixColumns (The Blur)
•	What happens: Each column is multiplied by a mathematical matrix. This combines the 4 bytes in a column to create 4 brand new bytes.
•	Analogy: Think of mixing colors. If you have a column with [Red, Blue, Yellow, White], MixColumns mixes them so they all influence each other. If you change even one tiny bit of the "Red," the result of the whole column changes.
 
Move 4: AddRoundKey (The Lock)
•	What happens: The Data Grid is combined (XORed) with the Key Grid.
•	Analogy: This is the actual "locking" step. Even if you knew the shuffling moves above, without this Key, you can't proceed.
Part 3: The Repetition (Rounds 1-10)
If we did the moves in Part 2 just once, a computer could figure it out pretty quickly. To make it secure, AES repeats the process.
1. The Rounds: For AES-128, the process repeats 10 times.
•	Rounds 1 through 9: Perform all 4 moves (SubBytes, ShiftRows, MixColumns, AddRoundKey).
•	Round 10 (Final Round): Performs only 3 moves (It skips MixColumns).
2. Key Expansion: We don't use the exact same key for all 10 rounds. That would be weak. AES takes your original master key and mathematically stretches it out to create 10 distinct "Round Keys"—one unique key for each round.
Summary
1.	Input: You take 128 bits of data and put them in a grid.
2.	Scramble: You Substitute, Shift, Mix, and Add the Key.
3.	Repeat: You do this 10 times in a row.
By the time the data comes out the other side, it looks like complete noise. The only way to get it back to the original grid is to run the process in reverse order using the exact same key.
Counter Mode
•	CTR (“Counter”) mode transforms AES from a block cipher into a keystream generator. You don’t encrypt the message directly with AES; you encrypt “counter blocks” and XOR those outputs with the message.
•	For each chunk of your message:
•	• 	Build a 16‑byte counter block from the nonce and a running counter. In your code:
•	First 8 bytes: nonce prefix.
•	Last 8 bytes: counter value (0, 1, 2, …).
 
•	Encrypt the counter block with AES → you get 16 bytes of keystream.




 
HMAC
•	Encryption alone doesn’t tell you if someone modified the message. HMAC gives you that check.
•	In our project we are using 32-byte(256 bit) HMAC key
•	Compute HMAC
o	It takes your HMAC key and the data (here ,nounce+ciphertext) and produces a fixed‑length tag (MAC).
