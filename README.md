# Homework-algo-sumtree.-
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>

struct Node{
    int value;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(int x){
    struct Node* newNode=(struct Node*)malloc(sizeof(struct Node));
    newNode->value=x;
    newNode->left=NULL;
    newNode->right=NULL;
    return newNode;
}

// verify if x exists or not in the binary tree.
bool exist(struct Node* r, int x){
    if(r==NULL) return false;
    else {
        if(r->value==x) return true;
        else 
           return exist(r->left,x) || exist(r->right,x);
    }
}

// the number of nodes.
int size(struct Node* r){
    if(r==NULL) return 0;
    else return 1 + size(r->left) + size(r->right);
}

int hight(struct Node* r){
    if(r==NULL) return 0;
    else {
        int h_left = hight(r->left);
        int h_right = hight(r->right);

        if(h_left > h_right) return h_left + 1;
        else return h_right + 1;
    }
}

//   SUM OF ALL NODES
int sumTree(struct Node* root){
    if(root == NULL)
        return 0;
    return root->value 
         + sumTree(root->left) 
         + sumTree(root->right);
}

void preOrder(struct Node* r){
    //Root Left Right
    if(r!=NULL){
        printf(" %d ",r->value);
        preOrder(r->left);
        preOrder(r->right);
    }
}

void inOrder(struct Node* r){
    //Left Root Right
    if(r!=NULL){
        inOrder(r->left);
        printf(" %d ",r->value);
        inOrder(r->right);
    }
}

void postOrder(struct Node* r){
    //Left Right Root
    if(r!=NULL){
        postOrder(r->left);
        postOrder(r->right);
        printf(" %d ",r->value);
    }
}

int main(){
   struct Node* root=createNode(1);
   root->left=createNode(2);
   root->left->left=createNode(4);
   root->left->right=createNode(5);
   root->right=createNode(3);
   root->right->left=createNode(6);
   root->right->left->right=createNode(8);
   root->right->right=createNode(7);

   printf("\nPre-order traversal :\n");
   preOrder(root);

   printf("\nin-order traversal :\n");
   inOrder(root);

   printf("\nPost-order traversal :\n");
   postOrder(root);

   int x;
   printf("\nPlease enter a value ? ");
   scanf("%d",&x);

   if(exist(root,x)==true) printf("\n %d exists in the tree!",x);
   else printf("\n %d doesn't exist in the tree",x);

   int s = size(root);
   printf("\nThe size of the tree is %d",s);

   int h = hight(root);
   printf("\nThe height of this tree is %d",h);

   // test sumTree()
   int total = sumTree(root);
   printf("\nThe sum of all node values is %d\n", total);
}
