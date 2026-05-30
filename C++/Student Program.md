
```c++
#include<iostream>  
using namespace std;  
  
class Student{  
int roll_no = 0, marks = 0;  
float percentage = 0;  
  
public:  
void getData(){  
cout<<"Enter roll number: ";  
cin>>roll_no;  
cout<<"Enter marks (out of 500): ";  
cin>>marks;  
}  
  
void putData(){  
percentage=static_cast<float>(marks)*100/500;  
cout<<"Roll No: "<<roll_no << endl;  
cout<<"Marks: "<<marks <<endl;  
cout<<"Percentage: "<<percentage << "%";  
}  
};  
  
int main(){  
Student s1;  
cout<<"Enter the detail of student:- " << endl;  
s1.getData();  
s1.putData();  
}
```