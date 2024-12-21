# Shan
Code
#include <stdio.h>
#include <stdlib.h>
#define MAX_EMPLOYEES 5
#define HT_SIZE 10

// Employee structure
struct Employee {
    int key;
    char name[30];
};

// Hash table structure
struct EmployeeHashTable {
    struct Employee *employees[HT_SIZE]; // Array of pointers to Employee
};

// Hash function
int hash(int key, int m) {
    return key % m;
}

// Insert an employee into the hash table
void insert(struct EmployeeHashTable *ht, struct Employee *emp, int m) {
    int index = hash(emp->key, m); // Compute hash index
    while (ht->employees[index] != NULL) { // Resolve collision using linear probing
        index = (index + 1) % m;
    }
    ht->employees[index] = emp;
}

// Display the hash table
void display(struct EmployeeHashTable *ht, int m) {
    printf("Hash Table:\n");
    for (int i = 0; i < m; i++) {
        if (ht->employees[i] != NULL) {
            printf("Index %d: Key=%d, Name=%s\n", i, ht->employees[i]->key, ht->employees[i]->name);
        } else {
            printf("Index %d: Empty\n", i);
        }
    }
}

int main() {
    struct EmployeeHashTable ht;
    int m = HT_SIZE;

    // Initialize all elements of the hash table to NULL
    for (int i = 0; i < m; i++) {
        ht.employees[i] = NULL;
    }

    // Employee records
    struct Employee e1 = {1000, "Ram"};
    struct Employee e2 = {1001, "Naga"};
    struct Employee e3 = {1002, "Lakshmi"};
    struct Employee e4 = {2002, "Sontosh"};

    // Insert employees into the hash table
    insert(&ht, &e1, m);
    insert(&ht, &e2, m);
    insert(&ht, &e3, m);
    insert(&ht, &e4, m);

    // Display the hash table
    display(&ht, m);

    return 0;
}
