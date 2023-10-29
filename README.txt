#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX_LEN 20

void encrypt(char* input_password, char* output_password);
void decrypt(char* input_password, char* output_password);

int main() {
    int choice;
    char password[MAX_LEN + 1];
    char encrypted_password[MAX_LEN + 1];
    char decrypted_password[MAX_LEN + 1];

    printf("==============================\n");
    printf("欢迎使用密码管理系统\n");
    printf("==============================\n");
    printf("请选择操作：\n");
    printf("1. 加密\n");
    printf("2. 解密\n");
    printf("5. 退出\n");

    while (1) {
        printf("请输入选项序号: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            printf("==============================\n");
            printf("欢迎使用密码管理系统\n");
            printf("==============================\n");
            printf("请输入要加密的数字密码： ");
            scanf("%s", password);
            encrypt(password, encrypted_password);
            printf("加密后的结果是： %s\n", encrypted_password);
            break;
        case 2:
            printf("==============================\n");
            printf("欢迎使用密码管理系统\n");
            printf("==============================\n");
            printf("输入需要解密的密码： ");
            scanf("%s", password);
            decrypt(password, decrypted_password);
            printf("解密后的密码是: %s\n", decrypted_password);
            break;
        case 5:
            printf("Goodbye!\n");
            exit(0);
        default:
            printf("Invalid choice. Please try again.\n");
            break;
        }
    }

    return 0;
}

void encrypt(char* input_password, char* output_password) {
    int len = strlen(input_password);

    for (int i = 0; i < len; i++) 
      input_password[i] = input_password[i] + i + 1 + 3;

    strcpy(output_password, input_password);

    output_password[0] = input_password[len - 1];
    output_password[len - 1] = input_password[0];