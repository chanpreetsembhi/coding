
```cpp
#include<iostream>  
using namespace std;  
  
class item {  
    static int count;  
    int number = 0;  
  
public:  
    void getData(const int a) {  
        number = a;  
        count++;  
    };  
  
    static void getCount() {  
        cout << "count: ";  
        cout << count << "\n";  
    };  
};  
  
int item::count;  
  
int main() {  
    item a, b, c;  
    item::getCount();  
    item::getCount();  
    item::getCount();  
  
    a.getData(100);  
    b.getData(200);  
    c.getData(300);  
  
    cout << "After reading data" << "\n";  
  
    item::getCount();  
    item::getCount();  
    item::getCount();  
  
    return 0;  
}
```