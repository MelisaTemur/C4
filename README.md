# C4
Using Push Pop functions
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

struct Stack {
	int top;
	unsigned capacity;
	int* array;
};

struct Stack* createStack(unsigned capacity)
{
	struct Stack* stack = (struct Stack*)malloc(sizeof(struct Stack));
	stack->capacity = capacity;
	stack->top = -1;
	stack->array = (int*)malloc(stack->capacity * sizeof(int));
	return stack;
}

int isFull(struct Stack* stack)
{
	return stack->top == stack->capacity - 1;
}

int isEmpty(struct Stack* stack)
{
	return stack->top == -1;
}

void push(struct Stack* stack, int item)
{
	if (isFull(stack))
		return;
	stack->array[++stack->top] = item;
}

int pop(struct Stack* stack)
{
	if (isEmpty(stack))
		return INT_MIN;
	return stack->array[stack->top--];
}

int peek(struct Stack* stack)
{
	if (isEmpty(stack))
		return INT_MIN;
	return stack->array[stack->top];
}

int main()
{
	struct Stack* stack = createStack(100);
	
	char word[100] = {'\0'};
	printf("Enter myMath statement: ");
	fgets(word, 100, stdin);
	
	int i;
	for ( i = 0; i < 100; i++)
	{
		if (word[i] == '\0')
			break;

		if (isdigit(word[i]) > 0)
		{
			int val = word[i] - '0';
			push(stack, val);
		}

		if(word[i] == '+' || word[i] == '-' || word[i] == '*' || word[i] == '/')
		{
			int b = pop(stack);
			int a = pop(stack);
			if (word[i] == '+')
			{
				push(stack,a + b);
			}
			if (word[i] == '-')
			{
				push(stack, a - b);
			}
			if (word[i] == '*')
			{
				push(stack, a * b);
			}
			if (word[i] == '/')
			{
				push(stack, a / b);
			}
		}
	}

	int result = pop(stack);
	printf("Result of myMath statement: %d", result);
	return 0;
}
