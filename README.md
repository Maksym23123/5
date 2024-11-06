#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>

using namespace std;

// Функція для відображення матриці
void displayMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) {
        for (int element : row) {
            cout << element << "\t";
        }
        cout << endl;
    }
}

// Завдання 1: Модифікація квадратної матриці
void task1(int size) {
    vector<vector<int>> matrix(size, vector<int>(size));
    
    // Ініціалізація матриці випадковими значеннями
    srand(time(0));
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            matrix[i][j] = rand() % 10;
        }
    }

    cout << "Початкова матриця:\n";
    displayMatrix(matrix);

    // Модифікація матриці за правилами діагоналі
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            if (i == j) {
                matrix[i][j] = 0;        // Головна діагональ: замінити на 0
            } else if (i < j) {
                matrix[i][j] = 50;       // Вище головної діагоналі: замінити на 50
            } else {
                matrix[i][j] = 100;      // Нижче головної діагоналі: замінити на 100
            }
        }
    }

    cout << "\nМодифікована матриця:\n";
    displayMatrix(matrix);
}

// Перевірка, чи можна множити дві матриці
bool canMultiply(const vector<vector<int>>& A, const vector<vector<int>>& B) {
    return A[0].size() == B.size();
}

// Функція для множення матриць
vector<vector<int>> multiplyMatrices(const vector<vector<int>>& A, const vector<vector<int>>& B) {
    int rows = A.size();
    int cols = B[0].size();
    int commonDim = B.size();
    vector<vector<int>> result(rows, vector<int>(cols, 0));

    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            for (int k = 0; k < commonDim; ++k) {
                result[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    return result;
}

// Завдання 2: Множення двох матриць
void task2(int rowsA, int colsA, int rowsB, int colsB) {
    vector<vector<int>> A(rowsA, vector<int>(colsA));
    vector<vector<int>> B(rowsB, vector<int>(colsB));

    srand(time(0));

    // Заповнення матриць A та B випадковими значеннями
    for (int i = 0; i < rowsA; ++i)
        for (int j = 0; j < colsA; ++j)
            A[i][j] = rand() % 10;

    for (int i = 0; i < rowsB; ++i)
        for (int j = 0; j < colsB; ++j)
            B[i][j] = rand() % 10;

    cout << "Матриця A:\n";
    displayMatrix(A);

    cout << "\nМатриця B:\n";
    displayMatrix(B);

    if (canMultiply(A, B)) {
        cout << "\nРезультат множення A * B:\n";
        vector<vector<int>> result = multiplyMatrices(A, B);
        displayMatrix(result);
    } else {
        cout << "\nМатриці неможливо перемножити (некомпатибельні розміри).\n";
    }
}

int main() {
    int choice;
    cout << "Оберіть завдання (1 для модифікації діагоналі, 2 для множення матриць): ";
    cin >> choice;

    if (choice == 1) {
        int size;
        cout << "Введіть розмір матриці: ";
        cin >> size;
        task1(size);
    } else if (choice == 2) {
        int rowsA, colsA, rowsB, colsB;
        cout << "Введіть кількість рядків і стовпців для матриці A: ";
        cin >> rowsA >> colsA;
        cout << "Введіть кількість рядків і стовпців для матриці B: ";
        cin >> rowsB >> colsB;
        task2(rowsA, colsA, rowsB, colsB);
    } else {
        cout << "Невірний вибір.\n";
    }

    return 0;
}
