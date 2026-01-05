#include <stdio.h>
#include <stdlib.h>

struct Node {
    struct Node *prev;
    int data;
    struct Node *next;
} *newNode, *head = NULL, *temp, *pretemp;

// Insert at beginning
void insertAtBeginning() {
    int value;
    printf("Enter a value: ");
    scanf("%d", &value);

    newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = value;

    if (head == NULL) {
        head = newNode;
        head->next = head;
        head->prev = head;
    } else {
        temp = head->prev;
        newNode->next = head;
        newNode->prev = temp;
        temp->next = newNode;
        head->prev = newNode;
        head = newNode;
    }
}

// Insert at end
void insertAtEnd() {
    int value;
    printf("Enter a value: ");
    scanf("%d", &value);

    newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = value;

    if (head == NULL) {
        head = newNode;
        head->next = head;
        head->prev = head;
    } else {
        temp = head->prev;
        temp->next = newNode;
        newNode->prev = temp;
        newNode->next = head;
        head->prev = newNode;
    }
}

// Insert before a node
void insertAtBefore() {
    int num, key;
    printf("Enter a value to insert: ");
    scanf("%d", &num);
    printf("Enter the key before which to insert: ");
    scanf("%d", &key);

    newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = num;

    temp = head;
    while (temp->data != key && temp->next != head) {
        temp = temp->next;
    }

    if (temp->data == key) {
        pretemp = temp->prev;
        pretemp->next = newNode;
        newNode->prev = pretemp;
        newNode->next = temp;
        temp->prev = newNode;

        if (temp == head) {
            head = newNode;
        }
    } else {
        printf("Key not found!\n");
    }
}

// Insert after a node
void insertAtAfter() {
    int num, key;
    printf("Enter a value to insert: ");
    scanf("%d", &num);
    printf("Enter the key after which to insert: ");
    scanf("%d", &key);

    newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = num;

    temp = head;
    while (temp->data != key && temp->next != head) {
        temp = temp->next;
    }

    if (temp->data == key) {
        pretemp = temp->next;
        temp->next = newNode;
        newNode->prev = temp;
        newNode->next = pretemp;
        pretemp->prev = newNode;
    } else {
        printf("Key not found!\n");
    }
}

// Display list
void displayList() {
    if (head == NULL) {
        printf("List is empty!\n");
        return;
    }

    temp = head;
    printf("Circular Doubly Linked List: \n");
    do {
        printf("->[%d] ", temp->data);
        temp = temp->next;
    } while (temp != head);
    printf("\n");
}

// Main function
int main() {
    int value, choice;
    char ch;

    // Create initial list
    do {
        printf("Enter a value: ");
        scanf("%d", &value);

        newNode = (struct Node *)malloc(sizeof(struct Node));
        newNode->data = value;

        if (head == NULL) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            temp = head->prev;
            temp->next = newNode;
            newNode->prev = temp;
            newNode->next = head;
            head->prev = newNode;
        }

        printf("Do you want to add one more node? (y/n): ");
        scanf(" %c", &ch);
    } while (ch == 'y');

    while (1) {
        printf("\nMenu:\n");
        printf("1. Display List\n");
        printf("2. Insert At Beginning\n");
        printf("3. Insert At End\n");
        printf("4. Insert Before a Node\n");
        printf("5. Insert After a Node\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                displayList();
                break;
            case 2:
                insertAtBeginning();
                printf("After insertion:\n");
                displayList();
                break;
            case 3:
                insertAtEnd();
                printf("After insertion:\n");
                displayList();
                break;
            case 4:
                insertAtBefore();
                printf("After insertion:\n");
                displayList();
                break;
            case 5:
                insertAtAfter();
                printf("After insertion:\n");
                displayList();
                break;
            case 6:
                printf("Exiting...\n");
                return 0;
            default:
                printf("Invalid choice! Try again.\n");
        }
    }

    return 0;
}
