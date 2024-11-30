#include <iostream>
#include <queue>
using namespace std;

struct Node{
	int data;
	Node *left;
	Node *right;
};

Node *root=NULL, *n=NULL, *temp=NULL;

Node *createNode (int data){
	n = new Node;
	n->data = data;
	n->left = NULL;
	n->right = NULL;
	return n;
}

void insert (Node *&root, int data){
	if(root == NULL)
	root = createNode(data);
	else if(data <= root->data)
	insert(root->left, data);
	else if(data > root->data)
	insert(root->right, data);
}


void levelOrder (Node * root){
	if(root==NULL) return;
	queue<Node*> q;
	q.push(root);
	while(!q.empty()){
		cout<<q.front()->data <<" ";
		if(q.front()->left != NULL)
		q.push(q.front()->left);
		if(q.front()->right != NULL)
		q.push(q.front()->right);
		q.pop();
	}
}

void preOrder(Node *root){ 
	if (root==NULL) return; 
	
	cout << root->data << " "; 
	preOrder(root->left); 
	preOrder(root->right); 
} 

void inOrderasc(Node *root){ 
	if (root==NULL) return; 
	
	inOrderasc(root->left); 
	cout << root->data << " "; 
	inOrderasc(root->right); 
}
void inOrderdesc(Node *root){ 
	if (root==NULL) return; 
	inOrderdesc(root->right); 
	cout << root->data << " "; 
	inOrderdesc(root->left); 
}

void postOrder(Node *root){ 
	if (root==NULL) return; 
	
	postOrder(root->left); 
	postOrder(root->right); 
	cout << root->data << " "; 
} 

bool cari(Node *root, int data){ 
	if (root==NULL) 
	return false; 
	else if(data < root->data) 
	return cari(root->left, data); 
	else if(data > root->data) 
	return cari(root->right, data); 
	else 
	return true; 
}

Node *cariMin(Node *root){ 
	if (root==NULL) 
	return NULL; 
	while(root->left != NULL) 
	root = root->left; 
	return root; 
} 

void hapus(Node *&root, int data){ 
	if (root==NULL) 
	return; 
	else if(data < root->data) 
	return hapus(root->left, data); 
	else if(data > root->data) 
	return hapus(root->right, data); 
	else{ 
	
		if (root->left == NULL && root->right == NULL){ 
		delete(root); 
		root=NULL; 
		} 
		
		else if (root->left == NULL){ 
		temp = root; 
		root = root->right; 
		delete(temp); 
		temp=NULL; 
		} 
		else if (root->right == NULL){ 
		temp = root; 
		root = root->left; 
		delete(temp); 
		temp=NULL; 
		} 
		else{ 
		temp = cariMin(root->right); 
		root->data = temp->data; 
		hapus(root->right, root->data); 
		} 
	}
}


int main() {
    int pilihan, tampil;
    int data;

    do {
    	system("cls");
    	cout<<"Nama 	: Muh. Alif Faturahman"<<endl;
    	cout<<"Stambuk	: 13020230039"<<endl;
    	cout<<"======================================\n\n";
        
        cout << "Menu\n";
        cout << "1. Insert Node\n";
        cout << "2. Pencarian Data\n";
        cout << "3. Hapus Node\n";
        cout << "4. Binary Tree Traversal\n";
        cout << "5. Keluar\n";
        cout << "Masukkan Pilihan [1...5]: ";
        cin >> pilihan;
        cin.clear();
        cin.ignore();

        switch (pilihan) {
            case 1:
            	system("cls");
                cout << "Masukkan data: "; cin>>data;
                insert(root, data);
                cout << "Nilai " << data << " berhasil dimasukkan.\n";
                system("pause");
                break;
            
            case 2:
            	system("cls");
				if(root == NULL){
					cout<<"Masukkan Data Dulu"<<endl;
				}
				else{
					cout<<"Masukkan data yang ingin dicari: ";
					cin>>data;
				if(cari(root, data) == true){
					cout<<"Data "<<data<<" berhasil ditemukan"<<endl;
				}
				else{
					cout<<"Data "<<data<<" tidak ditemukan"<<endl;
					}
				}
				system("pause");
            	break;
            
            case 3:
				system("cls");
				if(root == NULL){
					cout<<"Masukkan Data Dulu"<<endl;
				}
				else{
                cout << "Hapus Data\n\n";
                cout<<"Massukkan data yang ingin dihapus: ";
				cin>>data;
				if(cari(root, data) == true){
                hapus(root, data);
                cout<<"Data "<<data<<" berhasil dihapus."<<endl;}
                else{
                	cout<<"Data "<<data<<" tidak ditemukan."<<endl;
					}
				}
                system("pause");
                break;
            case 4:
            	system("cls");
				if(root == NULL){
					cout<<"Masukkan Data Dulu"<<endl;
					system("pause");
				}
				else{
                do {
			        system("cls");
			        cout << "Traversal Binary Tree\n";
			        cout << "1. Level Order Traversal\n";
			        cout << "2. Preorder Traversal\n";
			        cout << "3. Inorder Traversal(ASC))\n";
			        cout << "4. Inorder Traversal(DESC)\n";
			        cout << "5. Postorder Traversal\n";
			        cout << "6. Kembali ke Menu Utama\n";
			        cout << "Masukkan pilihan [1..6]: ";
			        cin >> tampil;
					cin.clear();
       				cin.ignore();
			        switch (tampil) {
			            case 1:
			                system("cls");
			                cout << "Level Order Traversal: ";
			                levelOrder(root);
			                cout << endl;
			                system("pause");
			                break;
			            case 2:
			                system("cls");
			                cout << "Preorder Traversal: ";
			                preOrder(root);
			                cout << endl;
			                system("pause");
			                break;
			            case 3:
			                system("cls");
			                cout << "Inorder Traversal: ";
			                inOrderasc(root);
			                cout << endl;
			                system("pause");
			                break;
		                case 4:
			                system("cls");
			                cout << "Inorder Traversal: ";
			                inOrderdesc(root);
			                cout << endl;
			                system("pause");
		                break;
			            case 5:
			                system("cls");
			                cout << "Postorder Traversal: ";
			                postOrder(root);
			                cout << endl;
			                system("pause");
			                break;
			            case 6:
			                system("cls");
			                cout << "Kembali ke Menu Utama.\n";
			                system("pause");
			                break;
			            default:
			                cout << "Pilihan tidak valid.\n";
			                system("pause");
			        	}
			    	} while (tampil != 6);
				}
			    break;
            case 5:
                cout << "Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
                break;
        }
    } while (pilihan != 5);

    return 0;
}

//#include <iostream>
//#include <queue>
//#include <string>
//using namespace std;
//
//struct Node {
//    string data;
//    Node *left;
//    Node *right;
//};
//
//Node *root = NULL, *n = NULL, *temp = NULL;
//
//Node *createNode(string data) {
//    n = new Node;
//    n->data = data;
//    n->left = NULL;
//    n->right = NULL;
//    return n;
//}
//
//void insert(Node *&root, string data) {
//    if (root == NULL)
//        root = createNode(data);
//    else if (data <= root->data)
//        insert(root->left, data);
//    else if (data > root->data)
//        insert(root->right, data);
//}
//
//void levelOrder(Node *root) {
//    if (root == NULL) return;
//    queue<Node *> q;
//    q.push(root);
//    while (!q.empty()) {
//        cout << q.front()->data << " ";
//        if (q.front()->left != NULL)
//            q.push(q.front()->left);
//        if (q.front()->right != NULL)
//            q.push(q.front()->right);
//        q.pop();
//    }
//}
//
//void preOrder(Node *root) {
//    if (root == NULL) return;
//    cout << root->data << " ";
//    preOrder(root->left);
//    preOrder(root->right);
//}
//
//void inOrderasc(Node *root) {
//    if (root == NULL) return;
//    inOrderasc(root->left);
//    cout << root->data << " ";
//    inOrderasc(root->right);
//}
//
//void inOrderdesc(Node *root) {
//    if (root == NULL) return;
//    inOrderdesc(root->right);
//    cout << root->data << " ";
//    inOrderdesc(root->left);
//}
//
//void postOrder(Node *root) {
//    if (root == NULL) return;
//    postOrder(root->left);
//    postOrder(root->right);
//    cout << root->data << " ";
//}
//
//bool cari(Node *root, string data) {
//    if (root == NULL)
//        return false;
//    else if (data < root->data)
//        return cari(root->left, data);
//    else if (data > root->data)
//        return cari(root->right, data);
//    else
//        return true;
//}
//
//Node *cariMin(Node *root) {
//    if (root == NULL)
//        return NULL;
//    while (root->left != NULL)
//        root = root->left;
//    return root;
//}
//
//void hapus(Node *&root, string data) {
//    if (root == NULL)
//        return;
//    else if (data < root->data)
//        hapus(root->left, data);
//    else if (data > root->data)
//        hapus(root->right, data);
//    else {
//        if (root->left == NULL && root->right == NULL) {
//            delete (root);
//            root = NULL;
//        } else if (root->left == NULL) {
//            temp = root;
//            root = root->right;
//            delete (temp);
//            temp = NULL;
//        } else if (root->right == NULL) {
//            temp = root;
//            root = root->left;
//            delete (temp);
//            temp = NULL;
//        } else {
//            temp = cariMin(root->right);
//            root->data = temp->data;
//            hapus(root->right, root->data);
//        }
//    }
//}
//
//int main() {
//    int pilihan, tampil;
//    string data;
//
//    do {
//        system("cls");
//        cout << "Nama  : Muh. Alif Faturahman\n";
//        cout << "Stambuk : 13020230039\n";
//        cout << "======================================\n\n";
//
//        cout << "Menu\n";
//        cout << "1. Insert Node\n";
//        cout << "2. Pencarian Data\n";
//        cout << "3. Hapus Node\n";
//        cout << "4. Binary Tree Traversal\n";
//        cout << "5. Keluar\n";
//        cout << "Masukkan Pilihan [1...5]: ";
//        cin >> pilihan;
//
//        switch (pilihan) {
//            case 1:
//                system("cls");
//                cout << "Masukkan data (string): ";
//                cin >> data;
//                insert(root, data);
//                cout << "Nilai \"" << data << "\" berhasil dimasukkan.\n";
//                system("pause");
//                break;
//
//            case 2:
//                system("cls");
//                if (root == NULL) {
//                    cout << "Masukkan Data Dulu\n";
//                } else {
//                    cout << "Masukkan data yang ingin dicari: ";
//                    cin >> data;
//                    if (cari(root, data) == true) {
//                        cout << "Data \"" << data << "\" berhasil ditemukan\n";
//                    } else {
//                        cout << "Data \"" << data << "\" tidak ditemukan\n";
//                    }
//                }
//                system("pause");
//                break;
//
//            case 3:
//                system("cls");
//                if (root == NULL) {
//                    cout << "Masukkan Data Dulu\n";
//                } else {
//                    cout << "Hapus Data\n\n";
//                    cout << "Masukkan data yang ingin dihapus: ";
//                    cin >> data;
//                    if (cari(root, data) == true) {
//                        hapus(root, data);
//                        cout << "Data \"" << data << "\" berhasil dihapus.\n";
//                    } else {
//                        cout << "Data \"" << data << "\" tidak ditemukan.\n";
//                    }
//                }
//                system("pause");
//                break;
//
//            case 4:
//                system("cls");
//                if (root == NULL) {
//                    cout << "Masukkan Data Dulu\n";
//                    system("pause");
//                } else {
//                    do {
//                        system("cls");
//                        cout << "Traversal Binary Tree\n";
//                        cout << "1. Level Order Traversal\n";
//                        cout << "2. Preorder Traversal\n";
//                        cout << "3. Inorder Traversal (ASC)\n";
//                        cout << "4. Inorder Traversal (DESC)\n";
//                        cout << "5. Postorder Traversal\n";
//                        cout << "6. Kembali ke Menu Utama\n";
//                        cout << "Masukkan pilihan [1..6]: ";
//                        cin >> tampil;
//                        switch (tampil) {
//                            case 1:
//                                system("cls");
//                                cout << "Level Order Traversal: ";
//                                levelOrder(root);
//                                cout << endl;
//                                system("pause");
//                                break;
//                            case 2:
//                                system("cls");
//                                cout << "Preorder Traversal: ";
//                                preOrder(root);
//                                cout << endl;
//                                system("pause");
//                                break;
//                            case 3:
//                                system("cls");
//                                cout << "Inorder Traversal: ";
//                                inOrderasc(root);
//                                cout << endl;
//                                system("pause");
//                                break;
//                            case 4:
//                                system("cls");
//                                cout << "Inorder Traversal: ";
//                                inOrderdesc(root);
//                                cout << endl;
//                                system("pause");
//                                break;
//                            case 5:
//                                system("cls");
//                                cout << "Postorder Traversal: ";
//                                postOrder(root);
//                                cout << endl;
//                                system("pause");
//                                break;
//                            case 6:
//                                system("cls");
//                                cout << "Kembali ke Menu Utama.\n";
//                                system("pause");
//                                break;
//                            default:
//                                cout << "Pilihan tidak valid.\n";
//                                system("pause");
//                        }
//                    } while (tampil != 6);
//                }
//                break;
//
//            case 5:
//                cout << "Keluar dari program.\n";
//                break;
//
//            default:
//                cout << "Pilihan tidak valid.\n";
//                break;
//        }
//    } while (pilihan != 5);
//
//    return 0;
//}
