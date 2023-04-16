# HomeWorkJvmGarbage
## Начало работы программы
1. При запуске программа подгружает системные классы в *Metaspace*.
1. Класс *JvmComprehension* при помощи **ApplicationClassLoader** загружается в *Metaspace*.
1. В стэк передается фрейм с методом *main()*

[![Image1.jpg](https://i.postimg.cc/GpLnwScN/Image1.jpg)](https://postimg.cc/5XRR8gQq)

4. Примитив *int i = 1* записывается во фрейме *main()*.
5. Создаётся объект типа *Object* и записывается в кучу, а ссылка на объект *Object o* записывается во фрейм *main()*.
6. Создаётся объект типа *Integer* и записывается в кучу, а ссылка на объект *Integer ii* записывается во фрейм *main()*.

[![Image2.jpg](https://i.postimg.cc/MHtv1Z7D/Image2.jpg)](https://postimg.cc/wRyqppby)

## Вызов метода printAll(o, i, ii)
7. Вызывается метод *printAll(o, i, ii)* в новый фрейм и передается в стэк.
Его ссылки на объекты будут ссылаться на сущесвующие объекты в куче, а от примитива *int i = 1* возьмётся только само значение.
8. Создаётся объект типа *Integer* и записывается в кучу, а ссылка на объект *Integer ii* записывается во фрейм *main()*.

[![Image3.jpg](https://i.postimg.cc/C575dd1w/Image3.jpg)](https://postimg.cc/7JCwWH0R)

9. Вызывается метод *System.out.println()* в новый фрейм и передается в стэк.
10. Внутри метода *System.out.println()* у объекта вызывается метод *o.toString()* в новый фрейм и передается в стэк.

[![Image4.jpg](https://i.postimg.cc/Xv0fPjq4/Image4.jpg)](https://postimg.cc/NKp29wRz)

## Закрытие метода printAll(o, i, ii)
11. После результат метода *o.toString()*, передается в *System.out.println()*, а фрейм удаляется.
12. Метод *System.out.println()* выводит результат на экран и фрейм также удаляется и поток возвращается к методу *printAll(o, i, ii)*.
13. Поскольку все строки выполнились фрейм метода *printAll(o, i, ii)* также удаляется, но поскольку объект *Integer*, находящийся по ссылке *uselessVar* больше не имеет других ссылок, **сборщик мусора** удалит объект.

[![Image5.jpg](https://i.postimg.cc/kgrndMHp/Image5.jpg)](https://postimg.cc/MvDk7wq7)

14. Теперь поток вернётся к методу *main()* и в нём выполнит метод *System.out.println("finished")*, который также сначала запишется в стек с новым фреймом, а после выполнения удалится.
15. После этого программа завершится и все данные удалятся.
