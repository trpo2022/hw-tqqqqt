# hw-tqqqqt
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct spis{
	char fam[10];
	int num1;
	int num2;
	int num3;
	int num4;
	spis *next;
} *head, *tail, *p, *q;

struct spis1{
	char fam[10];
	int num1;
	int num2;
	int num3;
	int num4;
	spis1 *back;
	spis1 *next1;
} *heead, *taill, *pp, *qq;

void creat(struct spis *head, int n){
	int f=0;
	for(int i=0;i<n;i++){
		p=new spis;
		printf("\n \n fam - "); scanf("%s",p->fam);
		printf(" num1 - "); scanf("%d",&f); p->num1=f;
		printf(" num2 - "); scanf("%d",&f); p->num2=f;
		printf(" num3 - "); scanf("%d",&f); p->num3=f;
		printf(" num4 - "); scanf("%d",&f); p->num4=f;
		if(head->next!=NULL) tail->next=p;
		else{
			tail->next=p;
		}
		tail=p;
	}
	tail->next=NULL;
}

void creat1(struct spis1 *heead, int n){
	int f=0;
	for(int i=0;i<n;i++){
		pp=new spis1;
		printf("\n \n fam - "); scanf("%s",pp->fam);
		printf(" num1 - "); scanf("%d",&f); pp->num1=f;
		printf(" num2 - "); scanf("%d",&f); pp->num2=f;
		printf(" num3 - "); scanf("%d",&f); pp->num3=f;
		printf(" num4 - "); scanf("%d",&f); pp->num4=f;
		if(heead->next1!=NULL){
			taill->next1=pp;
			pp->back=taill;
		}
		else{
			taill->next1=pp;
		}
		taill=pp;
	}
	taill->next1=NULL;
}

void del(struct spis *head, int n){
	p=q=head->next;
	while(p!=NULL){
		p=q->next;
		free(q);
		q=p;
	}
	head->next=NULL;
}

void del1(struct spis1 *heead, int n){
	pp=qq=heead->next1;
	while(pp!=NULL){
		pp=qq->next1;
		free(qq);
		qq=pp;
	}
	heead->next1=NULL;
}

void sort(struct spis *head, int n){ 
	char obm[10];
	int flag=0;
	for(int i=0;i<n*4;i++){
		flag=0;
	for(p=head->next; p->next!=NULL ;p=p->next){
		q=p->next;
		if(strcmp(p->fam,q->fam)>0){
			strncpy(obm,p->fam,10);
			strncpy(p->fam,q->fam,10);
			strncpy(q->fam,obm,10);
			flag=1;
		}
	}
	if(flag==0) break;
	}
}

void check(struct spis1 *heead){
	for(pp=heead->next1; pp->next1!=NULL ;pp=pp->next1){
		qq=pp->next1;
		if(pp->num1<=2 || pp->num2<=2 || pp->num3<=2 || pp->num4<=2){
			qq->back=pp->back;
			qq=pp->back;
			qq->next1=pp->next1;
			free(pp);
		}
	}
}

int main(){
	int n=0;
	head=new spis; tail=new spis;е
	head->next=NULL; tail=head;
	printf(" Skolko - "); scanf("%d",&n);
	if(n>0) creat(head,n);
	printf("\n \n Spisok:");
	for(p=head->next;p;p=p->next){
		printf("\n %s - %d %d %d %d ",p->fam,p->num1,p->num2,p->num3,p->num4);
	}
	sort(head,n);
	printf("\n \n");
	printf(" Sortir: ");
	for(p=head->next;p;p=p->next){
		printf("\n %s - %d %d %d %d ",p->fam,p->num1,p->num2,p->num3,p->num4);
	}
	del(head,n);
	free(p); free(head); free(tail);
	
	heead=new spis1; taill=new spis1;
	heead->next1=NULL; taill=heead;
	printf("\n \nSkolko - "); scanf("%d",&n);
	if(n>0) creat1(heead,n);
	printf("\n \n Spisok:");
	for(pp=heead->next1;pp;pp=pp->next1){
		printf("\n %s - %d %d %d %d ",pp->fam,pp->num1,pp->num2,pp->num3,pp->num4);
	}
	check(heead); printf(" \n \n");
	for(pp=heead->next1;pp;pp=pp->next1){
		printf("\n %s - %d %d %d %d ",pp->fam,pp->num1,pp->num2,pp->num3,pp->num4);
	}
	del1(heead,n);
	free(pp); free(heead); free(taill);
	return 0;
}
