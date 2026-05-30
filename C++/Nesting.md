```cpp
#include<iostream>  
#include<iomanip>  
using namespace std;  
  
class Array {  
    int list[100] = {}, i = 0, max = 0, size = 0;  
  
public:  
    void input(int);  
    void output();  
    void largest();  
};  
  
void Array::input(int n) {  
    size = n;  
    cout << "Enter number of elements: " << endl;  
    for (i = 0; i < size; i++) {  
        cin >> list[i];  
    }  
}  
  
void Array::output() {  
    cout << endl << "Entered elements of array are: " << endl;  
    for (i = 0; i < size; i++) {  
        cout << setw(5) << list[i];  
    }  
    largest();  
    cout << endl << "The largest element of the array is: " << max;  
}  
  
void Array::largest() {  
    max = list[0];  
    for (i = 0; i < size; i++) {  
        if (list[i] > max) {  
            max = list[i];  
        }  
    }  
}  
  
int main() {  
    Array obj;  
    int no;  
    cout << "Enter no. of elements of the array" << endl;  
    cin >> no;  
    obj.input(no);  
    obj.output();  
};
```