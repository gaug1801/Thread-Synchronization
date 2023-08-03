README - How to compile and run the program, known problems, data structures, pseudocode

*How to compile and run the program

To compile the program, navigate to the directory containing the source file (threadSync.c) using the terminal.
Once in the appropriate directory, compile the program using the gcc compiler, like this:

gcc -o thread_sync thread_sync.c -Wall -Werror

*To run the program:

If you want to enter information manually, type:

./threadSync

If you want to read data from a file, type:

./threadSync [filename].txt

*How to enter schedule information through the user interface

When you run the program without passing a file, it will ask for inputs from the user.

Enter the number of groups in the schedule:
Enter the number of vehicles:
Enter the Northbound probability: //The sum of Northbound and Southbound probabilities should be 1.
Enter the Southbound probability: 
Enter the delay before the next group: //In seconds

EXAMPLE:

Enter the number of groups in the schedule: 2

Group 1
Enter the number of vehicles: 5
Enter the Northbound probability: 0.6
Enter the Southbound probability: 0.4
Enter the delay before the next group: 3

Group 2
Enter the number of vehicles: 3
Enter the Northbound probability: 0.7
Enter the Southbound probability: 0.3
Enter the delay before the next group: 2

*Known Problems

As of the latest implementation, there are no known problems with the program. It operates as intended, accurately modeling vehicles traffic across a bridge using multithreading, mutexes and condition variables. However, it is worth mentioning one should be aware of the following limitations:

The implementation doesn't currently handle cases where the entered northbound and southbound probabilities don't add up to 1. The user should ensure this manually.
The program doesn't perform robust error checks on user input. Please ensure that inputs are within the correct range and type.

When the number of vehicles exceeds the MAX_VEHICLES macro, the program does not handle it. It's advisable to keep the total number of vehicles below this limit.

*Data Structures

pthread_t *threads: An array of type pthread_t is allocated dynamically to store the thread IDs of all the vehicles.

vehicle_args: A struct type which is dynamically allocated for each vehicle. This struct holds the vehicle_id and northbound_prob. This struct is passed as an argument to each thread.

*Pseudocode

Define necessary mutexes and condition variables

Initialize mutexes and condition variables

Allocate space for storing thread IDs

Read inputs (from a file or stdin) for number of groups

FOR each group DO

	Read inputs (from a file or stdin) for number of vehicles, northbound probability, southbound probability and delay
   
	FOR each vehicle in the group DO
       		
		Allocate memory for a `vehicle_args` struct and set `vehicle_id` and `northbound_prob`
       		
		Create a new thread with `vehicle_routine` function and pass the allocated `vehicle_args` struct as an argument
	
	END FOR
	
	Delay before the next group arrives

END FOR

Wait for all the threads (vehicles) to complete

Cleanup: Destroy all the mutexes and condition variables, close the file (if opened), and free allocated memory.

Exit program


Author: Gabriel Augustin