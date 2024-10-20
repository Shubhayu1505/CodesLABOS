#include <stdio.h>
#include <limits.h>

void FIFO(int pages[], int n, int capacity) {
    int frame[capacity];
    int front = 0, count = 0, page_faults = 0;

    // Initialize all frames to -1 (indicating they're empty)
    for (int i = 0; i < capacity; i++)
        frame[i] = -1;

    printf("FIFO Page Replacement\n");
    for (int i = 0; i < n; i++) {
        int found = 0;

        // Check if the page is already in the frame
        for (int j = 0; j < capacity; j++) {
            if (frame[j] == pages[i]) {
                found = 1;
                break;
            }
        }

        // If the page is not found, replace the oldest page (FIFO)
        if (!found) {
            frame[front] = pages[i];
            front = (front + 1) % capacity;
            page_faults++;
        }

        // Print the current state of the frame
        printf("Page %d -> ", pages[i]);
        for (int j = 0; j < capacity; j++) {
            if (frame[j] != -1)
                printf("%d ", frame[j]);
            else
                printf("- ");
        }
        printf("\n");
    }

    printf("Total Page Faults: %d\n", page_faults);
}

void LRU(int pages[], int n, int capacity) {
    int frame[capacity], recent[capacity];
    int page_faults = 0;

    // Initialize frames and recent array to -1
    for (int i = 0; i < capacity; i++) {
        frame[i] = -1;
        recent[i] = -1;
    }

    printf("\nLRU Page Replacement\n");
    for (int i = 0; i < n; i++) {
        int found = 0;

        // Check if the page is already in the frame
        for (int j = 0; j < capacity; j++) {
            if (frame[j] == pages[i]) {
                found = 1;
                recent[j] = i; // Update recent access time
                break;
            }
        }

        // If the page is not found, replace the least recently used page
        if (!found) {
            int lru_index = 0;
            for (int j = 1; j < capacity; j++) {
                if (recent[j] < recent[lru_index])
                    lru_index = j;
            }

            frame[lru_index] = pages[i];
            recent[lru_index] = i;
            page_faults++;
        }

        // Print the current state of the frame
        printf("Page %d -> ", pages[i]);
        for (int j = 0; j < capacity; j++) {
            if (frame[j] != -1)
                printf("%d ", frame[j]);
            else
                printf("- ");
        }
        printf("\n");
    }

    printf("Total Page Faults: %d\n", page_faults);
}

void LFU(int pages[], int n, int capacity) {
    int frame[capacity], freq[capacity];
    int time[capacity], page_faults = 0;

    // Initialize frames, frequency, and time arrays to -1
    for (int i = 0; i < capacity; i++) {
        frame[i] = -1;
        freq[i] = 0;
        time[i] = -1;
    }

    printf("\nLFU Page Replacement\n");
    for (int i = 0; i < n; i++) {
        int found = 0;

        // Check if the page is already in the frame
        for (int j = 0; j < capacity; j++) {
            if (frame[j] == pages[i]) {
                freq[j]++;
                found = 1;
                break;
            }
        }

        // If the page is not found, replace the least frequently used page
        if (!found) {
            int lfu_index = 0;
            for (int j = 1; j < capacity; j++) {
                if (freq[j] < freq[lfu_index] || (freq[j] == freq[lfu_index] && time[j] < time[lfu_index]))
                    lfu_index = j;
            }

            frame[lfu_index] = pages[i];
            freq[lfu_index] = 1;
            time[lfu_index] = i;
            page_faults++;
        }

        // Print the current state of the frame
        printf("Page %d -> ", pages[i]);
        for (int j = 0; j < capacity; j++) {
            if (frame[j] != -1)
                printf("%d ", frame[j]);
            else
                printf("- ");
        }
        printf("\n");
    }

    printf("Total Page Faults: %d\n", page_faults);
}

int main() {
    int pages[] = {1, 3, 0, 3, 5, 6, 3};
    int n = sizeof(pages) / sizeof(pages[0]);
    int capacity = 3;

    FIFO(pages, n, capacity);
    LRU(pages, n, capacity);
    LFU(pages, n, capacity);

    return 0;
}
