#include <stdio.h>
#include <stdlib.h>

struct Node{
        int data;
        struct Node* next;
};

void print(struct Node* head);
void insertBegin(struct Node **head, int data);
void insertEnd(struct Node **head, int data);
void insert(struct Node **head, int data, int position);
void deleteNode(struct Node **head, int position);
void search(struct Node *head, int element);

int main(){
        struct Node* head = NULL;
        insertEnd(&head, 15);
        insertBegin(&head, 5);
        insertEnd(&head, 1);
        insertEnd(&head, 10);
        insert(&head, 3, 1);
        insert(&head, 20, 0);
        insert(&head, 25, 6);
        deleteNode(&head, 5);
        deleteNode(&head, 0);
        deleteNode(&head, 3);
        search(head, 0);
        print(head);
}

void search(struct Node *head, int element){
        struct Node *temp = head;
        int i=1;
        while(temp != NULL){
                if(temp->data == element){
                        printf("Element found in position %d\n", i);
                        return;
                }
                i++;
                temp = temp->next;
        }
        printf("Element not found in the linked list\n");
}

void deleteNode(struct Node **head, int position){
        if(*head == NULL)return;
        struct Node* temp = *head;
        if(position == 1){
                *head = temp->next;
                printf("Node Deleted\n");
                return;
        }
        for(int i=1; temp!=NULL && i<position-1; i++)
                temp=temp->next;
        if(temp==NULL || temp->next == NULL){
                printf("Node Not Deleted\n");
                return;
        }
        struct Node *next = temp->next->next;
        temp->next = next;
        printf("Node Deleted\n");
}

void insert(struct Node **head, int data, int position){
        int i = 0;
        struct Node* temp = *head;
        while(temp != NULL){
                temp = temp->next;
                i++;
        }
        if(position < 1 || position > i+1){
                printf("Invalid Position\n");
                return;
        }
        temp = *head;
        struct Node *newNode = (struct Node*)malloc(sizeof(struct Node));
        newNode->data = data;
        if(position == 1){
                newNode->next = *head;
                *head = newNode;
                printf("Node inserted\n");
                return;
        }
        for(i=1; i<position-1; i++){
                temp = temp->next;
        }
        newNode->next = temp->next;
        temp->next = newNode;
        temp->next = newNode;
        printf("Node inserted\n");
}

void insertBegin(struct Node **head, int data){
        struct Node* temp = *head;
        struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));

        newNode->data = data;
        newNode->next = temp;
        *head = newNode;
        printf("Node inserted\n");
}

void insertEnd(struct Node **head, int data){
        struct Node* temp = *head;
        struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));

        newNode->data = data;
        newNode->next = NULL;

        if(*head == NULL){
                *head = newNode;
                printf("Node inserted\n");
                return;
        }

        while(temp->next != NULL){
                temp = temp->next;
        }
        temp->next = newNode;
        printf("Node inserted\n");
}

void print(struct Node* head){
        struct Node* temp = head;
        while(temp != NULL){
                printf("%d ", temp->data);
                temp = temp->next;
        }
        printf("\n");
}
