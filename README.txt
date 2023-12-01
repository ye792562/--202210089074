 #define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <time.h>

#define MAX_LEN 16

void encrypt(char* intut_password, char* output_password);
void decrypt(char* password, char* decrypted_password);
void judge_passwordstrength(char *passsword);
void generatePassword(int type,char* genertepassword);
int main() {
    char password[MAX_LEN + 1];
    char encrypted_password[MAX_LEN + 1];
    char decrypted_password[MAX_LEN + 1];
    char generate_password[MAX_LEN + 1];
    int choice,num;
    printf("==============================\n");
    printf("欢迎陈卓权hh使用密码管理系统\n");
    printf("==============================\n");
    printf("请选择操作: \n");
    printf("1. 加密\n");
    printf("2. 解密\n");
    printf("3. 判断密码强度\n");
    printf("4. 密码生成\n");
    printf("5. 退出\n");
    while (1) {
        printf("输入你的选择:\n ");
        scanf("%d", &choice);
        switch (choice) {
        case 1:
            printf("==============================\n");
            printf("欢迎使用密码管理系统\n");
            printf("==============================\n");
            printf("请输入要加密的数字密码：");
            scanf("%s", password);
            encrypt(password, encrypted_password);
            printf("加密后的结果是：%s\n", encrypted_password);
            break;
        case 2:
            printf("==============================\n");
            printf("欢迎使用密码管理系统\n");
            printf("==============================\n");
            printf("请输入要解密的数字密码：");
            scanf("%s", password);
            decrypt(password, decrypted_password);
            printf("解密后的结果是：%s\n", decrypted_password);
            break;
        case 3:
            printf("==============================\n");
            printf("欢迎使用密码管理系统\n");
            printf("==============================\n");
            printf("请输入需要判断密码强度的密码：");
            scanf("%s", password);
            judge_passwordstrength(password);
            break;
        case 4:
            printf("==============================\n");
            printf("欢迎使用密码管理系统\n");
            printf("==============================\n");
            printf("请输入需要生成的密码长度：");
            scanf("%d", &num);
            generatePassword(num, generate_password);
            printf("生成的密码为：%s\n", generate_password);
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

    for (int i = 0; i < len / 2; i++) {
        char temp = output_password[i];
        output_password[i] = output_password[len - i - 1];
        output_password[len - i - 1] = temp;
    }
}
    void decrypt(char* input_password, char* output_password) {
        int len = strlen(input_password);
        strcpy(output_password, input_password);
        for (int i = 0; i < len / 2; i++) {
            char temp = output_password[i];
            output_password[i] = output_password[len - i - 1];
            output_password[len - i - 1] = temp;
        }
        strcpy(input_password, output_password);
        output_password[0] = input_password[len - 1];
        output_password[len - 1] = input_password[0];
        for (int i = 0; i < len; i++)
            output_password[i] = output_password[i] - i - 1 - 3;
    }
    void judge_passwordstrength(char* password)
    {
        int judge_number=0,judge_supper=0,judge_lower=0;
        int len = strlen(password);
        for (int i = 0;i < len;i++) {          
            if (isdigit(password[i]))
                judge_number = 1;
             if (isupper(password[i]))
                judge_supper = 1;
             if (islower(password[i]))
                judge_lower = 1;
        }
        if (len < 8)
            printf("弱强度\n");
        else if ((judge_number && judge_supper && judge_lower) == 1)
            printf("高强度\n");
        else if (((judge_supper || judge_lower)==1) && judge_number == 1)
            printf("中强度\n");    
        else
            printf("弱强度\n");
    }
    void generatePassword(int num,char* generate_password)
    {
        srand(time(NULL));
        for (int i = 0;i < num;i++)
        {
            int type = rand() % 3;
            if (type == 0)
                generate_password[i] = 'a' + rand() % 26;
            if(type == 1)
                generate_password[i] = 'A' + rand() % 26;
            if(type == 2)
                generate_password[i] = '0' + rand() % 10;
        }
        generate_password[num] = '\0';
    }
