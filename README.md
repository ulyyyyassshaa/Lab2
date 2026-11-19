
## Лабораторная работа № 2

#### № группы: `ПМ-2601`

#### Выполнила: `Кулагина Ульяна Юрьевна`

#### Вариант: `№12`


### 1. Программа
```java
import java.io.PrintStream;
import java.util.Scanner;
class oooo {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;
    public static void main(String[] args){
        int n = in.nextInt(); //считывание N
        int[] arr = new int[n]; //создание массива 1)
        for(int i = 0;i<=n-1;i++){ //заполнение массива
            arr[i] = in.nextInt();
        }
        out.println("Исходный массив");//вывод исходного массива
        for (int i = 0;i<=n-1;i++){
            out.print(arr[i]+" ");
        }
        //2) сортировка массива
        // создание массива флагов
        boolean[] isSquare = new boolean[n]; //проверка является ли число квадратом целого числа
        for(int i = 0;i<=n-1;i++){ // проверяем каждое число в исходном массиве, вешаем флажок на каждый элемент
            if(arr[i]>=0){
                int root = (int)Math.sqrt(arr[i]);
                if(root*root==arr[i]){
                    isSquare[i]=true;
                }
            }
        }
        //пузырьковая сортировка массива
        for(int i = 0;i<=n-1;i++){
            for(int j = 0;j<n-1;j++){
                boolean swap = false; //переменная, отвечающая за перестановку элементов
                if(!isSquare[j] && isSquare[j+1]){ //если первый элемент не квадрат целого числа, а соседний да, то меняем местами
                    swap = true;
                }
                else if(isSquare[j] && isSquare[j+1]){ //если оба элемента квадраты, но первый элемент больше, то переставляем
                    if(arr[j]>arr[j+1]){
                        swap = true;
                    }
                }
                else if(!isSquare[j] && !isSquare[j+1]){ // если оба числа не являются квадратами, но первый элемент меньше, то меняем местами
                    if(arr[j]<arr[j+1]){
                        swap = true;
                    }
                }
                if(swap){ //если для элементов нужна перестановка, то меняем местами
                    int a = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = a;

                    boolean after = isSquare[j]; // также меняем флаги
                    isSquare[j] = isSquare[j+1];
                    isSquare[j+1] = after;
                }
            }
        }
        out.println(" ");
        out.println("Отсортированный массив:");//вывод отсортированного массива 2)
        for(int i = 0;i<=n-1;i++){
            out.print(arr[i]+" ");
        }
        //находим количество чисел в массиве, который являются кубами целых чисел
        int count = 0;// счетчик
        for (int i = 0; i<=n-1;i++){
            int root3 = (int)Math.cbrt(arr[i]);
            if(root3*root3*root3==arr[i]){
                count++;
            }
        }
        out.println(" ");
        out.println("Вывод кол-ва кубов целых чисел в массиве:");
        out.println(count);
        //4) замена элементов, являющихся квадратами целых чисел, на их квадратные корни
        for (int i =0; i<=n-1;i++){ //проходимся по массиву, находим квадраты и вычисляем их корни
            if(isSquare[i]){
                arr[i] =(int) Math.sqrt(arr[i]);//замена
            }
        }
        out.println("Вывод массива с заменами на квадратные корни:");
        for (int i =0; i<=n-1;i++){
            out.print(arr[i]+" ");
        }
        //5)Замена каждого неотриц. элемента на его факториал
        out.println(" ");
        out.println("Вывод массива с заменами на факториал каждого неотрицательного числа:");
        for(int i = 0; i<=n-1;i++){//создаем цикл
            if(arr[i]>=0){//проверка
                int fact = 1;//для каждого числа 1 первый множитель
                for (int j = 2; j<=arr[i];j++){
                    fact *= j;
                }
                arr[i] = fact;
            }
            out.print(arr[i]+" ");
        }
        }
}
