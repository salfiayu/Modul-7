
# <h1 align="center">Laporan Praktikum Struktur Data<br> Modul 7 Stack </h1>
<p align="center">Salfi Ayu Ramadhani / 103112430224</p>

## Dasar Teori

Stack adalah struktur data linear yang bekerja dengan prinsip LIFO (Last In, First Out), yaitu elemen yang terakhir dimasukkan akan menjadi yang pertama dikeluarkan. Stack memiliki satu titik akses bernama TOP, sehingga operasi dasarnya hanya dilakukan dari satu sisi, yaitu push menambahkan elemen ke TOP, pop mengambil dan menghapus elemen dari TOP, serta peek/top melihat elemen paling atas tanpa menghapus. Stack dapat diimplementasikan menggunakan array maupun linked list, dan umumnya digunakan dalam mekanisme undo/redo, call stack pada pemanggilan fungsi, serta pengecekan pasangan tanda kurung pada ekspresi.

## Guided

### Soal 1

```cpp
 #include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;
}
void push (Node *&top, int data)
{
    Node *newNode = new Node();
    newNode-> data = data;
    newNode-> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }
    int poppedData = top-> data;
    Node *temp = top;
    top = top-> next;

    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
{
    cout << "Stack Kosong." << endl;
    return;
}
cout << "TOP ->";
Node *temp = top;

while (temp != nullptr)
{
    cout << temp-> data << " ->";
    temp = temp-> next;
}
cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push (stack, 10);
    push (stack, 20);
    push (stack, 30);

    cout << "Menampilkan isi stack: " << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack: " << endl;
    show(stack);

    return 0;
}

```

> Screenshoot 
> ![Screenshot Soal 1](https://github.com/salfiayu/Modul-6/blob/main/Modul%206/Screenshoot/Screenshot%20(125).png)

Program ini membuat struktur data stack menggunakan linked list, di mana push() menambahkan data ke bagian atas stack, pop() mengambil dan menghapus data teratas, dan show() menampilkan seluruh isi stack dari atas ke bawah; pada fungsi main, program menambahkan data 10, 20, dan 30 ke stack, menampilkannya, kemudian melakukan pop satu elemen dan menampilkan sisa isi stack.

---

## Unguided

### Soal 1 (stack.h)

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “stack.h”
Buatlah implementasi ADT Stack menggunakan Array pada file “stack.cpp” dan “main.cpp”

```cpp
#ifndef STACK_H
#define STACK_H

#define MAX 20
using namespace std;

typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif

```

> Screenshoot  
> ![Screenshot Soal 1](https://github.com/salfiayu/Modul-6/blob/main/Modul%206/Screenshoot/Screenshot%20(127).png)

Header file STACK_H ini berfungsi untuk mendefinisikan struktur dan fungsi-fungsi Stack agar bisa digunakan di file C++ lain misalnya main.cpp dan stack.cpp.

---

### Soal 2 (Stack.cpp)

Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)

```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    }
    return -1;
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top != -1) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);
    while (S.top != -1 && S.info[S.top] > x) {
        push(temp, pop(S));
    }
    push(S, x);
    while (temp.top != -1) {
        push(S, pop(temp));
    }


```

> Sreenshoot 
> ![Screenshot Soal 2](https://github.com/salfiayu/Modul-6/blob/main/Modul%206/Screenshoot/Screenshot%20(128).png)

File ini mengimplementasikan operasi stack seperti membuat stack, push, pop, menampilkan isi, membalik isi stack, dan push dengan urutan ascending menggunakan array dan stack sementara.

### Soal 3 (all main.cpp)

Tambahkan prosedur getInputStream( in/out S : Stack ). Prosedur akan terus membaca dan
menerima input user dan memasukkan setiap input ke dalam stack hingga user menekan
tombol enter. Contoh: gunakan cin.get() untuk mendapatkan inputan user.

```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    cout << endl;

    createStack(S);
    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    cout << endl;

    createStack(S);
    push(S, 1);
    push(S, 0);
    push(S, 6);
    push(S, 9);
    push(S, 2);
    push(S, 7);
    push(S, 4);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}

```

> Sreenshoot 
> ![Screenshot Soal 3](https://github.com/salfiayu/Modul-6/blob/main/Modul%206/Screenshoot/Screenshot%20(129).png)

Program ini berfungsi untuk mencoba seluruh operasi stack, mulai dari push, pop, printInfo, balikStack, dan pushAscending; program membuat stack, melakukan berbagai kombinasi push-pop, menampilkan hasilnya, membalik stack, lalu menguji kembali stack dengan mode ascending serta data lain untuk memastikan semua fungsi berjalan dengan benar.

## Referensi

1. https://www.geeksforgeeks.org/dsa/stack-data-structure/ (diakses 4-11-2025)
2. https://en.wikipedia.org/wiki/Stack_(abstract_data_type)? (diakses 4-11-2025)
