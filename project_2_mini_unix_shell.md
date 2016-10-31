# Project 2: Mini UNIX Shell

##Challenges:
1. **Data Structures**:  
For this problem, I need to first parse the commands to identify the input type, output type, and also identify whether it is a pipe.  
To store these information, a create a structure. I can use a vector to store these information or use pointer.  
It is easy to implement in vector, but it is not as effective as pointer does.  
But, when there's a mistake, it is really hard to debug for stack overflow/memory leakage. 