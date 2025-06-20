# teste
teste

```
#include <stdio.h>

#define N 100

int main() {
    int i, j, temp;
    int arr[N];

    // Inicializa o vetor em ordem decrescente
    for (i = 0; i < N; i++)
        arr[i] = N - i;

    // Bubble Sort
    for (i = 0; i < N - 1; i++) {
        for (j = 0; j < N - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    // Imprime primeiro e último elemento para evitar otimização excessiva
    printf("Min: %d Max: %d\n", arr[0], arr[N-1]);
    return 0;
}



########################



#include <stdio.h>
#include <stdlib.h>

#define N 100

typedef struct node {
    int value;
    struct node *left, *right;
} Node;

Node* insert(Node* root, int value) {
    if (!root) {
        Node* node = malloc(sizeof(Node));
        node->value = value;
        node->left = node->right = NULL;
        return node;
    }
    if (value < root->value)
        root->left = insert(root->left, value);
    else
        root->right = insert(root->right, value);
    return root;
}

int search(Node* root, int value) {
    if (!root) return 0;
    if (root->value == value) return 1;
    if (value < root->value) return search(root->left, value);
    else return search(root->right, value);
}

int main() {
    Node* root = NULL;

    // Inserindo elementos
    for (int i = 0; i < N; i++)
        root = insert(root, i * 2);

    // Busca por elementos existentes e inexistentes
    int hits = 0;
    for (int i = 0; i < 2 * N; i++) {
        hits += search(root, i);
    }

    printf("Encontrados: %d\n", hits);
    return 0;
}




############




#include <stdio.h>
#include <math.h>

#define PI 3.14159265358979323846
#define N 64

typedef struct {
    double real;
    double imag;
} Complex;

Complex x[N];

void compute_fft() {
    for (int k = 0; k < N; k++) {
        Complex sum = {0.0, 0.0};
        for (int n = 0; n < N; n++) {
            double angle = 2 * PI * k * n / N;
            sum.real += cos(angle) * x[n].real + sin(angle) * x[n].imag;
            sum.imag += -sin(angle) * x[n].real + cos(angle) * x[n].imag;
        }
        x[k] = sum;
    }
}

int main() {
    for (int i = 0; i < N; i++) {
        x[i].real = i;
        x[i].imag = 0.0;
    }

    compute_fft();

    // Imprime um valor para impedir otimização excessiva
    printf("FFT[0] = %f + %fi\n", x[0].real, x[0].imag);
    return 0;
}




```