using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace PiramidalnoTurnirnayaSortirovka
{
    class Program
    {
        static void Main(string[] args)
        {
            Sort A = new Sort();
            A.Vvod(); // вывод не сортированного массива
            A.Tourn(); // 1 передача не сортрованного массива из метода Vvod и 2 передача сортированного массива в метод Vyvod
            A.Vyvod(); // вывод сортированного массива
            Console.ReadLine();
        }
    }

    static class Consts
    {
        public static readonly Int32 N = 18; // количество элементов массива
    }
    class Sort
    {   // считывание константы количества элементов массива
        private Int32[] A = new Int32[Consts.N + 1];

        // построенной пирамидальной кучи/бинарного дерева из исходного массива
        private void Initialize(Int32[] tree, Int32 size)
        {   // Инициализация оставшихся листьев исходного массива
            Int32 j = 1, k;
            while (j <= Consts.N)
            {
                tree[size + j - 1] = A[j]; j++;
            }
            // Вычисление веpхних уpовней деpева, где уpовень, находящийся над листьями обpабатывается отдельно.
            for (j = size + Consts.N; j <= 2 * size - 1; j++) tree[j] = Int32.MinValue;
            j = size; //size из метода Tourn
            while (j <= 2 * size - 1)
            {
                if (tree[j] >= tree[j + 1]) tree[j / 2] = j; // сдвиг элементов массива с меньшими значениями к началу
                else tree[j / 2] = j + 1;
                j += 2;
            }
            // составление бинарного дерева из оставшихся 50% необработанных элементов исходного массива
            k = size / 2; // позволяет определить меньший элемент в каждой турнирной паре одинакового уровня N/2  
            while (k > 1)
            {
                j = k;
                while (j <= 2 * k - 1)
                {
                    if (tree[tree[j]] >= tree[tree[j + 1]])
                        tree[j / 2] = tree[j];
                    else tree[j / 2] = tree[j + 1];
                    j += 2;
                }
                k /= 2;
            }
        }

        private void Readjust(Int32[] tree, ushort i)
        {
            unchecked // присвоение любому элементу его максимального значения при перегрузке на случай если не хватит выделенного количества индексов узлов сортировки 
            {
                ushort j;
                // сдвиг всех нечетных чисел самого нижнего-крайнего уровня пирамидальной кучи выше четных по принципу 1 < 2 для последующей более быстрой сортировки 
                if ((i % 2) != 0) tree[i / 2] = i - 1;
                else tree[i / 2] = i + 1;
                // Последний этап составления бинарного дерева из оставшихся 25% необработанных элементов исходного массива
                i /= 2;
                while (i > 1)
                { // 
                    if ((i % 2) != 0) j = (ushort)(i - 1);
                    else j = (ushort)(i + 1);
                    if (tree[tree[i]] > tree[tree[j]]) tree[i / 2] = tree[i];
                    else tree[i / 2] = tree[j];
                    i /= 2;
                }
            }
        }
        public void Tourn()
        {  // сортировка построенной пирамидальной кучи/бинарного дерева методом пирамидально-турнирной сортировки 
            unchecked
            {
                const Int32 size = 128; // Число листьев, необходимых в полном бинаpном деpеве, так, как значение пеpеменной size в наименьшей степени 2, в наибольшей N.
                Int32[] tree = new Int32[256]; // для 2 вариантов каждого из 128 листьев полного бинарного дерева 
                Int32 k;
                ushort i;

                Initialize(tree, size);
                // Тепеpь после того, как деpево постpоено, повтоpяется опеpация пеpемещения элемента, пpедставленного коpнем, в следующую позицию с меньшим индексом в массиве и пеpеупоpядочивается деpево.
                for (k = Consts.N; k >= 2; k--)
                {
                    i = (ushort)tree[1];  // i - индекс узла с листом, соответствующим коpню.
                    A[k] = tree[i];  // Перемещение элемента, на котоpый ссылается коpень в позицию k.
                    tree[i] = Int32.MinValue;
                    Readjust(tree, i);   // Пеpеупоpядочивание деpева в соответствии с новым содеpжимым tree[i].
                }
                A[1] = tree[tree[1]];
            }
        }

        public void Vvod()
        {
            Random r = new Random(); // присвоение рандомных значений элементам массива 
            Console.WriteLine("Исходный массив:"); 
            for (Int32 i = 1; i <= Consts.N; i++)
            {
                A[i] = r.Next(0, 100);
                Console.Write("{0} ", A[i]);
            }
            Console.WriteLine();
        }

        public void Vyvod()
        {
            Console.WriteLine("Результат соpтиpовки:");
            for (int i = 1; i <= Consts.N; i++) Console.Write("{0} ", A[i]);
            Console.WriteLine();
        }
    }
}