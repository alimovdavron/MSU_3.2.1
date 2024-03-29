Документация.

Данная программа решает задачу поиска решения системы линейных уравнений методом Гаусса с выбором главной матрицы.

Описание алгоритма:

/* Описание */

Компоненты программы:
    1. main_lss_01_03.c
    2. lss_01_03.c

Функции реализованные в файле main_lss_01_03.c:
    int _strlen(char const *input) - функция принимает на вход строку и возвращает её длину.
        Аргументы функции:
            Строка
        Возвращаемые значения:
            Целые неотрицательные числа - длина строки.

    int validateFile(char* filename) - функция принимает на вход путь к файлу в виде строки.
        Аргументы функции:
            Строка
        Возвращаемые значения:
            0 - Такого файла по данному пути не существует.
            1 - Файл по данному пути существует.

    int validateParameters(int argc, char **argv) - функция принимает на вход количество аргументов переданных в качестве параметра в командной строке и аргументы.
        Возвращаемые значения:
            0 - Валидация прошла успешно и параметры соответствуют условиям
            1 - Ошибка ввода параметров. Данное значение возвращается, в случае, если количество строк воспринимаемых как названия файлов больше 2.
            2 - Ошибка ввода параметров. Длина одного из флагов больше 1.
            3 - Ошибка ввода параметров. Такого флага не существует.

    int readInputData(char *inputFile, double** A, double** B, double** X, int *n)
        Описание:
            Функция принимает на вход название файла, указатели на матрицы и размер матрицы.
            Выделяет память для них, проверяет входные данные на корректность.
        Аргументы функции:
            Строка - название файла
            Указатель на указатель - матрица коэффициентов
            Указатель на указатель - вектор B
            Указатель на указатель - вектор ответов
            Указатель на переменную типа целое число - размер матрицы
        Возвращаемые значения:
            0 - Успешно. Функция выделила память, считала нужно количество данных, проверила их на корректность и не выявила ошибок
            1 - Ошибка. Размер матрицы отрицательный или равен нулю.
            2 - Ошибка. В файле недостаточно данных для решения задачи.
            3 - Ошибка. Один из коеффициентов или один из элементов вектора значений не являются числом.
                        Или размер матрицы не является целым положительным числом.
            4 - Ошибка. Файл пуст.
            5 - Ошибка. В файле недостаточно данных для решения задачи. (Вектор значений не полон)

    void writeAnswer(char *outputFile, int n, const double* X, int notExist)
        Описание:
            Функция принимает на вход выходной файл, размер матрицы, указатель на решение и переменную для обозначения существования ответа
        Аргументы функции:
            Строка - название выходного файла
            Целое число - размер матрицы
            Указатель на вещественное число - массив с решением задачи
            Целое число - параметр (1, если ответа не существует, иначе - 0)
        Возвращаемые значения:
            Нет

    void printHelp()
        Описание:
            Функция выводит в консоль справочную информацию
        Аргументы функции:
            Нет
        Возвращаемые значения:
            Нет

    void printMatrix(int n, int m, const double* A)
        Описание:
            Функция принимает на вход размеры матрицы, матрицу и выводит её в консоль
        Аргументы функции:
            Целое число - количество строк в матрице
            Целое число - количество столбцов в матрице
            Указатель на вещественное число - матрица
        Возвращаемые значения:
            Нет

Функции реализованные в файле lss_01_03.c:
    size_t lss_memsize_SS_NN(int n)
        Описание:
            Функция принимает на вход размер квадратной матрицы и возвращает количество памяти,
            необходимое алгоритму для решения задачи
        Аргументы функции:
            Целое число - размер матрицы
        Возвращаемые значения:
            Целое неотрицательное число - необходимое количество памяти


    struct pair - структура из двух целых чисел
    struct pair getMax(int n, const double *A, int k)
        Описание:
            Функция принимает на вход квадратную матрицу, индекс k.
            Пусть i, j - индекс элемента в матрице. Функция возвращает пару индексов элемента с максимальным абсолютным значением
            для всех i, таких, что k <= i < n и для всех j таких, что k <= j < n
        Аргументы функции:
            Целое число - размер матрицы (n > 0)
            Указатель на вещественное число - матрица
            Целое число - параметр номера итерации (0 <= k < n)
        Возвращаемые значения:
            Пара чисел -1 ({-1, -1}) - Максимальный по абсолютному значению элемент подматрицы равен нулю.
            Пара целых положительных чисел меньше n - индекс максимального элемента подматрицы отличного от нуля

    void setReplacement(struct pair replacement, double* pMem)
        Описание:
            Функция принимает на вход пару индексов и указатель на вещественное число и в присваивает значение переменной i структуры pair
            в первые 4 байта по данному указателю и присваивает значение переменной j структуры pair в 5-8 байты по данному указателю
        Аргументы функции:
            Структура pair
            Указатель на вещественное число
        Возвращаемые значения:
            Нет

    void replaceColumn(int n, int k, int column, double* A)
        Описание:
            Функция принимает на вход размеры матрицы, индекс k, индекс столбца и матрицу.
            Осуществляет замену местами столбцов k и column матрицы A
        Аргументы функции:
            Целое число - размер квадратной матрицы (n > 0)
            Целое число - индекс первого столбца (0 <= k < n)
            Целое число - индекс второго столбца (0 <= column < n)
            Указатель на вещественное число - матрица
        Возвращаемые значения:
            Нет

    void replaceRow(int n, int k, int row, double *A, double *B)
       Описание:
           Функция принимает на вход размеры матрицы, индекс k, индекс строки и матрицу.
           Осуществляет замену местами строк k и row матрицы A
       Аргументы функции:
           Целое число - размер квадратной матрицы (n > 0)
           Целое число - индекс первой строки (0 <= k < n)
           Целое число - индекс второй стркои (0 <= row < n)
           Указатель на вещественное число - матрица
       Возвращаемые значения:
           Нет

    void prettyPrint(int n, int m, const double* A)
        Описание:
           Функция принимает на вход размеры матрицы, матрицу и выводит её в консоль
       Аргументы функции:
           Целое число - количество строк
           Целое число - количество столбцов
           Указатель на вещественное число - матрица
       Возвращаемые значения:
           Нет

    void pp(int n, const double* A, const double* B)
        Описание:
           Функция принимает на вход размеры матрицы, матрицу системы, вектор свободных членов.
       Аргументы функции:
           Целое число - размер матрицы системы
           Указатель на вещественное число - матрица системы
           Указатель на вещественное число - вектор свободных членов
       Возвращаемые значения:
           Нет

    void printOrderOfReplacements(double *tmp, int n)
        Описание:
            Функция принимает на вход массив дополнительной памяти и размер матрицы системы.
            Выводит в консоль порядок изменения столбцов и строк построчно по каждой итерации.
        Аргументы функции:
            Указатель на вещественное число - массив дополнительной памяти
            Целое число - размер матрицы системы
        Возвращаемые значения:
            Нет

    int lss_01_03(int n, double* A, double* B, double* X, double* tmp)
        Описание:
            Реализует алгоритм описанный в начале документации.
            Состоит из n итераций.
            На k-ой итерации алгоритм вызывает функцию getMax с аргументами (n, A, k) и находит максимальный по абсолютному значению элемент подматрицы (определение подматрицы дано в описании функции getMax).
            Если getMax вернул пару -1, -1, то алгоритм проходится по вектору свободных членов, начиная с k-го элемента.
                Если какой-то элемент не равен нулю, то решения не существует. Алгоритм возвращает 1.
                Если все элементы вектора свободных членов начиная с k-го элемента равны нулю, то решений бесконечно много. Алгоритм присваивает переменным с индексами k,...,n значение 0 и решает задачу на оставшейся матрице.
                В этом случае алгоритм вызывает функцию setReplacement и присваивает элементам массива дополнительной памяти начиная с индекса k пары -1, -1
                Цикл итераций прерывается и начинается конструирование ответа.
                В массиве ответа элементам X, начиная с k-го, присваивается значение 0.
                Осуществляется обратный ход метода Гаусса, где на каждом этапе вычисляется значение i-го элемента решения путём подстановки уже известных коеффицентов.
                Алгоритм осуществляет итерацию по списку замен и восстанавливает ответ, вызывая метод replaceColumn.
                Алгоритм возвращает 0.
            Если getMax вернул пару с целыми неотрицательными числами, то осуществляется замена с помощью функций replaceColumn и replaceRow, записывается очередной элемент в порядке замен функцией setReplacement.
            /*тут нужно написать про то как вычисляется дальше*/
            Если за n итераций getMax не вернул -1, -1, то начинается конструирование ответа.
            Осуществляется обратный ход метода Гаусса, где на каждом этапе вычисляется значение i-го элемента решения путём подстановки уже известных коеффицентов.
            Алгоритм осуществляет итерацию по списку замен и восстанавливает ответ, вызывая метод replaceColumn.
            Алгоритм возвращает 0.
        Аргументы функции:
            Целое число - размер матрицы системы
            Указатель на вещественное число - матрица системы
            Указатель на вещественное число - вектор свободных членов
            Указатель на вещественное число - вектор-ответ
            Указатель на вещественное число - массив дополнительной памяти
        Возвращаемые значения:
            0 - Успешно. Задача решена, решение существует
            1 - Успешно. Задача решение, решения не существует


Коды возвращаемых значений:
0 - Программа решила задачу и вывела ответ
1 - Программа решила задачу и вывела, что ответа не существует
2 - Одного из файлов не существует
3 - Ошибка ввода параметров (Забыли поставить '-' или ввели флаг длина которого больше 2)
4 - Ошибка ввода параметров (Введенного вами параметра не существует)
5 - Ошибка валидации входных данных (Размер матрицы не положительный)
6 - Ошибка валидации входных данных (Количество коеффициентов меньше ожидаемого)
7 - Ошибка валидации входных данных (Как минимум один из введенных коеффициентов не является числом)


Данному методу требуется дополнительно n*sizeof(double) памяти для хранения порядка замены столбцов и строк. Для каждого шага необходимо 8 байтов, по 4 байта на индекс строки и столбца. Порядок необходим для восстановления ответа.

Метод применим для всех видов матриц. Для задачи, у которой нет решения, на определенном шаге алгоритм обнаружит противоречие, а именно, что строка с нулевыми коеффициентами равна числу отличному от нуля. Для задачи с бесконечным количеством решений программа выведет одно решение. На определенном этапе алгоритм обнаружит, что оставшиеся строки обнулились, равны они соответственно все нулю, тогда он присвоит свободным переменным 0 и решит задачу для меньшего количества переменных. 

Сложность метода - O(n^3). Программе было выдано около 15 тестировых входных данных с размерами матриц от 3 до 1000. Тесты были взяты с сайта https://sparse.tamu.edu/. 
Тестирование прооводилось с помощью скрипта написанного на языке Python с использованием библиотек scipy (необходимо для считывания формата .mtx) и numpy.
Точность проверялась сверкой с решением, полученным с помощью функции numpy.linalg.solve. 

Алимов Даврон. М2-16.