#include <stdio.h>
#include <stdlib.h>
struct Node {
        int data;
        struct Node* next;
};
struct Node* createNode(int data) {
        struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
        newNode->data = data;
        newNode->next = NULL;
        return newNode;
}
void inend(struct Node** head, int data) {
        struct Node* newNode = createNode(data);
        if (*head == NULL) {
                *head = newNode;
                return;
        }
        struct Node* temp = *head;
        while (temp->next != NULL) {
                temp = temp->next;
        }
        temp->next = newNode;
}
void dislist(struct Node* head) {
        struct Node* temp = head;
        while (temp != NULL) {
                printf("%d -> ", temp->data);
                temp = temp->next;
        }
 printf("NULL\n");
}
int main() {
        struct Node* head = NULL;
        int n, data;
        printf("Enter the numbr of nodes?: ");
        scanf("%d", &n);
        for (int i = 0; i < n; i++) {
                printf("Enter data for node %d: ", i+1);
                scanf("%d", &data);
                inend(&head, data);
        }
        printf("The linked list is: ");
        dislist(head);
        return 0;
}
