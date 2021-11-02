#include <iostream>
#include <string>
#include <stdlib.h>
#include <iomanip>

using namespace std;

int n;	//The number of operations

void cout_fix(double x)
{
	if(int(x) == x)
	{
		cout << x << ".0" << endl;
	}
	else
	{
		cout << x << endl;
	}
}

struct node
{
	double value;
	node * right;
	node * left;
	int height;	
};

typedef struct node *root;

class AVL
{
	public:
		int h(root &r)
		{
			if(r == NULL)
				return -1;
			else
				return r->height;	
		}
		int BalanceFactor(root &r)
		{
			return h(r->left) - h(r->right);
		}
		void add(double, root &);
		root rotate_right(root &);
		root rotate_left(root &);
		root rotate_left_right(root &);
		root rotate_right_left(root &);
		void find(double, root &, double);
		void remove (double, root &);
		root balance(root &);
};

root AVL::balance(root & u)
{
	int BF = BalanceFactor(u);
	if(BF < -1)
	{
		cout << "balancing ";
		cout_fix(u->value);
		if (BalanceFactor(u->right) > 0)
		{
			u->right = rotate_left(u->right);
			u = rotate_left(u);
		}
		else
		{
			u = rotate_left(u);
		}
	}
	else if(BF > 1)
	{
		cout << "balancing ";
		cout_fix(u->value);
		if (BalanceFactor(u->left) >= 0)
		{
			u = rotate_right(u);
		}
		else
		{
			u->left = rotate_left(u->left);
			u = rotate_right(u);
		}
	}
	return u;
}

void AVL::add(double x, root & r)
{
	if(r == NULL)
	{
		r = new node;
		r->value = x;
		r->left = NULL;
		r->right = NULL;
		cout << "added" << endl;
	}
	else
	{
		if(x < r->value)
		{
			add(x, r->left);
			r = balance(r);
		}
		else if(x > r->value)
		{
			add(x, r->right);
			r = balance(r);
		}
		else
		{
			cout << "already in there" << endl;
		}
	}
	r->height = 1 + max(h(r->left) , h(r->right));
}

root AVL::rotate_right(root &r1) 	//rotate right
{
	root r2;
	r2 = r1->left;
	r1->left = r2->right;
	r2->right = r1;
	r1->height = max(h(r1->left) , h(r1->right)) + 1;
	r2->height = max(h(r2->left),h(r2->left)) + 1;
	return r2;
}

root AVL::rotate_left(root &r1) 	//rotate left
{
	root r2;
	r2 = r1->right;
	r1->right = r2->left;
	r2->left = r1;
	r1->height = max(h(r1->left) , h(r1->right)) + 1;
	r2->height = max(h(r2->left) , h(r2->right)) + 1;
	return r2;
}


root AVL::rotate_left_right(root &r1) 	//First rotate left then rotate right
{
	r1->left = rotate_left(r1->left);
	return rotate_right(r1);
}

root AVL::rotate_right_left(root &r1) 	//First rotate right then rotate left
{
	r1->right = rotate_right(r1->right);
	return rotate_left(r1);
}

void AVL::find(double x, root & r, double result)
{
	if(r == NULL)
	{
		if(result == -1)
			cout << "not found" << endl;
		else
			cout_fix(result);	
	}
	else
	{
		if(x < r->value)
		{
			result = r->value;
			find(x, r->left, result);
		}
		else if (x > r->value)
		{
			find(x, r->right, result);
		}
		else	//Founded!
		{
			cout_fix(x);
		}
	}
}

void AVL::remove(double x, root & r)
{
	root r2;
	if(r == NULL)
	{
		cout << "does not exist" << endl;
	}
	else
	{
		if(x < r->value)
		{
			remove(x, r->left);
			r->height = max(h(r->left) , h(r->right)) + 1;
			r = balance(r);
		}
		else if(x > r->value)
		{
			remove(x, r->right);
			r->height = max(h(r->left) , h(r->right)) + 1;
			r = balance(r);
		}
		else
		{
			if( (r->left == NULL) && (r->right == NULL) )
			{
				r2 = r;
				free(r2);
				r = NULL;
				cout << "removed" << endl;
			}
			else if(r->left == NULL)
			{
				r2 = r;
				free(r2);
				r = r->right;
				cout << "removed" << endl;
			}
			else if(r->right == NULL)
			{
				r2 = r;
				free(r2);
				r = r->left;
				cout << "removed" << endl;
			}
			else	//no subtree is NULL
			{
				r2 = r->left;
				while(r2->right != NULL)
				{
					r2 = r2->right;
				}
				r->value = r2->value;
				remove(r2->value, r->left);
				r = balance(r);
			}
		}
	}
}

int main()
{
	cin >> n;
	string operation;
	double value;
	
	root ROOT;
	AVL avlTree;
	ROOT = NULL;
	
	while(n--)
	{
		cin >> operation >> value;
		if (operation == "add")
		{
			avlTree.add(value, ROOT);
		}
		else if (operation == "remove")
		{
			avlTree.remove(value, ROOT);
		}
		else if(operation == "find")
		{
			avlTree.find(value, ROOT, -1);
		}
	}
	return 0;
}
