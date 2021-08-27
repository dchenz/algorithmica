---
title: Скалярное и векторное произведение
weight: 2
---

Помимо очевидных сложения, вычитания и умножения на константу, у векторов можно ввести и свои особенные операции, которые нам упростят жизнь.

## Скалярное произведение

**Скалярное произведение** (англ. *dot product*) двух векторов равно произведению их длин и *косинуса* угла между ними. Для него справедлива следующая формула:

$$
a \cdot b = |a| \cdot |b| \cdot \cos \theta = x_a x_b + y_a y_b
$$

Она доказывается муторно и чисто технически, так что мы это делать не будем.

Геометрически, она равна проекции вектора $b$ на вектор $a$, помноженный на длину $а$:

![](../img/dot.jpg)

Полезные свойства:

- Скалярное произведение симметрично ($a \cdot b = b \cdot a$).
- Перпендикулярные вектора должны иметь нулевое скалярное произведение.
- Если угол *острый*, то скалярное произведение *положительное*.
- Если угол *тупой*, то скалярное произведение *отрицательное*.

Добавим в нашу реализацию отдельный оператор для него:

```c++
int operator*(r a, r b) { return a.x * b.x + a.y * b.y; }
```

## Векторное произведение

**Векторное произведение** (англ. *cross product*, также называется *косым* или *псевдоскалярным*) для двух векторов равно произведению их длин и *синуса* угла между ними — причём знак этого синуса зависит от порядка операндов. Оно тоже удобно выражается в координатах:

$$
a \times b = |a| \cdot |b| \cdot \sin \theta = x_a y_b - y_a x_b
$$

Так же, как и со скалярным произведением, доказательство координатной формулы оставляется упражнением читателю. Если кто-то захочет это сделать: это следует из линейности обоих произведений (что в свою очередь тоже нужно доказать) и разложения и разложения по базисным векторам $\overline{(0, 1)}$ и $\overline{(1, 0)}$.

Геометрически, это ориентированный объем параллелограмма, натянутого на вектора $a$ и $b$:

![](../img/cross.jpg)

Его свойства:

* Векторное произведение *анти*симметрично: $a \times b = - (b \times a)$.
* Коллинеарные вектора имеют нулевое векторное произведение.
* Если $b$ «слева» от $a$, то векторное произведение *положительное*.
* Если $b$ «справа» от $a$, то векторное произведение *отрицательное*.

Для него обычно тоже перегружают оператор — либо `^`, либо `%`:

```c++
int operator^(r a, r b) { return a.x*b.y - b.x*a.y; }
```

*Примечание.* Вообще говоря, формально векторное произведение определяется не так. Оно определено как вектор такой же длины, но перпендикулярный обоим исходным векторам. Это имеет применение в трёхмерной геометрии и физике, но пока в нашем двумерном мире об этом думать не надо.

---

Скалярное и векторное произведения тесно связаны с углами между векторами и могут использоваться для подсчета величин вроде ориентированных углов и площадей, которые обычно используются для разных проверок.

Когда они уже реализованы, использовать произведения гораздо проще, чем опираться на алгебру. Например, можно легко угол между двумя векторами, подставив в знакомый нам `atan2` векторное и скалярное произведение:

```c++
double angle(r a, r b) {
    return atan2(a ^ b, a * b);
}
```

В дальнейшем, свойства произведений помогут нам в определении взаимного расположения точек и, например, прямой, поэтому важно эти свойства понять и крепко запомнить.