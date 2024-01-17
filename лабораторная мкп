#include <iostream>
#include <cmath>
#include <fstream>
#define ra (422+6378) //радиус вектор апоцентра
#define rp (415+6378) //радиус вектор перицентра
#define T 5400 //период обращения ка в секундах
#define mu 398600.0 //грав пар в км
#define PI 3.1415926535
#define EPS 0.00001
double Iter(double M, double e);

int main()
{
    double a = (ra + rp) / 2.0; //большая полуось
    double e = (ra - rp) / (2.0 * a); //эксцентриситет
    double p = a * (1.0 - (e * e)); //фокальный параметр
    //double n = (sqrt(mu / pow(a, 3)));
    //double T = 2 * PI / n;  // средняя угловая скорость
    //double T = 2.0 * PI * (sqrt((pow(a, 3) / mu)));
    double n = (2.0 * PI) / T; //средняя скорость движения по орбите
    double r, Vn, Vr, V, M, E, Theta;
    std::ofstream file;
    file.open("Data.txt");
    file << a << "\t" << e << "\t" << p << "\t" << T << "\t" << n << std::endl;
    if (file) {
        file << "t, c\t" << "M(t), рад\t" << "E(t), рад\t" << "Theta(t), рад\t" << "r\t" << "Vr\t\t" << "Vn\t\t" << "V\t" << std::endl;
    }
    else {
        std::cout << "Error: unabled to open file" << std::endl;
    }


    for (double t = 0; t <= T; t++) {
        M = n * t;
        E = Iter(M, e);
        Theta = atan(sqrt((1.0 + e) / (1.0 - e)) * tan(E / 2)) * 2;
        if (Theta < 0)
            Theta += 2.0 * PI;
        r = p / (1.0 + e * cos(Theta));
        Vn = (sqrt(mu / p) * (1.0 + e * cos(Theta)));
        Vr = (sqrt(mu / p) * (e * sin(Theta)));
        V = sqrt(pow(Vr, 2) + pow(Vn, 2));

       
        file << t << "\t" << M << "\t" << E << "\t" << Theta << "\t" << r << "\t" << Vr << "\t" << Vn << "\t" << V << std::endl;
    }
    file.close();
    std::cout << "U can find output files in directory" << std::endl;

    return 0;
}
double Iter(double M, double e) { 
    double Ek = M, Ek1 = e * sin(Ek) + M;; //Нулевая итерация: 𝐸(0)=𝑀- Ek     
    while ((abs(Ek1 - Ek) > EPS)) 
    { 
        Ek = Ek1; 
        Ek1 = e * sin(Ek) + M; 
    } 
    return Ek1; 
  
} 
