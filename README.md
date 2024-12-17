[# 2d-arrays practice. ](https://www.programiz.com/online-compiler/0jRmRCKPnvTzQ)

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

// Function to allocate memory for 2D array
int** createArray(int n, int m) {
    int** arr = new int*[n];
    for (int i = 0; i < n; i++) {
        arr[i] = new int[m];
    }
    return arr;
}

// Function to deallocate memory
void deleteArray(int** arr, int n) {
    for (int i = 0; i < n; i++) {
        delete[] arr[i];
    }
    delete[] arr;
}

// Function for manual array filling
void manualFill(int** arr, int n, int m) {
    cout << "Enter array elements:" << endl;
    for (int i = 0; i < n; i++) {
        cout << "Row " << i + 1 << ":" << endl;
        for (int j = 0; j < m; j++) {
            cout << "Element [" << i << "][" << j << "]: ";
            cin >> arr[i][j];
        }
    }
}

// Function for automatic array filling
void automaticFill(int** arr, int n, int m, int min, int max) {
    srand(time(0));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            arr[i][j] = min + rand() % (max - min + 1);
        }
    }
}

// Function to print array
void printArray(int** arr, int n, int m) {
    cout << "\nArray contents:" << endl;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

// Function to count rows without positive elements
int countRowsWithoutPositive(int** arr, int n, int m) {
    int count = 0;
    for (int i = 0; i < n; i++) {
        bool hasPositive = false;
        for (int j = 0; j < m; j++) {
            if (arr[i][j] > 0) {
                hasPositive = true;
                break;
            }
        }
        if (!hasPositive) {
            count++;
        }
    }
    return count;
}

int main() {
    int n, m, choice;
    
    // Get array dimensions
    cout << "Enter number of rows (n): ";
    cin >> n;
    cout << "Enter number of columns (m): ";
    cin >> m;
    
    // Create dynamic array
    int** arr = createArray(n, m);
    
    // Menu for filling method
    cout << "\nSelect filling method:" << endl;
    cout << "1. Manual filling" << endl;
    cout << "2. Automatic filling" << endl;
    cout << "Enter your choice (1 or 2): ";
    cin >> choice;
    
    if (choice == 1) {
        manualFill(arr, n, m);
    }
    else if (choice == 2) {
        int min, max;
        cout << "Enter minimum value for random range: ";
        cin >> min;
        cout << "Enter maximum value for random range: ";
        cin >> max;
        automaticFill(arr, n, m, min, max);
    }
    else {
        cout << "Invalid choice!" << endl;
        deleteArray(arr, n);
        return 1;
    }
    
    // Print array
    printArray(arr, n, m);
    
    // Count and display rows without positive elements
    int result = countRowsWithoutPositive(arr, n, m);
    cout << "\nNumber of rows without positive elements: " << result << endl;
    
    // Clean up
    deleteArray(arr, n);
    return 0;
}
