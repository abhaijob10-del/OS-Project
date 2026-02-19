#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_SEGMENTS 3
#define MAX_PAGES 5
#define FRAME_SIZE 100

// Page Table Entry
typedef struct {
    int frame;
    int valid;
} Page;

// Segment Table Entry
typedef struct {
    Page pages[MAX_PAGES];
    int limit;
    int valid;
} Segment;

Segment segment_table[MAX_SEGMENTS];

// Initialize predefined segment and page tables
void initialize_memory() {

    for(int i = 0; i < MAX_SEGMENTS; i++) {
        segment_table[i].valid = 1;
        segment_table[i].limit = 3;  // Each segment has 3 pages

        for(int j = 0; j < segment_table[i].limit; j++) {
            segment_table[i].pages[j].valid = 1;
            segment_table[i].pages[j].frame = (i * 10) + j;
        }
    }
}

// Display memory tables in HTML
void display_tables() {
    printf("<h3>Segment Table</h3>");
    printf("<table border='1'><tr><th>Segment</th><th>Limit</th><th>Valid</th></tr>");

    for(int i = 0; i < MAX_SEGMENTS; i++) {
        printf("<tr><td>%d</td><td>%d</td><td>%d</td></tr>",
               i,
               segment_table[i].limit,
               segment_table[i].valid);
    }
    printf("</table><br>");

    for(int i = 0; i < MAX_SEGMENTS; i++) {
        printf("<h4>Page Table for Segment %d</h4>", i);
        printf("<table border='1'><tr><th>Page</th><th>Frame</th><th>Valid</th></tr>");

        for(int j = 0; j < segment_table[i].limit; j++) {
            printf("<tr><td>%d</td><td>%d</td><td>%d</td></tr>",
                   j,
                   segment_table[i].pages[j].frame,
                   segment_table[i].pages[j].valid);
        }
        printf("</table><br>");
    }
}

int main() {

    printf("Content-type: text/html\n\n");

    char *data = getenv("QUERY_STRING");

    int segment, page, offset;

    if(data == NULL) {
        printf("<h2>No input received</h2>");
        return 0;
    }

    sscanf(data, "segment=%d&page=%d&offset=%d",
           &segment, &page, &offset);

    initialize_memory();

    printf("<html><body style='font-family:Arial;'>");
    printf("<h2>Segmentation + Paging Hybrid Model</h2>");

    display_tables();

    printf("<h3>Address Translation Steps</h3>");

    // Step 1: Segment validation
    if(segment < 0 || segment >= MAX_SEGMENTS || 
       segment_table[segment].valid == 0) {
        printf("<p style='color:red;'>Invalid Segment Number!</p>");
        printf("</body></html>");
        return 0;
    }
    printf("<p>✔ Segment %d is valid.</p>", segment);

    // Step 2: Page limit check
    if(page < 0 || page >= segment_table[segment].limit) {
        printf("<p style='color:red;'>Page exceeds segment limit!</p>");
        printf("</body></html>");
        return 0;
    }
    printf("<p>✔ Page %d is within segment limit.</p>", page);

    // Step 3: Page validation
    if(segment_table[segment].pages[page].valid == 0) {
        printf("<p style='color:red;'>Page Fault! Page not in memory.</p>");
        printf("</body></html>");
        return 0;
    }
    printf("<p>✔ Page %d is valid.</p>", page);

    // Step 4: Offset validation
    if(offset < 0 || offset >= FRAME_SIZE) {
        printf("<p style='color:red;'>Offset exceeds frame size!</p>");
        printf("</body></html>");
        return 0;
    }
    printf("<p>✔ Offset %d is valid.</p>", offset);

    int frame = segment_table[segment].pages[page].frame;
    int physical_address = (frame * FRAME_SIZE) + offset;

    printf("<h3>Frame Number: %d</h3>", frame);
    printf("<h3>Physical Address = (%d × %d) + %d = %d</h3>",
           frame, FRAME_SIZE, offset, physical_address);

    printf("<br><a href='/index.html'>Go Back</a>");
    printf("</body></html>");

    return 0;
}
