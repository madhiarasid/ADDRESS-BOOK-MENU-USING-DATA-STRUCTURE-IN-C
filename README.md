# ADDRESS-BOOK-MENU-USING-DATA-STRUCTURE-IN-C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Contact {
    char name[50];
    char phone[15];
    struct Contact* next;
} Contact;

// Function to insert a new contact into the linked list
void insertContact(Contact** head, char name[], char phone[]) {
    Contact* newContact = (Contact*)malloc(sizeof(Contact));
    strcpy(newContact->name, name);
    strcpy(newContact->phone, phone);
    newContact->next = NULL;

    if (*head == NULL) {
        *head = newContact;
    } else {
        Contact* current = *head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newContact;
    }
}

// Function to display all contacts in the linked list
void displayContacts(Contact* head) {
    if (head == NULL) {
        printf("No contacts found!\n");
    } else {
        Contact* current = head;
        printf("Contacts:\n");
        while (current != NULL) {
            printf("Name: %s, Phone: %s\n", current->name, current->phone);
            current = current->next;
        }
    }
}

// Function to search for a contact by name
void searchContact(Contact* head, char name[]) {
    Contact* current = head;
    while (current != NULL) {
        if (strcmp(current->name, name) == 0) {
            printf("Contact found:\n");
            printf("Name: %s, Phone: %s\n", current->name, current->phone);
            return;
        }
        current = current->next;
    }
    printf("Contact not found!\n");
}

// Function to delete a contact by name
void deleteContact(Contact** head, char name[]) {
    Contact* current = *head;
    Contact* previous = NULL;

    while (current != NULL && strcmp(current->name, name) != 0) {
        previous = current;
        current = current->next;
    }

    if (current == NULL) {
        printf("Contact not found!\n");
        return;
    }

    if (previous == NULL) {
        *head = current->next;
    } else {
        previous->next = current->next;
    }

    free(current);
    printf("Contact deleted successfully.\n");
}
// Function to free memory allocated for the linked list
void freeContacts(Contact* head) {
    Contact* current = head;
    while (current != NULL) {
        Contact* temp = current;
        current = current->next;
        free(temp);
    }
}

int main() {
    Contact* head = NULL;
    int choice;
    char name[50];
    char phone[15];

    while (1) {
        printf("\nAddress Book Menu:\n");
        printf("1. Add Contact\n");
        printf("2. Display Contacts\n");
        printf("3. Search Contact\n");
        printf("4. Delete Contact\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter name: ");
                scanf("%s", name);
                printf("Enter phone: ");
                scanf("%s", phone);
                insertContact(&head, name, phone);
                break;
            case 2:
                displayContacts(head);
                break;
            case 3:
                printf("Enter name to search: ");
                scanf("%s", name);
                searchContact(head, name);
                break;
            case 4:
                printf("Enter name to delete: ");
                scanf("%s", name);
                deleteContact(&head, name);
                break;
            case 5:
                freeContacts(head);
                printf("Exiting...\n");
                exit(0);
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }

    return 0;
}






