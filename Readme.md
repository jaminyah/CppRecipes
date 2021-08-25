# Cpp Recipes

1. Threads
1.1 Thread Join

```cpp
/*
 *  Reference: 
 *  https://stackoverflow.com/questions/14650885/how-to-create-timer-events-using-c-11/14665230
 *  
 *  Compile: clang++ -std=c++11  main.cpp -o main
 */

#include <chrono>
#include <thread>
#include <iostream>

using namespace std;

void helloTimer() {
    int delay = 5000;
    this_thread::sleep_for(chrono::milliseconds(delay));
    cout << "Hello, Thread World!" << endl;
}

int main() {
    thread hello_thread(helloTimer);
   // hello_thread.detach();                  // async
    hello_thread.join();                      // sync
    cout << "Hello, Timer World!" << endl;
}
```

1.2 Thread Detach

```cpp
/*
 *  Reference: 
 *  https://stackoverflow.com/questions/14650885/how-to-create-timer-events-using-c-11/14665230
 *  
 *  Compile: clang++ -std=c++11  main.cpp -o main
 */

#include <chrono>
#include <thread>
#include <iostream>

using namespace std;

void helloTimer() {
    int delay = 5000;
    this_thread::sleep_for(chrono::milliseconds(delay));
    cout << "Hello, Thread World!" << endl;
}

int main() {
    thread hello_thread(helloTimer);
    hello_thread.detach();                  // async
    cout << "Hello, Timer World!" << endl;
}
```