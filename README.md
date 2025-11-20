Q1 #include <iostream>
using namespace std;
class node{
    public:
    int data;
    node* left;
    node* right;
    node(int value){
        data=value;
        left=right=nullptr;
    }
};
void preorder(node*root){
    if(root==nullptr){
    return;
    }
    else{
    cout<<root->data<<" ";
    preorder(root->left);
    preorder(root->right);
        }
}
void inorder(node*root){
    if(root==nullptr){
        return;
    }
    else{
    inorder(root->left);
    cout<<root->data<<" ";
    inorder(root->right);
        }
}
void postorder(node*root){
    if(root==nullptr){
        return;
    }
    else{
    postorder(root->left);
    postorder(root->right);
    cout<<root->data<<" ";
        }
}
int main()
{
    node* root= new node(1);
    root->left= new node(3);
    root->left->left= new node(2);
    root->left->right= new node(9);
    root->right= new node(5);
    root->right->right= new node(6);
    root->right->left= new node(8);
    cout<<"Pre-order traversal: ";
    preorder(root);
    cout<<"In-order traversal: ";
    inorder(root);
    cout<<"Post-order traversal: ";
    postorder(root);
    }
Q2 a) 
#include<iostream.h>
using namespace std;
class node{
    public:
    int data;
    node* left;
    node* right;
    node(int value){
        data=value;
        left=right=nullptr;
    }
};
void searchRecursive(node* root, int key){
    if(root=nullpointer root->data=key){
      cout << "Not Found (Recursive)";
        return root;
    }
    if(root->data=key){
    cout << "Found (Recursive)";
    }
    else{
        if(key<root->data){
            return searchRecursive(root->left, key);
        }
        else{
            return searchRecursive(root->right, key);
        }
    }
}
void searchNonRecursive(node* root, int key) {
    while (root != nullptr) {
        if (root->data == key) {
            cout << "Found (Non-Recursive)\n";
            return;
        }
        if (key < root->data)
            root = root->left;
        else
            root = root->right;
    }
    cout << "Not Found (Non-Recursive)\n";
}
b)
void tree_minimum(node* root){
while(root->left != nullptr){
    root=root->left;
   }
   if(root==nullptr){
     cout << "BST is empty";
        return;
   }
}
c)
void tree_maximum(node* root){
while(root->right != nullptr){
    root=root->right;
   }
   if(root==nullptr){
     cout << "BST is empty";
        return;
   }
}
d)
void tree_Successor(node* root) {
    if (root->right != nullptr) {
        successor = tree_minimum(root->right);
        return;
    }
    node* y = root->parent;
    while (y != nullptr && root == y->right) {
        root = y;
        y = y->parent;
    }
    successor = y;
}
e)
void tree_Predecessor(node* root) {
    if (root->left != nullptr) {
        predecessor = tree_maximum(root->left);
        return;
    }
    node* y = root->parent;
    while (y != nullptr && root == y->left) {
        root = y;
        y = y->parent;
    }
    predecessor = y;
}
int main()
{
    node* root= new node(1);
    root->left= new node(3);
    root->left->left= new node(2);
    root->left->right= new node(9);
    root->right= new node(5);
    root->right->right= new node(6);
    root->right->left= new node(8);
    int key;
    cout<<"Enter key: ";
    cin>>key;
    cout<<endl;
    searchRecursive(root, key);
    searchnonRecursive(root, key);
    tree_maximum(root);
    tree_minimum(root);
    }
    Q3 #include <iostream>
using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
    Node(int k) : key(k), left(NULL), right(NULL) {}
};
Node* insert(Node* root, int key) {
    if (!root) return new Node(key);
    if (key < root->key)
        root->left = insert(root->left, key);
    else if (key > root->key)
        root->right = insert(root->right, key);
    return root;
}
Node* deleteNode(Node* root, int key) {
    if (!root) return NULL;
    if (key < root->key)
        root->left = deleteNode(root->left, key);
    else if (key > root->key)
        root->right = deleteNode(root->right, key);
    else {
        if (!root->left) {
            Node* t = root->right;
            delete root;
            return t;
        }
        if (!root->right) {
            Node* t = root->left;
            delete root;
            return t;
        }
        Node* succ = findMin(root->right);
        root->key = succ->key;
        root->right = deleteNode(root->right, succ->key);
    }
    return root;
}
int maxDepth(Node* root) {
    if (!root) return 0;
    int L = maxDepth(root->left);
    int R = maxDepth(root->right);
    return 1 + max(L, R);
}
int minDepth(Node* root) {
    if (!root) return 0;
    int L = minDepth(root->left);
    int R = minDepth(root->right);
    return 1 + min(L, R);
}
Q4 #include <iostream>
using namespace std;
class Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(NULL), right(NULL) {}
};
void BSTUtil(Node* root, int min, int max) {
    if (!root) return true;
    if (root->data <= min || root->data >= max)
        return false;
    return BSTUtil(root->left, min, root->data) &&
           BSTUtil(root->right, root->data, max);
}
bool isBST(Node* root) {
    return BSTUtil(root, INT_MIN, INT_MAX);
}
Q5
#include <iostream>
using namespace std;
class Node {
    int key;
    Node* left;
    Node* right;
    Node(int k) : key(k), left(NULL), right(NULL) {}
};
void heapify(int arr[], int n, int i) {
    int largest = i;
    int l = 2*i + 1;
    int r = 2*i + 2;
    if (l < n && arr[l] > arr[largest])
        largest = l;
    if (r < n && arr[r] > arr[largest])
        largest = r;
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}
void heapSort(int arr[], int n) {
    for (int i = n/2 - 1; i >= 0; i--) 
        heapify(arr, n, i);
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}
Q6
#include <iostream>
using namespace std;
class Node {
    int key;
    Node* left;
    Node* right;
    Node(int k) : key(k), left(NULL), right(NULL) {}
};

void heapInsert(int heap[], int &n, int val) {
    heap[n] = val;
    int i = n;
    n++;
    while (i != 0 && heap[(i-1)/2] < heap[i]) {
        swap(heap[i], heap[(i-1)/2]);
        i = (i-1)/2;
    }
}
int heapDelete(int heap[], int &n) {
    int root = heap[0];
    heap[0] = heap[n-1];
    n--;
    heapify(heap, n, 0);
    return root;
}
    postorder(root);
    return 0;
}......
