#include <iostream>
#include <stdio.h>
#include <string.h>
using namespace std;
class Diem
{
private:
    int diemToan;
    int diemLy;
    int diemHoa;
public:
    void nhapD();
    void xuatD();
    int getDiemtoan()
    {
        return diemToan;
    }
    int getDiemly()
    {
        return diemLy;
    }
    int getDiemhoa()
    {
        return diemHoa;
    }
    void setDiemtoan(int t)
    {
        diemToan = t;
    }
    void setDiemly(int l)
    {
        diemLy = l;
    }
    void setDiemhoa(int h)
    {
        diemHoa = h;
    }
    friend class student;
};
class student:public Diem
{
public:
    char hoten[30];
    int namsinh;
    Diem diem;
public:
    double getTBC()
    {
        return (diemToan +diemLy +diemHoa)/3;
    }
    student();
    student(const student &a);
    student & operator =(const student &);
    friend  istream& operator >>(istream &is, student &a);
    friend ostream&operator <<(ostream &os, student a);
    friend void nhapDs(student b[], int n);
    friend void xuatDs(student b[],int n);
};
void Diem::nhapD()
{
    cout<<"\nNhap diem toan :";
    cin>>diemToan;
    cout<<"\nNhap diem ly:";
    cin>>diemLy;
    cout<<"\nNhap diem hoa :";
    cin>>diemHoa;
}
void Diem::xuatD()
{
    cout<<"\nDiem toan:"<<diemToan;
    cout<<"\nDiem ly:"<<diemLy;
    cout<<"\nDiem hoa:"<<diemHoa;
}
student::student()
{
    strcpy(hoten,"");
    namsinh = 0;
    diemToan = diemLy =diemHoa = 0;
}
student::student(const student &a)
{
    {
        strcpy(hoten,a.hoten);
        namsinh = a.namsinh;
        diem = a.diem;
        diemToan = a.diemToan;
        diemHoa = a.diemHoa;
        diemLy = a.diemLy;
    }
}
student& student::operator=(const student &a)
{
    diemToan = a.diemToan;
    diemLy = a.diemLy;
    diemHoa = a.diemHoa;
    return *this;
}
void nhapDs(student a[], int n)
{
    for(int i=0;i<n;i++)
    {
        cout<<"\nNhap thong tin student thu :"<<i+1;
        cin>>a[i];
    }
}
void xuatDs(student a[],int n)
{
    for(int i=0;i<n;i++)
    {
        cout<<"\nThong tin student thu :"<<i+1;
        cout<<a[i];
    }
}
void Diemtbmax(student a[100],int n)
{
    double max = a[0].getTBC() ;
    for(int i=0;i<n;i++)
    {
        if(max < a[i].getTBC())
        {
            max = a[i].getTBC();
        }
    }
    cout<<"\nSinh vien co diem trung binh lon nhat la :";
    for(int i=0;i<n;i++)
    {
        if(max == a[i].getTBC())
        {
            cout<<a[i];
        }
    }
}
istream& operator >>(istream &is, student &a)
{
    cout<<"\nNhap ho ten :";is>>a.hoten;
    cout<<"\nNhap nam sinh :";is>>a.namsinh;
    a.nhapD();
    return is;
}
ostream&operator <<(ostream &os, student a)
{
    os<<"\nHo ten :"<<a.hoten;
    os<<"\nNam sinh :"<<a.namsinh;
    a.xuatD();
    os<<"\nDiem tb:"<<a.getTBC();
    return os;
}
//void MaxTBC()
int main()
{
    student a[100];
    int n;
    cout<<"\nNhap n = :";
    cin>>n;
    nhapDs(a,n);
    xuatDs(a,n);
    Diemtbmax(a,n);

//    cout<<"\nNhap student a :";
//    cin>>a;
//    cout<<"\nNhap student b:";
//    cin>>b;
//    cout<<"\nThong tin sv a:"<<a<<endl;
//    cout<<"\nThong tin sv b:"<<b;
    //c = a;
    //cout<<"\nSinh vien c la :";
    //cout<<c;
    return 0;
}

