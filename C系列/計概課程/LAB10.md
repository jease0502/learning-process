---
tags: 計概
---

# LAB10


## stack
```cpp=
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAXSTACK 5

typedef struct{
	int arr[MAXSTACK];
	int top;
}stack;

//確認堆疊是否為空
int is_empty(stack* s){
	if(s->top == -1)	return 1;
	else	return 0;
}

int top(stack *s)
{
	if (s->top == -1)
	{
		printf("-1\n");
	}
	else
	{
		printf("%d\n",s->arr[s->top]);
    	return (s->arr[s->top]);
	}
}

//確認堆疊是否為滿
int is_full(stack* s){
	if(s->top == MAXSTACK-1)	return 1;
	else	return 0;
}

//依序印出堆疊內容
void print(stack* s){
    int i;
    for (i=0; i<=s->top; i++)
    {
        printf("%d",s->arr[i]);
    	if (i== s->top)
    	{
    		printf("\n");
    	}
    	else printf(" ");
    }
}

//從top新增
void push(stack* s, int add){
	if(is_full(s))	printf("Stack is full!\n");
	else{
		s->arr[++s->top] = add;
	}
}

//從top刪除
int pop(stack* s)
{
	if(is_empty(s))	printf("Stack is empty!\n");
	else	return s->arr[s->top--];
}

int main(){
	stack s;
	s.top = -1;
	char input[20];
	int i;
	while(scanf("%s",input) != EOF){
		if(strcmp(input,"push") == 0){
			scanf("%d",&i);
			push(&s, i);
		}else if(strcmp(input,"pop") == 0){
			pop(&s);
		}else if(strcmp(input, "is_empty") == 0){
			if(is_empty(&s))	printf("True\n");
			else	printf("False\n");
		}else if(strcmp(input,"print") == 0){
			print(&s);
		}else if(strcmp(input,"top")==0){
			top(&s);
		}
	}
	return 0;
}

```

## linklist

```cpp=
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct node{
	int num;
	struct node* nptr;
}Node;

Node* creat_node(int num){
	Node* tmp = (Node*)malloc(sizeof(Node));
	tmp->num = num;
	tmp->nptr = NULL;
	return tmp;
}

Node* insert_node(Node* head, int num){
	Node* newNode = creat_node(num);
	Node* tmp = head;

	if(head == NULL){
		head = newNode;
	}else{
		while(tmp->nptr != NULL)	tmp = tmp->nptr;
		tmp->nptr = newNode;
	}
	return head;
}

Node* insert_node_front(Node* head, int num){
	Node* newNode = creat_node(num);
	Node* tmp = head;

	if(head == NULL){
		head = newNode;
	}else{
		newNode->nptr = head;
		head = newNode;
	}

	return head;

}



Node* search_node(Node* head, int want){
	Node* tmp = head;

	while(tmp != NULL){
		if(tmp->num == want)	return tmp;
		else	tmp = tmp->nptr;
	}
	return NULL;
}

Node* search_node_before_node(Node* head, Node* want){
	Node* tmp = head;

	while(tmp != NULL){
		if(tmp->nptr == want)	return tmp;
		else	tmp = tmp->nptr;
	}
	return NULL;
}

Node* delete_node(Node* head){
	Node* tmp = head;
	Node* del;

	if(head == NULL){
		printf("No data!\n");
	}else if(head->nptr == NULL){
		head = NULL;
		free(tmp);
	}else{
		while(tmp->nptr->nptr != NULL)	tmp = tmp->nptr;
		del = tmp->nptr;
		free(del);
		tmp->nptr = NULL;
	}
	return head;
}

Node* delete_node_front(Node* head){
	Node* tmp = head;

	if(head == NULL){
		printf("No data!\n");
	}else if(head->nptr == NULL){
		head = NULL;
		free(tmp);
	}else{
		head = head->nptr;
		free(tmp);
	}
	return head;
}

Node* delete_int(Node* head, int del){
	Node* tmp = head;
	Node* wantDel = search_node(head, del);

	if(head == NULL)	printf("No data!\n");
	else if(wantDel == NULL)	printf("No Number!\n");
	else if(head == wantDel){
		head = wantDel->nptr;
		free(wantDel);
	}else{
		tmp = search_node_before_node(head, wantDel);
		tmp->nptr = wantDel->nptr;
		free(wantDel);
	}
	return head;
}

void print(Node* head){
	Node* tmp = head;

	if(head == NULL)	printf("No data!\n");
	while(tmp != NULL)
	{
		printf("%p %d %p\n",tmp,tmp->num,tmp->nptr);
		tmp = tmp->nptr;
	}
}

int main(){
	Node* head = NULL;
	Node* tmp_search;
	char input[20];
	int i;

	while(scanf("%s", &input) != EOF){
		if(strcmp(input, "append") == 0){
			scanf("%d", &i);
			head = insert_node(head, i);
		}else if(strcmp(input, "delete") == 0){
			scanf("%d", &i);
			head = delete_int(head, i);
		}else if(strcmp(input, "check") == 0){
			scanf("%d", &i);
			tmp_search = search_node(head, i);
			if(tmp_search == NULL)	printf("False\n");
			else	printf("True\n");
		}else if(strcmp(input, "print") == 0){
			print(head);
		}
	}
	return 0;
}

```


## binary

```cpp=
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct node{
    int num;
    struct node* rptr;
    struct node* lptr;
}Node;

//生成
Node* creat(int num){
    Node* tmp = (Node*)malloc(sizeof(Node));

    tmp->num = num;
    tmp->rptr = NULL;
    tmp->lptr = NULL;

    return tmp;
}

//新增node
Node* insert_node(Node* root, Node* newNode){
    Node* tmp = root;
    if(root == NULL)    root = newNode;
    else{
        while(1){
            if(tmp->num > newNode->num){
                if(tmp->lptr == NULL){
                    tmp->lptr = newNode;
                    break;
                }else   tmp = tmp->lptr;
            }else if(tmp->num < newNode->num){
                if(tmp->rptr == NULL){
                    tmp->rptr = newNode;
                    break;
                }else   tmp = tmp->rptr;
            }
        }
    }
    return root;
}

//找node並回傳node
Node* search_node(Node* root, int want){
    Node* tmp = root;
    while(tmp != NULL){
        printf("%d ", tmp->num);
        if(tmp->num == want)    return tmp;
        else if(tmp->num > want)    tmp = tmp->lptr;
        else    tmp = tmp->rptr;
    }
    return NULL;
}

int main(){
    Node* root = NULL;
    char input[20];
    int i;
    while(scanf("%s",&input) != EOF){
        if(strcmp(input, "add") == 0){
            scanf("%d", &i);
            root = insert_node(root, creat(i));
        }else if(strcmp(input, "search") == 0){
            scanf("%d", &i);
            if(search_node(root, i) == NULL)    printf("False\n");
            else    printf("True\n");
        }
    }
    return 0;
}
```