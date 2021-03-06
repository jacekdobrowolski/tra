Wykrywanie dobrych punktów do śledzenia w obrazie
-------------------------------------------------

Do wykrywania narożników w obrazie można wykorzystać różne metody.
Najbardziej popularne są Harrisa-Stephens :cite:`Harris` i
Shi-Tomasi :cite:`Shi-Tomasi`, są one do siebie podobnę i
część algorytmu jest wspólna. Obie metody zakładają że narożnik to punkt
obrazu w którym intensywność zmienia się w więcej niż dwóch kierunkach.
Zmiana w jednym kierunku oznacza krawędź. Niech :math:`I(x, y)` równa
się intensywności pixela o koordynatach x i y. :math:`I(x + u, y + v)`
równa się intensywności pixela odległego o u i v od poprzedniego.
Narożnik znajdzie się się więc w punkcie gdzie suma kwadratów różnic
między tymi wartościami będzie największa. Co można zapisać jako

.. math:: S(x,y) = \Sigma_{u}\Sigma_{v}w(u, v)[I(x + u, y + v) - I(x, y)]^2

gdzie :math:`w(u, v)` to funkcja okna przesuwanego po obrazie,
zwracająca wartość jeden dla małego obszaru i zero dla reszty. Obszarem
do zbadania jest działanie innych okien okrągłych, niebinarnych. To
równanie możemy przybliżyć wielomianem korzystając z twierdzenia
Taylora. Niech :math:`I_x` i :math:`I_y` będą pochodnymi :math:`I` tak
aby :math:`I(x + u, y + v) \approx I(u, v) + I_x(u, v)x + I_y(u, v)y`
Daje to wielomian

.. math:: S(x, y) \approx \Sigma_u \Sigma_v w(u, v)(I_x(u, v)x+I_y(u,v)y)^2

Zapisane w formie macierzowej:

.. math::

   S(x, y) \approx 
           \begin{pmatrix}
               x & y 
           \end{pmatrix}
           \mathbf{A} 
           \begin{pmatrix}
               x \\
               y \\
           \end{pmatrix}

.. math::

   {\displaystyle 
       A=\sum _{u}\sum _{v}w(u,v){
           \begin{bmatrix}
               I_{x}(u,v)^{2}&I_{x}(u,v)I_{y}(u,v)\\
               I_{x}(u,v)I_{y}(u,v)&I_{y}(u,v)^{2}
           \end{bmatrix}}={
           \begin{bmatrix}
               \langle I_{x}^{2}\rangle &\langle I_{x}I_{y}\rangle \\
               \langle I_{x}I_{y}\rangle &\langle I_{y}^{2}\rangle 
           \end{bmatrix}}
       }

Poprzez analizę wartości własnych macierzy :math:`\mathbf{A}` można
znaleźć narożniki.

-  Obie wartości są bliskie zeru dany pixel nie ma dobrych punktów do
   śledzenia

-  Jedna z wartości własnych jest bliska zeru a druga ma duża wartość
   dany pixel znajduje się na krawędzi

-  Obie wartości własne mają duże dodatnie wartości dany pixel jest
   narożnikiem

W tym punkcie metody Harrisa i Shi-Tomasi zaczynają się różnić.


.. toctree::
    :maxdepth: 1
    
    harris
    shi_tomasi
    fast
