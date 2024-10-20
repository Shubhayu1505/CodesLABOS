#include <stdio.h>
#include <stdlib.h>

struct block {
    int bno;
    int flag; // 0 = free, 1 = allocated
} b[100]; // Assume we have 100 blocks

int r[10][10]; // r stores block numbers for each file

// Function to allocate blocks for a file using indexed allocation
void allocate(int file_num, int size, int p[], int *used_blocks) {
    int index_block;
    
    // Find a free block for the index block
    while (1) {
        index_block = rand() % 100; // Select a random block for the index
        if (b[index_block].flag == 0) {
            b[index_block].flag = 1; // Allocate the index block
            (*used_blocks)++;
            printf("File %d: Index block allocated at %d\n", file_num + 1, index_block);
            break;
        }
    }

    // Now allocate blocks for the file data
    for (int j = 0; j < size; j++) {
        int data_block;
        while (1) {
            data_block = rand() % 100; // Select a random block for the file data
            if (b[data_block].flag == 0) {
                b[data_block].flag = 1; // Allocate the data block
                r[file_num][j] = data_block; // Store the data block in the index table
                (*used_blocks)++;
                break;
            }
        }
    }

    p[file_num] = size; // Store the file size
}

// Function to display file block allocation details
void display(int file_num, int p[]) {
    printf("\nFile %d: ", file_num + 1);
    printf("Length: %d, Data Blocks: ", p[file_num]);

    for (int j = 0; j < p[file_num]; j++) {
        printf("%d ", r[file_num][j]); // Print data block numbers
    }
    printf("\n");
}

int main() {
    int n, p[10]; // p stores the size of each file
    int used_blocks = 0;

    printf("Enter the number of files: ");
    scanf("%d", &n);

    // Initialize block flags (0 = free, 1 = allocated)
    for (int i = 0; i < 100; i++) {
        b[i].flag = 0;
    }

    // Input the size for each file and allocate blocks
    for (int i = 0; i < n; i++) {
        int size;
        printf("Enter the size (in blocks) for file %d: ", i + 1);
        scanf("%d", &size);

        if (used_blocks + size + 1 > 100) { // Check if enough blocks are free (size + 1 for the index block)
            printf("Not enough free blocks for file %d!\n", i + 1);
            continue;
        }

        allocate(i, size, p, &used_blocks);
    }

    // Display the allocation details
    for (int i = 0; i < n; i++) {
        display(i, p);
    }

    return 0;
}
