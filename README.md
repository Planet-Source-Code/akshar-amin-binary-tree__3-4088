<div align="center">

## Binary Tree


</div>

### Description

Advance Pointers
 
### More Info
 
Integers and Characters

This code is very useful for people who wants to learn pointers...

Everything


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Akshar Amin](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/akshar-amin.md)
**Level**          |Intermediate
**User Rating**    |3.8 (19 globes from 5 users)
**Compatibility**  |C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Data Structures](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/data-structures__3-8.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/akshar-amin-binary-tree__3-4088/archive/master.zip)





### Source Code

```

#include <iostream.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
struct node					//Node Structure basically created nodes and stores information
{							//and links the tree...
 int id;
 int phone;
 char name[100];
 node *left;
 node *right;
};
class btree				// Main Class for tree
{
public:
	node *root;			//root node
 btree();				//tree constructor
 void menu();			//main menu function
 void insert(int id, int phone, char first[100], char last[100], node *root);	//insert function passing in the root pointer
 void insert(int id, int phone, char first[100], char last[100]);				//insert function does not pass in pointer just the basic information
 node *find(int id, node *root);		// Find function passing in id and root pointer
 node *find(int id);					// Find Function passing in only ID
 void del(node *ptr, int id);			// Delete Function using pointer
 node *update(node *root, int id);		// Update Function using pointer
 void inorder(node *ptr);				// Printing inOrder
 void postorder(node *ptr);			// Printing Postorder
 void preorder(node *ptr);				// Printing Preorder
};
btree::btree()		// Constructor sets the root to NULL so won't have any garbadge
{
 root=NULL;
}
/********************** Main Menu for Binary Tree ******************************/
void btree::menu()
{
	int sel;
	btree selection;
	cout<<"********************* Binary Tree *********************"<<endl;
	cout<<"====================== Main Menu ======================"<<endl;
	cout<<"1. Insert"<<endl;
	cout<<"2. Delete"<<endl;
	cout<<"3. Find"<<endl;
	cout<<"4. Update"<<endl;
	cout<<"5. Print Inorder"<<endl;
	cout<<"6. Print Preorder"<<endl;
	cout<<"7. Print Postorder"<<endl;
	cout<<"0. Exit"<<endl;
	cout<<"Please make your selection between (0-7):";
	cin>>sel;
	int id;
	int phone;
	char first[100];
	char last[100];
	if (sel == 1)
	{
		cout<<"\nEnter a New Student's ID: ";
		cin>>id;
		cout<<"Enter Student's First Name: ";
		cin>>first;
		cout<<"Enter Student's Last Name: ";
		cin>>last;
		cout<<"Enter Student's phone Number: ";
		cin>>phone;
		insert(id, phone, first, last);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 2)
	{
		cout<<"\nEnter Student's ID: ";
		cin>>id;
		del(root, id);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 3)
	{
		cout<<"\nEnter Student's ID: ";
		cin>>id;
		find(id);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 4)
	{
		cout<<"\nEnter Student's ID: ";
		cin>>id;
		update(root, id);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 5)
	{
		cout<<"\n\n Inorder: "<<endl;
		inorder(root);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 6)
	{
		cout<<"\n\n Preorder: "<<endl;
		preorder(root);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 7)
	{
		cout<<"\n\n Postorder: "<<endl;
		postorder(root);
		cout<<"\n"<<endl;
		menu();
	}
	else if(sel == 0)
	{
		cout<<"Thank You For using my Program! BYE!!!!!!!"<<endl;
	}
	else
	{
		cout<<"\n Enter numbers between 1-7 "<<endl;
		cout<<"\n";
		menu();
	}
}
/********************** Insert Function ******************************/
void btree::insert(int id, int phone, char first[100], char last[100])
{
 if(root!=NULL)			// make sure the the root is not NULL
  insert(id, phone, first, last, root);
 else
 {							//If the entry is the root entry then it puts the entry into root
  root=new node;
  root->id=id;
	root->phone=phone;
	strcpy(root->name,first);
	strcat(root->name,last);
  root->left=NULL;
  root->right=NULL;
 }
}
/********************** Insert Function Using the Pointer passing in ******************************/
void btree::insert(int id, int phone, char first[100], char last[100], node *root)
{
 if(id< root->id)		// Checks if it should go to the right or left...
 {
  if(root->left!=NULL)			//GOES TO LEFT
   insert(id, phone, first, last, root->left);
  else
  {
   root->left=new node;
   root->left->id=id;
	 root->left->phone=phone;
	 strcpy(root->left->name,first);
	 strcat(root->left->name,last);
   root->left->left=NULL;  //Sets the left child of the child node to null
   root->left->right=NULL;  //Sets the right child of the child node to null
  }
 }
 else if(id>=root->id)			// GOES TO RIGHT
 {
  if(root->right!=NULL)
   insert(id, phone, first, last, root->right);
  else
  {
   root->right=new node;
   root->right->id=id;
	 root->right->phone=phone;
	 strcpy(root->right->name,first);
	 strcat(root->right->name,last);
   root->right->left=NULL; //Sets the left child of the child node to null
   root->right->right=NULL; //Sets the right child of the child node to null
  }
 }
}
/********************** Find Function ******************************/
node *btree::find(int id, node *root)
{
 if(root!=NULL)
 {
  if(id==root->id)		//Once found it prints out
	{
   cout<<root->id<<" "<<root->phone<<" "<<root->name<<endl;
	 return NULL;
	}
  if(id<root->id)		// if not the root then go to left and find
   return find(id, root->left);
  else				// if not the root then go to right and find
   return find(id, root->right);
 }
 else
 {
  cout<<"The ID Does not Exists in TREE"<<endl;
	return NULL;
 }
}
/********************** Find Function just passing in Root Pointer ******************************/
node *btree::find(int id)
{
 return find(id, root);
}
/********************** Delete Function ******************************/
void btree::del(node *ptr, int id)
{
	node *ptr1 = NULL;
	node *ptr2 = NULL;
	if(ptr!=NULL)
 {
  if(id==ptr->id)
	{
   if(ptr->left==NULL && ptr->right==NULL)
	 {
		 ptr = NULL;
		 cout<<"ID DELETED SUCCESSFULLY!!!"<<endl;
	}
	 else
		 cout<<"THE ROOT HAS NO CHILDREN"<<endl;
	}
  else if(id<ptr->id)
   del(ptr->left, id);
  else if(id>ptr->id)
   del(ptr->right, id);
 }
 else
 {
  cout<<"The ID Does not Exists in TREE"<<endl;
 }
}
/********************** UPdate Function ******************************/
node *btree::update(node *root, int id)
{
	char first[100];
	char last[100];
	int phone;
	if(root!=NULL)
 {
  if(id==root->id)		// once found perform the taks of chaning stuff..
	{
   cout<<root->id<<" "<<root->phone<<" "<<root->name<<endl;
	 cout << "Enter First Name: ";
		cin>>first;
		cout << "Enter Last Name: ";
		cin>>last;
		cout<<"Enter new phone number: ";
		cin>>phone;
		strcpy(root->name,first); // copy the new Surname into current->sn
		strcat(root->name,last);
		root->phone=phone;
		cout<<"ID Updated SuccessFully!!!!"<<endl;
	 return NULL;
	}
  if(id<root->id)		//finds the id to the left
   return update(root->left, id);
  else			//finds the id to the right
   return update(root->right, id);
 }
 else
 {
  cout<<"The ID Does not Exists in TREE"<<endl;
	return NULL;
 }
}
/********************** Inorder Printing Function ******************************/
void btree::inorder(node *ptr)
{
	if (ptr->left != NULL)
		inorder (ptr->left);
	cout<< ptr->id << " " <<ptr->phone<<" "<<ptr->name<<" "<<endl;
	if (ptr->right != NULL)
		inorder (ptr->right);
}
/********************** Postorder Printing Function ******************************/
void btree::postorder(node *ptr)
{
	if (ptr->left != NULL)
		postorder (ptr->left);
  if (ptr->right != NULL)
		postorder (ptr->right);
  cout<< ptr->id << " " <<ptr->phone<<" "<<ptr->name<<" "<<endl;
}
/********************** Preorder Printing Function ******************************/
void btree::preorder(node *ptr)
{
	cout<< ptr->id << " " <<ptr->phone<<" "<<ptr->name<<" "<<endl;
   if (ptr->left != NULL)
		preorder (ptr->left);
   if (ptr->right != NULL)
		preorder (ptr->right);
}
void header(int n);
/********************** Main Function ******************************/
int main ()
{
	header(2);
	btree insert;
	// Entries to Enter...
	insert.insert(5254, 5552121, "Stacy", "Sinclair");
	insert.insert(8754, 5557854, "Walter","Sobchak");
	insert.insert(4848, 5556547, "Max", "Fisher");
	insert.insert(8854, 5552424, "Flash", "Thompson");
	insert.insert(5142, 5550022, "Maude", "Lebowski");
	insert.insert(1110, 5558301, "Larry", "Sellers");
	insert.insert(6254, 5551236, "Bob", "Zimmerman");
	insert.menu();
	return 0;
}
/********************** Header Function ******************************/
void header(int n)
{
	cout<<"******************************************************"<<endl;
	cout<<"Name:		Akshar J. Amin"<<endl;
	cout<<"Homework:	Homework Assignment - "<<n<<endl;
	cout<<"Purpose:	Binary Trees using Pointers and Linked Lists"<<endl;
	cout<<"Created:	June 1st, 2002"<<endl;
	cout<<"Modified:	June 1st, 2002 Modification: NONE"<<endl;
	cout<<"******************************************************"<<endl;
	cout<<endl;
}
```

