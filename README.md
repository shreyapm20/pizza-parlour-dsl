# pizza-parlour-dsl
//Pizza Parlour 
#include<iostream>
#include<cstdlib>

using namespace std;

class pizza {
    int front, rear, q[5];

public:
    pizza() {
        front = -1;
        rear = -1;
    }

    int isfull() {
        if ((front == 0 && rear == 4) || front == (rear + 1) % 5) {
            return 1;
        }
        else {
            return 0;
        }
    }

    int isEmpty() {
        if (front == -1 && rear == -1) {
            return 1;
        }
        else {
            return 0;
        }
    }

    void add() {
        if (isfull() == 0) {
            cout << "\n Enter the Pizza ID: ";
            if (front == -1 && rear == -1) {
                front = 0;
                rear = 0;
                cin >> q[rear];
            }
            else {
                rear = (rear + 1) % 5;
                cin >> q[rear];
            }
            char c;
            cout << " Do you want to add another order? (y/n): ";
            cin >> c;
            if (c == 'y' || c == 'Y') {
                add();
            }
        }
        else {
            cout << "\n Orders are full ";
        }
    }

    void serve() {
        if (isEmpty() == 0) {
            cout << "\n Order served is: " << q[front];
            if (front == rear) {
                front = -1;
                rear = -1;
            }
            else {
                front = (front + 1) % 5;
            }
        }
        else {
            cout << "\n Orders are empty ";
        }
    }

    void display() {
        if (isEmpty() == 0) {
            int i = front;
            while (i != rear) {
                cout << q[i] << " <- ";
                i = (i + 1) % 5;
            }
            cout << q[rear];
        }
        else {
            cout << "\n Orders are empty";
        }
    }

    void check() {
        int ch;
        cout << "\n\n**** PIZZA PARLOUR **** \n\n";
        cout << "\n 1. Add a Pizza \n 2. Display the Orders \n 3. Serve a pizza \n 4. Exit\n Enter your choice: ";
        cin >> ch;

        switch (ch) {
        case 1:
            add();
            break;
        case 2:
            display();
            break;
        case 3:
            serve();
            break;
        case 4:
            exit(0);
        default:
            cout << "Invalid choice ";
        }

        char ch1;
        cout << "\n Do you want to continue? (y/n): ";
        cin >> ch1;
        if (ch1 == 'y' || ch1 == 'Y') {
            check();
        }
    }
};

int main() {
    pizza pl;
    pl.check();
    return 0;
}

