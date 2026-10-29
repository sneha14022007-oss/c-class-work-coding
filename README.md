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


