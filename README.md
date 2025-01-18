# Table Of Contents

1. [Time Complexity](#Time Complexity)
2. [Space Complexity](#Space Complexity)
3. [Pointers](#Pointers)
4. [Structs](#Structs)
5. [Essential Functions from <string.h>](#Essential Functions from <string.h>)
6. [Lists](#Lists)
7. [Basic Operations on Binary Trees](#Basic Operationson Binary Trees)
8. [Quicksort Algorithm](#Quicksort Algorithm)
9. [Mergesort Algorithm](#Mergesort Algorithm)
10. [File Manipulation Functions](#File Manipulation Functions)

# Time Complexity

**O(1) - Constant Time**

Where it's encountered:
  -Accessing an element in an array by index: arr[i]
  -Assigning a value to a variable
  -Simple arithmetic operations (addition, multiplication)

Example function:

  ```c
  int getFirstElement(int arr[]) {
       return arr[0]; // O(1)
  }
  ```

**𝑂(log𝑛) - Logarithmic Time**

Where it's encountered:
  --Binary search (e.g., searching in a sorted array)
  --Certain tree-based operations (e.g., binary search tree, balanced trees like AVL)

Example function:

  ```c
  int binarySearch(int arr[], int target, int low, int high) {
       if (low > high) return -1;
       int mid = (low + high) / 2;
       if (arr[mid] == target) return mid;
       if (arr[mid] > target) return binarySearch(arr, target, low, mid - 1);
       return binarySearch(arr, target, mid + 1, high);
  }
  ```

**𝑂(𝑛) - Linear Time**

Where it's encountered:
  --Iterating through an array, list, or string once
  --Simple loops that iterate through all elements

Example function:

  ```c
  int sumArray(int arr[], int n) {
       int sum = 0;
       for (int i = 0; i < n; i++) {
            sum += arr[i]; // O(n)
       }
       return sum;
  }
  ```

**𝑂(𝑛log𝑛) - Log-Linear Time**

Where it's encountered:
  --Efficient sorting algorithms (e.g., Merge Sort, Quick Sort)
  --Divide and conquer algorithms
  --Example function:

  ```c
  void mergeSort(int arr[], int low, int high) {
       if (low < high) {
             int mid = (low + high) / 2;
             mergeSort(arr, low, mid);    // O(log n)
             mergeSort(arr, mid + 1, high);
             merge(arr, low, mid, high);  // O(n)
       }
  }
  ```

**O(n^2 ) - Quadratic Time**

Where it's encountered:
  --Nested loops that iterate over the array or list
  --Brute force algorithms (e.g., bubble sort, selection sort, insertion sort)

Example function:

  ```c
  void bubbleSort(int arr[], int n) {
       for (int i = 0; i < n; i++) {
            for (int j = 0; j < n - 1; j++) { // O(n^2)
                 if (arr[j] > arr[j + 1]) {
                      swap(&arr[j], &arr[j + 1]);
                 }
            }
       }
  }
  ```

**O(n^3 ) - Cubic Time**

Where it's encountered:
  --Triple nested loops (often in algorithms like matrix multiplication or 3D problems)

Example function:

  ```c
  void matrixMultiply(int A[][3], int B[][3], int C[][3], int n) {
       for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                 for (int k = 0; k < n; k++) { // O(n^3)
                      C[i][j] += A[i][k] * B[k][j];
                 }
            }
       }
  }
  ```

**O(2^n ) - Exponential Time**

Where it's encountered:
  --Algorithms that try every possible solution (e.g., brute force for generating subsets, Fibonacci recursion without memoization)
  --Problems like the Traveling Salesman Problem (TSP)

Example function:

  ```c
  int fib(int n) {
       if (n <= 1) return n;
         return fib(n-1) + fib(n-2); // O(2^n)
    }
  }
  ```

**O(n!) - Factorial Time**

Where it's encountered:
  --Algorithms that generate all permutations (e.g., generating permutations of a set)
  --Problems like solving the Traveling Salesman Problem (TSP) by brute force

Example function:

  ```c
  void generatePermutations(int n, int idx, int* arr, int* perm) {
       if (idx == n) {
            for (int i = 0; i < n; i++) {
                 printf("%d ", perm[i]); // O(n)
            }
            printf("\n");
            return;
       }
       for (int i = idx; i < n; i++) {
            swap(&arr[idx], &arr[i]);
            perm[idx] = arr[idx];
            generatePermutations(n, idx + 1, arr, perm); // O(n!)
            swap(&arr[idx], &arr[i]); // backtrack
       }
  }
  ```

# Space Complexity

**O(1) - Constant Space**

Where it's encountered:
  --No additional memory is allocated (no arrays or structures).
  --Functions with only local variables or constant-size variables.

Example:

  ```c
  int addTwoNumbers(int a, int b) {
       return a + b; // O(1)
  }
  ```

**O(n) - Linear Space**

Where it's encountered:
  --Algorithms where the space grows linearly with input size (e.g., storing input data in an array).
  --Recursive algorithms that have a call stack proportional to the input size.

Example:

  ``c
  void copyArray(int* arr, int n) {
       int* copy = malloc(n * sizeof(int)); // O(n)
       for (int i = 0; i < n; i++) {
            copy[i] = arr[i];
       }
  }
  ```


**O(n^2) - Quadratic Space**

Where it's encountered:
  --Algorithms that use 2D arrays or matrices.
  --Recursion with two parameters (e.g., storing solutions in a DP table with dimensions 𝑛×𝑛).

Example:

  ```c
  int** createMatrix(int n) {
     int** matrix = malloc(n * sizeof(int*));
     for (int i = 0; i < n; i++) {
        matrix[i] = malloc(n * sizeof(int)); // O(n^2)
     }
     return matrix;
  }
  ```

**O(2^n) - Exponential Space**

Where it's encountered:
  --Algorithms that store subsets of all possible elements (e.g., generating all subsets of a set).
  --Algorithms where each recursive call adds a new data element.

Example:

  ```c
  void generateSubsets(int n, int idx, int* arr, int* subset, int size) {
       if (idx == n) {
            printf("%d\n", subset[0]); // O(2^n) for subsets
            return;
       }
       generateSubsets(n, idx + 1, arr, subset, size);
       generateSubsets(n, idx + 1, arr, subset, size + 1);
  }
  ```

# Pointers

Pointers are variables that store the memory address of another variable. They are powerful tools in C and C++ for dynamic memory management, function arguments, and data structures.

**Syntax:**
```c
int a = 10;
int *ptr = &a; // ptr now points to the address of a
printf("Value of a: %d\n", *ptr); // Dereferencing ptr gives the value of a
```
**Output:**
```
Value of a: 10
```

**Key Concepts:**
- **Declaration:** `type *pointer_name;`
- **Dereferencing:** Access the value stored at the memory address using `*pointer_name`.
- **Pointer Arithmetic:** Incrementing/decrementing a pointer moves it to the next/previous memory block of its type.

**Example:**
```c
int arr[] = {10, 20, 30};
int *p = arr;
for (int i = 0; i < 3; i++) {
    printf("%d ", *(p + i)); // Accessing elements using pointer arithmetic
}
```
**Output:**
```
10 20 30
```

# Structs

A `struct` (short for structure) is a user-defined data type that groups variables under a single name.

**Syntax:**

   ```c
   typedef struct {
       int id;
       char name[50];
       float marks;
   } Student;
   ```

**Example:**

   ```c
   Student s1 = {1, "Alice", 92.5};
       printf("ID: %d, Name: %s, Marks: %.2f\n", s1.id, s1.name, s1.marks);
   ```

**Output:**
 
   ```
   ID: 1, Name: Alice, Marks: 92.50
   ```

**Key Features:**

- Organizes related data.
- Can include pointers, arrays, and other structs.

# Essential Functions from `<string.h>`

   1. `strlen`: Returns the length of a string.

   ```c
      char str[] = "Hello";
      printf("Length: %lu\n", strlen(str));
   ```

   2. `strcpy`: Copies one string to another.

   ```c
      char dest[10];
      strcpy(dest, "Hi");
   ```

   3. `strcat`: Concatenates two strings.

   ```c
      char str1[20] = "Good";
      strcat(str1, " Morning");
   ```

   4. `strcmp`: Compares two strings.

   ```c
      if (strcmp("a", "b") < 0) printf("a comes before b\n");
   ```

   5. `strchr`: Finds the first occurrence of a character.

   ```c
      char *pos = strchr("Hello", 'e');
   ```

   6. `strstr`: Finds the first occurrence of a substring.

   ```c
      char *sub = strstr("Hello World", "World");
      if (sub) printf("Substring found: %s\n", sub);
   ```

   7. `strncpy`: Copies a specified number of characters from one string to another.

   ```c
      char src[] = "Hello";
      char dest[10];
      strncpy(dest, src, 3);
      dest[3] = '\0';
      printf("%s\n", dest); // Output: Hel
   ```

   8. `strncat`: Appends a specified number of characters from one string to another.

   ```c
      char str1[20] = "Good";
      strncat(str1, " Evening", 4);
      printf("%s\n", str1); // Output: Good Even
   ```

   9. `memset`: Fills memory with a constant byte.

   ```c
      char buffer[10];
      memset(buffer, '-', sizeof(buffer));
      buffer[9] = '\0';
      printf("%s\n", buffer); // Output: ---------
   ```

   10. `memcpy`: Copies a block of memory.

   ```c
      char src[] = "Data";
      char dest[10];
      memcpy(dest, src, strlen(src) + 1);
      printf("%s\n", dest); // Output: Data
   ```   

   11. `strncmp`: Compares up to a specified number of characters of two strings.

   ```c
      if (strncmp("abc", "abd", 2) == 0) printf("First two characters are the same\n");
   ```

# Lists

Lists are dynamic data structures for storing sequential data. A **linked list** is a common implementation.

**Functions:**  
1. **Check if Empty:**
   ```c
   int is_empty(ListNode *head) {
       return head == NULL;
   }
   ```

2. **Insert an Element:**
   ```c
   void insert(ListNode **head, int value) {
       ListNode *newNode = malloc(sizeof(ListNode));
       newNode->value = value;
       newNode->next = *head;
       *head = newNode;
   }
   ```

3. **Print Elements:**
   ```c
   void print(ListNode *head) {
       while (head) {
           printf("%d -> ", head->value);
           head = head->next;
       }
       printf("NULL\n");
   }
   ```

4. **Find Length:**
   ```c
   int length(ListNode *head) {
   int len = 0;
       while (head) {
           len++;
           head = head->next;
       }
       return len;
   }
   ```

5. **Find an Element:**
   ```c
   ListNode* find(ListNode *head, int value) {
       while (head) {
           if (head->value == value) return head;
           head = head->next;
       }
       return NULL;
   }
   ```

6. **Delete an Element:**
   ```c
   void delete(ListNode **head, int value) {
       ListNode *current = *head, *prev = NULL;
       while (current && current->value != value) {
           prev = current;
           current = current->next;
       }
       if (current) {
           if (prev) prev->next = current->next;
           else *head = current->next;
           free(current);
       }
   }
   ```

# Basic Operations on Binary Trees

**1.Check if Empty:**

    ```c
   int is_empty(TreeNode *root) {
        return root == NULL;
   }
   ```

**2. Find Depth:**
   
   ```c
   int depth(TreeNode *root) {
       if (!root) return 0;
       int leftDepth = depth(root->left);
       int rightDepth = depth(root->right);
       return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
   }
   ```

**3. Print Elements:**

   Pre order traversal: First current then kids

   ```c
   void print(TreeNode *root) {
       if (root == NULL) return;
       printf("%d ", root->value);
       print(root->left);
       print(root->right);
   } 
   ```

   In order traversal: First left kid then current then right kid

   ```c
   void print(TreeNode *root) {
       if (root == NULL) return;
       print(root->left);
       printf("%d ", root->value);
       print(root->right);
   }
   ```

   Post order traversal: First kids then current

   ```c
   void print(TreeNode *root) {
       if (root == NULL) return;
       print(root->left);
       print(root->right);
       printf("%d ", root->value);
}

   ```

**4. Find an Element:**

   ```c
   TreeNode* find(TreeNode *root, int value) {
       if (!root || root->value == value) return root;
       if (value < root->value) return find(root->left, value);
       return find(root->right, value);
   }
   ```

**5. Insert an Element:**

   ```c
   struct Node* createNode(int value) {
       struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
       newNode->data = value;
       newNode->left = NULL;
       newNode->right = NULL;
       return newNode;
   }

   // Function to insert a new node in the binary search tree
   struct Node* insertNode(struct Node* root, int value) {
       // If the tree is empty, return a new node
       if (root == NULL) {
           return createNode(value);
       }

       // Otherwise, recur down the tree
       if (value < root->data) {
           root->left = insertNode(root->left, value);  // Insert in left subtree
       } else {
           root->right = insertNode(root->right, value); // Insert in right subtree
       }

       // Return the (unchanged) node pointer
       return root;
   }
   ```

   **Explanation of Necessary Functions:**
      1. createNode(int value): This function allocates memory for a new node and initializes it with the given value.
      2. insertNode(struct Node* root, int value): This function inserts a new node into the binary search tree. If the tree is empty, it creates the root node. Otherwise, it recursively finds the correct position to insert the new value.

**6. Delete an Element (DIY):**

   ```c
   struct Node* createNode(int value) {
       struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
       newNode->data = value;
       newNode->left = NULL;
       newNode->right = NULL;
       return newNode;
   } 

   // Function to find the minimum value node in a given subtree
   struct Node* findMin(struct Node* root) {
       while (root->left != NULL) {
           root = root->left;
       }
       return root;
   }

   // Function to delete a node from the binary search tree
   struct Node* deleteNode(struct Node* root, int value) {
       // Base case: If the tree is empty
       if (root == NULL) {
           return root;
       }

       // Recur down the tree
       if (value < root->data) {
           root->left = deleteNode(root->left, value);  // Search in left subtree
       } else if (value > root->data) {
           root->right = deleteNode(root->right, value); // Search in right subtree
       } else {
           // Node to be deleted is found

           // Case 1: Node has no children (leaf node)
           if (root->left == NULL && root->right == NULL) {
               free(root);
               root = NULL;
           }
           // Case 2: Node has only one child
           else if (root->left == NULL) {
               struct Node* temp = root;
               root = root->right;
               free(temp);
           }
           else if (root->right == NULL) {
               struct Node* temp = root;
               root = root->left;
               free(temp);
           }
           // Case 3: Node has two children
           else {
               struct Node* temp = findMin(root->right);  // Find the minimum value in the right subtree
               root->data = temp->data;  // Replace the node's value with the inorder successor's value
               root->right = deleteNode(root->right, temp->data);  // Delete the inorder successor
           }
       }

       return root;
   }
   ``` 

   **Explanation of the Deletion Logic:**
      1. createNode(int value): Creates a new node with the given value, same as before.
      2. findMin(struct Node* root): Finds the minimum value node in the right subtree. This is used when deleting a node with two children to replace it with its inorder successor.
      3. deleteNode(struct Node* root, int value):
         I. If the value to be deleted is smaller than the current node's value, the function recursively looks in the left subtree.
         II. If the value is larger, it looks in the right subtree.
         III. If the node to be deleted is found:
         IV. If the node has no children (leaf node), it is simply deleted.
         V. If the node has one child, it is replaced by its child.
         VI. If the node has two children, it is replaced by its inorder successor (the smallest node in the right subtree), and the successor is then deleted recursively.

   **Example:**
   For the following tree:

   ```sh
       50
      /  \
    30    70
   /  \   /  \
  20  40 60  80
   ```
   Deleting 70 will replace it with its inorder successor (80), and 80 will be removed from the tree.
   Deleting 30 will replace it with 40 (since 30 has two children, and the minimum value in the right subtree is 40).

# Quicksort Algorithm

**Definition:** Quicksort is a divide-and-conquer algorithm that partitions an array around a pivot element and recursively sorts the subarrays.

**Code Example:**
```c
#include <stdio.h>

void quicksort(int *arr, int low, int high) {
    if (low < high) {
        int pivot = arr[(low + high) / 2];
        int i = low, j = high;
        while (i <= j) {
            while (arr[i] < pivot) i++;
            while (arr[j] > pivot) j--;
            if (i <= j) {
                int temp = arr[i];
                arr[i++] = arr[j];
                arr[j--] = temp;
            }
        }
        quicksort(arr, low, j);
        quicksort(arr, i, high);
    }
}

int main() {
    int arr[] = {9, 7, 5, 11, 12, 2, 14, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    printf("Before sorting:\n");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");

    quicksort(arr, 0, n - 1);

    printf("After sorting:\n");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");

    return 0;
}
```
**Output:**
```
Before sorting:
9 7 5 11 12 2 14 3
After sorting:
2 3 5 7 9 11 12 14
```

---

# Mergesort Algorithm

**Definition:** Mergesort is a divide-and-conquer algorithm that splits the array into halves, recursively sorts them, and then merges the sorted halves.

**Code Example:**
```c
#include <stdio.h>

void merge(int *arr, int l, int m, int r) {
    int n1 = m - l + 1, n2 = r - m;
    int left[n1], right[n2];

    for (int i = 0; i < n1; i++) left[i] = arr[l + i];
    for (int j = 0; j < n2; j++) right[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (left[i] <= right[j]) arr[k++] = left[i++];
        else arr[k++] = right[j++];
    }
    while (i < n1) arr[k++] = left[i++];
    while (j < n2) arr[k++] = right[j++];
}

void mergesort(int *arr, int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergesort(arr, l, m);
        mergesort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

int main() {
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Before sorting:\n");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");

    mergesort(arr, 0, n - 1);

    printf("After sorting:\n");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");

    return 0;
}
```
**Output:**
```
Before sorting:
38 27 43 3 9 82 10
After sorting:
3 9 10 27 38 43 82
```

# File Manipulation Functions

**Opening a File:**

Files can be opened in different modes:
  --r: Read (file must exist).
  --w: Write (creates a new file or truncates an existing one).
  --a: Append (adds to the end of the file, creating it if it doesn't exist).
  --r+: Read and write.
  --w+: Write and read (overwrites existing content).
  --a+: Append and read.

  ```c
  FILE *file = fopen("example.txt", "r"); 
  if (!file) {
     perror("Error opening file");
  }
  ```

**Reading and Writing:**

1. `fgets` for reading a line:

  ```c
  char buffer[100];
  fgets(buffer, sizeof(buffer), file);
  ```

2. `fprintf` for writing:

  ```c
  FILE *file = fopen("output.txt", "w");
  fprintf(file, "Hello World\n");
  fclose(file);
  ```

3. `fscanf` for formatted input:

  ```c
  int x;
  fscanf(file, "%d", &x);
  ```

4. `fputc` and `fgetc`: Write and read a single character.

  ```c
  fputc('A', file);
  char c = fgetc(file);
  ```

5. `fwrite` and `fread`: Write and read binary data.

  ```c
  int numbers[] = {1, 2, 3};
  fwrite(numbers, sizeof(int), 3, file);
  fread(numbers, sizeof(int), 3, file);
  ```

6. `ftell` and `fseek`: Tell and move the file pointer.

  ```c
  long position = ftell(file); // Get current position
  fseek(file, 10, SEEK_SET);   // Move to the 10th byte
  ```

7. `fclose`: Close the file when done.

  ```c
  fclose(file);
  ```
