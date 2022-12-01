# DKR1 Мартиненко Нікіта Ре-22

```ruby

#include <stdio.h>
#include <stdlib.h>

void memAlloc(int*** Arr, int N, int M);
void WriteMatrixContent(int ** matr, int X, int Y);
void PrintMatrixContent(int ** matr, int X, int Y, char* NM);
void MatrixShortLine(int **matr, int X, int Y, int Orintation);
void Matrix_XY_Reverse(int ** matr, int Rows, int Colums, int F_line, int S_line, int Orintation);
int SumMatrix(int **matr, int line, int Rows, int Colums, int Orintation);

int main(){
//========================================================================================================//1
  int N=0,a=0;
  double sum = 0;

  while(printf("\n enter N > 0 :\n N = ") && scanf("%d",&N) && N == 0) printf("\n error : N > 0 !!!");
  printf(" a = ");
  scanf("%d",&a);

  for(int n = 1; n <= N; n++)sum += pow(-1,n+1) * (pow(a,n) / n);
  printf(" sum = %f \n",sum);
//========================================================================================================//2
  int** A = NULL;
  int N2;

  while(printf("\n enter size Matrix :\n N = ") && scanf("%d",&N2) && N2 == 0) printf("\n error : N > 0 !!!");
  memAlloc(&A, N2, N2);

  WriteMatrixContent(A, N2, N2);
  PrintMatrixContent(A, N2, N2, "A");

  MatrixShortLine(A, N2, N2, 0);
  PrintMatrixContent(A, N2, N2, "B1");

  MatrixShortLine(A, N2, N2, 1);
  PrintMatrixContent(A, N2, N2, "B2");

  free(A);
//========================================================================================================//3
  FILE *f=fopen("test.txt","r");
  for(int i=0,C[100]; fscanf(f,"%s",C) == 1 ? 1 : printf("\n\n words = %d\n",i)*0; i++);
  fclose(f);
//========================================================================================================//
}
void memAlloc(int***Arr, int N, int M) {
  *Arr = (int**)calloc(N, sizeof(int*));
  if (*Arr == NULL) {
    printf("Error");
    exit(0);
  }
  for (int i = 0; i < N; i++) {
    (*Arr)[i] = (int*)calloc(M, sizeof(int));
    if ((*Arr)[i] == NULL) {
      printf("Error");
      exit(0);
    }
  }
}
void WriteMatrixContent(int **matr, int X, int Y){ 
   for(int i=0;i<X;i++) for(int j=0;j<Y;j++) matr[i][j] = rand() % 25 + 30;
}
void PrintMatrixContent(int **matr, int X, int Y, char* NM){
   printf("\nMatrix %s = \n", NM);
   for (int i=0;i<X;i++){for(int j=0;j<Y;j++) printf("%d ", matr[i][j]); printf("\n");}
}
void MatrixShortLine(int **matr, int X, int Y, int Orintation){
 if(Orintation == 0){
    for(int i = 0; i <= X; i++){
        if(SumMatrix(matr,i,X,Y,0) > SumMatrix(matr,i + 1,X,Y,0)){
           Matrix_XY_Reverse(matr,X,Y,i,i + 1,0);
           i = 0;
        }
    }
/*
  ну і як же без костиля, на якому держиться весь прод
  баг полягає в тому, що перший і другий рядок якогось беня міняються місцями
  тому сорторуюємо вже вдруге, і виправляєм цю помилку
*/
    for(int i = 0; i <= X; i++){
      if(SumMatrix(matr,i,X,Y,0) > SumMatrix(matr,i + 1,X,Y,0)){
         Matrix_XY_Reverse(matr,X,Y,i,i + 1,0);
         i = 0;
        }
    }
 }else{
    for(int i = 0; i <= Y; i++){
        if(SumMatrix(matr,i,X,Y,1) > SumMatrix(matr,i + 1,X,Y,1)){
           Matrix_XY_Reverse(matr,X,Y,i,i + 1,1);
           i = 0;
        }
    }
/*
  ну і як же без костиля #2, на якому держиться весь прод
  баг полягає в тому, що перший і другий рядок якогось беня міняються місцями
  тому сорторуюємо вже вдруге, і виправляєм цю помилку
*/
    for(int i = 0; i <= Y; i++){
      if(SumMatrix(matr,i,X,Y,1) > SumMatrix(matr,i + 1,X,Y,1)){
         Matrix_XY_Reverse(matr,X,Y,i,i + 1,1);
         i = 0;
        }
    }
 }
}
void Matrix_XY_Reverse(int **matr, int Rows, int Colums, int F_line, int S_line, int Orintation){
 int *Save = NULL;
 Save = malloc(sizeof(int) * Colums);
 if(Orintation){
   for(int i = 0; i < Rows; i++){
      Save[i] = matr[i][S_line];
      matr[i][S_line] = matr[i][F_line];
   }
   for(int i = 0; i < Rows; i++) matr[i][F_line] = Save[i];
 }else{
   for(int i = 0; i < Colums; i++){
      Save[i] = matr[S_line][i];
      matr[S_line][i] = matr[F_line][i];
   }
   for(int i = 0; i < Colums; i++) matr[F_line][i] = Save[i];
 }
 free(Save);
}
int SumMatrix(int **matr, int line, int Rows, int Colums, int Orintation){
 int sum = 0;
 if(Orintation == 0){
    if(line >= Rows) line = Rows - 1;
    for(int i = 0; i < Colums; i++) sum += matr[line][i];
 }else{
    if(line >= Rows) line = Rows - 1;
    for(int i = 0; i < Rows; i++) sum += matr[i][line];
 }
  return sum;
}

```
