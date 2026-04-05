#include<stdio.h>
#include<stdlib.h>
#include<string.h>

struct tdata{
	char bookName[51];
	struct tdata *next;
}*head=NULL, *tail=NULL, *curr=NULL;

void pushFront(char bookName[]){
	//preparing the new node
	struct tdata *newNode = (struct tdata*)malloc(sizeof(struct tdata));
	strcpy(newNode->bookName, bookName);
	newNode->next = NULL;
	
		//if the linked list is empty
	if(head == NULL){
		head = tail = newNode;
	}
	else{
		newNode->next=head;
		head = newNode;
	}
}

void pushBack(char bookName[]){
	//preparing the newnode
	struct tdata *newNode =(struct tdata*)malloc(sizeof(struct tdata));
	strcpy(newNode->bookName, bookName);
	newNode->next = NULL;
	
	//if the linked list is empty
	if(tail == NULL){
		head = tail = newNode;
	}
	else{
		tail->next = newNode;
		tail = newNode;
		tail->next = NULL; //just in case
	}
}

void viewAllData(){
	if(head == NULL){
		printf("EMPTY\n");
	}
	else{
		//traverse all the node in the linked list from head
		curr = head;
		while(curr!=NULL){
			if(curr==tail)
				printf("%s\n", curr->bookName);
			else
				printf("%s, ", curr->bookName);
			curr = curr->next;
		}
	}
}

void popFront(){
	//if the linked is empty
	if(head == NULL) return;
	//if there's only one node
	else if(head == tail){
		head = tail = NULL;
	}
	//if there's more than one node
	else{
		curr = head;
		head = head->next;
		free(curr);
	}
}

void popBack(){
    if(head == NULL)return;
    
    else if (head == tail){
        head = tail = NULL;
    }
    else{
        struct tdata *prev = head;

        while(prev->next != tail){
            prev = prev->next;
        }

        curr = tail;
        tail = prev;
        tail->next = NULL;
        free(curr);
    }
}

int main(){
	// ask how many operations
	int N;
	scanf("%d", &N);
	
	//input the operation
	int i, menu;
	char bookName[51];
	for(i = 0; i < N; i++){
		scanf("%d", &menu); getchar();
			switch(menu){
				case 1:	scanf("%[^\n]", bookName); getchar();
						pushFront(bookName);
						//puts("Push Back");
						break;
				case 2: popFront();
						//puts("Pop Front");
						break;	
				case 3: viewAllData();
						//puts("View");
						break;
		}		
	}
	return 0;
}

