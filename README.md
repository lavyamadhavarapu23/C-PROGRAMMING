# C-PROGRAMMING
PALINDROME
#include <stdio.h>

int main() {
    int num, original, remainder, reverse = 0;

    printf("Enter a number: ");
    scanf("%d", &num);

    original = num;

    while (num != 0) {
        remainder = num % 10;
        reverse = reverse * 10 + remainder;
        num = num / 10;
    }

    if (original == reverse)
        printf("Palindrome number\n");
    else
        printf("Not a palindrome\n");

    return 0;
}
DYNAMIC MEMORY ALLOCATION
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr, n, i, newSize;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    // Allocate memory using malloc
    arr = (int*)malloc(n * sizeof(int));

    if(arr == NULL) {
        printf("Memory allocation failed\n");
        return 0;
    }

    printf("Enter %d elements:\n", n);
    for(i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Elements are:\n");
    for(i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    // Reallocate memory using realloc
    printf("\nEnter new size of array: ");
    scanf("%d", &newSize);

    arr = (int*)realloc(arr, newSize * sizeof(int));

    printf("Enter %d new elements:\n", newSize - n);
    for(i = n; i < newSize; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Updated array:\n");
    for(i = 0; i < newSize; i++) {
        printf("%d ", arr[i]);
    }

    // Free allocated memory
    free(arr);

    return 0;
}
STACK USING DYNAMIC MEMORY ALLOCATION
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* top = NULL;

void push(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));

    if(newNode == NULL) {
        printf("Stack Overflow\n");
        return;
    }

    newNode->data = value;
    newNode->next = top;
    top = newNode;

    printf("Inserted %d\n", value);
}

void pop() {
    if(top == NULL) {
        printf("Stack Underflow\n");
        return;
    }

    struct Node* temp = top;
    printf("Deleted element: %d\n", top->data);

    top = top->next;
    free(temp);
}

void display() {
    struct Node* temp = top;

    if(temp == NULL) {
        printf("Stack is empty\n");
        return;
    }

    printf("Stack elements:\n");
    while(temp != NULL) {
        printf("%d\n", temp->data);
        temp = temp->next;
    }
}

int main() {
    int choice, value;

    while(1) {
        printf("\n1.Push\n2.Pop\n3.Display\n4.Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                printf("Enter value: ");
                scanf("%d", &value);
                push(value);
                break;

            case 2:
                pop();
                break;

            case 3:
                display();
                break;

            case 4:
                exit(0);

            default:
                printf("Invalid choice\n");
        }
    }
}
BINARY SEARCH TREE
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *left, *right;
};

struct node* create(int data) {
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    newnode->data = data;
    newnode->left = newnode->right = NULL;
    return newnode;
}

struct node* insert(struct node* root, int data) {
    if (root == NULL)
        return create(data);

    if (data < root->data)
        root->left = insert(root->left, data);
    else
        root->right = insert(root->right, data);

    return root;
}

void inorder(struct node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

struct node* minValue(struct node* root) {
    while (root->left != NULL)
        root = root->left;
    return root;
}

struct node* deleteNode(struct node* root, int key) {
    if (root == NULL)
        return root;

    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) {
            struct node* temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL) {
            struct node* temp = root->left;
            free(root);
            return temp;
        }

        struct node* temp = minValue(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

int main() {
    struct node* root = NULL;
    int choice, value;

    while (1) {
        printf("\n1.Insert\n2.Delete\n3.Display(Inorder)\n4.Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value: ");
                scanf("%d", &value);
                root = insert(root, value);
                break;

            case 2:
                printf("Enter value to delete: ");
                scanf("%d", &value);
                root = deleteNode(root, value);
                break;

            case 3:
                printf("BST elements: ");
                inorder(root);
                printf("\n");
                break;

            case 4:
                exit(0);

            default:
                printf("Invalid choice\n");
        }
    }
}
INSERTION SORT
#include <stdio.h>

int main() {
    int arr[100], n, i, j, key;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");
    for(i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    for(i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        while(j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }

    printf("Sorted array:\n");
    for(i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
MERGE SORT
#include <stdio.h>

void merge(int arr[], int l, int m, int r) {
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[n1], R[n2];

    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    i = 0;
    j = 0;
    k = l;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;

        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

int main() {
    int arr[100], n, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");
    for (i = 0; i < n; i++)
        scanf("%d", &arr[i]);

    mergeSort(arr, 0, n - 1);

    printf("Sorted array:\n");
    for (i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
QUICK SORT
#include <stdio.h>

void quicksort(int a[], int low, int high);
int partition(int a[], int low, int high);

void quicksort(int a[], int low, int high) {
    int p;
    if (low < high) {
        p = partition(a, low, high);
        quicksort(a, low, p - 1);
        quicksort(a, p + 1, high);
    }
}

int partition(int a[], int low, int high) {
    int pivot = a[low];
    int i = low + 1;
    int j = high;
    int temp;

    while (1) {
        while (i <= high && a[i] <= pivot)
            i++;
        while (a[j] > pivot)
            j--;

        if (i < j) {
            temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        } else {
            temp = a[low];
            a[low] = a[j];
            a[j] = temp;
            return j;
        }
    }
}

int main() {
    int a[100], n, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);

    quicksort(a, 0, n - 1);

    printf("Sorted elements:\n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
CIRCULAR QUEUE PROGRAM
#include <stdio.h>
#define MAX 5

int queue[MAX];
int front = -1, rear = -1;

void enqueue() {
    int value;

    if ((rear + 1) % MAX == front) {
        printf("Queue Overflow\n");
    } else {
        printf("Enter value: ");
        scanf("%d", &value);

        if (front == -1)
            front = 0;

        rear = (rear + 1) % MAX;
        queue[rear] = value;
    }
}

void dequeue() {
    if (front == -1) {
        printf("Queue Underflow\n");
    } else {
        printf("Deleted element: %d\n", queue[front]);

        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX;
        }
    }
}

void display() {
    int i;

    if (front == -1) {
        printf("Queue is empty\n");
    } else {
        printf("Queue elements:\n");
        i = front;
        while (i != rear) {
            printf("%d ", queue[i]);
            i = (i + 1) % MAX;
        }
        printf("%d", queue[rear]);
        printf("\n");
    }
}

int main() {
    int choice;

    while (1) {
        printf("\n1.Enqueue\n2.Dequeue\n3.Display\n4.Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: enqueue(); break;
            case 2: dequeue(); break;
            case 3: display(); break;
            case 4: return 0;
            default: printf("Invalid choice\n");
        }
    }
}
