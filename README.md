using System;
using System.IO;

abstract class Ordenamiento
{
    public abstract void Ordenar(int[] numeros);

    public void GuardarResultado(string nombreArchivo, int[] numeros)
    {
        File.WriteAllText(nombreArchivo, string.Join(", ", numeros));
    }
}

class OrdenamientoBurbuja : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        int n = numeros.Length;
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = 0; j < n - i - 1; j++)
            {
                if (numeros[j] > numeros[j + 1])
                {
                    int temp = numeros[j];
                    numeros[j] = numeros[j + 1];
                    numeros[j + 1] = temp;
                }
            }
        }

    }
}
class OrdenamientoShell : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        int n = numeros.Length;
        int gap = n / 2;

        while (gap > 0)
        {
            for (int i = gap; i < n; i++)
            {
                int temp = numeros[i];
                int j = i;

                while (j >= gap && numeros[j - gap] > temp)
                {
                    numeros[j] = numeros[j - gap];
                    j -= gap;
                }

                numeros[j] = temp;
            }

            gap /= 2;
        }
    }
}

class OrdenamientoSeleccion : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        int n = numeros.Length;
        for (int i = 0; i < n - 1; i++)
        {
            int minIndex = i;

            for (int j = i + 1; j < n; j++)
            {
                if (numeros[j] < numeros[minIndex])
                {
                    minIndex = j;
                }
            }

            int temp = numeros[minIndex];
            numeros[minIndex] = numeros[i];
            numeros[i] = temp;
        }
    }
}

class OrdenamientoInsercion : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        int n = numeros.Length;
        for (int i = 1; i < n; i++)
        {
            int key = numeros[i];
            int j = i - 1;

            while (j >= 0 && numeros[j] > key)
            {
                numeros[j + 1] = numeros[j];
                j--;
            }

            numeros[j + 1] = key;
        }
    }
}


class Program
{
    static void Main(string[] args)
    {
        int[] numeros = PedirNumeros();

        Ordenamiento[] metodos = {
            new OrdenamientoBurbuja(),
            new OrdenamientoShell(),
            new OrdenamientoSeleccion(),
            new OrdenamientoInsercion()
        };

        foreach (Ordenamiento metodo in metodos)
        {
            int[] copiaNumeros = (int[])numeros.Clone();
            metodo.Ordenar(copiaNumeros);

            string nombreMetodo = metodo.GetType().Name;
            Console.WriteLine("Ordenado con {0}: {1}", nombreMetodo, string.Join(", ", copiaNumeros));

            metodo.GuardarResultado(nombreMetodo + ".txt", copiaNumeros);
        }

        Console.ReadKey();
    }

    private static int[] PedirNumeros()
    {
        int[] numeros = new int[10];
        Console.WriteLine("Ingrese 10 numeros diferentes: ");

        for (int i = 0; i < numeros.Length; i++)
        {
            Console.Write("Numero {0}: ", i + 1);
            numeros[i] = Convert.ToInt32(Console.ReadLine());
        }

        return numeros;
    }
}
