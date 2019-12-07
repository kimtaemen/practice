#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>//없으면 오류나서 넣었다.
#include<time.h>

int printer(int user_input[9][9])
{

	int index = 9;
	printf("     ");  // 맨위 가로줄 123456789와 바로 다음줄의 배열의 줄을 예쁘게 맞추기 위해 처음에 한칸 띄었다.
	for (int j = 0; j < index; j++) { printf("%2d", j + 1); } // 맨 위 가로줄에 123456789 표시
	printf("\n");
	for (int j = 0; j <= index + 1; j++) { printf("--"); } // 맨위 123456789 밑에 경계선 표시
	printf("\n");

	for (int i = 0; i < 9; i++)
	{
		printf("%2d | ", i + 1); // 맨왼쪽에 표시하기 위한 세로줄 및 숫자
		for (int j = 0; j < 9; j++)
		{
			printf("%2d", user_input[i][j]); //user 배열 표시
		}
		printf("\n");
	}
}

int FuncOne(int user_input[9][9], int right_input[9][9])  // 스도쿠 푼 문제와 정답 비교
{
	int i, j;
	int is_ok = 0;
	for (i = 0; i < 9; i++)
	{
		for (j = 0; j < 9; j++)
		{
			if (user_input[i][j] != right_input[i][j])
			{
				is_ok = 1;
				break;
			}

		}
	}


	if (is_ok == 0) { printf("정답 \n"); }
	else { printf("정답이 아닙니다. \n"); }

	printf("게임종료!! \n");
	system("pause"); // 프로그램 종료 안되게 하는것

}





int main() // void는 없어도 된다는 점.
{
	int i = 0, j = 0, num;
	int user_input[9][9] =                   // 스도쿠 문제 배열
	{
	 {2,3,5,1,4,7,9,8,6},
	 {4,1,8,9,6,5,7,2,3},
	 {6,9,7,2,8,3,1,4,5},
	 {9,8,6,5,7,4,2,3,1},
	 {5,7,3,8,1,2,4,6,9},
	 {1,4,2,6,3,9,8,5,7},
	 {7,5,9,3,2,8,6,1,4},
	 {8,6,4,7,5,1,3,9,2},
	 {3,2,1,4,9,6,5,7,8}
	};
	int right_input[9][9] =                // 스도쿠 정답 배열
	{
	 {2,3,5,1,4,7,9,8,6},
	 {4,1,8,9,6,5,7,2,3},
	 {6,9,7,2,8,3,1,4,5},
	 {9,8,6,5,7,4,2,3,1},
	 {5,7,3,8,1,2,4,6,9},
	 {1,4,2,6,3,9,8,5,7},
	 {7,5,9,3,2,8,6,1,4},
	 {8,6,4,7,5,1,3,9,2},
	 {3,2,1,4,9,6,5,7,8}
	};
	int c[9][9];

	printf("start.\n");



	srand(time(NULL)); //랜덤함수 시작

	int	re = 0;
	re = rand() % 10;  // 범위 0~9
	int num1 = 12;

	while (num1 > re) // 랜덤함수 여러번 돌려 
	{
		i = rand() % 10;
		j = rand() % 10; // 배열의 가로, 세로줄 랜덤으로 선택
		int origin_x = user_input[i][j];
		user_input[i][j] = 0; //선택된 배열 자리에 0 채워 넣어.
		printf("i => %d, j => %d, origin => %d, => %d\n", i, j, origin_x, user_input[i - 1][j - 1]);
		num1--;

	}
	printer(user_input);


	num = 0;
	int sum = 5;
	while (sum > 0)
	{


		printf("choice index x and y  ex)2 1 \n"); //배열의 세로 가로줄 선택
		scanf("%d %d", &i, &j);

		if (user_input[i - 1][j - 1] != 0) { printf("옳지 않은 위치입니다. \n"); } //0이 아닌 정답이 들어가있는 수를 선택한 경우
		else if (user_input[i - 1][j - 1] == 0) //0이 들어가 있는(정답을 넣어야 하는)위치를 선택한 경우
		{
			printf("숫자를 입력하세요: \n");
			scanf("%d", &num);
			//for (j = 0; j < 9; j++) { printf("1 2 3 4 5 6 7 8 9\n%2d", user_input[i][j]); } // 뭐지 이건***************

			user_input[i - 1][j - 1] = num; //*** 화면에서 또 배열이 추가되는 것이 아닌(스도쿠 배열이 한개, 두개... 점점 늘어남.) 기존의 스도쿠에서 해당(0)숫자만 바꾸게 하는법...

		}
		else { printf("장난하지 마시오 \n"); } //11, 12 등 엉뚱한 수를 넣은 경우

		user_input[i - 1][j - 1] = num;

		sum--;
		system("cls");
		printer(user_input);

	}


	FuncOne(user_input, right_input); // 다 풀고나서 정답과 비교

}
