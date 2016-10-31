# Project1: Apartment Finder Website

* challenges:  
(1) **Code resuable**: make the code clean and easy to maintain. For the MVC based architecture, it is straightforward to implement different parts. However, it takes time to think about how to make the code succinct.  
Many codes are reusable. So I spent much time on design the java bean, and make it relates to different functions.  
(2) **Synchronization problem**: if multiple users visit the website and book the room, we should synchronize the number of available rooms.  
***thread safe***:  
**Approach 1**: Synchronizing the critical sections  
Step1: Make fields private    
Step2: Identify and synchronize critical sections  
**Approach 2**: Immutable objects  
**Approach 3**: Thread-safe wrappers