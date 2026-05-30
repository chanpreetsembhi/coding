#### Old Method

```c++
#include<iostream>  
using namespace std;  
  
int main() {  
    int *a;  
    int *b;  
    int *c;

	a = new int;
	b = new int;
	c = new int;
  
    *a = 10;  
    *b = 20;  
    *c = *a + *b;  
  
    cout << "Sum of " << *a << " and " << *b << " is " << *c;  
  
    // Free allocated memory  
    delete a;  
    delete b;  
    delete c;  
}
```

#### New Method

```c++
#include<iostream>  
using namespace std;  
  
int main() {  
    const auto a = new int;  
    const auto b = new int;  
    const auto c = new int;  
  
    *a = 10;  
    *b = 20;  
    *c = *a + *b;  
  
    cout << "Sum of " << *a << " and " << *b << " is " << *c;  
  
    // Free allocated memory  
    delete a;  
    delete b;  
    delete c;  
}
```