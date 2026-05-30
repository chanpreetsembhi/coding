#### In C Language.

```c
#include<stdio.h>  
  
struct Student {  
    int roll_no, marks;  
    float percentage;  
};  
  
void main() {  
    struct Student s;  
    s.roll_no = 100;  
    s.marks = 400;  
    s.percentage = ((float)s.marks * 100.0f) / 500;  
    printf("Your Roll No = %d\n", s.roll_no);  
    printf("Your Marks = %d\n", s.marks);  
    printf("Your percent = %f", s.percentage);  
}
```

--------------------------------------------------------------------------
#### In C++ Language

```cpp
#include<iostream>  
using namespace std;  
  
struct student {  
    int roll_no, marks;  
    float percentage;  
};  
  
int main() {  
    // struct student s1 = {100, 400, 0.0f};  
    // or   
    student s1{};  
    s1.roll_no = 100;  
    s1.marks = 400;  
    s1.percentage = (static_cast<float>(s1.marks) / 500) * 100;  
    cout << "Your Roll NO = " << s1.roll_no << endl;  
    cout << "Your Marks = " << s1.marks << endl;  
    cout << "Your percent = " << s1.percentage << endl;  
}
```


