# dzlab10
```
#include <stdio.h>
#include <math.h>
#include <locale.h>
double fact(int n) {
    double f = 1.0;
    for (int i = 2; i <= n; i++) f *= i;
    return f;
}
double sin_n(double x, int N) {
    double s = 0.0;
    for (int k = 1; k <= N; k++) {
        s += (pow(-1, k - 1) * pow(x, 2 * k - 1)) / fact(2 * k - 1);
    }
    return s;
}
double sin_eps(double x, double eps) {
    double s = 0.0, t = x; 
    int k = 1;
    while (fabs(t) >= eps) {
        s += t;
        k++;
        t = (pow(-1, k - 1) * pow(x, 2 * k - 1)) / fact(2 * k - 1);
    }
    return s;
}

int main() {
    setlocale(LC_ALL, "RUS");
    double x;
    printf("Введите x: ");
    scanf("%lf", &x);
    double s1 = sin(x);
    printf("\n N |   sin_N    |   отклонение\n");
    printf("--------------------------------\n");
    for (int n = 1; n <= 10; n++) {
        double s2 = sin_n(x, n);
        printf("%2d | %9.4lf | %+12.4e\n", n, s2, s1 - s2);
    }
    double s3 = sin_eps(x, 0.000001);
    printf("\nТочность eps = 1e-6:\nsin_eps = %.6lf\n", s3);

    return 0;
}
'''
