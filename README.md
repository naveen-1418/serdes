# serdes
SERDES is a high-speed data communication circuit that converts parallel data into serial  data for transmission and then reconverts it back into parallel data at the receiving end

• At the transmitter side, the Serializer converts multiple parallel data lines into a 
single high-speed serial data stream, reducing the number of transmission paths 
required. 
• At the receiver side, the Deserializer reconstructs the original parallel data from the 
incoming serial data stream, enabling efficient processing at the destination. 


Serializer Architecture in 8b/10b SERDES 

1. Encoder

The Encoder is a crucial component in the SERDES system, responsible for converting data 
from one format to another while ensuring data integrity. It functions as a data transformer, 
modifying the original data into a structured format that enhances transmission reliability. In 
this case, the encoder takes a 8-bit data input and transforms 
it into a 10-bit encoded output. 
The primary purpose of this encoding process is to ensure synchronization, maintain DC 
balance, and enable error detection during data transmission. By encoding the data into a 
10-bit format, the system can differentiate between valid and erroneous data more 
effectively. If a properly encoded 10-bit data sequence is received at the Decoder, it will 
successfully retrieve the original data. However, if an incorrect sequence is detected, the 
decoder will produce a default output, indicating an error in transmission. 
One of the key advantages of this encoding scheme is DC balance, which helps prevent long 
runs of consecutive 1s or 0s that could cause synchronization issues. Maintaining DC balance 
ensures a more stable and error-free data transfer. After the 12-bit to 10-bit conversion, the 
encoder sends the 10-bit encoded output to the PISO (Parallel Input Serial Output) 
module, where it will be prepared for serial transmission.

3. Parallel-In Serial-Out (PISO) Shift Register

The Parallel Input to Serial Output (PISO) module is a fundamental component of the 
SERDES (Serializer/Deserializer) system, responsible for converting parallel data into a serial 
stream. This conversion is crucial for efficient high-speed data transmission, as serial 
communication reduces the number of required physical connections, making it suitable for 
long-distance or high-speed applications. 
In the serializer, the PISO module receives a 10-bit parallel data input from the encoder and 
converts it into a serial stream. The module operates in a First-In, First-Out (FIFO) manner, 
meaning that the data is transmitted in the same order in which it was received. The 
transmission starts from the Least Significant Bit (LSB) to the Most Significant Bit (MSB), 
ensuring an organized flow of data. 
Once the parallel-to-serial conversion is complete, the serialized data is sent to the Serial 
Input to Parallel Output (SIPO) module at the receiving end, where it will be reconstructed 
into its original form. The PISO module plays a crucial role in maintaining synchronization 
and data integrity, ensuring that the transmitted bits are correctly received and interpreted 
at the destination.

Deserializer and Its Blocks 

1. Serial Input to Parallel Output (SIPO)

The SIPO (Serial Input to Parallel Output) module is the core component of the deserializer. 
It receives the serial data stream from the transmitter (PISO) and converts it into a parallel 
format for further processing. Parallel data is crucial in real-time systems because it allows 
for faster processing and computation. 
The SIPO module operates in a First-In, First-Out (FIFO) manner, meaning that the first bit 
received is the first bit stored and output. Once all 10 bits are received, they are transferred 
in parallel to the Decoder for further processing. 
In older communication systems, parallel transmission was used directly. However, this 
method had several disadvantages such as Electromagnetic Interference (EMI), data 
mismatching, and high complexity due to multiple transmission lines. Serial communication 
overcomes these issues by using fewer data lines, reducing interference, and improving 
efficiency.

2. Decoder 

The Decoder plays a key role in converting the received encoded 10-bit data back to its 
original 8-bit format. The decoder functions similarly to a password authentication system, 
where only the correctly encoded data is accepted. If the received 10-bit data does not 
match any valid encoded pattern, it indicates an error, and a default data value is provided 
instead. 
The 10-bit input from the SIPO is matched against predefined encoded values. If a valid 
match is found, the 8-bit decoded data will appear at the output. 
