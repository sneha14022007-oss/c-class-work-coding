WRITE A PROGRAM TO CHECK NUMBERS PALINDROME AND STRING PALINDROME?
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
2. WRITE A PROG
