# CHFNFRN
# Question
Chef invited N of his friends in his birthday party. All the friends are numbered from 1 to N. Some of the friends might know each other. You are given this information by M pairs each of form (ai, bi), denoting that the persons ai and bi know each other.

Chef wants all of his guests to seat at the two tables set up for dinner. He wants that all the people sitting at a table must know each other, otherwise they will feel awkward with mutual eating habits. Chef is okay if a table is not occupied by any person. Chef is worried whether all the guests can seat at the dinner tables in the desired way.

Please help Chef fast to identify whether his worry is real or not!! The delicacies at the table are getting cold.

Input

The first line of the input contains an integer T denoting the number of test cases. The description of T test cases follows.

The first line of each test case contains two space-separated integers N and M, denoting the number of Chef's friends and the number of pairs representing information whether two person know each other or not.

The next M lines contain two space-separated integers ai and bi, denoting that persons ai and bi know each other.

Output

For each test case, output a single line containing word "YES" (without quotes) if Chef can divide all of his friends into two groups that in each group all the people know each other and "NO" (without quotes) otherwise.

Constraints

    1 ≤ T ≤ 103
    1 ≤ N ≤ 103
    0 ≤ M ≤ 106
    1 ≤ ai, bi ≤ N
    The sum of N over all test cases in a single test file does not exceed 104
    The sum of M over all test cases in a single test file does not exceed 106
    
Subtasks

Subtask #1 (30 pts)
    
    1 ≤ N ≤ 10

Subtask #2 (70 pts)

    Original constraints
    
Example

Input:

    3
    3 2
    1 2
    2 3
    4 3
    1 2
    2 3
    2 4
    6 7
    1 2
    1 3
    2 3
    2 4
    4 5
    4 6
    5 6

Output:

    YES
    NO
    YES

*******************************************************************************************************************************

#Solution

    #include <iostream>
    #include <cmath>
    using namespace std;
 
    long long int v[1001],z[1000][1000];
    template <typename T>
    struct node{
                T data;
                node *right,*left;
                };
 
    template <class T>
    class list{
                    node<T> *front,*rear;
                    public:
                    void push_back(T);
                    bool recursemark(long long int);
                    void clear();
                    void print();
                    list()
                    {
                        front=NULL;
                    }
                };
    list<long long int> A[1001];
    template <class T>
    void list<T>::push_back(T a)
    {
        node<T> *add;
        add=new struct node<T>;
        add->data=a;
        add->right=NULL;
        add->left=NULL;
        if(front==NULL)
        {
            front=add;
            rear=add;
        }
        else
        {
            rear->right=add;
            add->left=rear;
            rear=add;
        }
    }
    template <class T>
    void list<T>::print()
    {
        node<T> *ptr;
        ptr=front;
        if(front==NULL)
            cout<<"Underflow.\n";
        else
        {
            while(ptr!=NULL)
            {
                cout<<ptr->data;
                ptr=ptr->right;
                if(ptr!=NULL)
                    cout<<"->";
            }
            cout<<"\n";
        }
    }
    bool mark(long long int k)
    {
        long long int i;
        bool f=true;
        for(i=k;i>=1;i--)
        {
            if(v[i]==0)
            {
                v[i]=1;
                f=A[i].recursemark(1);
            }
            if(f==false)
                break;
        }
        return f;
    }
    template <class T>
    bool list<T>::recursemark(long long int g)
    {
        node<T> *ptr;
        ptr=front;
        bool f;
        if(front==NULL)
            return true;
        else
        {
            while(ptr!=rear)
            {
                if(v[ptr->data]==0)
                {
                    v[ptr->data]=(3-g);
                    f=A[ptr->data].recursemark((3-g));
                    if(f==false)
                        return f;
                }
                else if(v[ptr->data]==(3-g));
                else
                    return false;
                ptr=ptr->right;
            }
            if(v[ptr->data]==0)
                {
                    v[ptr->data]=(3-g);
                    f=A[ptr->data].recursemark((3-g));
                    if(f==false)
                        return f;
                }
                else if(v[ptr->data]==(3-g));
                else
                    return false;
        }
        return true;
    }
    template <class T>
    void list<T>::clear()
    {
        node<T> *ptr;
        ptr=front;
        while(ptr!=rear)
        {
            node<T> *del;
            del=ptr;
            ptr=ptr->right;
            delete del;
        }
        delete ptr;
        front=NULL;
        rear=NULL;
    }
    int main()
    {
        long long int n,k,i,u,l,j,m,t;
        cin>>t;
        bool f;
        while(t--)
        {
            cin>>n>>m;
            if(m==0)
            {
                if(n<=2)
                    cout<<"YES\n";
                else
                    cout<<"NO\n";
            }
            else
            {
            for(j=0;j<=n;j++)
                v[j]=0;
            for(i=0;i<n;i++)
            {
                for(j=0;j<n;j++)
                {
                    if(i==j)
                        z[i][j]=1;
                    else
                        z[i][j]=0;
                }
            }
            for(i=1;i<=m;i++)
            {
                cin>>k>>u;
                z[k-1][u-1]=1;
                z[u-1][k-1]=1;
            }
            for(j=0;j<n;j++)
            {
                for(l=0;l<n;l++)
                {
                    if(z[j][l]==0)
                        A[j+1].push_back(l+1);
                }
            }
            f=mark(n);
            if(f)
                cout<<"YES\n";
            else
                cout<<"NO\n";
            for(j=1;j<=n;j++)
                A[j].clear();
            }
            //cout<<"Case "<<i<<": "<<p<<" "<<min(x,y)<<" "<<max(y,x)<<"\n";
        }
        return 0;
    }
 
