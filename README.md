# Atividade-45

#include <stdio.h>
int tabuleiro[9][9]={{0}};
int lista[9][9][9]={{{0}}};
int main(){
int alea;
srand(time(0));
coloca();
mostra();
}
void mostra(){
int i,j;
for(i=1;i<=19;i++){
    for(j=1;j<=19;j++){
        if(i==1&&j==1)
            printf("\xc9");
        else if(i==1 && (j==7 || j==13))
            printf("\xcb");
        else if(i==1 && j==19)
            printf("\xbb");
        else if((i==7 || i==13) && j==1)
            printf("\xcc");
        else if((i==7 || i==13) && j==19)
            printf("\xb9");
        else if(i==19 && j==1)
            printf("\xc8");
        else if(i==19 && (j==7 || j==13))
            printf("\xca");
        else if(i==19 && j==19)
            printf("\xbc");
        else if((i==1 || i==7 || i==13 || i==19) && (j!=7 && j!=13))
            printf("\xcd");
        else if((i!=7 && i!=13) && (j==1 || j==7 || j==13 || j==19))
            printf("\xba");
        else if((i==7 && j==7) || (i==7 && j==13) || (i==13 && j==7) || (i==13 && j==13))
            printf("\xce");
        else if(i%2==0 && (j==3 || j==5 || j==9 || j==11 || j==15 || j==17))
            printf("\xb3");
        else if((i==3 || i==5 || i==9 || i==11 || i==15 || i==17) && j%2==0)
            printf("\xc4");
        else if((i==3 || i==5 || i==9 || i==11 || i==15 || i==17) && (j==3 || j==5 || j==9 || j==11 || j==15 || j==17))
            printf("\xc5");
        else if(tabuleiro[i/2-1][j/2-1]==0)
            printf(" ");
        else
            printf("%d",tabuleiro[i/2-1][j/2-1]);
    }
    printf("\n");
}
}
int aleatorio(int i, int j){
int a;
int min = 1;
int max = 9;
do{
    a = min + rand() % (max - min + 1);
}while(lista[i][j][a]==1);
return a;

}
int coloca(){
int i,j,alea,b;
for(i=0;i<=8;i++){
    for(j=0;j<=8;j++){
        mostra();
        do{
            alea=aleatorio(i,j);
            b=colocaBem(alea,i,j);
        //tabuleiro[i][j] = aleatorio();
        }while(b==0);
    }
}
}
int colocaBem(int alea, int linha, int coluna){

int i,j,a,b;
for(i=0;i<=8;i++){
        if(tabuleiro[linha][i] == alea)
            return 0;
}
for(i=0;i<=8;i++){
    if(tabuleiro[i][coluna] == alea)
            return 0;
}
a=linha/3;
b=coluna/3;
for(i=0;i<=2;i++){
    for(j=0;j<=2;j++)
        if(tabuleiro[i+a*3][j+b*3]==alea)
            return 0;
}
VerificaDispLista(linha,coluna,alea);
return 1;
}
void VerificaDispLista(int i, int j, int alea){
if(lista[i][j][alea-1]==0){
    tabuleiro[i][j]=alea;
    lista[i][j][alea-1]=1;
}
}
void PercorreLista(int i, int j){
int k,c;
for(k=0;k<=8;k++){
    if(lista[i][j][k]==1)
        c++;
}
if(c==9){
    lista[i][j][k]=0;
    lista[i][j-1][k]=0;
}
}
