#include <stdio.h>
#include <stdlib.h>

void FCFS(int requests[], int n, int head) {
    int seek_count = 0, distance, current;
    
    printf("\nFCFS Disk Scheduling\n");
    printf("Seek Sequence is: \n");
    
    for (int i = 0; i < n; i++) {
        current = requests[i];
        distance = abs(current - head);
        seek_count += distance;
        head = current;
        
        printf("%d ", current);
    }
    
    printf("\nTotal Seek Operations: %d\n", seek_count);
}

void SCAN(int requests[], int n, int head, int disk_size, int direction) {
    int seek_count = 0, distance, current;
    int left[n], right[n], left_count = 0, right_count = 0;

    // Add the ends of the disk (0 and disk_size) to the request sequence
    if (direction == 0)  // Going left
        left[left_count++] = 0;
    else  // Going right
        right[right_count++] = disk_size - 1;

    // Split requests into left and right arrays based on the current head position
    for (int i = 0; i < n; i++) {
        if (requests[i] < head)
            left[left_count++] = requests[i];
        if (requests[i] > head)
            right[right_count++] = requests[i];
    }

    // Sort left and right arrays
    for (int i = 0; i < left_count - 1; i++)
        for (int j = i + 1; j < left_count; j++)
            if (left[i] < left[j])
                left[i] ^= left[j] ^= left[i] ^= left[j];
    
    for (int i = 0; i < right_count - 1; i++)
        for (int j = i + 1; j < right_count; j++)
            if (right[i] > right[j])
                right[i] ^= right[j] ^= right[i] ^= right[j];
    
    printf("\nSCAN Disk Scheduling\n");
    printf("Seek Sequence is: \n");

    // Scan towards the direction (either left or right)
    if (direction == 0) {  // Move towards left (0)
        for (int i = 0; i < left_count; i++) {
            current = left[i];
            distance = abs(current - head);
            seek_count += distance;
            head = current;
            printf("%d ", current);
        }

        // Once it reaches the end, move to the right side
        for (int i = 0; i < right_count; i++) {
            current = right[i];
            distance = abs(current - head);
            seek_count += distance;
            head = current;
            printf("%d ", current);
        }
    } else {  // Move towards right (disk_size - 1)
        for (int i = 0; i < right_count; i++) {
            current = right[i];
            distance = abs(current - head);
            seek_count += distance;
            head = current;
            printf("%d ", current);
        }

        // Once it reaches the end, move to the left side
        for (int i = 0; i < left_count; i++) {
            current = left[i];
            distance = abs(current - head);
            seek_count += distance;
            head = current;
            printf("%d ", current);
        }
    }

    printf("\nTotal Seek Operations: %d\n", seek_count);
}

void CSCAN(int requests[], int n, int head, int disk_size) {
    int seek_count = 0, distance, current;
    int left[n], right[n], left_count = 0, right_count = 0;

    // Add the ends of the disk (0 and disk_size) to the request sequence
    left[left_count++] = 0;
    right[right_count++] = disk_size - 1;

    // Split requests into left and right arrays based on the current head position
    for (int i = 0; i < n; i++) {
        if (requests[i] < head)
            left[left_count++] = requests[i];
        if (requests[i] > head)
            right[right_count++] = requests[i];
    }

    // Sort left and right arrays
    for (int i = 0; i < left_count - 1; i++)
        for (int j = i + 1; j < left_count; j++)
            if (left[i] < left[j])
                left[i] ^= left[j] ^= left[i] ^= left[j];
    
    for (int i = 0; i < right_count - 1; i++)
        for (int j = i + 1; j < right_count; j++)
            if (right[i] > right[j])
                right[i] ^= right[j] ^= right[i] ^= right[j];
    
    printf("\nC-SCAN Disk Scheduling\n");
    printf("Seek Sequence is: \n");

    // First move towards the right
    for (int i = 0; i < right_count; i++) {
        current = right[i];
        distance = abs(current - head);
        seek_count += distance;
        head = current;
        printf("%d ", current);
    }

    // Jump from the end to the start (circular behavior)
    head = 0;
    seek_count += disk_size - 1;

    // Then move towards the left
    for (int i = 0; i < left_count; i++) {
        current = left[i];
        distance = abs(current - head);
        seek_count += distance;
        head = current;
        printf("%d ", current);
    }

    printf("\nTotal Seek Operations: %d\n", seek_count);
}

int main() {
    int requests[] = {176, 79, 34, 60, 92, 11, 41, 114};
    int n = sizeof(requests) / sizeof(requests[0]);
    int head = 50;
    int disk_size = 200;
    int direction = 1;  // 0 for left, 1 for right

    FCFS(requests, n, head);
    SCAN(requests, n, head, disk_size, direction);
    CSCAN(requests, n, head, disk_size);

    return 0;
}
