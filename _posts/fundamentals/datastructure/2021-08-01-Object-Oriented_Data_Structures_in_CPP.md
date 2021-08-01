---
layout: post
title: <ACSF> Object Oriented Data Structure in C++
subtitle : Accelerated Computer Science Fundamentals Specialization course from Coursera
tags: [datastructure, coursera]
author: Leena Kim
comments : true
---



< Coursera Object-Oriented Data Structures in C++ >



# Week 1

cpp-class/Cube.h

```c++
/**
 * Simple C++ class for representing a Cube.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

// All header (.h) files start with "#pragma once":
#pragma once

// A class is defined with the `class` keyword, the name
// of the class, curly braces, and a required semicolon
// at the end:
class Cube {
  public:  // Public members:
    double getVolume();
    double getSurfaceArea();
    void setLength(double length);

  private: // Private members:
    double length_;
};

```

- .h 파일 : 헤더파일. 
- #pragma once : only compile once
- public / private 
- variable + '_' : to refer to private variable



cpp-class/Cube.cpp

```c++
/**
 * Simple C++ class for representing a Cube.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"

double Cube::getVolume() {
  return length_ * length_ * length_;
}

double Cube::getSurfaceArea() {
  return 6 * length_ * length_;
}

void Cube::setLength(double length) {
  length_ = length;
}

```

- .cpp 파일 : contains all logic to implement to hour .h file 
- 3 functions to implement to .h file 
  - ` Cube::getVolume()` : these functions name needs to include the name of the class where they're defined in.  => going to define the implementation of the cubes getVolume function
  - `setLength()` : update internal variable 'length' 



cpp-class/main.cpp

```c++
/**
 * C++ code for creating a Cube of length 2.4 units.
 * - See ../cpp-std/main.cpp for a similar program with print statements.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>
#include "Cube.h"

int main() {
  Cube c;

  c.setLength(3.48);
  double volume = c.getVolume();
  std::cout << "Volume: " << volume << std::endl;

  return 0;
}

```

- #include "Cube.h" : let compiler know what a cube object is. To insert the contents of another file at the current location while processing the current file.



## 1.3 C++'s Standard Library (std)

```c++
/**
 * C++ program for a simple "Hello, world!"
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

int main() {
  std::cout << "Hello, world!" << std::endl;
  return 0;
}

```

- C++ standard library(std) : common tools, functionality
  - #include 
  - iostream : std::cout 

- Std::cout << content << std::endl;
- 콘솔에 파일이름 치면됨 ./cout



```c++
/**
 * C++ program for a simple "Hello, world!" with `using`.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  cout << "Hello, world!" << endl;
  return 0;
}

```

- using std::cout; => 선언하면 그냥 cout 만 해도 가능. cout 쓰면 std::cout 으로 인식하게 하겠다. 



```c++
/**
 * Simple C++ making use of std::cout and a `Cube` class.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>
#include "Cube.h"

int main() {
  uiuc::Cube c;
  c.setLength(2.4);
  std::cout << "Volume: " << c.getVolume() << std::endl;

  double surfaceArea = c.getSurfaceArea();
  std::cout << "Surface Area: " << surfaceArea << std::endl;

  return 0;
}

```

- uiuc::Cube c; 

  - There are so may Cubes. 
  - We will be specific about our Cube and specify that our Cube is within the uiuc namespace. 
  - Cube.h 에서 클래스를 namespace로 감싸면 됨. cpp 파일에서도 똑같음. 

  ```c++
  /**
   * Simple C++ class for representing a Cube.
   * 
   * @author
   *   Wade Fagen-Ulmschneider <waf@illinois.edu>
   */
  
  #include "Cube.h"
  
  namespace uiuc {
    double Cube::getVolume() {
      return length_ * length_ * length_;
    }
  
    double Cube::getSurfaceArea() {
      return 6 * length_ * length_;
    }
  
    void Cube::setLength(double length) {
      length_ = length;
    }
  }
  
  ```

  

# Week 2

## 2.1 Stack Memory and Pointers

- A Variable has four things 
  - name
  - type
  - value
  - location in memory ('memory address')
- A variable's memory address
  - & returns the memory address of a variable

cpp-memory/addressOf.cpp

```c++
/**
 * C++ program using the & operator to find the address of a variable in memory.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

int main() {
  int num = 7;

  std::cout << "Value: "   <<  num << std::endl;
  std::cout << "Address: " << &num << std::endl;

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-memory % ./addressOf
Value: 7
Address: 0x7ffeedf0c908
*/
```

- &num : num 변수의 address. address는 stack 메모리에 저장됨 
- Stack Memory
  - default memory for all C++ variables. 
  - associated with the current function. Lifecycle of this memory = lifecycle of the function. 
  - function이 return 하기전까지 function 내에 있는 variable은 스택메모리에 있음. 
  - start from highest spot of the meory and grows down toward zero. 

cpp-memory/foo.cpp

```c++
/**
 * C++ program printing memory addresses of variables across two functions.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

void foo() {
  int x = 42;
  std::cout << " x in foo(): " <<  x << std::endl;
  std::cout << "&x in foo(): " << &x << std::endl;
}

int main() {
  int num = 7;
  std::cout << " num in main(): "   <<  num << std::endl;
  std::cout << "&num in main(): " << &num << std::endl;

  foo();

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-memory % ./foo
 num in main(): 7
&num in main(): 0x7ffeea166928
 x in foo(): 42
&x in foo(): 0x7ffeea1668fc
*/
```

- main 내에서 num이 정의된 후, main 함수가 끝나지 않은채로 foo 함수를 호출해보자. 
- 스택 메모리는 가장 높은 메모리 주소에서 시작해서 밑으로 내려가므로 num 변수는 foo의 x 변수의 주소값보다 높을것. 메인이 아직 안끝났으니까 스택엔 num 변수의 주소가 남아있음. 9가 8보다 높음. 



- Pointer : a variable that stores the memory address of the data 

- int * p = &num 

- dereference operator : 

  - we want the content of the pointer. 

  - '*' 를 선언할때 붙이면 포인터 변수로서 주소를 저장하지만, *p = 42 이런식으로 변수앞에 붙여서 사용하면 dereference the memory address and get the actual value. 

  - ```c++
    int num = 7;
    int * p = &num; // p엔 num의 주소값 저장 
    int value_in_num = *p; // value_in_num 이라는 새 변수에 p 주소가 가리키는 값인 7 저장
    *p = 42; // p 주소가 가리키는 값에 42를 저장 
    ```

cpp-memory/puzzle.cpp

```c++
/**
 * C++ code showing improper use of memory (returning a reference to a stack variable).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

double someOtherFunction();  // Forward decl

#include <iostream>
#include "Cube.h"
using uiuc::Cube;

Cube *CreateUnitCube() {
  Cube cube;
  cube.setLength(15);
  return &cube;
}

int main() {
  Cube *c = CreateUnitCube();
  someOtherFunction();
  double a = c->getSurfaceArea();
  std::cout << "Surface Area: " << a << std::endl;
  double v = c->getVolume();
  std::cout << "Volume: " << v << std::endl;
  return 0;
}


// Some other function that does something that uses some stack memory.
// In this code, we calculate the total volume of cubes of length from 0..99.
double someOtherFunction() {
  Cube cubes[100];
  double totalVolume = 0;

  for (int i = 0; i < 100; i++) {
    cubes[i].setLength(i);
    totalVolume += cubes[i].getVolume();
  }

  return totalVolume;
}
```

- main을 위해 할당된 main stack에서 Cube *c  = CreateUnitCube() 함수가 작동되며 메모리가 할당되기 시작 
- Cube cube, cube.setLength(15)를 작동 후 cube의 주소를 리턴. 
- 그렇게 Cube *c의 c는 Cube의 메모리 주소를 가리키게됨. 

![LeenaKim-1507277](/assets/img/post_img/LeenaKim-1507277.png)

- CreateUnitCube() 에서 return &cube를 해버리고나면 함수가 끝나기때문에 주황색 영역에 대한 할당이 사라지고 다른 호출되는 함수의 메모리공간으로 사용됨. 

```c++
linakim@Linaui-MacBookPro cpp-memory % ./puzzle  
Surface Area: 0
Volume: 0
```

- surface area와 volume이 0으로 나온걸 볼 수 있음. foo()의 함수가 끝났기때문에 메모리 할당이 해제되고, 다른 함수로 overwritten되어 해당 변수는 0으로 초기화됨. 
- 주황색부분은 이어 호출된 someOtherFunction() 이 할당되게됨. 
- because we returned a value from am function as the function runs.
- :star:never return a reference to a local variable. 



cpp-memory/main.cpp

```c++
/**
 * C++ program printing various memory values with references and pointers.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

int main() {
  int num = 7;
  std::cout << " num: " <<  num << std::endl;
  std::cout << "&num: " << &num << std::endl;

  int *p = &num;
  std::cout << " p: " <<  p << std::endl;
  std::cout << "&p: " << &p << std::endl;
  std::cout << "*p: " << *p << std::endl;

  *p = 42;
  std::cout << "*p changed to 42" << std::endl; 
  std::cout << " num: " <<  num << std::endl;

  return 0;
}

/*
linakim@Linaui-MacBookPro cpp-memory % ./main
 num: 7
&num: 0x7ffee61f2918
 p: 0x7ffee61f2918
&p: 0x7ffee61f2910
*p: 7
*p changed to 42
 num: 42
 */
```

- p : num의 메모리주소 
- &p : num의 메모리주소보다 조금 더 작은 주소를 가진 메모리주소 
- *p : num의 값이므로 7
- *p = 42 로 num의 값을 42로 변경 



## 2.2 Heap Memory

- heap memory

  - for longer than the lifecycle of the function
  - 'new' keyword 

- what C++'s New Operator does

  - allocate memory on the heap for the data structure

  - initialize the data structure

  - return a pointer to the start of the data structure

    The memory is only ever reclaimed by the system when the pointer is passed to the 'delete' operator

- ex) int * numPtr = new int;
  - Stack 영역에 저장되는 numPtr
  - numPtr의 value에 new int가 할당되면서 heap메모리에 할당되고, stack의 numPtr은 heap의 int를 가리키게 됨. 이 heap 메모리영역은 우리가 delete 하지 않는이상 프로그램 내내 살아있음. 

cpp-heapMemory/main.cpp

```c++
/**
 * C++ program printing various memory values using heap-allocated memory.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

int main() {
  int *numPtr = new int;

  std::cout << "*numPtr: " << *numPtr << std::endl; // 값 자체를 할당한건 아니라서 뭐가나올지 모름 
  std::cout << " numPtr: " <<  numPtr << std::endl; // address of heap memory
  std::cout << "&numPtr: " << &numPtr << std::endl; // address of stack memory 

  *numPtr = 42; // set 42 to heap memory 
  std::cout << "*numPtr assigned 42." << std::endl;

  std::cout << "*numPtr: " << *numPtr << std::endl;
  std::cout << " numPtr: " <<  numPtr << std::endl;
  std::cout << "&numPtr: " << &numPtr << std::endl;

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-heapMemory % ./main
*numPtr: 0
 numPtr: 0x7fc3fa401760
&numPtr: 0x7ffee6ba2910
*numPtr assigned 42.
*numPtr: 42
 numPtr: 0x7fc3fa401760
&numPtr: 0x7ffee6ba2910
*/
```

- heap memory grows from low memory to high memory (<-> stack memory)
- that's why numPtr is smaller than &numPtr



cpp-heapMemory/heap1.cpp

```c++
/**
 * C++ program allocating and free'ing heap memory.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
using uiuc::Cube;

int main() {
  int *p = new int;
  Cube *c = new Cube;

  *p = 42;
  (*c).setLength(4);

  delete c;  c = nullptr;
  delete p;  p = nullptr;
  return 0;
}

```



  ![LeenaKim-1513122](/assets/img/post_img/LeenaKim-1513122.png)



- delete를 통해 heap 메모리는 할당해제했지만, stack에 남아있는 포인터 메모리들은 어떡할까?

- nullptr

  - a pointer that points to the memory address 0X0
  - represents a pointer to "nowhere"
  - address 0X0 is reserved and never used by the system
  - address 0X0 will always generate an "segmentation fault" when accessed
  - calls to delete 0X0 are ignored

- as soon as delete c, c is nullptr because it doens't point anything. 

- Remember that after the line "delete c;" the pointer c still stores the address of the deleted variable, which is no longer valid to dereference and is therefore dangerous. The pointer won't be automatically set to nullptr. Then, you should *manually* set c to nullptr if you want to better protect against coding mistakes:

  delete c;

  c = nullptr;

- (*c) : 현실에선 잘 안씀. 대신, arrow Operator을 씀. 

- Arrow Operator (->)

  - When an object is stored via a pointer, access can be made to member functions using the -> operation.
  - c->getVolume() : (*c) 처럼 dereference 후 .를 이용해 접근하는것보다, 바로 c로 dereference 하고 member function을 사용할 수 있게함 

cpp-heapMemory/heap2.cpp

```c++
/**
 * C++ program allocating and double-freeing (!!) memory.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
using uiuc::Cube;

int main() {
  Cube *c1 = new Cube;
  Cube *c2 = c1;

  c2->setLength( 10 );

  delete c2;
  delete c1;  // !!

  return 0;
}

```

- c1과 c2 모두 같은 heap의 new Cube를 가리키게 됨
- delete c2 이후에 c1을 delete 하려고 봤더니 같은걸 가리키고있었기때문에 c2로 인해 이미 지워져서 에러가 나게됨. 



## 2.3 Heap Memory Puzzles

cpp-heapPuzzles/puzzle1.cpp

```c++
#include <iostream>

using std::cout;
using std::endl;

int main() {
  int  i =  2,  j =  4,  k =  8;
  int *p = &i, *q = &j, *r = &k;

  k = i;
  cout << i << j << k << *p << *q << *r << endl; // 2 4 2 2 4 2

  p = q;
  cout << i << j << k << *p << *q << *r << endl; // 2 4 2 4 4 2 

  *q = *r;
  cout << i << j << k << *p << *q << *r << endl; // 2 2 2 2 2 2 

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-heapPuzzles % ./puzzle1
242242
242442
222222
*/
```

- new 키워드가 없기때문에 모든 변수는 stack에 저장. 



cpp-heapPuzzles/puzzle2.cpp

```c++
/**
 * C++ puzzle program.  Try to figure out the result before running!
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  int *x = new int;
  int &y = *x;
  y = 4;

  cout << &x << endl; // 0xffff4567 (stack)
  cout << x << endl; // 0x12345 (heap)
  cout << *x << endl; // 4

  cout << &y << endl; // 0x12345 (heap)
  cout << y << endl; // 4
  //cout << *y << endl; // can't do that. error. because it's not a pointer, we cannot dereference a non pointer.

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-heapPuzzles % ./puzzle2
0x7ffee612d900
0x7febb7401760
4
0x7febb7401760
4
*/
```

- stack : x -> heap: new int 
- int &y : reference variable. Allows us to give a name to a piece of memory. so y is going to alias the dereference value of x. So 'new int' memory can be called y. 
- y = 4 => y가 *x 였으므로 heap의 new int 공간의 value가 4가 됨 



cpp-heapPuzzles/puzzle3.cpp

```c++
/**
 * C++ puzzle program.  Try to figure out the result before running!
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  int *p, *q;
  p = new int;
  q = p;
  *q = 8;
  cout << *p << endl;

  q = new int;
  *q = 9;
  cout << *p << endl;
  cout << *q << endl;

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-heapPuzzles % ./puzzle3
8
8
9
*/
```



cpp-heapPuzzles/puzzle4.cpp

```c++
/**
 * C++ puzzle program.  Try to figure out the result before running!
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  int *x;
  int size = 3;
  x = new int[size];

  for (int i = 0; i < size; i++) {
    x[i] = i + 3;
  }

  delete[] x; // 배열을 지울땐 delete[] 
}

```



## Readings

- **.h** files are "header files". These usually have definitions of objects and declarations of global functions. Recently, some people name header files with a ".hpp" suffix instead.

- **.cpp** files are often called the "implementation files," or simply the "source files". This is where most function definitions and main program logic go.
- Instructions beginning with **#** are special commands for the compiler, called preprocessor directives. This instruction prevents the header file from being automatically included multiple times in a complex project, which would cause errors.
- Notice that the first thing it does is **#include "Cube.h"** to include all the text from the Cube.h file in the same directory. Because the filename is specified in quotes, as "Cube.h", the compiler expects it to be in the same directory as the current file, Cube.cpp. 
- When you write **#include <iostream>**, the compiler will look for the **iostream** header file in a system-wide library path that is located outside of your current directory.
- Next, it does **#include "Cube.h"** just like in the Cube.cpp file. You have to include the necessary headers in every cpp file where they are needed. However, you shouldn't use #include to literally include one cpp file in another! **There is no need to write #include "Cube.cpp"** because the function definitions in the Cube.cpp file will be compiled separately and then *linked* to the code from the main.cpp file.



# Week 3

- If there's no constructor, there's default constructor with the default value of member variables.
- Custom Default Constructor
  - overriding automatic default constructor to customize, specify the state of the object 
  - conditions for constructor
    - function name is same name as class itself
    - zero parameters
    - no return type 



## 3.1 Class Constructors

cpp-ctor/ex1/Cube.h

```c++
/**
 * Simple C++ class for representing a Cube (with a custom constructor).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#pragma once

namespace uiuc {
  class Cube {
    public:
      Cube();  // Custom default constructor

      double getVolume();
      double getSurfaceArea();
      void setLength(double length);

    private:
      double length_;
  };
}

```

- Cube(); : 커스텀 디폴트 생성자 선언



Cpp-ctor/ex1/Cube.cpp

```c++
/**
 * Simple C++ class for representing a Cube (with a custom constructor).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"

namespace uiuc {
  Cube::Cube() { // Cube 클래스의 Cube 생성자 
    length_ = 1;
  }

  double Cube::getVolume() {
    return length_ * length_ * length_;
  }

  double Cube::getSurfaceArea() {
    return 6 * length_ * length_;
  }

  void Cube::setLength(double length) {
    length_ = length;
  }
}

```

- define custom default constructor



cpp-ctor/ex1/main.cpp

```c++
/**
 * C++ program using the Cube's custom default constructor.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
#include <iostream>

int main() {
  uiuc::Cube c;
  std::cout << "Volume: " << c.getVolume() << std::endl;
  return 0;
}
```



- Custom Constuctors : with parameters / default Custom Constructor : no parameters

cpp-ctor/ex2/Cube.h

```c++
/**
 * Simple C++ class for representing a Cube (with constructors).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#pragma once

namespace uiuc {
  class Cube {
    public:
      Cube();  // Custom default constructor
      Cube(double length);  // One argument constructor

      double getVolume();
      double getSurfaceArea();
      void setLength(double length);

    private:
      double length_;
  };
}

```

cpp-ctor/ex2/Cube.cpp

```c++
/**
 * Simple C++ class for representing a Cube (with constructors).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"

namespace uiuc {
  Cube::Cube() {
    length_ = 1;
  }

  Cube::Cube(double length) {
    length_ = length;
  }
}

```

cpp-ctor/ex2/main.cpp

```c++
/**
 * C++ program using the Cube's one arugment constructor.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
#include <iostream>

int main() {
  uiuc::Cube c(2);
  std::cout << "Volume: " << c.getVolume() << std::endl;
  return 0;
}
```

- uiuc::Cube c(2) : call custom constructor



- Automatic Default Constructor : automatically provided by C++. 커스텀 생성자가 하나라도 있으면 오토매틱 디폴트 생성자는 생기지 않음.

cpp-ctor/ex3/Cube.h

```c++
/**
 * Simple C++ class for representing a Cube (custom constructor, no default).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#pragma once

namespace uiuc {
  class Cube {
    public:
      // No default constructor
      Cube(double length);  // One argument constructor

      double getVolume();
      double getSurfaceArea();
      void setLength(double length);

    private:
      double length_;
  };
}

```

cpp-ctor/ex3/main.cpp

```c++
/**
 * C++ program using the Cube's one arugment constructor.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
#include <iostream>

int main() {
  uiuc::Cube c;  // !!!
  std::cout << "Volume: " << c.getVolume() << std::endl;
  return 0;
}
```

- Cube(double length) 가 유일한 생성자. 그럼 there's no automatic default constructor. 

- 그런데 main에선 uiuc::Cube c; 에서 디폴트 생성자를 호출하고있다. 

- 어떻게 될까? => 에러남. 

  ```
  main.cpp:12:14: fatal error: no matching constructor for initialization of
        'uiuc::Cube'
    uiuc::Cube c;  // !!!
               ^
  ./Cube.h:14:7: note: candidate constructor not viable: requires single argument
        'length', but no arguments were provided
        Cube(double length);  // One argument constructor
        ^
  ./Cube.h:11:9: note: candidate constructor (the implicit copy constructor) not
        viable: requires 1 argument, but 0 were provided
    class Cube {
          ^
  ./Cube.h:11:9: note: candidate constructor (the implicit move constructor) not
        viable: requires 1 argument, but 0 were provided
  1 error generated.
  ```

  

## 3.2 Copy Constructors

- Automatic Copy Constructor
  - If we do not provide a custom copy constructor, the C++ compiler provides an automatic copy constructor 
  - it will copy the contents of all member variables
- Custom Copy Constructor
  - a class constructor
  - has exactly one argument (the argument must be const reference of the same type as the class)
  - ex) Cube::Cube(const Cube &obj)



- Copy Constructor Invocation
  - Often, copy constructors are invoked automatically: (자동으로 copy constructor가 호출되는 세 가지 경우)
    - passing an object as a parameter (by value)
    - returning an object from a function (by value)
    - initializing a new object

cpp-cctor/Cube.cpp

```c++
/**
 * Simple C++ class for representing a Cube (with constructors).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
#include <iostream>

namespace uiuc {
  Cube::Cube() {
    length_ = 1;
    std::cout << "Default constructor invoked!" << std::endl;
  }

  // custom copy constructor
  Cube::Cube(const Cube & obj) {
    length_ = obj.length_;
    std::cout << "Copy constructor invoked!" << std::endl;
  }
  ...
}
```

- 아래의 여러 main 들에서 default constructor 과 copy constructor가 호출되는 순서를 보기 위함 



cpp-cctor/ex1/main.cpp

```c++
/**
 * C++ program copying a Cube class.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "../Cube.h"
using uiuc::Cube;

void foo(Cube cube) {
  // Nothing :)
}

int main() {
  Cube c; // default constructor
  foo(c); // call copy constructor (1st case)

  return 0;
}
/*
linakim@Linaui-MacBookPro ex1 % ./main
Default constructor invoked!
Copy constructor invoked!
*/
```



cpp-cctor/ex2/main.cpp

```c++
/**
 * C++ program copying a Cube class.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "../Cube.h"
using uiuc::Cube;

Cube foo() {
  Cube c;
  return c;
}

int main() {
  Cube c2 = foo();
  return 0;
}
/*
linakim@Linaui-MacBookPro ex2 % ./main
Default constructor invoked!
Copy constructor invoked!
Copy constructor invoked!
*/
```

- 호출 순서 :
  - Foo() 의 Cube c 로 인해 default constructor 호출 
  - return c 가 main으로 가져와지며 copy constructor 호출 
  - 리턴값이 c2에 저장되며 다시 copy constructor 호출 



cpp--cctor/ex3/main.cpp

```c++
/**
 * C++ program copying a Cube class. 
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "../Cube.h"
using uiuc::Cube;

int main() {
  Cube c; // default constructor
  Cube myCube = c; // copy constructor

  return 0;
}
/*
linakim@Linaui-MacBookPro ex3 % ./main
Default constructor invoked!
Copy constructor invoked!
*/
```



cpp-cctor/ex4/main.cpp

```c++
/**
 * C++ program copying a Cube class. 
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "../Cube.h"
using uiuc::Cube;

int main() {
  Cube c; // default constructor
  Cube myCube; // default constructor

  myCube = c; // nothing

  return 0;
}
/*
linakim@Linaui-MacBookPro ex4 % ./main
Default constructor invoked!
Default constructor invoked!
*/
```

- myCube = c 에서 copy constructor가 호출될거라고 생각하지만, 여기선 어떠한 constructor도 호출되지 않는다. myCube나 c나 모두 이미 constructed 됬기때문. A constructor's job is to actually create the object itself, and not just copy things between two existing objects. 



## 3.3 Copy Assignment Operator

- In C++, a copy assignment operator defines the behavior when an object is copied using the assignment operator =.
- Copy Constructor vs. Assignment
  - A copy constructor creates a new object (constructor).
  - An assignment operator assigns a value to an existing object. 
  - An assignment operator is always called on an object that has already been constructed.
- Automatic Assignment Operator
  - if an assignment operator is not provided, the C++ compiler provides an automatic assignment operator. 
  - The automatic assignment operator will copy the contents of all member variables.
- Custom Assignment Operator
  - Is a public member function of the class
  - Has the function name operator=
  - Has a return value of a reference of the class' type
  - Has exactly one argument
    - The argument must be const reference of the class' type
  - ex) Cube & Cube::operator=(const Cube & obj)
  - goal of custom assignment operator : to assign the contents in object to the instance of the class that's being called upon. 위의 예에선, &obj의 값을 &Cube에 할당하는것이 goal. 



cpp-assignmentOp/Cube.cpp

```c++
/**
 * Simple C++ class for representing a Cube (with constructors).
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
#include <iostream>

namespace uiuc {
  Cube::Cube() {
    length_ = 1;
    std::cout << "Default constructor invoked!" << std::endl;
  }

  Cube::Cube(const Cube & obj) {
    length_ = obj.length_;
    std::cout << "Copy constructor invoked!" << std::endl;
  }

  Cube & Cube::operator=(const Cube & obj) {
    length_ = obj.length_;
    std::cout << "Assignment operator invoked!" << std::endl;    
    return *this; // this : instance of the class itself
  }
  ...
}

```



cpp-assignmentOp/Cube.cpp

```c++
/**
 * C++ program invoking Cube's assignment operator.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"
using uiuc::Cube;

int main() {
  Cube c; // default constructor
  Cube myCube; // default constructor

  myCube = c; // assignment operator 

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-assignmentOp % ./main
Default constructor invoked!
Default constructor invoked!
Assignment operator invoked!
*/
```

- copy constructor vs assignment operator
  - both copy the content of the class from one to another
  - assignment operator : no need to instruct



## 3.4 Variable Storage

- In C++, an instance of a variable can be stored **directly in memory, accessed by pointer, or accessed by reference.** 
- Direct Storage
  - By default, variables are stored directly in memory.
    - The type of a variable has no modifiers.
    - The object takes up exactly its size in memory. 
- Storage by Pointer
  - The type of a variable is modified with an asterisk (*).
  - A pointer takes a "memory address width" of memory (ex: 64 bits on a 64-bit system).
  - The pointer "points" to the allocated space of the object.
- Storage by Reference 
  - A reference is an alias to existing memory and is denoted in the type with an ampersand (&)
  - A reference does not store memory itself, it is only an alias to another variable.
  - The alias must be assigned when the variable is initialized.
  - ex) 
    - Cube &c = cube; 					// Alias to the variable 'cube'
    - int &i = count;                         // Alias to the variable 'i'
    - Uiuc::HSLAPixel &p;               // Illegal! Must alias something <u>at the moment when variable is initialized.</u>
    - i 를 바꾸든, count를 바꾸든 같은걸 바꾸는것. 
- Example: Cube Currency 



cpp-memory2/Cube.cpp

```c++
#include "Cube.h"
#include <iostream>

namespace uiuc {  
  Cube::Cube(double length) {
    length_ = length;
    std::cout << "Created $" << getVolume() << std::endl;
  }

  Cube::Cube(const Cube & obj) {
    length_ = obj.length_;
    std::cout << "Created $" << getVolume() << " via copy" << std::endl;
  }

  Cube & Cube::operator=(const Cube & obj) {
    std::cout << "Transformed $" << getVolume() << "-> $" << obj.getVolume() << std::endl;
    length_ = obj.length_;
    return *this;
  }
	...
}

```

- 첫번째 생성자 호출시 : create some amount of money 
- 두번째 copy constructor 호출시 : no create a new cube, but just an alias cube 
  - 첫번째, 두번째 다 돈을 만듦.
- 세번째 assignment operator 호출시 : transforms an instance from one value to another value. Change value of the old cube. 



cpp-memory2/ex1/byValue.cpp

```c++
#include "../Cube.h"
using uiuc::Cube;

int main() {
  // Create a 1,000-valued cube
  Cube c(10);

  // Transfer the cube
  Cube myCube = c; // copy constructor called 

  return 0;
}
/*
linakim@Linaui-MacBookPro ex1 % ./byValue
Created $1000
Created $1000 via copy
*/
```

- copy by value case
- 큐브 두개를 갖게됨. $2000 



cpp-memory2/ex1/byRef.cpp

```c++
#include "../Cube.h"
using uiuc::Cube;

int main() {
  // Create a 1,000-valued cube
  Cube c(10);

  // Transfer the cube
  Cube & myCube = c;

  return 0;
}
/*
linakim@Linaui-MacBookPro ex1 % ./byRef
Created $1000
*/
```

- myCube becomes an alias of C
- my Cube is going to be this cube as well as C is also going to be this cube.
- Because we're simply creating an alias of existing memory and not creating a new memory, we expect for the cube to construct exactly once and nothing else to happen



cpp-memory2/ex1/byPointer.cpp

```c++
#include "../Cube.h"
using uiuc::Cube;

int main() {
  // Create a 1,000-valued cube
  Cube c(10);

  // Transfer the cube
  Cube * myCube = &c;

  return 0;
}
/*
linakim@Linaui-MacBookPro ex1 % ./byPointer
Created $1000
*/
```

- myCube now is a pointer that points to c. 
- two variables point exactly same cube 
- only create one cube.



- Pass by _____________________________
  - identical to storage, arguments can be passed to functions in three different ways:
    - pass by value (default)
    - pass by pointer (modified with *)
    - pass by reference (modified with &, acts as an alias)



Cpp-memory2/ex2/byValue.cpp

```c++
#include "../Cube.h"
using uiuc::Cube;

bool sendCube(Cube c) {    
  // ... logic to send a Cube somewhere ...
  return true;
}

int main() {
  // Create a 1,000-valued cube
  Cube c(10);

  // Send the cube to someone via copy 
  sendCube(c);

  return 0;
}
/*
linakim@Linaui-MacBookPro ex2 % ./byValue
Created $1000
Created $1000 via copy
*/
```



cpp-memory2/ex2/byRef.cpp

```c++
#include "../Cube.h"
#include <iostream>

using uiuc::Cube;

bool sendCube(Cube & c) {    
  // ... logic to send a Cube somewhere ...
  return true;
}

int main() {
  // Create a 1,000-valued cube
  Cube c(10);

  // Send the cube to someone by reference
  sendCube(c);

  return 0;
}
/*
linakim@Linaui-MacBookPro ex2 % ./byRef
Created $1000
*/
```

- sending the variable 'c' by reference (&)
- we aren't copying this variable anywhere, just sending an alias of this variable because no copies are made, we expect a cube to only ever have been constructed once and only $1,000 should ever be created



Cpp-memory2/ex2/byPointer.cpp

```c++
#include "../Cube.h"
#include <iostream>

using uiuc::Cube;

bool sendCube(Cube * c) {    
  // ... logic to send a Cube somewhere ...
  return true;
}

int main() {
  // Create a 1,000-valued cube
  Cube c(10);

  // Send the cube to someone
  sendCube(&c);

  return 0;
}
/*
linakim@Linaui-MacBookPro ex2 % ./byPointer
Created $1000
*/
```

- only creates $1,000 cube once 



- Return by ___________________________
  - Similarly, values can be returned all three ways as well:
    - Return by value (default)
    - Return by pointer (modified with *)
    - Return by reference (modified with &, acts as an alias)
      - Never return a reference to a stack variable created on the stack of your current function!



## 3.5 Class Destructor

- Automatic Default Destructor 
  - An automatic default destructor is added to your class if no other destructor is defined
  - The only action of the automatic default destructor is to call the default destructor of all member objects.
  - An destructor should never be called directly. Instead, it is automatically called when the object's memory is being reclaimed by the syustem.
    - object in **stack** : when the function returns
    - object in **heap** : when `delete` is used

- Custom Destructor
  - To add custom behavior to the end-of-life of the function, a custom destructor can be defined as:
    - A custom destructor is a member function
    - The function's destructor is the name of the class, preceded by a tilde ~.
    - All destuctors have zero arguments and no return type
    - ex) Cube::~Cube();



cpp-dtor/Cube.cpp

```c++
#include "Cube.h"
#include <iostream>

using std::cout;
using std::endl;

namespace uiuc {  
  Cube::Cube() {
    length_ = 1;
    cout << "Created $1 (default)" << endl;
  }

  Cube::Cube(double length) {
    length_ = length;
    cout << "Created $" << getVolume() << endl;
  }

  Cube::Cube(const Cube & obj) {
    length_ = obj.length_;
    cout << "Created $" << getVolume() << " via copy" << endl;
  }

  Cube::~Cube() {
    cout << "Destroyed $" << getVolume() << endl;
  }

  Cube & Cube::operator=(const Cube & obj) {
    cout << "Transformed $" << getVolume() << "-> $" << obj.getVolume() << endl;
    length_ = obj.length_;
    return *this;
  }
  ...
}

```



cpp-dtor/main.cpp

```c++
#include "Cube.h"
using uiuc::Cube;

double cube_on_stack() {
  Cube c(3);
  return c.getVolume(); // stack 영역은 return 되며 destroy 됨
}

void cube_on_heap() {
  Cube * c1 = new Cube(10);
  Cube * c2 = new Cube;
  delete c1; // 힙 영역은 delete 하지 않으면 자동으로 지워지지 않으므로 c2는 안지워짐 
}

int main() {
  cube_on_stack();
  cube_on_heap();
  cube_on_stack();
  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-dtor % ./main
Created $27
Destroyed $27
Created $1000
Created $1 (default)
Destroyed $1000
Created $27
Destroyed $27
*/
```



- Custom Destructor
  - A custom destructor is essential when an object allocates an external resource that must be closed or freed when the object is destroyed. Examples:
    - Heap memory
    - Open files
    - Shared memory



# Week 4

## 4.1 Template Types

- A template type is a special type that can take on different types when the type is initialized. std::vector uses a template type:
  - std::vector<char>
  - std::vector<int>
  - std::vector<uiuc::Cube>
- std::vector 
  - standard library class that provides the functionality of a dynamically growing array with a "templated" type. Key ideas:
    - Define in : #include <vector>
    - Initialization : std::vector<T> v;
    - Add to (back) of array: ::push_back(T);
    - Access specific element: ::operator[](unsigned pos);
    - Number of elements: ::size()
- Template Type
  - when initializing a "templated" type, the template type goes inside of <>



Cpp-vector/ex1/main.cpp

```c++
#include <vector>
#include <iostream>

int main() {
  std::vector<int> v;
  v.push_back( 2 );
  v.push_back( 3 );
  v.push_back( 5 );

  std::cout << v[0] << std::endl; // 2
  std::cout << v[1] << std::endl; // 3
  std::cout << v[2] << std::endl; // 5

  return 0;
}

```





Cpp-vector/ex2/main.cpp

```c++
#include <vector>
#include <iostream>

int main() {
  std::vector<int> v;
  for (int i = 0; i < 100; i++) {
    v.push_back( i * i );
  }

  std::cout << v[12] << std::endl;

  return 0;
}

```



## 4.2 Tower of Hanoi - Introduction



cpp-tower/uiuc/Cube.h

```c++
#pragma once

#include "HSLAPixel.h"

namespace uiuc {
  class Cube {
    public:
      Cube(double length, HSLAPixel color);

      double getLength() const;
      void setLength(double length);

      double getVolume() const;
      double getSurfaceArea() const;

    private:
      double length_;
      HSLAPixel color_;
  };
}

```

- add ''color' 



- Building the Stack Class
  - A single stack must contain:
    - An vector of cubes
    - Operations to interact with the top of the stack 



cpp-tower/Stack.h

```c++
#pragma once

#include <vector>
#include "uiuc/Cube.h"
using uiuc::Cube;

class Stack {
  public:
    void push_back(const Cube & cube);
    Cube removeTop(); // remove the cube on top (return Cube by value)
    Cube & peekTop(); // get the cube on top 
    unsigned size() const;

    // An overloaded operator<<, allowing us to print the stack via `cout<<`:
    friend std::ostream& operator<<(std::ostream & os, const Stack & stack);

  private:
    std::vector<Cube> cubes_;
};

```

- `ostream` : java의 toString() 과 비슷 
  - ostream 이 첫번째 파라미터, 출력하고자하는 객체 형이 두번째 매개변수 



- Building the Tower of Hanoi Game
  - Finally, the game is built from the components we have already built:
    - An array of three stacks
    - The initial state has four cubes in the first stack



cpp-tower/Game.h

```c++
#pragma once

#include "Stack.h"
#include <vector>

class Game {
  public:
    Game();
    void solve();

    // An overloaded operator<<, allowing us to print the stack via `cout<<`:
    friend std::ostream& operator<<(std::ostream & os, const Game & game);

  private:
    std::vector<Stack> stacks_;
};
```





cpp-tower/Game.cpp

```c++

#include "Game.h"
#include "Stack.h"
#include "uiuc/Cube.h"
#include "uiuc/HSLAPixel.h"

#include <iostream>
using std::cout;
using std::endl;

// Solves the Tower of Hanoi puzzle.
// (Feel free to call "helper functions" to help you solve the puzzle.)
void Game::solve() {
  // Prints out the state of the game:
  cout << *this << endl;

  // @TODO -- Finish solving the game!
}

// Default constructor to create the initial state:
Game::Game() {
  // Create the three empty stacks:
  for (int i = 0; i < 3; i++) {
    Stack stackOfCubes;
    stacks_.push_back( stackOfCubes );
  }

  // make initial state
  // Create the four cubes, placing each on the [0]th stack:
  Cube blue(4, uiuc::HSLAPixel::BLUE);
  stacks_[0].push_back(blue);

  Cube orange(3, uiuc::HSLAPixel::ORANGE);
  stacks_[0].push_back(orange);

  Cube purple(2, uiuc::HSLAPixel::PURPLE);
  stacks_[0].push_back(purple);

  Cube yellow(1, uiuc::HSLAPixel::YELLOW);
  stacks_[0].push_back(yellow);
}

std::ostream& operator<<(std::ostream & os, const Game & game) {
  for (unsigned i = 0; i < game.stacks_.size(); i++) {
    os << "Stack[" << i << "]: " << game.stacks_[i];
  }
  return os;
}

```



cpp-tower/main.cpp

```c++

#include "Game.h"
#include <iostream>

int main() {
  Game g;

  std::cout << "Initial game state: " << std::endl;
  std::cout << g << std::endl;

  g.solve();

  std::cout << "Final game state: " << std::endl;
  std::cout << g << std::endl;

  return 0;
}
/*
linakim@Linaui-MacBookPro cpp-tower % ./main
Initial game state: 
Stack[0]: 4 3 2 1 
Stack[1]: 
Stack[2]: 

Stack[0]: 4 3 2 1 
Stack[1]: 
Stack[2]: 

Final game state: 
Stack[0]: 4 3 2 1 
Stack[1]: 
Stack[2]: 
*/
```



## 4.3 Tower of Hanoi - Solution 1

Cpp-tower-solution/Game.cpp

```c++
#include "Game.h"
#include "Stack.h"
#include "uiuc/Cube.h"
#include "uiuc/HSLAPixel.h"

#include <iostream>
using std::cout;
using std::endl;

// Game default constructor
Game::Game() {
  // The initial default game state has three stacks four cubes.
  
  // Create the three empty stacks:
  for (int i = 0; i < 3; i++) {
    Stack stackOfCubes;
    stacks_.push_back( stackOfCubes );
  }

  // Create the four cubes, placing each on the [0]th stack:
  // - A blue cube of length=4, on the bottom
  // - A orange cube of length=3, on top of the blue cube
  // - A purple cube of length=2, on top of the orange cube
  // - A yellow cube of length=1 at the very top
  Cube blue(4, uiuc::HSLAPixel::BLUE);
  stacks_[0].push_back(blue);

  Cube orange(3, uiuc::HSLAPixel::ORANGE);
  stacks_[0].push_back(orange);

  Cube purple(2, uiuc::HSLAPixel::PURPLE);
  stacks_[0].push_back(purple);

  Cube yellow(1, uiuc::HSLAPixel::YELLOW);
  stacks_[0].push_back(yellow);
}

void Game::_move(unsigned index1, unsigned index2) {
  // index1에 있는 큐브를 제거하여 index2에 넣음 
  Cube cube = stacks_[index1].removeTop();
  stacks_[index2].push_back(cube);
}


void Game::_legalMove(unsigned index1, unsigned index2) {
  // 한 스택에 큐브가 없고 다른 스택에만 큐브가 있을경우 
  if (stacks_[index1].size() == 0 && stacks_[index2].size() > 0) {
    _move(index2, index1);
  // 위와 반대의 경우 
  } else if (stacks_[index1].size() > 0 && stacks_[index2].size() == 0) {
    _move(index1, index2);
  // 둘 다 큐브가 있을경우 
  } else if (stacks_[index1].size() > 0 && stacks_[index2].size() > 0) {
    // 두 스택의 가장 위에 있는 큐브의 길이를 비교하여 가능한 방법으로 위치를 바꿈
    if (stacks_[index1].peekTop().getLength() < stacks_[index2].peekTop().getLength() ) {
      _move(index1, index2);
    } else {
      _move(index2, index1);
    }
  }
  
  cout << *this << endl;
}

// 마지막 stack 에 큐브가 4개가 될때까지 같은 패턴을 반복 
void Game::solve() {
  while (stacks_[2].size() != 4) {
    _legalMove(0, 1); // stack 0 <-> stack 1
    _legalMove(0, 2); // stack 0 <-> stack 2
    _legalMove(1, 2); // stack 1 <-> stack 2
  }
}

std::ostream& operator<<(std::ostream & os, const Game & game) {
  for (unsigned i = 0; i < game.stacks_.size(); i++) {
    os << "Stack[" << i << "]: " << game.stacks_[i];
  }
  return os;
}

```



main의 결과 

```c++
linakim@Linaui-MacBookPro cpp-tower-solution % ./main
Initial game state: 
Stack[0]: 4 3 2 1 
Stack[1]: 
Stack[2]: 

Stack[0]: 4 3 2 
Stack[1]: 1 
Stack[2]: 

Stack[0]: 4 3 
Stack[1]: 1 
Stack[2]: 2 

Stack[0]: 4 3 
Stack[1]: 
Stack[2]: 2 1 

Stack[0]: 4 
Stack[1]: 3 
Stack[2]: 2 1 

Stack[0]: 4 1 
Stack[1]: 3 
Stack[2]: 2 

Stack[0]: 4 1 
Stack[1]: 3 2 
Stack[2]: 

Stack[0]: 4 
Stack[1]: 3 2 1 
Stack[2]: 

Stack[0]: 
Stack[1]: 3 2 1 
Stack[2]: 4 

Stack[0]: 
Stack[1]: 3 2 
Stack[2]: 4 1 

Stack[0]: 2 
Stack[1]: 3 
Stack[2]: 4 1 

Stack[0]: 2 1 
Stack[1]: 3 
Stack[2]: 4 

Stack[0]: 2 1 
Stack[1]: 
Stack[2]: 4 3 

Stack[0]: 2 
Stack[1]: 1 
Stack[2]: 4 3 

Stack[0]: 
Stack[1]: 1 
Stack[2]: 4 3 2 

Stack[0]: 
Stack[1]: 
Stack[2]: 4 3 2 1 

Final game state: 
Stack[0]: 
Stack[1]: 
Stack[2]: 4 3 2 1 

```



## 4.4 Tower of Hanoi - Solution 2

Cpp-tower-solution2/Game.cpp

```c++
#include "Game.h"
#include "Stack.h"
#include "uiuc/Cube.h"
#include "uiuc/HSLAPixel.h"

#include <iostream>
using std::cout;
using std::endl;

// Game default constructor
Game::Game() {
  // The initial default game state has three stacks four cubes.
  
  // Create the three empty stacks:
  for (int i = 0; i < 3; i++) {
    Stack stackOfCubes;
    stacks_.push_back( stackOfCubes );
  }

  // Create the four cubes, placing each on the [0]th stack:
  // - A blue cube of length=4, on the bottom
  // - A orange cube of length=3, on top of the blue cube
  // - A purple cube of length=2, on top of the orange cube
  // - A yellow cube of length=1 at the very top
  Cube blue(4, uiuc::HSLAPixel::BLUE);
  stacks_[0].push_back(blue);

  Cube orange(3, uiuc::HSLAPixel::ORANGE);
  stacks_[0].push_back(orange);

  Cube purple(2, uiuc::HSLAPixel::PURPLE);
  stacks_[0].push_back(purple);

  Cube yellow(1, uiuc::HSLAPixel::YELLOW);
  stacks_[0].push_back(yellow);
}

// Move a Cube from Stack `s1` to Stack `s2`:
void Game::_moveCube(Stack & s1, Stack & s2) {
  Cube cube = s1.removeTop();
  s2.push_back(cube);
}

// Move the cubes in the range [start...end] from `source` to `target`, using spare as a spare spot:
void Game::_move(
  unsigned start, unsigned end,
  Stack & source, Stack & target, Stack & spare,
  unsigned depth
) {
  cout << "Planning (depth=" << depth++ << "): Move [" << start << ".." << end << "] from Stack@" << &source << " -> Stack@" << &target << ", Spare@" << &spare << "]" << endl;

  // Check if we are only moving one cube:
  if (start == end) {
    // If so, move it directly:
    _moveCube( source, target );
    cout << *this << endl;
  } else {
    // Otherwise, use our move strategy:
    _move(start + 1, end  , source, spare , target, depth);
    _move(start    , start, source, target, spare , depth);
    _move(start + 1, end  , spare , target, source, depth);
  }
}

void Game::solve() {
  _move(
    0, stacks_[0].size() - 1,  //< Move the entire set of cubes, [0 .. size-1]
    stacks_[0], //< Source stack is [0]
    stacks_[2], //< Target stack is [2]
    stacks_[1], //< Spare stack is [1]
    0   //< Initial depth (for printouts only) is 0
  );
}

std::ostream& operator<<(std::ostream & os, const Game & game) {
  for (unsigned i = 0; i < game.stacks_.size(); i++) {
    os << "Stack[" << i << ", " << &game.stacks_[i] << "]: " << game.stacks_[i] << endl;
  }
  return os;
}

```

- 재귀함수 이용 



## 4.5 Templates and Classes

- Templated Functions

  - A template variable is defined by declaring it before the beginning of a class or function

  ```c++
  template <typename T>
  class List {
    private:
    	T data_;
  }
  ```

- Compile-Time Binding

  - Templated variables are checked at compile time, which allows for errors to be caught before running the program



cpp-templates/main.cpp

```c++

#include <iostream>
#include <string>
using std::cout;
using std::endl;

#include "Cube.h"
using uiuc::Cube;

// We'll call this my_max to avoid conflicts with the "max" in the
// standard libraries.
template <typename T>
T my_max(T a, T b) {
  if (a > b) { return a; }
  return b;
}

int main() {
  cout << "my_max(3, 5): " << my_max(3, 5) << endl;
  cout << "my_max('a', 'd'): " << my_max('a', 'd') << endl;
  
  // Here we construct std::string objects from the literal strings in
  // quotation marks, because the std::string object already implements
  // the ">" operator to do alphabetical ordering. A plain string literal
  // is an array of const char, which wouldn't support that correctly.
  // (Instead, it would just compare the addresses of the arrays.)
  cout << "my_max(std::string(\"Hello\"), std::string(\"World\")): "
       << my_max(std::string("Hello"), std::string("World")) << endl;

  // You need to finish implementing the ">" operator for Cube to get the
  // next line to work!
  // cout << "my_max( Cube(3), Cube(6) ): " << my_max( Cube(3), Cube(6) ) << endl;

  return 0;
}

```

- cube는 어느게 더 큰지 알 수 없으므로 컴파일 안됨. 
- template 를 활용해 함수에 다양한 자료형이 올 수 있게함 



## 4.6 Inheritance

- Generic to Specialized
  - A base class is a generic form of a specialized, derived class



Cpp-inheritance/Shape.h

```c++
#pragma once

class Shape {
  public:
    Shape();
    Shape(double width);
    double getWidth() const;

  private:
    double width_;
};

```



Cpp-inheritance/Cube.h

```c++
#pragma once

#include "Shape.h"
#include "HSLAPixel.h"

namespace uiuc {
  // 항상 public 
  class Cube : public Shape {
    public:
      Cube(double width, uiuc::HSLAPixel color);
      double getVolume() const;

    private:
      uiuc::HSLAPixel color_;
  };
}
```



- Initialization
  - When a derived class is initialized, the derived class must construct the base class:
    - Cube must construct Shape
    - By default, uses default constructor
    - Custom constructor can be used with an initialization list



Cpp-inheritance/Cube.cpp

```c++

#include "Cube.h"
#include "Shape.h"

namespace uiuc {
  Cube::Cube(double width, uiuc::HSLAPixel color) : Shape(width) {
    color_ = color;
  }

  double Cube::getVolume() const {
    // Cannot access Shape::width_ due to it being `private`
    // ...instead we use the public Shape::getWidth(), a public function

    return getWidth() * getWidth() * getWidth();
  }
}
```

- Cube 객체가 만들어질때 Shape 객체도 만들어지도록 
- width 는 cube가 아니라 shape의 private 변수이므로 직접 접근이 불가해 `getWidth()` 로 접근 



- Access Control
  - When a base class is inherited, the derived class 
    - can access all public
    - can not access to private 
- Initializer List
  - The syntax to initialize the base class is called the initializer list and can be used for several purposes:
    - initialize a base class
    - initialize the current class using another constructor
    - initialize the default values of member variables



cpp-inheritance/Shape.cpp

```c++
#include "Shape.h"

Shape::Shape() : Shape(1) {
  // Nothing
}

Shape::Shape(double width) : width_(width){
  // Nothing
}

double Shape::getWidth() const {
  return width_;
}
```

