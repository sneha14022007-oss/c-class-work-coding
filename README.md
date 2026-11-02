1.WRITE A PROGRAM TO CHECK NUMBERS PALINDROME AND STRING PALINDROME?
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    // Check number palindrome
    int num, original, reversed = 0, digit;

    cout << "Enter a number: ";
    cin >> num;

    original = num;
    int temp = num;

    if (num < 0) {
        cout << num << " is not a number palindrome." << endl;
    } else {
        while (temp > 0) {
            digit = temp % 10;
            reversed = reversed * 10 + digit;
            temp = temp / 10;
        }

        if (original == reversed)
            cout << original << " is a number palindrome." << endl;
        else
            cout << original << " is not a number palindrome." << endl;
    }

    // Check string palindrome
    string str, rev;

    cout << "\nEnter a string: ";
    cin >> str;

    rev = str;
    reverse(rev.begin(), rev.end());

    if (str == rev)
        cout << str << " is a string palindrome." << endl;
    else
        cout << str << " is not a string palindrome." << endl;

    return 0;
}
2. WRITE A PROGRAM TO SHOW THE EFFECT OF CALL BY VALUE AND CALL BY REFERENCE IN FUNCTION

#include <iostream>
using namespace std;

// Call by Value
void callByValue(int x) {
    x = x + 10;
    cout << "Inside Call by Value: " << x << endl;
}

// Call by Reference
void callByReference(int &x) {
    x = x + 10;
    cout << "Inside Call by Reference: " << x << endl;
}

int main() {
    int a = 5, b = 5;

    cout << "Before Call by Value: " << a << endl;
    callByValue(a);
    cout << "After Call by Value: " << a << endl;

    cout << endl;

    cout << "Before Call by Reference: " << b << endl;
    callByReference(b);
    cout << "After Call by Reference: " << b << endl;

    return 0;
}
3 .WRITE A PROGRAM TO PREFORM FOLLOWING OPERATIONS ON MATRIX USING FUNCTION AND SWITCH CASE a) ADDITION b) substraction c) multiply d) transpose

#include <iostream>
using namespace std;

const int MAX = 10;

void readMatrix(int a[MAX][MAX], int r, int c) {
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            cin >> a[i][j];
        }
    }
}

void displayMatrix(int a[MAX][MAX], int r, int c) {
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            cout << a[i][j] << "\t";
        }
        cout << endl;
    }
}

void addMatrix(int a[MAX][MAX], int b[MAX][MAX],
               int r, int c) {
    int result[MAX][MAX];

    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            result[i][j] = a[i][j] + b[i][j];
        }
    }

    cout << "Addition of matrices:\n";
    displayMatrix(result, r, c);
}

void subtractMatrix(int a[MAX][MAX], int b[MAX][MAX],
                    int r, int c) {
    int result[MAX][MAX];

    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            result[i][j] = a[i][j] - b[i][j];
        }
    }

    cout << "Subtraction of matrices:\n";
    displayMatrix(result, r, c);
}

void multiplyMatrix(int a[MAX][MAX], int b[MAX][MAX],
                    int r1, int c1, int c2) {
    int result[MAX][MAX] = {};

    for (int i = 0; i < r1; i++) {
        for (int j = 0; j < c2; j++) {
            for (int k = 0; k < c1; k++) {
                result[i][j] += a[i][k] * b[k][j];
            }
        }
    }

    cout << "Multiplication of matrices:\n";
    displayMatrix(result, r1, c2);
}

void transposeMatrix(int a[MAX][MAX], int r, int c) {
    int result[MAX][MAX];

    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            result[j][i] = a[i][j];
        }
    }

    cout << "Transpose of matrix:\n";
    displayMatrix(result, c, r);
}

int main() {
    int a[MAX][MAX], b[MAX][MAX];
    int r1, c1, r2, c2, choice;

    do {
        cout << "\n--- MATRIX OPERATIONS ---\n";
        cout << "1. Addition\n";
        cout << "2. Subtraction\n";
        cout << "3. Multiplication\n";
        cout << "4. Transpose\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
        case 2:
            cout << "Enter rows and columns of matrices: ";
            cin >> r1 >> c1;

            if (r1 <= 0 || c1 <= 0 ||
                r1 > MAX || c1 > MAX) {
                cout << "Invalid matrix size.\n";
                break;
            }

            cout << "Enter elements of first matrix:\n";
            readMatrix(a, r1, c1);

            cout << "Enter elements of second matrix:\n";
            readMatrix(b, r1, c1);

            if (choice == 1)
                addMatrix(a, b, r1, c1);
            else
                subtractMatrix(a, b, r1, c1);
            break;

        case 3:
            cout << "Enter rows and columns of first matrix: ";
            cin >> r1 >> c1;

            cout << "Enter rows and columns of second matrix: ";
            cin >> r2 >> c2;

            if (r1 <= 0 || c1 <= 0 || r2 <= 0 || c2 <= 0 ||
                r1 > MAX || c1 > MAX ||
                r2 > MAX || c2 > MAX) {
                cout << "Invalid matrix size.\n";
                break;
            }

            if (c1 != r2) {
                cout << "Multiplication is not possible.\n";
                break;
            }

            cout << "Enter elements of first matrix:\n";
            readMatrix(a, r1, c1);

            cout << "Enter elements of second matrix:\n";
            readMatrix(b, r2, c2);

            multiplyMatrix(a, b, r1, c1, c2);
            break;

        case 4:
            cout << "Enter rows and columns of matrix: ";
            cin >> r1 >> c1;

            if (r1 <= 0 || c1 <= 0 ||
                r1 > MAX || c1 > MAX) {
                cout << "Invalid matrix size.\n";
                break;
            }

            cout << "Enter elements of matrix:\n";
            readMatrix(a, r1, c1);

            transposeMatrix(a, r1, c1);
            break;

        case 5:
            cout << "Exiting program.\n";
            break;

        default:
            cout << "Invalid choice. Try again.\n";
        }

    } while (choice != 5);

    return 0;
}
4. DEFINE A CLASS SHAPE WHOSE ATTRIBUTES ARE RADIUS LENGTH AND WIDTH CALCULATE THE PERIMETER OF THE RECTANGLE AND CIRCLE USE CONSTRUCTOE AND DESTRUCTOR

#include <iostream>
using namespace std;

class Shape {
private:
    float radius, length, width;

public:
    // Constructor
    Shape(float r, float l, float w) {
        radius = r;
        length = l;
        width = w;
        cout << "Constructor called." << endl;
    }

    // Calculate perimeter of circle
    float circlePerimeter() {
        return 2 * 3.14 * radius;
    }

    // Calculate perimeter of rectangle
    float rectanglePerimeter() {
        return 2 * (length + width);
    }

    // Display results
    void display() {
        cout << "Perimeter of Circle: "
             << circlePerimeter() << endl;

        cout << "Perimeter of Rectangle: "
             << rectanglePerimeter() << endl;
    }

    // Destructor
    ~Shape() {
        cout << "Destructor called." << endl;
    }
};

int main() {
    float r, l, w;

    cout << "Enter radius of circle: ";
    cin >> r;

    cout << "Enter length of rectangle: ";
    cin >> l;

    cout << "Enter width of rectangle: ";
    cin >> w;

    Shape s(r, l, w);

    s.display();

    return 0;
}
5. Create a class Person which includes: character array name of size 64, age in numeric, character array address of size 64, and total salary in real numbers
(divide salary in different components, if required). Make an array of objects of class Person of size 10.
(a) Write inline function that obtains the youngest and eldest age of a person from a class person using arrays.
(b) Write a program to develop the salary slip and display result by using constructors.
#include <iostream>
#include <cstring>
using namespace std;

class Person
{
    char name[64];
    int age;
    char address[64];
    float salary;

public:
    void getData()
    {
        cout << "Enter name: ";
        cin >> name;

        cout << "Enter age: ";
        cin >> age;

        cout << "Enter address: ";
        cin >> address;

        cout << "Enter salary: ";
        cin >> salary;
    }

    int getAge()
    {
        return age;
    }

    // Inline function to find youngest age
    inline int youngest(Person p[], int n)
    {
        int min = p[0].age;

        for (int i = 1; i < n; i++)
        {
            if (p[i].age < min)
                min = p[i].age;
        }

        return min;
    }

    // Inline function to find eldest age
    inline int eldest(Person p[], int n)
    {
        int max = p[0].age;

        for (int i = 1; i < n; i++)
        {
            if (p[i].age > max)
                max = p[i].age;
        }

        return max;
    }
};

int main()
{
    Person p[10];

    for (int i = 0; i < 10; i++)
    {
        cout << "\nEnter details of Person " << i + 1 << endl;
        p[i].getData();
    }

    cout << "\nYoungest Age = " << p[0].youngest(p, 10);
    cout << "\nEldest Age = " << p[0].eldest(p, 10);

    return 0;
}
(b) C++ program to generate salary slip using constructors
In this program, salary is divided into different components:

Basic Salary = 50% of total salary

HRA = 20% of basic salary

DA = 10% of basic salary

TA = 5% of basic salary

Gross Salary = Basic + HRA + DA + TA


cpp
#include <iostream>
#include <cstring>
using namespace std;

class Person
{
    char name[64];
    int age;
    char address[64];

    float basic, hra, da, ta, gross;

public:

    // Parameterized constructor
    Person(char n[], int a, char addr[], float salary)
    {
        strcpy(name, n);
        age = a;
        strcpy(address, addr);

        basic = salary * 0.50;
        hra = basic * 0.20;
        da = basic * 0.10;
        ta = basic * 0.05;

        gross = basic + hra + da + ta;
    }

    void display()
    {
        cout << "\n========== SALARY SLIP ==========";
        cout << "\nName          : " << name;
        cout << "\nAge           : " << age;
        cout << "\nAddress       : " << address;

        cout << "\n---------------------------------";
        cout << "\nBasic Salary  : " << basic;
        cout << "\nHRA           : " << hra;
        cout << "\nDA            : " << da;
        cout << "\nTA            : " << ta;

        cout << "\n---------------------------------";
        cout << "\nGross Salary  : " << gross;
        cout << "\n=================================";
    }
};

int main()
{
    char name[64], address[64];
    int age;
    float salary;

    cout << "Enter Name: ";
    cin >> name;

    cout << "Enter Age: ";
    cin >> age;

    cout << "Enter Address: ";
    cin >> address;

    cout << "Enter Total Salary: ";
    cin >> salary;

    // Creating object using constructor
    Person p(name, age, address, salary);

    // Display salary slip
    p.display();

    return 0;
}
7. Write a program to find the area (function name AREA) of circle, rectangle and triangle by Function overloading concept.

#include <iostream>
using namespace std;

class Shape
{
public:

    // Area of circle
    float AREA(float r)
    {
        return 3.14 * r * r;
    }

    // Area of rectangle
    float AREA(float l, float b)
    {
        return l * b;
    }

    // Area of triangle
    float AREA(float b, float h, int)
    {
        return 0.5 * b * h;
    }
};

int main()
{
    Shape s;
    float r, l, b, h;

    // Circle
    cout << "Enter radius of circle: ";
    cin >> r;
    cout << "Area of Circle = " << s.AREA(r);

    // Rectangle
    cout << "\n\nEnter length and breadth of rectangle: ";
    cin >> l >> b;
    cout << "Area of Rectangle = " << s.AREA(l, b);

    // Triangle
    cout << "\n\nEnter base and height of triangle: ";
    cin >> b >> h;
    cout << "Area of Triangle = " << s.AREA(b, h, 0);

    return 0;
}

8. Design three classes: Student, Exam and Result. The student class has data members such as roll no, name etc. Create a class Exain by inheriting the Student class. The Exam class adds data members representing the marks scored in six subjects. Derive the Result from class Exam and it has its own members such as total marks. Write an interactive program to model this relationship. What type of inheritance this model belongs to?

#include <iostream>
using namespace std;

// Base class
class Student
{
protected:
    int rollno;
    char name[50];

public:
    void getStudent()
    {
        cout << "Enter Roll Number: ";
        cin >> rollno;

        cout << "Enter Student Name: ";
        cin >> name;
    }

    void displayStudent()
    {
        cout << "\nRoll Number: " << rollno;
        cout << "\nStudent Name: " << name;
    }
};

// Derived class from Student
class Exam : public Student
{
protected:
    int marks[6];

public:
    void getMarks()
    {
        cout << "\nEnter marks of six subjects:\n";

        for(int i = 0; i < 6; i++)
        {
            cout << "Subject " << i + 1 << ": ";
            cin >> marks[i];
        }
    }

    void displayMarks()
    {
        cout << "\nMarks Obtained:\n";

        for(int i = 0; i < 6; i++)
        {
            cout << "Subject " << i + 1
                 << ": " << marks[i] << endl;
        }
    }
};

// Derived class from Exam
class Result : public Exam
{
    int total;
    float percentage;

public:
    void calculate()
    {
        total = 0;

        for(int i = 0; i < 6; i++)
        {
            total = total + marks[i];
        }

        percentage = total / 6.0;
    }

    void displayResult()
    {
        displayStudent();
        displayMarks();

        cout << "\nTotal Marks: " << total;
        cout << "\nPercentage: " << percentage << "%";

        if(percentage >= 40)
            cout << "\nResult: PASS";
        else
            cout << "\nResult: FAIL";
    }
};

int main()
{
    Result r;

    r.getStudent();
    r.getMarks();

    r.calculate();

    cout << "\n\n========== STUDENT RESULT ==========\n";

    r.displayResult();

    return 0;
}
9. Write a program to swap two numbers (create two classes) by using Friend function.

#include <iostream>
using namespace std;

class B;

class A
{
    int x;

public:
    void getData()
    {
        cout << "Enter first number: ";
        cin >> x;
    }

    friend void swap(A &, B &);
};

class B
{
    int y;

public:
    void getData()
    {
        cout << "Enter second number: ";
        cin >> y;
    }

    friend void swap(A &, B &);
};

// Friend function
void swap(A &a, B &b)
{
    int temp;

    temp = a.x;
    a.x = b.y;
    b.y = temp;
}

int main()
{
    A obj1;
    B obj2;

    obj1.getData();
    obj2.getData();

    cout << "\nBefore Swapping:";
    cout << "\nFirst Number = " << obj1.x;
    cout << "\nSecond Number = " << obj2.y;

    swap(obj1, obj2);

    cout << "\n\nAfter Swapping:";
    cout << "\nFirst Number = " << obj1.x;
    cout << "\nSecond Number = " << obj2.y;

    return 0;
}
10. Consider an example of book shop which sells books and video tapes. These two classes are inherited from base class called media. The media class has command data members such as title and publication. The book class has data members for storing number of pages in a book and tape class has playing time in a tape. Each class will have member functions such as read() and show (). In the base class, these members have to be defined as virtual functions. Write a program to models the class hierarchy for book shop and processes objects of these classes using pointers to base class. Write the rules of virtual functions

#include <iostream>
using namespace std;

// Base class
class Media
{
protected:
    char title[50];
    char publication[50];

public:
    virtual void read()
    {
        cout << "Enter title: ";
        cin >> title;

        cout << "Enter publication: ";
        cin >> publication;
    }

    virtual void show()
    {
        cout << "\nTitle: " << title;
        cout << "\nPublication: " << publication;
    }

    virtual ~Media() {}
};

// Derived class Book
class Book : public Media
{
    int pages;

public:
    void read()
    {
        Media::read();

        cout << "Enter number of pages: ";
        cin >> pages;
    }

    void show()
    {
        Media::show();

        cout << "\nNumber of Pages: " << pages;
    }
};

// Derived class Tape
class Tape : public Media
{
    float time;

public:
    void read()
    {
        Media::read();

        cout << "Enter playing time (in minutes): ";
        cin >> time;
    }

    void show()
    {
        Media::show();

        cout << "\nPlaying Time: " << time << " minutes";
    }
};

int main()
{
    Media *ptr;
    Book b;
    Tape t;

    cout << "\nEnter Book Details:\n";
    ptr = &b;
    ptr->read();

    cout << "\nEnter Tape Details:\n";
    ptr = &t;
    ptr->read();

    cout << "\n\n========== BOOK DETAILS ==========";
    ptr = &b;
    ptr->show();

    cout << "\n\n========== TAPE DETAILS ==========";
    ptr = &t;
    ptr->show();

    return 0;
}
11. Write a program to calculate the total mark of a student using the concept of virtual base class.

#include <iostream>
using namespace std;

// Base class
class Student
{
protected:
    int rollno;
    char name[50];

public:
    void getStudent()
    {
        cout << "Enter Roll Number: ";
        cin >> rollno;

        cout << "Enter Student Name: ";
        cin >> name;
    }

    void displayStudent()
    {
        cout << "\nRoll Number: " << rollno;
        cout << "\nName: " << name;
    }
};

// Virtual base class inheritance
class Test : virtual public Student
{
protected:
    int m1, m2, m3;

public:
    void getMarks()
    {
        cout << "\nEnter marks of three subjects:\n";
        cin >> m1 >> m2 >> m3;
    }
};

class Sports : virtual public Student
{
protected:
    int sportsMarks;

public:
    void getSportsMarks()
    {
        cout << "Enter Sports Marks: ";
        cin >> sportsMarks;
    }
};

// Derived class
class Result : public Test, public Sports
{
    int total;

public:
    void calculate()
    {
        total = m1 + m2 + m3 + sportsMarks;
    }

    void display()
    {
        displayStudent();

        cout << "\nMarks in Subject 1: " << m1;
        cout << "\nMarks in Subject 2: " << m2;
        cout << "\nMarks in Subject 3: " << m3;
        cout << "\nSports Marks: " << sportsMarks;

        cout << "\nTotal Marks: " << total;
    }
};

int main()
{
    Result r;

    r.getStudent();
    r.getMarks();
    r.getSportsMarks();

    r.calculate();

    cout << "\n\n========== STUDENT RESULT ==========\n";

    r.display();

    return 0;
}
