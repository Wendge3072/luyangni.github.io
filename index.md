# 主页

## 板块

### 算法设计

![zuoye](algorithm.jpg)

```c++
#include<bits/stdc++.h>
using namespace std;

int gcd(int a,int b){
    return b?gcd(b,a%b):a;
}

struct number{
    int a, b;
    number(int aa,int bb){
        int f=gcd(abs(aa), abs(bb));
        aa/=f,bb/=f;
        a=aa, b=bb;
        if(b<0) b=-b,a=-a;
    }
};

int num[5];
int target;
int brackets[3]={202,178,170};
int opt[4]={0,1,2,3}; //+, -, *, /
stack<number> NUM;
stack<int> OPT;

bool cunzai(int i){
    while(!NUM.empty()) NUM.pop();
    while(!OPT.empty()) OPT.pop();
    NUM.push({num[0],1});
    for(int i=0;i<4;i++){
        OPT.push(opt[i]);
    }
    int nu_i=1;
    int bracket=brackets[i];
    while(bracket){
        if(bracket & 1){
            number m(0,1),n(0,1);
            m=NUM.top();
            NUM.pop();
            n=NUM.top();
            NUM.pop();
            int option=OPT.top();
            OPT.pop();
            if(option==0) NUM.push({m.a*n.b+m.b*n.a, m.b*n.b});
            else if(option==1) NUM.push({m.a*n.b-n.a*m.b, m.b*n.b});
            else if(option==2) NUM.push({m.a*n.a, m.b*n.b});
            else {
                if(n.a==0) return false;
                NUM.push({m.a*n.b, m.b*n.a});
            }
        }
        else{
            NUM.push({num[nu_i++],1});
        }
        bracket>>=1;
    }
    if(NUM.top().a==target && NUM.top().b==1) return true;
    else return false;
}

void printit(int i){
    char opsign[7]="+-*/()";
    stack<string> ans;
    stack<int> myopt;
    ans.push(to_string(num[0]));
    int nu_i=1;
    for(int i=0;i<4;i++){
        myopt.push(opt[i]);
    }
    int bracket=brackets[i];
    while(bracket){
        if(bracket & 1){
            string a=ans.top();
            ans.pop();
            string b=ans.top();
            ans.pop();
            int optnow=myopt.top();
            myopt.pop();
            if(optnow==0) ans.push(opsign[4]+a+opsign[0]+b+opsign[5]);
            else if(optnow==1) ans.push(opsign[4]+a+opsign[1]+b+opsign[5]);
            else if(optnow==2) ans.push(opsign[4]+a+opsign[2]+b+opsign[5]);
            else ans.push(opsign[4]+a+opsign[3]+b+opsign[5]);
        }
        else {
            ans.push(to_string(num[nu_i++]));
        }
        bracket>>=1; 
    }
    cout<<ans.top().substr(1,ans.top().length()-2)<<endl;
}

int main(){
    for(int i=0;i<5;i++) cin>>num[i];
    sort(num, num+5);
    cin>>target;
    int flag=0;
    do{
        do{
            for(int i=0;i<3;i++){
                if(cunzai(i)){
                    printit(i);
                    flag=1;
                }
            }
        }while(next_permutation(opt,opt+4));
    }while(next_permutation(num,num+5));
    if(!flag) cout<<"no way"<<endl;
}

```

### 数据结构

## 联系我

Email:[wendge@outlook.com](mailto:wendge@outlook.com)
