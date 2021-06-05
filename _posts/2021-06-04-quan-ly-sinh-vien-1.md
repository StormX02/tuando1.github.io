---
title: Quản lý sinh viên 1
date: 2021-06-05 00:12
category:
    - Programming
    - Struct
tags: [C]
---

Thông tin về sinh viên gồm có:

1. mã sinh viên là số nguyên tự động tăng;
2. tên sinh viên;
3. điểm sinh viên là số thực gồm điểm môn A, môn B, môn C.

 
Viết chương trình thực hiện 3 chức năng:

1. thêm mới
2. cập nhật điểm theo mã sinh viên
3. hiển thị danh sách các sinh viên có điểm 3 môn tăng dần (theo thứ tự xuất hiện)

**Input:**

* Dòng thứ nhất là lựa chọn chức năng thực hiện
* Dòng thứ hai
    * Nếu lựa chọn ở dòng thứ nhất là 1 thì nhập số sinh viên sẽ thêm mới
    * Nếu lựa chọn ở dòng thứ nhất là 2 thì nhập mã sinh viên sẽ sửa đổi
- Dòng tiếp theo là thông tin sinh viên
- Chức năng 3 cũng là kết thúc của luồng input

 

**Output:**

- Nếu lựa chọn là 1 thì in ra số sinh viên được thêm
- Nếu lựa chọn là 2 thì in ra mã sinh viên được sửa
- Nếu lựa chọn là 3 thì in ra danh sách theo mô tả dưới đây (các thông tin cách nhau một khoảng trắng)

### Ví dụ
![image](https://user-images.githubusercontent.com/82562559/120839298-f4ecf880-c592-11eb-9593-c3d2e4f248c1.png)

### Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

typedef struct
{
  int maSV;
  char ten[20];
  float monA, monB, monC;
  float tong;
} SV;

int n;
int vitri;
int funtion;
SV arr[20];

void nhap(SV *sv);          //Hàm nhập thông tin của 1 sinh viên
void SapXep(SV a[], int n); //Hàm sắp xếp tổng điểm tăng dần của n sinh viên
void xuat(SV sv);           //Hàm xuất thông tin của 1 sinh viên
void capnhat(int vitri);    //Hàm cập nhật thông tin của 1 sinh viên
int sort(const void *a, const void *b)
{
  SV *data_1 = (SV *)a;
  SV *data_2 = (SV *)b;
  return (data_1->tong - data_2->tong);
}
int main()
{
  int funtion;
  while (1)
  {
    scanf("%d", &funtion);
    switch (funtion)
    {
    case 1:
      scanf("%d", &n);
      for (int i = 0; i < n; ++i)
      {
        arr[i].maSV = i + 1;
        nhap(arr + i);
      }
      printf("%d\n", n);
      break;
      getch();
    case 2:
      scanf("%d", &vitri);
      capnhat(vitri);
      printf("%d\n", vitri);
      break;
      getch();
    case 3:
      qsort(arr, n, sizeof(SV), sort);
      for (int i = 0; i < n; ++i)
      {
        printf("%d ", arr[i].maSV);
        xuat(arr[i]);
        printf("\n");
      }
      break;
      getch();
      return 0;
    }
    if(funtion==3) break;
  }
}

void nhap(SV *sv)
{
  char s[100];
  gets(s);
  fflush(stdin);
  gets(sv->ten);
  scanf("%f%f%f", &sv->monA, &sv->monB, &sv->monC);
  sv->tong = sv->monA + sv->monB + sv->monC;
}

void xuat(SV sv)
{
  printf("%s ", sv.ten);
  printf("%.1f %.1f %.1f ", sv.monA, sv.monB, sv.monC);
}

void capnhat(int vitri)
{
  for (int i = 0; i < n; i++)
  {
    if (arr[i].maSV == vitri)
    {
      nhap(arr + i);
      break;
    }
  }
}
// 1
// 2
// nguyen van hai
// 8.5 5.5 7.5
// tran van tuan
// 8.5 .50 9.0
// 2
// 2
// tran van nam
// 5.5 5.0 6.0
// 3
```
