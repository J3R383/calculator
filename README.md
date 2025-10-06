#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX_NUMBERS 100

int main() {
    char input[256];
    //incresed buffer size for safety
    float numbers[MAX_NUMBERS];
    char *token;
    char operation;
    int count = 0;
    float result = 0.0f;
    printf("Enter your input (e.g., 1, 2, 3,...)\n");
    fgets(input, sizeof(input), stdin);
    //remove trailing newline if present
    input[strcspn(input, "\n")] = 0;
    token = strtok(input, ", ");
    while (token != NULL) {
        numbers[count++] = atof(token);
        token = strtok(NULL, ", ");
    }
    printf("choose the operation (+, -, *, /)\n");
    scanf(" %c", &operation);
    //note the space before %c to consume any leftover newline
    result = numbers[0];
    //initialize result with the first number
    for (int i = 1; i < count; i++) {
        switch (operation) {
            case '+':
                result += numbers[i];
                break;
            case '-':
                result -= numbers[i];
                break;
            case '*':
                result *= numbers[i];
                break;
            case '/':
                if (numbers[i] == 0) {
                    printf("Division by zero is not allowed\n");
                    return 1;
                //indicate an error
                }
                break;
            default:
                printf("Invalid operation\n");
                return 1;
                //indicate an error
            }
        }
        printf("Result: %.2f\n", result);
        return 0;
}
