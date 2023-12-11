# KarenStepanyanProjectS1
#include <stdio.h>
#include <stdlib.h>
#include <string.h>



// Structure to represent a tree
struct Tree {
    int age;
    int waterNeeded;
    int x;
    int y;
};


void displayTree(struct Tree tree) {

    printf("Tree at position (%d, %d): %d-year-old, Water Needed: %d liters\n", tree.x, tree.y, tree.age, tree.waterNeeded);

}
void calculateAverageAge(struct Tree* trees, int n) {
    int totalAge = 0;
   
    for (int i = 0; i < n; ++i) {
        totalAge += trees[i].age;
    }

    double averageAge = (double)totalAge / n;

    printf("Average Age of Trees: %.2f years\n", averageAge);
}

int main() {
    int n;   
    printf("please print the number of trees : ");
    scanf("%d", &n);

    struct Tree* trees;   
    int garden[20][30];
    FILE* fptr;    
    int i;
    int j; 
    fptr = fopen("data.txt", "wb");
    trees = (struct Tree*)malloc(n * sizeof(struct Tree));    
    for (int i = 0; i < n; ++i) {
        printf("Enter age and water, x, y:\n");       
        scanf("%d %d %d %d", &(trees + i)->age, &(trees + i)->waterNeeded, &(trees + i)->x, &(trees + i)->y);
    }

    fwrite(trees, sizeof(trees), 8, fptr);   
    
    fclose(fptr);
    
    fptr = fopen("data.txt", "rb"); 
    
    fread(trees, sizeof(trees), 8, fptr);
   
    for (i = 0; i < n; ++i) {
        
        printf("age: %d waterneeded: %d, positioin: %d %d", trees[i].age, trees[i].waterNeeded, trees[i].x, trees[i].y);
  
    }
    
    fclose(fptr);
    
    for (i = 0;i < 20;i++) {
        
        for (j = 0;j < 30;j++) {
            
            garden[i][j] = 0;
       
        }
    }

    for (i = 0; i < n;i++) {
        garden[trees[i].x][trees[i].y] = trees[i].age;
    }
  
    printf("\n");
   
    for (i = 0;i < 20;i++) {
       
        for (j = 0;j < 30;j++) {
            
            if (garden[i][j] == 0) {
               
                printf("  ");
            }
           
            else printf(" %d ", garden[i][j]);
        }      
        
        printf("\n");
    }    
    
    calculateAverageAge(trees, n);
   
    printf("Water the trees after 3 days. ");


    return 0;
}

