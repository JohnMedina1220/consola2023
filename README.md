# consola2023
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
        //... (código de Burbuja)
    }
}

class OrdenamientoShell : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        //... (código de Shell)
    }
}

class OrdenamientoSeleccion : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        //... (código de Seleccion)
    }
}

class OrdenamientoInsercion : Ordenamiento
{
    public override void Ordenar(int[] numeros)
    {
        //... (código de Insercion)
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
