#include <stdio.h>
#include <stdlib.h>

struct block {
    int bno;
    int flag;
} b[100]; // Assume we have 100 blocks

void allocate(int file_num, int size, int k[][10], int p[], int *used_blocks) {
    int s1, count = 0, j, s;

    // Try to find sequential free blocks
    while (1) {
        s1 = rand() % 100; // Randomly select a starting block
        count = 0;

        if (b[s1].flag == 0) {
            // Check if the required number of locations are free
            for (j = s1; j < s1 + size; j++) {
                if (b[j].flag == 0) count++;
            }
            if (count == size) break; // Break if enough free blocks are found
        }
    }

    // Allocate the blocks sequentially
    for (s = s1, j = 0; s < (s1 + size); s++) {
        k[file_num][j] = s; // Store the block number for the file
        j++;
        b[s].bno = s;
        b[s].flag = 1; // Mark the block as allocated
        (*used_blocks)++;
    }

    p[file_num] = size; // Store the file size
}

void display(int file_num, int k[][10], int p[]) {
    printf("\nFile %d: ", file_num + 1);
    printf("Length: %d, Blocks Allocated: ", p[file_num]);

    for (int j = 0; j < p[file_num]; j++) {
        printf("%d ", k[file_num][j]);
    }
    printf("\n");
}

int main() {
    int n, p[10], k[10][10]; // p stores the size of each file, k stores allocated block numbers
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

        if (used_blocks + size > 100) {
            printf("Not enough free blocks for file %d!\n", i + 1);
            continue;
        }

        allocate(i, size, k, p, &used_blocks);
    }

    // Display the allocation details
    for (int i = 0; i < n; i++) {
        display(i, k, p);
    }

    return 0;
}
