#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node *next;
    struct Node *prev;
} Node;

void insertAtBeginning(Node **head, int data);
void insertAtEnd(Node **head, int data);
void insertAtPosition(Node **head, int data, int position);
void deleteNode(Node **head, int position);
void printList(Node *head);

int main() {
    Node *head = NULL;
    
    insertAtBeginning(&head, 10);
    insertAtEnd(&head, 20);
    insertAtPosition(&head, 15, 2);
    printList(head);
    deleteNode(&head, 2);
    printList(head);
    return 0;
}

void insertAtBeginning(Node **head, int data) {
    Node* temp = (Node*)malloc(sizeof(Node));
    temp->data = data;
    temp->next = *head;
    temp->prev = NULL;
    if (*head != NULL) {
        (*head)->prev = temp;
    }
    *head = temp;
}

void insertAtEnd(Node **head, int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    newNode->next = NULL;
    if (*head == NULL) {
        newNode->prev = NULL;
        *head = newNode;
        return;
    }
    Node *temp = *head;
    while (temp->next != NULL)
        temp = temp->next;
    temp->next = newNode;
    newNode->prev = temp;
}

void insertAtPosition(Node **head, int data, int position) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    if (position == 1) {
        newNode->next = *head;
        newNode->prev = NULL;
        if (*head != NULL)
            (*head)->prev = newNode;
        *head = newNode;
        return;
    }
    Node *temp = *head;
    for (int i = 1; i < position - 1 && temp != NULL; i++)
        temp = temp->next;
    if (temp == NULL) return;
    newNode->next = temp->next;
    newNode->prev = temp;
    if (temp->next != NULL)
        temp->next->prev = newNode;
    temp->next = newNode;
}

void deleteNode(Node **head, int position) {
    if (*head == NULL) return;
    Node *temp = *head;
    if (position == 1) {
        *head = temp->next;
        if (*head != NULL)
            (*head)->prev = NULL;
        free(temp);
        return;
    }
    for (int i = 1; temp != NULL && i < position - 1; i++)
        temp = temp->next;
    if (temp == NULL || temp->next == NULL) return;
    Node *next = temp->next->next;
    if (next != NULL)
        next->prev = temp;
    free(temp->next);
    temp->next = next;
}

void printList(Node *head) {
    Node *temp = head;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}
