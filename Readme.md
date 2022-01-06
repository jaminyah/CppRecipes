# Cpp Recipes

```bash
1. Threads
2. Vectors
```

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

1.3 Factorial with large numbers

```cpp
#include <stdio.h>

void factorial(int);

int main() {

    factorial(20);
    printf("\n");
    return 0;
}

void factorial(int number) {
    int store[30] = {0};
    int result = number;
    int factor = 0;
    int size = 0;
    int index = 0;
    int carry = 0;

    // store the number digit in reverse order
    while (result > 0) {
        store[size] = result % 10;
        result /= 10;
        size += 1;
    }

    // n*(n-1)*(n-2) operations
    factor = number - 1;              // (n-1)
    while (factor > 0) {
        index = 0;

        // multiply each array digit by factor, add carry
        while (index < size) {
            result = store[index] * factor + carry;
            store[index] = result % 10;
            carry = result / 10;
            index += 1;
        }

        // store last carry
        while (carry > 0) {   
            store[index] = carry % 10;
            carry /= 10;
            index += 1;
        }

        // decrement factorial multiplier
        factor -= 1;
        size = index;               // array count
    }

    printf("\ndisplay in reverse: ");
    for (int j = 0; j < size; j++) {
        printf("%d", store[j]);
    }

    printf("\ndisplay in order: ");
    for (int j = size - 1; j >= 0; j--) {
        printf("%d", store[j]);
    }
}
```