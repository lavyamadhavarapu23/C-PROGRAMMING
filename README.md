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
