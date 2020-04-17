# LinkedQueue
#include <stdio.h>
#include <malloc.h>
int count = 0;

struct node {
	int info;
	struct node* ptr;
}*front, *rear, *temp, *front1;

int frontelement();
void enq(int data);
void deq();
void empty();
void display();
void create();
void queuesize();

int main() {
	int choice = -1;
	int data = -1;
	printf("1 - Enque\n");
	printf("2 - Deque\n");
	printf("3 - Front element\n");
	printf("4 - Empty\n");
	printf("5 - Exit\n");
	printf("6 - Display\n");
	printf("7 - Queue size\n");
	while (1) {
		printf("Enter choice : ");
		scanf_s("%d", &choice);
		switch (choice) {
		case 1:
			printf("Enter data : ");
			scanf_s("%d", &data);
			enq(data);
			printf("\n");
			break;
		case 2:
			deq();
			printf("\n");
			break;
		case 3:
			printf("Front element : %d", frontelement());
			printf("\n");
			break;
		case 4:
			printf("Empty or Not Empty\n");
			empty();
			printf("\n");
			break;
		case 5:
			exit(0);
		case 6:
			display();
			printf("\n");
			break;
		case 7:
			queuesize();
			printf("\n");
			break;
		default:
			printf("wrong number\n");
			break;
		}
	}
}

void display() {
	front1 = front;

	if ((front1 == NULL) && (rear == NULL)) {
		printf("Queue is empty\n");
		return;
	}
	while(front1 != rear) {
		printf("%d ", front1->info);
		front1 = front1->ptr;
	}
	if (front1 == rear) {
		printf("%d", front1->info);
	}
}

int frontelement() {
	if ((front != NULL) && (rear != NULL))
		return (front->info);
	else
		return 0;
}

void create() {
	front = rear = NULL;
}

void empty() {
	if (front == rear)
		printf("\n empty\n");
	else
		printf("\n not empty\n");
}

void queuesize() {
	printf("\n Queue size : %d", count);
}

void enq(int data) {
	if (rear == NULL) {
		rear = (struct node*)malloc(1 * sizeof(struct node));
		rear->ptr = NULL;
		rear->info = data;
		front = rear;
	}
	else {
		temp = (struct node*)malloc(1 * sizeof(struct node));
		rear->ptr = temp;
		temp->info = data;
		temp->ptr = NULL;

		rear = temp;
	}
	count++;
}

void deq() {
	front1 = front;

	if (front1 == NULL) {
		printf("\n Error: Trying to display elements from empty queue");
		return;
	}
	else
		if (front1->ptr != NULL) {
			front1 = front1->ptr;
			printf("\n Deque value : %d", front->info);
			free(front);
			front = front1;
		}
		else {
			printf("\n Deque value : %d", front->info);
			free(front);
			front = NULL;
			rear = NULL;
		}
	count--;
}
