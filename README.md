# singlylinklist

#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node *next;

    Node(int data) {
        this->data = data;
        this->next = nullptr; 
    }

    ~Node() {
        cout << "Freeing memory for node with data: " << data << endl;
        if (next != nullptr) {
            delete next; // Recursively delete next nodes
        }
    }
};

void print(Node* head) {
    if (head == nullptr) {
        cout << "List is empty" << endl;
        return;
    }

    Node *temp = head;
    while (temp != nullptr) {
        cout << temp->data << " ";
        temp = temp->next;
    }
    cout << endl;
}

void insertatpos(Node* &head, int pos, int d) {
    Node* temp = new Node(d);

    if (head == nullptr) {
        head = temp;
        return;
    }

    if (pos == 1) {
        temp->next = head;
        head = temp;
        return;
    }

    Node* p = head;
    int i = 1;
    while (i < pos - 1 && p != nullptr) {
        p = p->next;
        i++;
    }

    if (p == nullptr) {
        cout << "Invalid position" << endl;
        return;
    }

    temp->next = p->next;
    p->next = temp;
}

void deleteatpos(Node* &head, int pos) {
    if (head == nullptr) {
        cout << "List is empty. Cannot delete." << endl;
        return;
    }

    if (pos == 1) {
        Node* temp = head;
        head = head->next;
        temp->next = nullptr;
        delete temp;
        return;
    }

    Node* curr = head;
    Node* prev = nullptr;
    int cnt = 1;

    while (curr != nullptr && cnt < pos) {
        prev = curr;
        curr = curr->next;
        cnt++;
    }

    if (curr == nullptr) {
        cout << "Invalid position" << endl;
        return;
    }

    prev->next = curr->next;
    curr->next = nullptr;
    delete curr;
}

int main() {
    Node *node1 = new Node(10);
    print(node1);

    Node *head = node1;
    insertatpos(head, 2, 20);
    print(head);

    insertatpos(head, 1, 5);
    print(head);

    insertatpos(head, 4, 15);
    print(head);

    deleteatpos(head, 2);
    print(head);

    return 0;
}
output:
10 
10 20 
5 10 20 
5 10 20 15 
Freeing memory for node with data: 10
5 20 15 
